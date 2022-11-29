# TEAM INTRODUCTION
* Team Members

  * [PETER MULENGA](intro/team/peter.md)
  * [SAFIN RAHMAN](intro/team/safin.md)
  * [AZAD MD TARIQUZZAMAN](intro/team/azad.md)
  * [AMIR UBED](intro/team/amir.md)
  * [DEAN LUBILO](intro/team/dean.md)
  * [JEFFREY](intro/team/jeffrey.md)


# INTRODUCTION
We used Docsify to write our website using the Markdown language Format and Github to build and deploy the page. Before we could do this, we first installed Microsoft visual Code, Git, Github Desktop and then created an account on github to manage and maintain the page. A repository was made for the group to effectively collaborate and maintain the flow of information.
![alt text](https://i.ibb.co/wRbHbSM/Image-1.png)
![alt text](https://i.ibb.co/bWd0msG/Image-2.png)
![alt text](https://i.ibb.co/n31jsp3/Image-3.png)

# Steps
## Preparation
- We created a project folder first, by cloning from the `github repository`.  

?> Installing `docsify`
+ We entered the following in the command terminal: ``` npm i docsify-cli -g```
+ this command installs `docsify-cli` globally, which helps initializing and previewing the website locally.
![alt text](https://i.ibb.co/qpZFw25/Image-4.png)
After typing the code, we had this pop up window
![alt text](https://i.ibb.co/khCBp9s/image-5.png)
magnified
![alt text](https://i.ibb.co/JFHK4sY/image-6.png)
This is due to to absense of node js; so we installed from the main website. 

!> Before installing `docsify`, we need to install the 
`npm` package manager.

To verify that node js is installed type `node -v` in the command terminal, which should display the version number
![alt text](https://i.ibb.co/SsmCT7P/image-7.png)
Install npm by typing `npm install -g npm` into the command terminal
![alt text](https://i.ibb.co/MByWnkT/image-8.png)
In visual studio, type `npm i docsify-cli -g` in the command terminal to install `docsify-cli`.
![alt text](https://i.ibb.co/HPGj2Y4/image-9.png)

 ## Initialize
- Enter the following in command terminal: ```docsify init ./docs```  
- After successful initialization, you can see several files created in the directory：  
  * `index.html`:Entry File.  
  * `README.md`:It will be rendered as the homepage content.  
  * `.nojekyll`: is Used to prevent GitHub Pages from ignoring files that begin with an underscore.

## Web Preview
A plugin called live preview was downloaded in visual code to view the code as we worked and host it on different browers for testing, all from visual studio.
![alt text](https://i.ibb.co/MSZWcC5/image-10.png)

## Image upload Service
- For the [image upload Service](https://petyr.imgbb.com/)
, we used imgbb.com to load images.
Which only required creating a free account on the website and uploading the images.

# Setting up `index.html`
The following code was copied into `index.html`
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>TECviz</title>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <meta name="description" content="Description">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css">
</head>
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
      name: 'PROJECTS',
      repo: '',
      loadSidebar: true,
      loadNavbar: true,
      coverpage: true,
      onlyCover: true,
      search: {
        noData: {
          '/': 'None!'
        },
        paths: 'auto',
        placeholder: {
          '/': 'Search...'
        }
      }
    }
  </script>
  <!-- Docsify v4 -->
  <script src="https://cdn.jsdelivr.net/npm/docsify@4"></script>
  <script src="https://cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>

</body>
</html>

```
The sidebar and its contraction, cover page and search bar will be described in the following steps.

# Setting sidebar
+ In order to have a sidebar, you can create your own _sidebar.md, First, you need to set loadSidebar in the html file to true
+ create `_sidebar.md` 
- Copy the following code into `_sidebar.md` 

```
<!-- 侧边栏 docs/_sidebar.md -->
- **Introduction**
  - [Introduction to Design Engineering](intro/introdesigneng.md)
  - [Team Introduction](1pm/web.md#coverpage)
- **Weekly Homework**
  - [1. Project Management](1pm/web.md)
    - [Introduce team](1pm/web.md)
    - [How we built our webpage](1pm/web.md)
    - [Introduce Final Project](finalproject.md)
  - [2. Computer Aided Design (CAD)](cad/cadprojects.md)
  - [3. 3D Printing](3dprinting/3d.md)
  - [4. Computer Controlled Cutting](computercontrolledcutting/lazercutting.md)

- **Final Project**
  - [Topic](finalproject.md#Topic)
  - [Innovation](finalproject.md#Innovation)
  - [Market](finalproject.md#Market)
  - [Design](finalproject.md#Design)
  - [Manufacturing](finalproject.md#Manufacturing)
  - [SDGs](finalproject.md#SDGs)

```  
> sidebar.md in ms visual code

![alt text](https://i.ibb.co/J3pm6P9/image-11.png)

# Coverpage
- Configure the coverpage parameter in `index.html` to open the coverpage. Usually, the cover page and the first page appear at the same time. After `onlyCover=true` is set, the cover page becomes an independent cover page.  
- Add the profile `_coverpage.md` to configure the coverpage, the code and rendering are as follows:  

```
![logo](_media/icon.svg ':size=20%')  
> Welcome to Design Engineering 2022 
* DESIGN
* ENGINEERING
* BUSINESS
[Github](https://github.com/NexMaker-Fab/2022zjudem-team1/tree/main)
[Course Work](./README.md)
[Project](finalproject.md)

```
> Preview of cover page
>![](https://i.ibb.co/pxth2nP/image-12.png)

# Setting search bar
- Configure search bar in `index.html` as follows  
>![alt text](https://i.ibb.co/xY6Mpbs/image-13.png)

# Setting up the Custom navbar using Markdown
You can create a custom markdown-based navigation file by setting `loadNavbar` to **true** and creating `_navbar.md`, compare [loadNavbar configuration](configuration.md#loadnavbar).

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadNavbar: true
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

```markdown
<!-- _navbar.md -->

* [Home](README.md)
* Team Members
  * [PETER MULENGA](intro/team/peter.md)
  * [SAFIN RAHMAN](intro/team/safin/index.html)
  * [AZAD MD TARIQUZZAMAN](intro/team/azad.md)
  * [AMIR UBED](intro/team/amir.md)
  * [IVAN ALEJAJANDRO BROCHE](intro/team/ivan.md)
  * [DEAN LUBILO](intro/team/dean.md)  
  * [JEFFREY](intro/team/jeffrey.md)
```

!> You need to create a `.nojekyll` in `./docs` to prevent GitHub Pages from ignoring files that begin with an underscore.

!> `_navbar.md` is loaded from each level directory. If the current directory doesn't have `_navbar.md`, it will fall back to the parent directory. If, for example, the current path is `/guide/quick-start`, the `_navbar.md` will be loaded from `/guide/_navbar.md`.

# Reference
-[Docsify](https://docsify.js.org/#/quickstart) Quick start <br>
-[Nexmaker](https://www.nexmaker.com/doc/1projectmanage/github&docsify.html) Course assessment