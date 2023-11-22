# Deploying your personal website using GitHub

### Why should you create a personal website?

A personal website can be a great way to build a more personalized portfolio to showcase your experience, projects, and achievements to potential employers. They give you more flexibility to present your authentic self and personality, and help you establish a personal brand, as opposed to traditional resumes and CVs. As a student, you might want to build a personal website to not only display your achievements, but also to demonstrate your web development skills and gain some practical learning experience. 

If you want to display the same content to every visitor of your site, and you’re looking for a cost-effective solution with lower hosting costs, you might want to opt for a static personal website. However, if you would like to add interactive features like allowing visitors to leave comments on your blog posts that require backend processing, or if you want to experiment with external APIs and databases, a dynamic personal website would be a better choice. 

## Deploying Static Websites

**Prerequisite:** 
Create a [GitHub](https://github.com/) account

**Step 1: Develop your website**

Locally develop your website on your computer. You can use static site generators like [Hugo](https://gohugo.io/), [Jekyll](https://jekyllrb.com/), [Next.js](https://nextjs.org/), or build a simple website using HTML, CSS, and Javascript. Locally test your website and view it using a development server to visualize your website before deployment.

**Step 2: Create a GitHub repository**

Login to GitHub and [create a new repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository) for your website. [Push](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github) your files from your local machine to your new GitHub repository. 

**Step 3: Deploy to Netlify**

- Login to [Netlify](https://app.netlify.com/login) with your GitHub account. Authorize Netlify to access your GitHub account.

<img width="1494" alt="Screenshot 2023-11-22 at 11 19 06 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/52506101/4949b73e-3e81-459e-8e6d-7c8b43d197d5">

- Click `Add new site` from the Netlify dashboard. Click `Import an existing project` and select `Deploy with GitHub.` 

<img width="1206" alt="Screenshot 2023-11-22 at 11 20 55 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/52506101/91bab809-3e24-4c11-80d6-fac1006800fd">

- Select the repository that you pushed your website code to. Click `Deploy Site` and Netlify will deploy your site for you. 

After you’ve deployed, Netlify provides a URL, but you can buy a custom domain and use that instead. You may also benefit from setting up continuous deployment so every time you push changes to your GitHub repository, they will be automatically deployed. 

## Deploying Dynamic Websites

**Prerequisites:**
Create a [GitHub](https://github.com/) account

**Step 1: Develop your website**

Build your dynamic website using a backend framework (ex. Flask, Node.js) and a frontend framework (ex. React) and thoroughly test your website locally using a development server. 

**Step 2: Create a GitHub repository**

Login to GitHub and [create a new repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository) for your website. [Push](https://docs.github.com/en/migrations/importing-source-code/using-the-command-line-to-import-source-code/adding-locally-hosted-code-to-github) your files from your local machine to your new GitHub repository. 

**Step 3: Choose appropriate hosting services**

For dynamic websites, there are hosting services that can deploy both frontend and backend components of your website. Some examples include [Heroku](https://www.heroku.com/), [Amazon Web Services](https://aws.amazon.com/), [Google Cloud Platform](https://cloud.google.com/), and others. However, choosing a separate hosting service for the backend and frontend can offer flexibility and provide you with options for your specific tech stack. 

For this tutorial, consider the following tech stack: Python to handle backend logic, Flask to serve JSON responses to be used by the frontend as well as to interact with MySQL, React for creating the frontend, and MySQL to store data.

**Hosting the React frontend:**
- Run `npm run build` or `yarn build` to compile your React app for production 
- You can use services like [Netlify](https://www.netlify.com/) or [Vercel](https://vercel.com/) (and many others) to deploy the frontend, but for the purposes of this tutorial, we will use Vercel

1. Login to Vercel with your GitHub account.
   
<img width="1486" alt="Screenshot 2023-11-22 at 11 25 07 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/52506101/0ac82ca6-953d-4995-8d42-55f45c3bd1c2">

2. Click `Import Project` on the Vercel dashboard and authorize Vercel to access your GitHub repositories. Choose the repository that you pushed your project to.

<img width="1299" alt="Screenshot 2023-11-22 at 11 26 28 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/52506101/c1e4ba4e-bf6a-4b37-84dc-b0cd84cc3aa6">


3. Vercel will automatically detect the build settings — all you have to do is click Deploy. Vercel will also automatically deploy your changes pushed to your GitHub repository. Note that Vercel provides a URL to access your website, but you can configure it with a custom domain if you have one. 

**Hosting the Python and Flask backend and MySQL server:**

For hosting the backend, we will use [Railway](https://railway.app/). Note that Railway provides a $5 credit to use their services but you may need to sign up for a usage-based subscription to host your Flask backend and MySQL server.

**Python and Flask backend:** 
- Login with GitHub.
- In your dashboard, create a new project and choose the option to ‘Deploy from GitHub repo.’ Connect your GitHub repo that has your project.
  <img width="1430" alt="Screenshot 2023-11-22 at 11 29 36 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/52506101/020f270d-5cc7-4367-9a24-6a8aa8fc9b06"> 
- Specify the root directory to be the directory that has your Flask app (usually a backend folder). 
  <img width="700" alt="Screenshot 2023-11-22 at 11 30 57 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/52506101/b6080193-93f5-4659-9aa8-ad4330e42825">
- Specify the language to build the service as Python. 
  <img width="700" alt="Screenshot 2023-11-22 at 11 31 14 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/52506101/57ffb91a-5fde-4089-99d4-6c608df319b6">

**MySQL server:**
- Go to the dashboard and create a new project. Choose the option to `Provision MySQL.`
  <img width="980" alt="Screenshot 2023-11-22 at 11 35 23 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/52506101/8e8edbaf-4912-4b32-aa32-1914d89a67d4">
- This automatically sets up a MySQL database for you.
  <img width="921" alt="Screenshot 2023-11-22 at 11 35 04 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/52506101/798378db-3eb5-43a5-b67b-0cd0f3de601a">
- Railway will provide you with all the necessary credentials to use your server (ex. Host, port, root username and password, etc). You can then configure your backend project settings to use the necessary environment variables that the Flask app will use to connect to the database (as it is generally not good practice to hardcode them in your backend).
  <img width="837" alt="Screenshot 2023-11-22 at 11 36 06 AM" src="https://github.com/learning-software-engineering/learning-software-engineering.github.io/assets/52506101/f65ea32c-110c-4875-9ae4-b18c41f586ae">

**Troubleshooting on Vercel and Railway**
A convenient benefit of using services like Vercel and Railway for deployment is that you can review the deployment logs in their respective dashboards to view error messages. In Railway, you can view both build logs and deployment logs for your backend to trace where your issue may be. 
