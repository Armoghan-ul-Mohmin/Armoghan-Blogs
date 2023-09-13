---
title: "Website Starter Template"
date: 2023-09-13T18:10:21+05:00
image:
summary: "A basic website starter template using Gulp and Sass."
showReadingTime: false
tags: ['gulp']
categories: ['Template' , 'Tutorial']
series: ['Frontend Developement']
series_order: 5
showComments : false
newsletter : true
draft : false
---

A basic website starter template using Gulp and Sass for building and managing your web project.

## Features

- Compiles Sass to CSS with autoprefixing, minification, and sourcemaps.
- Concatenates and minifies JavaScript files.
- Optimizes images for the web.
- Removes unused CSS rules with PurgeCSS.
- Copies HTML, JavaScript, and image files to the `public` folder.
- Auto-refresh with BrowserSync during development.

## Prerequisites

Before you begin, ensure you have met the following requirements:

- Node.js and npm (Node Package Manager) installed on your system.

## Installation

1. Clone the repository to your local machine:

{{< github repo="Armoghan-ul-Mohmin/Website-Starter" >}}

```bash
   git clone https://github.com/Armoghan-ul-MohminWebsite-Starter.git
```
2. Navigate to the project directory:

```bash
   cd Website-Starter
```
3. Install project dependencies:
```bash
  npm install
```

## Folder Structure
The project has the following folder structure:

*`` public/``: This is the output folder where the compiled and optimized files are generated. This is the folder you would deploy to a web server.
* ``src/``: This is the source folder where you'll work on your project.
* ``scss/``: Write your styles in Sass. This is where you'll find the SCSS files.
*`` assets/``: This folder contains your JavaScript files and images.
    * ``js/``: Add your JavaScript files here.
    * ``images/``: Place your images here.
* ``**/*.html``: Create your HTML files here.
## Usage
### Development
To start a development server with auto-refresh, run the following command:
```bash
npm start
```
This will compile Sass, watch for changes in your HTML, JavaScript, and image files, and open a live preview in your browser. Access the development server at [http://localhost:3000](http://localhost:3000).

### Build
To create a production-ready build of your project, run:
```bash
npm run build
```
This will compile and optimize your code, including minifying CSS and JavaScript, removing unused CSS rules, and copying necessary files to the public folder.

## Customization
You can customize the project by editing the following directories and files:

* ``src/scss/``: Write your styles in Sass.
* ``src/assets/js/``: Add your JavaScript files.
* ``src/assets/images/``: Place your images here.
* ``src/**/*.html``: Create your HTML files.

## Additional Details
* **Browser Compatibility**: The included CSS is compatible with modern browsers and Internet Explorer 11.
* **Responsive Design**: The template uses a responsive design approach, ensuring your site looks great on various screen sizes.
* **Performance**: The build process optimizes your assets for performance, including image compression and minification of CSS and JavaScript.
* **Version Control**: We recommend using a version control system like Git to track changes in your project.

## Acknowledgments
* [Gulp](https://gulpjs.com/)
* [Sass](https://sass-lang.com/)
* [PurgeCSS](https://purgecss.com/)
* [BrowserSync](https://www.browsersync.io/)

## Contact

If you have any questions, feedback, or need assistance, please feel free to [open an issue](https://github.com/Armoghan-ul-Mohmin/Website-Starter/issues) on GitHub or simply leave a comment below. We welcome your contributions and feedback!

---

Happy coding! 🚀