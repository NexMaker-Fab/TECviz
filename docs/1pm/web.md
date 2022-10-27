
# Introduction
   
[the main tutorial](https://www.nexmaker.com/doc/1projectmanage/github&docsify.html)
# Steps
  
## Install `docsify`
+ Enter the following in the command terminal: ``` npm i docsify-cli -g```
- You need to create a project folder first, here I use the folder cloned from `github repository`[Tutorial step2](https://www.nexmaker.com/doc/1projectmanage/github&docsify.html).  
- Then Enter the `cd` command into the folder path in `cmd.exe`. You can also drag the folder into the exe, and it will automatically generate the path, as shown in the following figure. 
>![](image link)

## Install `node.js`
Before installing `docsify`, we need to install the `npm` package manager, and the installation of `node.js` will automatically install `npm`.
### Installation  
- Download the installation program from [the official website](https://nodejs.org/en/).  
- Double click the downloaded exe to install it.Next step is the next step until it is completed.
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
![](image link)
Then opern browser to visit http://localhost:3000, you will get a initial website.   
What i want to emphasize is that :  
You need to hang a cmd service to modify the document before it can be updated to the website.

## Image upload Service
We use picgo+github to load images.
- The tutorial is at this [link](https://www.nexmaker.com/doc/1projectmanage/imageuploadservice.html).  
What i want to emphasize is 2 points.  
1.In the step to generate a new token ,the following boxes must be chosen, otherwise the images cannot be uploaded.  
image  
2.When the token has been generated, you must copy the token at time, otherwise the token would not be found again.

# Setting up `index.html`
Copy the following code into `index.html` for overwriting
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