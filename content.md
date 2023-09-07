# Deploying your personal site at github.io

* Table of Contents
{:toc}

You have already created a couple of project repositories to house static HTML for the ["Hello, World"](https://learn.firstdraft.com/lessons/55-hello-world) and [Link in bio](https://learn.firstdraft.com/lessons/57-linkinbio) lessons.

We saw that those pages were hosted at `https://<your-username>.github.io/hello-world/` and `https://<your-username>.github.io/links/`, respectively. 

But what about that root domain `https://<your-username>.github.io/`? If you try and visit that page now, you will get a 404 page not found error!

Let's turn that page into a new repository that you can use to host your personal website, including links to other pages.

## Generating from a template

As opposed to the majority of class projects, where you will be forking a repository and getting automated feedback with `rake grade`, in this case you will **create a repository from a template**.

You can find more information on this template and [other upcoming templates in this lesson](https://learn.firstdraft.com/lessons/60-appdev-templates). 

- Visit our [appdev-projects/html-template](https://github.com/appdev-projects/html-template) repository and click the "Use this template" button, and select "Create a new repository" from the dropdown:

<!-- ![](/assets/gh-pages-template-1.png) -->
![](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1686161492/gh-pages-template-1_tlxhbl.png)
{: .bleed-full }

- On the next screen, leave the "Owner" dropdown alone, it should be set to _your_ GitHub username.
- For "Repository name", enter "**your-username**.github.io". Substitute your own, real username for **your-username**.
    - So, for example, my repo name would be "raghubetina.github.io", or since I'm signed in as a demo student account here, it would be "bp-demostudent-2.github.io".
    - Make sure to include the ".github.io" part in the repo name.
- Make sure the "Public" option is selected. 
- Click "Create repository from template".

<!-- ![](/assets/gh-pages-template-2.png) -->
![](https://res.cloudinary.com/dmxgp9oq2/image/upload/v1686161704/gh-pages-template-2_cb0m1b.png)
{: .bleed-full }

After a moment you will be brought to the new page at `github.com/<your-username>/<your-username>.github.io`, with a copy of all the code from `appdev-projects/html-template`.

### This is not a fork

**This is not a fork, this is a newly generated codebase from a template repository.**

What does that mean for us practically?

* Just like a fork, the template generated repo contains a snapshot of all of the code in the repository you generated the template from.
* The template generated code is not tied to the upstream forked repository, meaning that changes to the upstream fork (i.e. commits) cannot be easily fetched into the new codebase.
* Creating Codespaces from the template generated repo [will use your free monthly Codespace hours](https://learn.firstdraft.com/lessons/60-appdev-templates#a-note-about-codespace-hours).
* Template generated code is not graded, so `rake grade` won't be necessary. The templates are just there for you to have fun with and build your own apps!

## The usual steps to deploy on GitHub Pages

As before, you will also need to [enable GitHub Pages](https://learn.firstdraft.com/lessons/55-hello-world#enable-github-pages-deployment), on the `github.com/<your-username>/<your-username>.github.io` repository that you just created.

With GitHub Pages setup, you can go ahead and begin adding content to your `<your-username>/<your-username>.github.io` repository in a fresh Codespace.

* open the live preview with `bin/dev`

* create an `index.html` file

* put the following into that file (just a suggestion to get you started):

```html
<h1>My personal page</h1>

<div>
  <a href="/links">Link in bio</a>
</div>

<div>
  <a href="/hello-world">Hello, World!</a>
</div>
```

* commit, push, and wait for deployment, then visit `https://<your-username>.github.io/`.

Presto! You now have a repository associated with the root URL of your domain. You can put whatever you want into this repo; treat it as your personal static HTML website that anyone on the internet can visit.

## Custom Domains

If you want to use a custom domain name like `yourname.com` rather than something like `<your-username>.github.io`, then you'll first have to purchase a domain.
  - I recommend [Porkbun](https://porkbun.com/), or, for more exotic top-level domains, [Gandi.net](https://www.gandi.net/en). 
  - [Here is a guide to adding your own domain to your Pages site](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site). Let me know if you get stuck.

## Addendum: Serving Other File Formats and Multiple Repositories

By default, GitHub Pages will deploy the repository `<your-username>/<your-username>.github.io` to the domain `https://<your-username>.github.io` and any files or HTML pages in the root of the repository will be found at e.g. `https://<your-username>.github.io/index` for an `index.html` file.

But what if: 

* you have another version of a file that you wanted to show, like `index.html` _and_ `index.json`, or
* you have another _different_ GitHub repository with some static HTML that you would also like to deploy and show off the contents of at your `https://<your-username>.github.io` domain?

Let's see how both cases work.

### Serving Other File Formats

What if you wanted to serve multiple versions of the same page on your static site, say at the URL `https://<your-username>.github.io/index`? 

For instance you had an `index.html` file and another `index.json` file, perhaps because you wanted the JSON version of the file as a nice API endpoint.

In that case, if you navigated to `https://<your-username>.github.io/index`, then you would only be shown the `index.html` file. It turns out that Pages automatically looks for an `.html` file with that name, so that you don't need to explicitly navigate to that file type!

And if you want to reach the JSON version, you just need to explicitly navigate to that other file, _including the file extension_: `https://<your-username>.github.io/index.json`.

### Serving Multiple Repositories

We already have experience with this from the "Hello, World" and "Link in bio" exercises, but let's make those findings explicit in this section.

Let's say you created another template repository from [appdev-projects/html-template](https://github.com/appdev-projects/html-template) with some different content for your portfolio, and you want to deploy this new repository to your domain.

1. From `appdev-projects/html-template`, you selected "Use this template" button, and "Create a new repository".

2. You gave the repository a different name under your personal GitHub account, let's say `my-cool-project`. (You can't have two repositories with the same name in your personal account, so `<your-username>.github.io`, `hello-world`, and `links` would be unavailable.)

3. You added some static website content in `my-cool-project`, like an `index.html` page.

4. You navigated to the new `<your-username>/my-cool-project` "Settings" > "Pages" and set "Deploy from a branch" under the "Source" tab, and for the "Branch" you selected `main` and `/(root)`, then clicked "Save".

5. After waiting a minute while the GitHub Action is running, you will see that the page is now deployed at `https://<your-username>.github.io/my-cool-project`. 

6. Visit that URL path on your static GitHub domain and see for yourself, you should see the contents of the `index.html` file from `my-cool-project`. 

In fact, _any_ other files (e.g. `.html`, `.json`, images) that you create and publish on `<your-username>/my-cool-project` would also be served at that domain. If you made a file there called `project_description.html`, then you would find it served at `https://<your-username>.github.io/my-cool-project/project_description`

Aha! So _any_ project that you deploy from your personal project repository will be hosted at the domain `https://<your-username>.github.io`. It's just a matter of deploying the repository from a branch in the settings and then navigating to the correct URL path!

#### Files vs. Repositories

One "gotcha" here: 

* What if you happen to have a page in the original repository `<your-username>/<your-username>.github.io` called `my-cool-project.html`, _and_ you were deploying the separate repository `<your-username>/my-cool-project`?

Well, it turns out that:

* if you navigate to `https://<your-username>.github.io/my-cool-project` (_without the `.html` extension_) then you would see the content of your `<your-username>/my-cool-project` repository, but
* if you navigate to `https://<your-username>.github.io/my-cool-project.html` (_with the `.html` extension_) then you would see the content of your `my-cool-project.html` file from the `<your-username>/<your-username>.github.io` repository.

Perhaps an edge-case, but good to know!
