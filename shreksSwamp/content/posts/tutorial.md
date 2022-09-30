---
title: "Static Webpage Tutorial"
date: 2022-09-30T16:13:15+06:00
---
## Making a simple yet powerful blog using Hugo and Github pages:
> In this tutorial we will walk you through how to make a simple static webpage using GitHub pages and hugo

Static sites refer to view only webpages. They are widely used for rapid development. Although [Hugo](https://en.wikipedia.org/wiki/Hugo_(software)) can be used to add various functionalities this tutorial will be laser focused on how to get a simple static webpage up and running to display the tutorial assigned to us. 
## Prerequisites and Precautions
- Some knowledge of [git](https://education.github.com/git-cheat-sheet-education.pdf) and the terminal
- This tutorial was made with gnu/Linux in mind. All steps shown have been done on an Arch-Linux 5.19 kernel system. We shall try to accommodate other Linux distros wherever needed. Users of other "special" OSes are requested to figure out the terminal and other platform specific stuff for themselves.
- A very basic knowledge of markdown. see [here]({{< ref "tutorial.md#step-8-adding-content-to-our-post" >}}).
- **Angle brackets shown in commands here are for illustrative purposes. Do not keep the angle brackets when actually running the command.  Replace the entire text bound inside the bracket (along with the brackets) with the parameters specified inside the brackets for your specific case.** One exception being Hugo snippets where it has been specified. 
## Step 1: Downloading Hugo
There are [several](https://gohugo.io/getting-started/installing/) ways to install Hugo. 

For Arch Linux and its derivatives, simply run
```bash
sudo pacman -S hugo
```

For Fedora, Red Hat and CentOs use-
```bash
sudo dnf install hugo
```

For Debian and it's derivatives use-
```bash
sudo apt-get install hugo
```

## Step 2: Opening GitHub repositories
While there are several ways to use Hugo to make and have GitHub pages host a static website, we will follow a very bare bones approach.
We shall open 2 GitHub repositories
- A repository to host the blog files *for* Hugo
- A repository for the generated html + JavaScript files *from* Hugo.
We need the generated website repo (henceforth called genrepo) to be a submodule  of the blog so it is easy to update the site by just changing the blog

### Opening the genrepo(generated website repository)
1. Log into your GitHub account and you should see a "new" button next to recent repositories. ![opening a repo](gitopen.png)
2. **In order to avoid errors and confusion name your repository as  {yourusername }.github.io**,  We couldn't get GitHub pages to host the web page otherwise, from a non pro account. Feel free to experiment, but yeah, expect errors if you skip this step. ![opening gen repo](openinggenrepo.png)
3. Add a "README.md" file to your main branch and commit the changes. (the file doesn't have to contain anything, this acts as your entry file for your site. GitHub pages looks for in index.html, index.md or README.md file as the entry file for your site).

### Opening the blog repository
1. Same as step one above
2. Name this repository whatever you like. We will call our blog repository, "blog"(marvel at our creativity).
3. Again add a readme and at least one commit.

## Step 3: Using Hugo to initialize a site
1. Clone the "blog" repository that is the repository that will host the files for Hugo into your local machine by simply running 
```bash
git clone <link to your hugo host repository that is blog repository>
```
![git clone](gitclone.png)
2. go into the cloned folder and run 
```bash
hugo new site <sitename>
```
![hugosetup](hugositesetup.png)
note that the "site name" specified here will be the name of your blog site. 
## Step 4: Specifying a theme for your web page
Go to [Hugo themes](https://themes.gohugo.io/). Feel free to check out and pick whatever theme you like. Read through your desired theme's page and follow instructions. In this tutorial we will use the following method to add a theme. Which is the easiest way and will require little to no configuration.
1. Go to [Hugo themes](https://themes.gohugo.io/).
2. Select a theme 
3. Navigate to your site's folder. That is `blog/sitename`
4. Run the following command to clone the theme to the themes folder.
We use the cactus theme in our example.
```bash
# generally
git clone <github page of the theme> themes/<theme name>
# for cactus
git clone https://github.com/monkeyWzr/hugo-theme-cactus.git themes/cactus
```
![themeDL](downloadingTheme.png)
## Step 5: Configure the site
1. Inside this `blog/sitename` directory you will find a `config.toml` file. All commands in this sections should be run from this directory.
2. Open this file inside your preferred text editor. You will see the following
```toml
baseURL = 'http://example.com/' 
languageCode = 'en-us' 
title = 'My New Hugo Site' 
```
We want to change it to
```toml
baseURL = 'https://<link to your genrepo>/' 
languageCode = 'en-us' 
title = '<blogname>' 
author = '<author>' 
theme = '<theme>'
```
For this example 
```toml
baseURL = 'https://sinhSlumbering.github.io/' 
languageCode = 'en-us' 
title = 'shrekSwamp' 
author = 'Me' 
theme = 'cactus'
```
Notice the 's' in `https` we want to enforce `https` 
3. Run the following command
```bash
hugo server
```
![hugo server view](hugoServerSetup.png)
This will host a static site from your localhost. click on the URL to view the web page in your browser.  
![local site](hugoserveroutput.png)
## Step 6: Adding the repo to hold the generated website
Now we add the genrepo to hold the generated code to be displayed as a GitHub pages site. 
1. clone the genrepo to your site directory
```bash
git clone <repo URL>
# example
git clone 
```
![genrepo clone](genrepopull.png)
2. add the genrepo as a submodule to your blog directory
```bash
git submodule add -b main <repo URL>
```
![adding the repo as a submodule](submoduleadd.png)
## Step 7: Creating a post
As we can see the site only contains a static page without any content. The idea is to add pages here to access. Sort of like a very rudimentary blog. Goal here is to create posts for your blog. For this tutorial we shall add a tutorial to our blog.
1. Run the following command to add a new post
```bash
# generally
hugo new posts/<post name>.md
# in this example
hugo new posts/tutorial.md
```
2. The post is at `content/posts/`  to edit the post simply navigate to post and open it in your preferred editor.
![edit the post](postedit.png)
4. To view the post in the site remove the draft mark. that is we shall see - 
```markdown
---
title: "Tutorial"
date: 2022-09-30T16:13:15+06:00
draft: true
---
```
we want to change it to - 
```markdown
---
title: "Tutorial"
date: 2022-09-30T16:13:15+06:00
---
```
5.  Run the following command to see if the new post shows up correctly in the structure
```bash
hugo server
```
You should see a post show up 
![post added](addedpost.png)
## Step 8: Adding content to our post
What Hugo does is generates JavaScript and html required to host a static site from markdown. Now learning a new thing might sound intimidating, but markdown is literally one of the easiest and the most intuitive thing ever. 5 mins should be enough to learn enough to get this blog up and running. As you are most probably, a fellow classmate, my man, you should enjoy this rare W. We know we do. And if you want to make life harder for yourself, feel free to use html. We, won't.
**Important: Please remember not to delete the already text generated at the top of the file that we edited in step 7.  This part is crucial metadata to generate the site.**

If you for whatever reason, like our tutorial and want us to make a more detailed section on markdown, [annoy Noki](https://www.facebook.com/mahdimohammad.noki).

### What even is markdown
Ask [wikipedia-sensei](https://en.wikipedia.org/wiki/Markdown). But basically it's a markup language. Used to create formatted text from plain-text. As opposed to [wysiwyg](https://en.wikipedia.org/wiki/WYSIWYG) editors, markdown has to be compiled/parsed later to show the formatted text. Although some editors exist which can compile/parse markdown on the fly.
### Markdown resources
- [Markdown Basics](https://www.markdownguide.org/basic-syntax/), convenient [cheat sheet](https://www.markdownguide.org/cheat-sheet/)
- Interactive [tutorial](https://commonmark.org/help/tutorial/)
- [Hugo specific](https://www.markdownguide.org/tools/hugo/) markdown guide. 
- Other [Hugo resources](https://gohugo.io/content-management/) related to editing.
There are an incredible amount of things possible with markdown and it's derivatives. Hugo uses the [goldmark](https://github.com/yuin/goldmark) parser.  Goldmark is very new. Therefore resources are sparse. A well worded Google search should help you through any queries(try searching with 'Hugo'/'Hugo GitHub' rather than goldmark)That's what we did. Better yet, Feel free to experiment and find out. 
### Images
"But tutorial guy" you ask, "How will I add this cool picture of sanic hegehog to my site?".  ![gottagofast](sanic.png)A common and understandable question. If you have seen the markdown guides you should know the syntax to add a picture is this
```markdown
![alt text](<link to image>)
![alt text](<path to image>)
```
We could pull images off other websites but we can't guarantee that picture remaining tied to the links (much like an nft lol). So ideally we want to control what picture we upload and how long it stays up. 
We therefore follow these simple steps
1. We store the images in the static folder inside of our site directory. The exact location is inside the a folder named the same as the post name inside the posts folder inside the static directory that is the path should be `static/posts/<post name>/<imagename>.<imageext>` for example `static/posts/tutorial/sanic.png`. Thus the images are stored in the blog repo.
2. We then simply link the images using
```markdown
<!--- general --->
![alt text](<imagename>.<extension>)
<!--- example -->
![gottagofast](sanic.png)
```

Your directory structure should look something like this

```bash
static
└── posts
    └── tutorial   <- Notice the name of the post
        └── sanic.png
```

```bash
content
└── posts
    └── tutorial.md    <- The image will be linked in this post.
```
As an added bonus note that adding images this way is easier as you don't have to specify a huge link or directory.
### Embedding other websites' content
 >**WARNING: So in this section we have to keep the angle brackets in the code**
 
 "But tutorial guy" you ask again, "I really need to embed a video to my site. I want to cater to the obliterated attention span of the internet users of current year."
Indeed that is very important. You can use [Hugo shortcodes](https://gohugo.io/content-management/shortcodes/) to achieve this functionality.
Let's add the most iconic YouTube video to this page.
![youtube link embed](youtubething.png)
Here the '*id*' part comes from the YouTube link. If you already haven't memorized it, this id comes from this link `https://www.youtube.com/watch?v=dQw4w9WgXcQ` the part after `?v=` is our id. Lets enjoy the video now - 
{{< youtube id=dQw4w9WgXcQ title="rickroll" >}}
Similarly we can embed tweets or Instagram posts check out [Hugo shortcodes](https://gohugo.io/content-management/shortcodes/) for more.
Finally, 
Run the following command
```bash
hugo server
```
To see if your edits show up nicely

## Step 9: Building the website and publishing it to GitHub pages
Startoff by going inside the site directory. 
1. Build the website by running the following
```bash
# general
hugo -t <theme name>
# example
hugo -t cactus
```
You can ignore the warning here. It didn't cause us any issues. (That we comprehend)
2. Clear the submodule 
```bash
rm -rf <name of genrepo>/*
# example
rm -rf sinhSlumbering.github.io/*
```
3. Copy the generated content into the genrepo to be hosted
```bash
cp -r public/* <name of genrepo>/
# example
cp -r public/* sinhSlumbering.github.io/
```
4. Go inside the genrepo
5. Push genrepo to GitHub
```bash
git add .
git commit -m "<commit message>"
git push
```
![gitstuffongenrepo](gitstuffongenrepo.png)
![git Push](gitpush.png)
6. Return to your blog repo.
7. Push changes made to blog repo into GitHub
```bash
git add .
git commit -m "<commit message>"
git push
```
8. **WAIT** it takes a while for GitHub to host the page.

## Step 10: Enjoy your site
After you have waited for a considerable amount of time you should be able to access your site by visiting {your username}.github.io 
## Step 11: changes
If you want to make changes like adding new posts and/or editing. follow steps 7 through to 10.
## Cautions
- **IT IS OF THE UTMOST IMPORTANCE that you remain in the specified directory when running a shell command** To help with this we have specified all changes in directory either in the screengrab or explicitly
- Remember to push to the genrepo repository first then the blog directory. 
- **WAIT** after pushing to GitHub to access the site. As Gabe Newell famously said
> "These things, they take time" -GabeN

## FAQ
**Why didn't you use Jekyll or any other generator? Why Hugo?**
You see, Jekyll need at least one more dependency than Hugo(Hugo comes with everything bundled). That is literally it. We chose the path of least resistance.

For further questions [annoy Noki](https://www.facebook.com/mahdimohammad.noki). And we will get back to you soon.

## References
- [GitHub markdown](https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax) and [GitHub advanced markdown](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting) 
- [Hugo Documentation](https://gohugo.io/documentation/)
- https://parzival2.github.io/blog/posts/add-images-hugo/
- [MarkdownGuide](https://www.markdownguide.org/)
- https://www.youtube.com/watch?v=LIFvgrRxdt4
- And finally [Wikipedia](https://en.wikipedia.org/)
## Comments
Comments in a static site? huh? [well it can be done apparently](https://gohugo.io/content-management/comments/).  We however have a simpler implementation. The comment section has been moved to [this wall](https://www.facebook.com/mahdimohammad.noki)
