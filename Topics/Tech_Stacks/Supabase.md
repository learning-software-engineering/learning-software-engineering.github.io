# Using Supabase with Vue.js

[Supabase](https://supabase.com) is an open source [Firebase](https://firebase.google.com/) alternative for building secure and high-performance PostgreSQL backends. It provides developers with a wide array of tools, such as real-time database configuration, authentication, and storage.

### Why use Supabase?

- As an open-source product, Supabase grants flexibility and control over your data and applications.
- Supabase provides an excellent UI that gives you a centralized view of your application’s data, authentication settings, APIs, etc. The dashboard is very user-friendly, which gives a great deal of control to developers of all experience levels.
- Supabase provides [extensive documentation](https://supabase.com/docs) to help you get started with the platform and make the most of its features.

### About this Guide

This document will include

- how to set up a basic [Vue.js](https://vuejs.org/) project
- installing Supabase into your Vue.js project
- an example of creating a small database using the Supabase dashboard

## Prerequisites

Before reading this guide, ensure you have [Node.js](https://nodejs.org/en/) and [npm](https://www.npmjs.com/) installed on your machine.

Also, this guide is written with the assumption that the reader has a basic understanding of Vue and PostgreSQL.

## Step 1: Setting Up a Basic Vue.js Project

1. **Create a Vue Project**: You can use the command line interface to create a new Vue.js project.

   ```bash
   npm init vue@latest vue-app
   ```

2. **Navigate to the Directory**: Move into your newly initialized directory.
   ```bash
   cd vue-app
   ```

## Step 2: Installing Supabase JS Client

1. **Install the Supabase Client**: Use npm again to install the Supabase JavaScript client.

   ```bash
   npm install @supabase/supabase-js
   ```

2. **Retrieve your Supabase API Keys**: Access your Supabase project dashboard and retrieve your Supabase URL and API keys (the dashboard is explained later).

## Step 3: Setting Up Supabase in Vue.js

1. **Create the Supabase Client**: create a `/src/lib` directory in your Vue app, and add a file called `supabaseClient.js`.

2. **Initialize Supabase Client**: In your `supabaseClient.js` file, add the following code using the keys you retrieved from the previous step.

   ```javascript
   import { createClient } from "@supabase/supabase-js";

   const supabaseUrl = "YOUR_SUPABASE_URL";
   const supabaseKey = "YOUR_SUPABASE_PUBLIC_KEY";

   export const supabase = createClient(supabaseUrl, supabaseKey);
   ```

3. **Import Supabase into Vue Components**: Import the created `supabase` client in your Vue components wherever you intend to use it.

   ```javascript
   // src/components/TemplateComponent.vue

   <script>
   import { supabase } from './lib/supabaseClient'

   export default {
     mounted() {
       // Supabase methods go here
     }
   }
   </script>
   ```

## Step 4: Use Supabase Methods in Vue Components

Perform database operations using Supabase methods in your Vue components.

```javascript
// src/components/TemplateComponent.vue

<script>
import { supabase } from './lib/supabaseClient'

export default {
  methods: {
    async getData() {
      const { data, error } = await supabase
        .from('table')
        .select('*');

      if (error) {
        console.error('Something went wrong', error.message);
      } else {
        console.log('Fetched data:', data);
      }
    }
  }
}
</script>
```

## Conclusion

Well done! You've successfully integrated Supabase into a simple Vue.js project. The Supabase client has been set up, initialized in Vue, and your Supabase methods are ready to perform database interactions.

To continue discovering what you can achieve with Supabase, dive into the [documentation](https://supabase.com/docs/guides/getting-started/features), or explore advanced topics such as [authentication](https://supabase.com/docs/guides/auth) or [real-time servers](https://supabase.com/docs/guides/realtime).
