# GitHub Pages

If you have ever created a "site" before using HTML, maybe with CSS and perhaps Javascript, and wondered how you could host it online through a link, here's your solution.

From the [GitHub docs](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages):

> GitHub Pages is a static site hosting service that takes HTML, CSS, and JavaScript files straight from a repository on GitHub, optionally runs the files through a build process, and publishes a website.

In other words, it is a **free static website host.** It's reliable, your pages will remain up forever (unless GitHub changes this), and can handle a reasonable amount of bandwidth (100GB/mo), given you aren't serving images or large files.

**Note:** Free for public repositories. You need [GitHub Pro](https://github.com/settings/billing/summary) if you want to do this for private repositories. The deployed "page" will be public but your repo will remain private. Students should be able to get Pro for free.

## Caveats

Many people use GitHub Pages to host blogs and personal portfolios. You can also host web applications, although I would only suggest using it for lightweight stuff -- mainly, things that would be **read**, not **written.** In other words, I **would not** use GitHub Pages as a substitute for Google Forms, even though you could still do that. **GitHub Pages is not a backend host; you'll need a separate backend for that.** Also, using routing with frameworks like React may be a bit more difficult. There are other great alternatives that you can find in this wiki, such as [Vercel](https://vercel.com/), [Render](https://render.com/), and so on, being platforms that are able to host web apps and backends as well.

**Beware:** [GitHub doesn't like using people using pages for](https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#prohibited-uses) commercial use or to handle sensitive data.

## Getting started - Deploying a static HTML site

Here's a quick overview on **how to deploy a simple, static HTML site.** It's simple, but it can be hard to remember clearly, so feel free to use this as a reference every time you do so.

1. Create a new GitHub repository.
2. Add your HTML/CSS/JS files to your GitHub repository and commit it.
   1. You should name your HTML file `index.html` -- that's the "home" page.
   2. Other than that, if your CSS/JavaScript works on your machine if you were to clone this repo, it should also work on GitHub Pages.
3. Go to your repository settings.
4. Navigate to Pages in the repository's settings.
5. Choose a branch you want to deploy your page to (it should say `None` by default`). **The moment you select your branch and hit save, GitHub Pages will be enabled and will start deploying.** It should take between 1-2 minutes. This point onwards, your GitHub page will update every time you commit something to the repository.

Your site by default will have this URL:

```
<your_GitHub_username>.github.io/<repository_name>/
```

By default, `index.html` will show up.

To access another file in your repository, your URL would be:

```
<your_GitHub_username>.github.io/<repository_name>/<path_to_file>
```

For example, if my GitHub username was `user`, my repo name was `repo`, and my repository had these files:

```
somerandomfolder/a.html
contact.html
index.html
styles.css
```

Then the links to these files would be, respectively:

```
https://user.github.io/repo/somerandomfolder/a.html
https://user.github.io/repo/somerandomfolder/contact.html
https://user.github.io/repo/somerandomfolder or user.github.io/repo/somerandomfolder/index.html
https://user.github.io/repo/somerandomfolder/styles.css
```

## Deploying a React Project

As simple as [following this tutorial](https://create-react-app.dev/docs/deployment#github-pages), from create-react-app, a well-known tool for, well, creating a React app.

If you want routing, follow [this](https://www.freecodecamp.org/news/deploy-a-react-app-to-github-pages/). This involves making changes to your React project, so don't worry about touching GitHub for this.

Maybe you might want to [automate the process with GitHub actions?](https://github.com/marketplace/actions/deploy-react-to-github-pages)

**NOTE:** Please don't use this for Next.js projects; Vercel's already got you.

## Deploying an Angular Project

- [Angular has a similar CLI tool for deploying projects to GitHub Pages.](https://github.com/angular-schule/angular-cli-ghpages)

- [Want to automate this?](https://github.com/marketplace/actions/angular-deploy-gh-pages-actions)

## Will I ever run out of bandwidth?

There's a 100GB monthly *soft* bandwidth limit. That's the amount of data that can be transferred from GitHub to users accessing the site until GitHub starts getting a bit upset -- GitHub won't take your site down right away, but they'll try contacting you first. Beware that images are orders of magnitude larger than HTML code or plain text.
