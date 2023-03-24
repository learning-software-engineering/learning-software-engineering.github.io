# Access to Salesforce API 
[Setup authentication documentation](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm)


## Getting authentication token
After logging into salesforce, at the top right corner, go to:
- setup > apps  > app manager
- look for the name of the app you want to connect with 
- click on the arrow down > view
- under **'API (Enable Oath settings)**, click on **'manage consumer details'** to get the consumer key and consumer secret

<img src='https://blog.coupler.io/wp-content/uploads/2022/02/1-salesforce-api-setup.png' width="175" height="230">

<img src="https://lh4.googleusercontent.com/qs95ISk2oMgxsg2jRGc34XGL7XlCigtrhLlKQHFiFnbHs-R87LPZn7zWPTDxAQkCogPxZtVeXe1quPx3gVl9MRsDZfcHVKZAv9sTUbIHsBJPzpAAUcnr6FFjP5crziQBhzQFTJEp">


<img src="https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiNRkGAZUW-jBmFZWukbBZbfayPEr2e-9uyGEY5GUOeeD22EXYR8PmxtiAHQnJgkwCaBmgpqFwUZKj4rGxPsEoN5hZCiN7J7rGr2AWqAWZVfJ5Okld5Cfnc3ZHewpmH61Lz9hqd4Pb12y1dPLVmeTxJm17PIM003-S9NQqAVcjQokKQmGVMjYOyMVbK/s993/Connected%20App%20Detail%20Page.jpg" width="500">
<br>
<br>

---
## Salesforce Objects and fields
Note: In the database language, salesforce objects refer to tables/entity sets and fields refer to the attributes of the table/entity set.<br><br>
After logging into salesforce, at the top right corner, go to:
- setup > object manager<br>
There will be a list of objects and their respective API name (name of the entity set)
- click on an object > **"Fields & Relationships"** tab to get its fields
<br>
<br>

---
## Querying data from Salesforce

After logging into salesforce, at the top right corner, go to **Developer console** to test queries in the **query editor**.<br>
The query editor uses SOQL - [Salesforce Object Query Language](https://developer.salesforce.com/docs/atlas.en-us.240.0.soql_sosl.meta/soql_sosl/sforce_api_calls_soql_sosl_intro.htm)

<img src="https://www.marksgroup.net/wp-content/uploads/2019/05/console1.png" width="500">

### Image References:
- https://blog.coupler.io/wp-content/uploads/2022/02/1-salesforce-api-setup.png
- https://lh4.googleusercontent.com/qs95ISk2oMgxsg2jRGc34XGL7XlCigtrhLlKQHFiFnbHs-R87LPZn7zWPTDxAQkCogPxZtVeXe1quPx3gVl9MRsDZfcHVKZAv9sTUbIHsBJPzpAAUcnr6FFjP5crziQBhzQFTJEp
- https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiNRkGAZUW-jBmFZWukbBZbfayPEr2e-9uyGEY5GUOeeD22EXYR8PmxtiAHQnJgkwCaBmgpqFwUZKj4rGxPsEoN5hZCiN7J7rGr2AWqAWZVfJ5Okld5Cfnc3ZHewpmH61Lz9hqd4Pb12y1dPLVmeTxJm17PIM003-S9NQqAVcjQokKQmGVMjYOyMVbK/s993/Connected%20App%20Detail%20Page.jpg
- https://www.marksgroup.net/wp-content/uploads/2019/05/console1.png
