# REST API Security
- Spring Security Model
	- Spring Security defines a framework for security
	- Implemented using Servlet filters in the background
		- Servlet filters pre-process / post-process web requests
		- Servlet filters route web requests based on security logic
		- Spring provides a bulk of security functionality with servlet filters
	- Two methods of securing an app: declarative and programmatic

![image](https://github.com/XavierQuan/spring-tools/assets/113052415/95a9299e-da14-40f2-8cb5-15f860133aff)


### Security Concepts
- Authentication
	- Check user id and password with credentials stored in app / db
- Authorization
	- Check to see if user has an authorized role
- Declarative Security
	- Define application's security constraints in configuration
		- All Java config: @Configuration
	- Provides separation of concerns between application code and security
- Programmatic Security
	- Spring Security provides an API for custom application coding
	- Provides greater customization for specific app requirements

### Enabling Spring Security
1. Edit pom.xml and add `spring-boot-starter-security`
2. This will automagically secure all endpoints for application
	- Accessing secured endpoints will prompt for login
	- Override default user name and generated password in application.properties

``` Java
// Spring Security Configuration
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
            .anyRequest().authenticated()
            .and()
            .formLogin()
            .and()
            .httpBasic();
    }
}
```

- Dev Process
	1. Create Spring Security Configuration (@Configuration)
	2. Add users, passwords and roles
		- In Spring Security, passwords are stored using a specific format
			- `{id}encodedPassword`
				- ID - Description
				- noop - Plain text passwords
				- bcrypt - BCrypt password hashing
``` Java
@Autowired
public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {
    auth.inMemoryAuthentication()
        .withUser("user").password("{noop}password").roles("USER")
        .and()
        .withUser("admin").password("{bcrypt}encodedPassword").roles("ADMIN");
}
```
- Cross-Site Request Forgery (CSRF)
	- Spring Security can protect against CSRF attackes
	- Embed additional authentication data / token into all HTML forms
	- On subsequent requests, web app will verify token before processing
	- Primary use case is traditional web applications (HTML forms etc...)

- When to use CSRF Protection
	- For any normal browser web requests
	- Traditional web apps with HTML forms to add / modify data
	- If building REST API for non-browser clients
		- disable CSRF protection, not required for stateless REST APIs that use POST, PUT, DELETE and / or PATCH

``` Java
@Override
protected void configure(HttpSecurity http) throws Exception {
    http
        .csrf().disable() // Disable CSRF for stateless REST APIs
        .authorizeRequests()
        .anyRequest().authenticated()
        .and()
        .httpBasic();
}
```

### Database Access
- Dev Process
	1. Develop SQL Script to set up database tables
	2. Add database support to Maven POM file
	3. Create JDBC properties file
	4. Update Spring Security Configuration to use JDBC

- Default Spring Security Database Schema
	- users
		- username
		- password
		- enabled
	- authorities (same as roles)
		- username
		- authority

- BCrypt Encryption
	- Performs one-way encrypted hashing
	- Adds a random salt to the password for additional protection
	- Includes support to defeat brute force attack

	- Generate password
		- Enter plaintext password
		- Generate a bcrypt password
		- Multiple runs will generate a different password due to random password salting

	- Dev Process
		1. Run SQL Script that contains encrypted passwords
			- Modify DDL for password field, length should be 68

	- Login Process
		1. Retrieve password from db for the user
		2. Read the encoding algorithm id (bcrypt)
		3. For case of bcrypt, encrypt plaintext password from login form (using salt from db password)
		4. Compare encrypted password from login form with encrypted password from db
		5. If there is a match, login successful
		6. If no match, login not successful
	- The password from db is NEVER decrypted because bcrypt is a one-way encryption algorithm

- Security Schema Customization
	- Tell Spring how to query the custom tables
	- Provide query to find user by user name
	- Provide query to find authorities / roles by user name

# MVC Security
- HTTP Basic Authentication
- Default login form
	- Spring Security provides a default login form
- Custom login form
	- HTML + CSS

``` Java
@Override
protected void configure(HttpSecurity http) throws Exception {
    http
        .authorizeRequests()
        .anyRequest().authenticated()
        .and()
        .formLogin()
            .loginPage("/login") // Custom login page URL
            .permitAll(); // Allow access to all for login page
}
```

- Dev Process
	1. Modify Spring Security Configuration to reference custom login form
	2. Develop a Controller to show the custom login form
	3. Create custom login form
		- HTML (CSS optional)

- Bootstrap
	- Web framework that includes CSS styles and JavaScript
	- Focused on front-end UI
	- Dev Process
		1. Modify form to point to our login processing URL
		2. Verify form fields for username and password
		3. Change our controller to use our new Bootstrap login form

- Logout
	- Dev Process
		1. Add logout support to Spring Security Configuration
		2. Add logout button to home page
		3. Update login form to display "logged out" message
	- Logout Process
		- When a logout is processed, by default Spring Security will
		- Invalidate user's HTTP session and remove session cookies
		- Send user back to the login page
		- Append a logout parameter: ?logout
``` Java
@Override
protected void configure(HttpSecurity http) throws Exception {
    http
        .logout()
            .logoutSuccessUrl("/login?logout") // Redirect after logout
            .permitAll();
}
```

- Restrict URLs Based on Roles
	- Dev Process
		1. Create supporting controller code and view pages
		2. Restricting Access to Roles
			- Update Spring Security Java configuration file
			- `requestMatchers(<< add path to match on >>).hasRole(<< authorized role >>)`
			- Multiple roles: `requestMatchers(<< add path to match on >>).hasAnyRole(<< comma-delimited list of authorized roles >>)`

``` Java
@Override
protected void configure(HttpSecurity http) throws Exception {
    http
        .authorizeRequests()
        .antMatchers("/admin/**").hasRole("ADMIN") // Restrict '/admin/**' URLs to users with 'ADMIN' role
        .antMatchers("/user/**").hasAnyRole("USER", "ADMIN") // '/user/**' for 'USER' and 'ADMIN'
        .anyRequest().authenticated()
        .and()
        .formLogin();
}
```

- Custom Access Denied Page
	- Dev Process
		1. Configure custom page access denied
``` Java
@Override
protected void configure(HttpSecurity http) throws Exception {
    http
        .exceptionHandling()
        .accessDeniedPage("/access-denied"); // Custom access denied page URL
}
```
