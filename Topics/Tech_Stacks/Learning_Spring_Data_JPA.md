# Learning Spring Data JPA
Spring Data JPA is a powerful tool that simplifies data access in Java applications by providing a higher-level abstraction for working with relational databases. It offers a streamlined approach to managing entities and their relationships, allowing developers to focus on business logic rather than boilerplate database code. With Spring Data JPA, you can easily perform CRUD operations, define custom queries, and leverage advanced features such as pagination, sorting, and locking. Whether you're building a small-scale application or a large enterprise system, Spring Data JPA empowers you to efficiently interact with the database, reducing development time and maintenance overhead.

This article is a step-by-step guide walking you through the process of building a 
Spring Boot application which stores and retrieves objects in a relational 
database. We will compare different options for working with databases in 
Java, specifically, Java Database Connectivity (JDBC), Spring JDBC, Java 
Persistence API (JPA), and Spring Data JPA. Don't worry if you find them 
confusing, by the end of this guide, you will understand their 
differences and appreciate the simplicity brought by Spring Data JPA.

This guide assumes you understand the fundamentals of the Spring 
Framework and the Spring Boot project (i.e., the concepts of dependency injection, 
IoC container, and annotations like `@Component`, `@Autowired`). 

Make sure you have installed an [IDE](https://www.jetbrains.com/idea/download), [Java 17+](https://www.oracle.com/java/technologies/downloads/), and [Maven 3.5+](https://maven.apache.org/download.cgi) on your machine.

## Table of Contents
* [Step 1 - Initializing A Spring Boot Application](#step-1---initializing-a-spring-boot-application)
* [Step 2 - Launching H2 Console and Creating Person Table in H2](#step-2---launching-h2-console-and-creating-person-table-in-h2)
* [Step 3 - Storing and Deleting Data Using Spring JDBC](#step-3---storing-and-deleting-data-using-spring-jdbc)
* [Step 4 - Storing and Deleting Data Using JPA](#step-4---storing-and-deleting-data-using-jpa)
* [Step 5 - Storing, Deleting, and Retrieving Data Using Spring Data JPA ](#step-5---storing-deleting-and-retrieving-data-using-spring-data-jpa)
* [Summary Graph](#summary-graph)
* [Further Reading](#further-reading)


## Step 1 - Initializing A Spring Boot Application
You can use this [pre-initialized project](https://start.spring.io/#!type=maven-project&language=java&platformVersion=3.2.0&packaging=jar&jvmVersion=17&groupId=com.learning-software-engineering&artifactId=learning-spring-data-jpa&name=learning-spring-data-jpa&description=Demo%20project%20for%20Spring%20Data%20JPA%20&packageName=com.learning-software-engineering.learning-spring-data-jpa&dependencies=data-jdbc,data-jpa,h2,web) and click Generate to download a ZIP file, unzip it and open the project folder in your IDE.
## Step 2 - Launching H2 Console and Creating Person Table in H2
The [H2 Database](https://www.h2database.com/html/main.html) is a Java SQL database. It is very fast, open source, light weight and great for learning purposes. It is an in-memory database, meaning that every time you stop your application, the data stored in H2 during the runtime is discarded. We will utilize its browser-based console to inspect our database table. (We use H2 for its simplicity, if you want to learn more about working with a persistent database, read [this](https://www.baeldung.com/java-connect-mysql).)  

- Configure the H2 Console by copying the following code into `application.properties` under folder `src/main/resources`
```properties
spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:testdb
```

- Create a file named `schema.sql` under `src/main/resources`
- Create a SQL table `Person` by adding the following SQL into `schema.sql`
```SQL
CREATE TABLE Person(
    id BIGINT NOT NULL,
    first_name VARCHAR(255) NOT NULL,
    last_name VARCHAR(255) NOT NULL,
    PRIMARY KEY(id)
);
``` 
- Launch the Spring Boot Application by running the main method of the `LearningSpringDataJpaApplication` class under the folder `src/main/java/com/learningsoftwareengineering/learningspringdatajpa`
- Open [H2 Console](http://localhost:8080/h2-console) in your browser. Copy `jdbc:h2:mem:testdb` and paste it into the field JDBC URL of the Login form. Click on Connect. 
You should be able to see a `Person` table is created in the database, click on Run to see its columns. 
  ![H2 Console Screenshot](https://github.com/learning-software-engineering/learning-software-engineering.github.io/blob/springdatajpa/Topics/Tech_Stacks/Learning_Spring_Data_JPA_Graphics/img.png)

## Step 3 - Storing and Deleting Data Using Spring JDBC
Now, let's add a few entries to the `Person` table and then delete an entry based on its id.

In the folder `src/main/java/com/learningsoftwareengineering/learningspringdatajpa`, create the following files and then rerun the application:
-   `Person.java`
```java
public class Person {
    private Long id;
    private String firstName; 
    private String lastName;
    /* Note that we don't need to use the same name for a java field and a table column
     * instead, we're following java's naming convention here and sql's convention in schema.sql
     */
    
    public Person(Long id, String firstName, String lastName) {
        this.id = id;
        this.firstName = firstName;
        this.lastName = lastName;
    }
    // getters for all fields 
    public Long getId() {
        return id;
    }

    public String getFirstName() {
        return firstName;
    }

    public String getLastName() {
        return lastName;
    }

}
```
- `PersonSpringJdbcRepository.java` 
```java
/* @Repository is an annotation more specific than the generic @Component.
 * it indicates the annotated class talks to the database to manipulate data
 */
@Repository
public class PersonSpringJdbcRepository {
    @Autowired // field dependency injector 
    private JdbcTemplate springJdbcTemplate;
    // We need to write SQL queries 
    private static final String INSERT_QUERY =
        """
            INSERT INTO Person (id, first_name, last_name)
            VALUES(?, ?, ?)
        """;
    private static final String DELETE_QUERY =
        """
            DELETE FROM Person
            WHERE id = ?
        """;

    public void save(Person person){
        springJdbcTemplate.update(INSERT_QUERY, person.getId(), person.getFirstName(), person.getLastName());
    }
    public void deleteById(Long id){
        springJdbcTemplate.update(DELETE_QUERY, id);
    }
}
```
- `PersonCommandLineRunner.java`
```java
@Component
// The run method will be invoked immediately after launching this Spring Boot app
public class PersonCommandLineRunner implements CommandLineRunner {
    @Autowired
    private PersonSpringJdbcRepository repository;
    @Override
    public void run(String... args) throws Exception {
        // populate the table with a few rows
        // stop and rerun the app, open H2 Console to see the populated table
        repository.save(new Person(1L, "Umberto",  "Eco"));
        repository.save(new Person(2L, "Conan", "Doyle"));
        repository.save(new Person(3L, "Agatha", "Christie"));
        repository.save(new Person(4L,"Miyuki", "Miyabe"));
        // uncomment the code below, stop and rerun the app,
        // open H2 Console to see Conan Doyle removed from the table
        // repository.deleteById(2L);

    }
}
```
### Comparison of JDBC and Spring JDBC
JDBC stands for Java Database Connectivity. It is an API that provides Java methods to interact with databases. Spring JDBC is a part of the Spring Framework that simplifies the use of JDBC. It provides a higher-level ***abstraction*** to work with the JDBC API, making database operations easier and more efficient. For example, we only need one line of code to implement the `deleteById` method using Spring's `JdbcTemplate`
```java
public void deleteById(Long id){
        springJdbcTemplate.update("DELETE FROM Person WHERE id=?", id);
    }
```
while we need much more boilerplate code when using plain JDBC.
```java 
public void deleteById(int id) {
        PreparedStatement st = null;
        try {
            st = db.conn.prepareStatement("DELETE FROM Person WHERE id=?");
            st.setInt(1, id);
            st.execute();
        } catch (SQLException e) {
            logger.fatal("Query Failed : ", e);
        } finally {
            if (st != null) {
                try {st.close();}
                catch (SQLException e) {}
            }
        }
}
```
However, Spring JDBC still require us to write SQL queries, which can be cumbersome and error-prone. That's where JPA comes in.

## Step 4 - Storing and Deleting Data Using JPA
JPA stands for Java Persistence API. It is a Java ***specification*** (a kind of interface) for managing relational data in applications. JPA provides a way to map Java objects to database tables and vice versa. We write pure Java while JPA's `EntityManager` takes care of SQL for us. Hibernate is one of the most popular ***implementation*** of JPA. 

Let's see JPA in action. 
- Delete the database script `schema.sql` under `src/main/resources`. We don't need this file anymore. JPA will create a table for us based on `Person.java`.
- Modify `Person.java` to add a few annotations and a default constructor
```java
/* Note we import from jakarta.persistence instead of Hibernate
 * This is because Hibernate is just one implementation of JPA
 * and we don't want to lock into Hibernate
 */
import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.Id;

@Entity 
/* @Entity indicates the annotated class is mapped to a database table
 * use @Entity(name="Another_name") if the db table has another name
 */
public class Person {
    @Id // indicate this field is used as the primary key in the db table
    private Long id;
    /* if you don't use @Column.name = "first_name" to overwrite the field name
     * JPA will automatically convert this field name into a column name: first_name_in_spanish
     */
    @Column(nullable = false, name = "first_name")
    private String firstNameInSpanish;
    @Column(nullable = false)
    private String lastName;

    // The default constructor exists only for the sake of JPA. You do not use it directly
    protected Person(){}

    // all-arg constructor and getters are the same as in the last step
    public Person(Long id, String firstName, String lastName) {
        this.id = id;
        this.firstNameInSpanish = firstName;
        this.lastName = lastName;
    }

    public Long getId() {
        return id;
    }

    public String getFirstName() {
        return firstNameInSpanish;
    }

    public String getLastName() {
        return lastName;
    }

}
```
- create `PersonJpaRepository.java` under `src/main/java/com/learningsoftwareengineering/learningspringdatajpa`
```java
@Repository
@Transactional // DON'T FORGET TO ADD @Transactional!
public class PersonJpaRepository {
    @Autowired
    private EntityManager entityManager;
    
    // we can directly perform database operations by calling the 
    // EntityManager's methods without worrying about SQL syntax details
    public void save(Person person){
        entityManager.merge(person);
    }

    public void deleteById(Long id){
        Person person = entityManager.find(Person.class, id);
        entityManager.remove(person);
    }
}
```
- Modify one line of code in `PersonCommandLineRunner.java` to use the new `PersonJpaRepository` class
```java
@Autowired
//  private PersonSpringJdbcRepository repository;
private PersonJpaRepository repository;

```
- Restart the application. Refresh the H2 Console to see the table `Person` is created and populated. 

## Step 5 - Storing, Deleting, and Retrieving Data Using Spring Data JPA 
Spring Data JPA is a higher-level ***abstraction*** of JPA, making it even simpler to work with databases. Spring Data JPA *automatically* generates the necessary boilerplate code for common database operations. This means that you don't even need to write any code for common methods like `save`, `findById`, `findAll`, `deleteById`, etc.! All you need to do is to create an interface that extends `JpaRepository` interface. 
- create `PersonSpringDataJpaRepository.java` under `src/main/java/com/learningsoftwareengineering/learningspringdatajpa`
```java
@Repository
// Note this is an interface instead of a class !!!
public interface PersonSpringDataJpaRepository extends JpaRepository<Person, Long> {
    // you don't need to implement anything
}
```
- Modify one line of code in `PersonCommandLineRunner.java` to use the new `PersonSpringDataJpaRepository` interface
```java
@Autowired
private PersonSpringDataJpaRepository repository;
```
- Restart the application. Open the H2 Console to check the `Person` table. 
- You can define customized methods by adding their function signatures (no implementation needed) to the `PersonSpringDataJpaRepository` interface and Spring Data JPA will implement them for you in the background. For example
```java
@Repository
public interface PersonSpringDataJpaRepository extends JpaRepository<Person, Long> {
    List<Person> findByLastName(String lastName);
}
```
- Add a `toString` method to the `Person` class to inspect the retrieved data
```java
@Override
    public String toString() {
        return "Person{" +
                "id=" + id +
                ", firstNameInSpanish='" + firstNameInSpanish + '\'' +
                ", lastName='" + lastName + '\'' +
                '}';
    }
```
- Play with various standard or customized methods in `PersonCommandLineRunner.java`. For example
```java
            // inside the run method body
            // add another person with the last name Eco
            repository.save(new Person(5L, "Ellery", "Eco"));
            // get every person with the last name Eco 
            System.out.println(repository.findByLastName("Eco"));
            // retrieve all persons in the db
            System.out.println(repository.findAll());
```
## Summary Graph
![Summary](https://github.com/learning-software-engineering/learning-software-engineering.github.io/blob/springdatajpa/Topics/Tech_Stacks/Learning_Spring_Data_JPA_Graphics/img_1.png)
## Further Reading
1. [Accessing Data with JPA by ](https://spring.io/guides/gs/accessing-data-jpa/): Spring's official Getting Started Guide for Spring Data JPA
2. [Spring Boot Reference Documentation](https://docs.spring.io/spring-boot/docs/3.0.0-M3/reference/htmlsingle/#data.sql): You can read section 9.1.1-9.1.5 for further information related to this guide.
3. [Connect Java to a MySql Database](https://www.baeldung.com/java-connect-mysql): read this if you want to work with a persistent database like MySql.

