# Set up
- There are many different libraries and frameworks you can use for social logins. For Django there is all-auth, for example. This guide will assume you have already chosen a framework/library and have set it up correctly on your side.
- After logging into Salesforce, in the top right corner, click on the gear icon and go to the SetUp page.
- Search "App" on the left hand searchbar in the Setup menu, and go to App Manager.
- Click on "New Connected App".
- Put in your details like Connected App Name, Email, etc. 
- Enable Oauth Settings 
- Provide your callback URI. The callback URI is the link Salesforce will redirect users to after users have successfully logged in. It needs to be HTTPS secure.
- Provide your scopes. Full Access is recommended for initial developmental purposes, but should be restricted down to only the necessary scopes in the future. (api), (openid), and (refresh_token) are the minimal scopes you may want.
- The OAuth settings are very customisable. This guide recommends disabling PKCE if you are in a time crunch as it adds another layer of complexity to the social login.
- Select configure ID token. In the ID Token Audiences, put in the domain of where your deployed app is hosted.
- Below are examples of what a basic conencted app might look like:
  
<img width="1135" alt="Screen Shot 2023-11-18 at 9 10 40 AM" src="https://github.com/MinGi-K/learning-software-engineering.github.io/assets/64427415/694a1f79-856b-4fd3-9901-c1deec814c9c">

<img width="888" alt="Screen Shot 2023-11-18 at 9 06 36 AM" src="https://github.com/MinGi-K/learning-software-engineering.github.io/assets/64427415/45c51f59-7490-49a6-bcfa-d9433348ef4d">

After creating the Connected App, navigate to your app Manage Connected Apps. You will see an option to get Consumer Key and Secret, which you can inject into your project. Now users can log into your application with their Salesforce credentials, and you can API calls to Salesforce by sending the access token you receive from Salesforce after successful user login in the credentials of the API request.
