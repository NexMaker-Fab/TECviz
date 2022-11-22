# TEAM INTRODUCTION
* Team Members

  * [PETER MULENGA](intro/team/peter.md)
  * [SAFIN RAHMAN](intro/team/safin.md)
  * [AZAD MD TARIQUZZAMAN](intro/team/azad.md)
  * [DEAN LUBILO](intro/team/dean.md)
  * [AMIR UBED](intro/team/amir.md)
  * [JEFFREY](intro/team/jeffrey.md)



# INTRODUCTION
We used Docsify to write our website using the Markup language Format and Github to build and deploy the page. Before we could do this, we first installed Microsoft visual Code, Git and then created an account on github to manage and maintaain the page. A repository was made for the group to effectively collaborate and maintain the flow of information.

# Steps
## Preparation
?> Installing `docsify`
+ We entered the following in the command terminal: ``` npm i docsify-cli -g```
+ this command installs `docsify-cli` globally, which helps initializing and previewing the website locally.

- We created a project folder first, by cloning from the `github repository`.  
- Then Enter the `cd` command into the folder path in `cmd.exe`. You can also drag the folder into the exe, and it will automatically generate the path, as shown in the following figure. 
>![]()

?> Install `node.js`
Before installing `docsify`, we need to install the `npm` package manager, and the installation of `node.js` will automatically install `npm`.

### verification
- Open the `cmd`command line and enter `node -v`.  
- If the node version is displayed, the nodejs installation is successful, as shown in the following figure.  
 ### Initialize
- Enter the following in command terminal: ```docsify init ./docs```  
- After successful initialization, you can see several files created in the directory：  
  - `index.html`:Entry File.  
  - `README.md`:It will be rendered as the homepage content.  
  - `.nojekyll`: is Used to prevent GitHub Pages from ignoring files that begin with an underscore.

### Preview
Enter the following in cmd.exe:``` docsify serve docs```  
You will get the following results.   
![]()
Then opern browser to visit http://localhost:3000, you will get a initial website.   
What i want to emphasize is that :  
You need to hang a cmd service to modify the document before it can be updated to the website.

## Image upload Service
- [image upload Service](https://petyr.imgbb.com/)
We used imgbb.com to load images.
Which only required creating a free account on the website and uploading the images.

# Setting up `index.html`
The following code was copied into `index.html`
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>TEAM ONE</title>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <meta name="description" content="Description">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css">
</head>
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
      name: 'TEAM PROJECTS',
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
  <script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>

</body>
</html>

```
The sidebar and its contraction, cover page and search bar will be described in the following steps.

# Setting sidebar
+ Configure sidebar
>![](image link) 
- The code in the image above modify the `index.html` configuration file to configure the `loadSidebar` option.
+ create `_sidebar.md` 
- Create folders and files as shown in the picture:  
>![](image link)  
- Copy the following code into `_sidebar.md`  
See this link for usage of the `markdown` language: [link](https://www.runoob.com/markdown/md-image.html)  

```
<!-- 侧边栏 docs/_sidebar.md -->
- **Team introduction**
  - [Introduction to Design Engineering](intro/introdesigneng.md)
  - [Team Introduction](team/intro.md)
- **Weekly Homework**
  - [1. Project Management](1pm/guide.md)
    - [-How to build web](1pm/web.md)
    - [-Introduce team](team/intro.md)
    - [-Introduce Final Project](1pm/final.md)
  - [2. Computer Aided Design (CAD)]()
  - [3. Arduino Basic]()
  - [4. 3D Printing]()
  - [5. Computer Controlled Cutting (CNC)]()
  - [6. Open source hardware and Arduino basic]()
  - [7. Interface application programming]()
- **Final Project**
  - [Topic]()
  - [Innovation]()
  - [Market]()
  - [How to Design]()
  - [How to Make]()
  - [SDGs]()
```  
# Coverpage
- Configure the coverpage parameter in `index.html` to open the coverpage. Usually, the cover page and the first page appear at the same time. After `onlyCover=true` is set, the cover page becomes an independent cover page.  
- The code settings in the following figure play such a role:  
>![](image link)  

- Add the profile `_coverpage.md` to configure the coverpage, the code and rendering are as follows:  
```
![logo](_media/icon.svg)

# TEAM ONE  
> Welcome to Design Engineering 2022 
* DESIGN
* INNOVATION
* BUSINESS
[Github](https://github.com/NexMaker-Fab/2022zjudem-team1/tree/main)
[Course Work](./README.md)
[Project](finalproject/finalproject.md)
```
>![](image link of cover page)

# Setting search bar
- Configure search bar in `index.html` as following  
>![](image link)

# Setting up the Custom navbar

## HTML

If you need custom navigation, you can create a HTML-based navigation bar.

!> Note that documentation links begin with `#/`.

```html
<!-- index.html -->

<body>
  <nav>
    <a href="#/">EN</a>
    <a href="#/zh-cn/">简体中文</a>
  </nav>
  <div id="app"></div>
</body>
```

## Markdown

Alternatively, you can create a custom markdown-based navigation file by setting `loadNavbar` to **true** and creating `_navbar.md`, compare [loadNavbar configuration](configuration.md#loadnavbar).

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

* [En](/)
```

!> You need to create a `.nojekyll` in `./docs` to prevent GitHub Pages from ignoring files that begin with an underscore.

`_navbar.md` is loaded from each level directory. If the current directory doesn't have `_navbar.md`, it will fall back to the parent directory. If, for example, the current path is `/guide/quick-start`, the `_navbar.md` will be loaded from `/guide/_navbar.md`.

# INTRODUCTION TO OUR PROJECT
>