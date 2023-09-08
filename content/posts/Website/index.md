---
title: "How I Setup My Website"
date: 2023-09-08T13:42:05+05:00
image: 
summary: "This shows you have I automate my workflows and setup my website for maximum productivity and search The best part is th"
showReadingTime: true
tags: ['Hugo' , 'Static Site']
categories: ['Website']
series: []
showComments : true
newsletter : true
draft : false
---

This shows you have I automate my workflows and setup my website for maximum productivity and search.

The best part is this is FREE and will produce a website faster than anything on the web. 

## Prerequisites
Before you begin this tutorial you must
1. [Install Hugo](https://gohugo.io/installation/)
2. [Install Go](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
   
 {{< alert "none" >}}
**Note!** You must also be comfortable working from the command line.
{{< /alert >}}

## Create a site

### Commands 

{{< timeline >}}

{{< timelineItem icon="none" header="If you are a Windows user"  footer="" >}}

<ul>
<li> Do not use the Command Prompt.</li>
<li> Do not use Windows PowerShell</li>
<li> Run these commands from <a href="https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows" target="_blank">PowerShell</a> or a Linux terminal such as WSL or Git Bash</li>
</ul>
PowerShell and Windows PowerShell <a href="https://learn.microsoft.com/en-us/powershell/scripting/whats-new/differences-from-windows-powershell?view=powershell-7.3" target="_blank">are different applications</a>.
{{< /timelineItem >}}
{{< /timeline >}}

Run these commands to create a Hugo site with the [Blowfish](https://github.com/nunocoracao/blowfish.git) theme. The next section provides an explanation of each command.

``` bash
hugo new site quickstart
cd quickstart
git init
git submodule add https://github.com/nunocoracao/blowfish.git themes/blowfish
echo "theme = 'blowfish'" >> hugo.toml
hugo server
```

### Explanation of commands

Create the [directory structure](https://gohugo.io/getting-started/directory-structure) for your project in the **quickstart** directory.

1. Create New Hugo Project.
``` bash
hugo new site quickstart
```

2. Change directory to your project.
``` bash
cd quickstart
```
3. Innitialize Git Repo.
``` bash
git init
```
4. Clone the Blowfish theme into the themes directory, adding it to your project as a Git submodule..
``` bash
git submodule add https://github.com/nunocoracao/blowfish.git themes/blowfish
```
5.  Append a line to the site configuration file, indicating the current theme.
``` bash
echo "theme = 'blowfish'" >> hugo.toml
```
6. Start Hugo’s development server to view the site.  
``` bash
hugo server
```

{{< alert icon="none" >}}
 View your site at the URL displayed in your terminal. Press <strong>Ctrl + C</strong> to stop Hugo’s development server.
{{< /alert >}}

## Add content
Add a new page to your site.

```bash
hugo new content posts/my-first-post.md
```

Hugo created the file in the ``content/posts`` directory. Open the file with your editor.

```toml
---
title: "My First Post"
date: 2023-09-08T13:42:05+05:00
draft: true
---
```

Notice the ``draft`` value in the [front matter](https://gohugo.io/content-management/front-matter) is ``true``. By default, Hugo does not publish draft content when you build the site. Learn more about [draft, future, and expired content](https://gohugo.io/getting-started/usage/#draft-future-and-expired-content).

Add some [markdown](https://commonmark.org/help/) to the body of the post, but do not change the ``draft`` value.

``` markdown
---
title: "My First Post"
date: 2022-11-20T09:03:20-08:00
draft: true
---
## Introduction

This is **bold** text, and this is *emphasized* text.

Visit the [Hugo](https://gohugo.io) website!
```

Save the file, then start Hugo’s development server to view the site. You can run either of the following commands to include draft content.

```bash
hugo server --buildDrafts
hugo server -D
```

View your site at the URL displayed in your terminal. Keep the development server running as you continue to add and change content.

## Configure the site
With your editor, open the[ site configuration](https://gohugo.io/getting-started/configuration/) file ``(hugo.toml)`` in the root of your project.

```toml
baseURL = 'http://example.org/'
languageCode = 'en-us'
title = 'My New Hugo Site'
theme = 'blowfish'
```
Make the following changes:

1. Set the ``baseURL`` for your production site. This value must begin with the protocol and end with a slash, as shown above.
2. Set the ``languageCode`` to your language and region.
3. Set the ``title`` for your production site.

Start Hugo’s development server to see your changes, remembering to include draft content.

```bash
hugo server -D
```

{{< alert icon="none" >}}
 Most theme authors provide configuration guidelines and options. Make sure to visit your theme’s repository or documentation site for details.
{{< /alert >}}

## Publish the site 
In this step you will publish your site, but you will not deploy it.

When you publish your site, Hugo creates the entire static site in the ``public`` directory in the root of your project. This includes the HTML files, and assets such as images, CSS files, and JavaScript files.

When you publish your site, you typically do not want to include [draft, future, or expired content](https://gohugo.io/getting-started/usage/#draft-future-and-expired-content). The command is simple.  

```bash
hugo
```

To learn how to deploy your site, see the [hugo hosting and deployment](https://gohugo.io/hosting-and-deployment/) section.