
# Make a Blog!
## Specifically with Octopress!

## Instructions

You're going to make yourself a blog.  It's an important part of being at Flatiron and being a programmer. If you want to be a part of the community you're going to be blogging.  A great place for an aspiring Rubyist to start is with Octopress.  Octopress is built on Ruby, but has it's own DSL (Domain Specific Language), which means it uses ruby to create its own little language that it uses to perform its functions.  But don't worry about it because while using Octopress you won't be using its DSL too often.

The main reason we want you to use Octopress is because it will help you get a better understanding of git and Github, which aren't the same thing!

Octopress depends on git and after any change you make you're going to want to commit those changes and push them up to Github, which will hold the repository for your Octopress Blog.  (Also, its easy commit cred for your Github profile.)

Some other things we want you to learn about are:
Rake tasks
  - Rake tasks are an important part of Ruby and were developed by the late Jim Weirich.
  - We run rake tasks little commands for a project that are written in Ruby, but are called through your command line.
  - They allow us to automate or simplify tasks by predefining them in a Rakefile at the top level of a project's directory.
  - They're used all over Rails, but you won't see much of them from now until then.

Markdown
  - Every project you do will have a README.md which is a markdown file type.
  - It's a markup language similar to HTML that is converted by browsers into HTML.
    - ex: one `#` is the equivalent of `<h1></h1>` in HTML.
    - Here's a [cheat sheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) to help you out.
  - If you use a rake task to generate a post it will be a markdown file.


## Getting Started

The first step is to open up a fresh tab in your command line and cd into a directory you want to keep your project in.

Next run these commands (it might take a bit to install everything)
```sh
  git clone git://github.com/imathis/octopress.git octopress
  cd octopress
  bundle install
```
- This will 
  - Clone the main octopress repository from Github to your computer
  - cd you into that new repository
  - Install all the necessary dependencies of Octopress on your computer so it can run

When that's done run `rake install`
  - Your very first rake task will install the default Octopress theme, so it isn't just some bland html website from 1996.

**NOTE ABOUT `rake install`**

If you get an error about bundler having already activated a version of rake and using a different of version of rake, simply preface the command you tried running, namely, `rake install` with `bundle exec rake install`.

Now that this is done let's add and commit the changes we made. Run the following.
```sh
  git add -A
  git commit -m "Creates and sets up my basic octopress blog"
```
These commands will:
  - add all of the changes you made to git's version tracker
  - commits those changes to "clean" your working directory (untracked changes make your directory "dirty")
    - commit messages are written in present tense as best practice (something about time machines, DeLoreans, and Doc Brown, but don't worry about using past tense instead)

## Configuring Your `_config.yml` File

Your `_config.yml` file lives in the top directory of your Octopress Blog.  This file is where a lot of important information about your blog.  We need to customize this file a little.

Run `subl .` in your command line to open this project in sublime. Next open `_config.yml` in sublime. Inside you should see a big block of code that looks like this.
```
  title:              # Used in the header and title tags
  subtitle:           # A description used in the header
  author:             # Your name, for RSS, Copyright, Metadata
  description:        # A default meta description for your site
```
Fill out each one of those with the title of your blog, some cute subtitle, your name, and a quick description about the blog.  Most of this is for Meta data in the head of your blog's pages; however, the title will be used often when your blog is compiled.

When you're done save your changes then add and commit them like we did before, but use a commit message like "Sets up my config.yml!"


## Hosting Octopress on Github
Finally, we're going to get ready to deploy this blog.

So there are two concerns we want to deal with next, having a repository to store our blog posts in so that they are under version control and backed up and having a place to host our blog. Fortunately, github will deal with both of those concerns.

### A Little on Github Pages

[Github Pages](http://pages.github.com/) is a service that will allow you to use github to host static HTML websites. It works in a sort of weird way. User Pages live in a special repository dedicated to only the Pages files. This repository uses the account name to create a url address for the blog.  To do so create a [new repository](https://github.com/new) and call it `username.github.io` where username is your user name, but ___DO NOT CREATE A README WITH THE REPO___. (It will prevent you from pushing to github and deploying the site.)  This will become the web address Github hosts your blog on.

- This repository must use the username/username.github.io naming scheme.
- Content from the `master` branch will be used to build and publish the Pages. Because of this, the master branch cannot contain the source code for our blog, but rather `master` ** can only contain statically generated HTML.**

To make sure your blog deploys to Github run, `rake setup_github_pages` in your terminal. You should see something like this,
```sh
Enter the read/write url for your repository
(For example, 'git@github.com:your_username/your_username.github.io.git)
           or 'https://github.com/your_username/your_username.github.io')
Repository url:
```
Go back to Github and find the line that says something like, (make sure to use ssh and _not_ https)
```sh
git remote add origin git@github.com:username/username.github.io.git
```
Copy and paste the entire part following origin, `git@github.com:username/username.github.io.git` into the `Repository url:` line in your command line, and press enter.
  - This will
    - change your `_config.yml` file's `url:` line to have the correct url
    - allow you to finally push your blog up to github so that your changes will both be stored remotely and actually host your blog!
    - also move you into a new git branch called source, this is the branch you want to do everything here on out in

### BUT... We should probably have a post first.

To make a new post run, `rake new_post["My First Post On Octopress"]`
  - This will generate a new, timestamped, empty blog post in the `source/_posts/` folder in your octopress blog.
  - The ```source/``` folder is where all of your content will go.

Go into sublime and open that folder and you should see something like, 
```
  ---
  layout: post
  title: "My First Post On Octopress"
  date: 2014-04-28 13:03:17 -0400
  comments: true
  categories: 
  ---
```
Add "Flatiron&nbsp;School" to the categories.
  - The `&nbsp;` is a non-breaking space; any normal space inside the quotation marks for categories will be split into categories.

Below the last `---` add something like "Hello, World." Then save the changes you made to the post.

### Starting Octopress Locally

If you'd like to see how the post looks before you deploy enter from within your octopress directory, `rake preview`.

That starts a local server that will allow you to preview your blog as you write. Open browser and go to [localhost:4000](http://localhost:4000). Pay attention to the output of rake preview, it should read and make it clear that the server started. You should see an empty octopress blog in your browser.

###Now let's deploy! 
All you need to do is enter these two commands,
```sh
  rake generate
  rake deploy
```
- This will
  - copy and compile the files from your `source/` and `sass/` folders into the `_deploy/` directories.
  - next it will add and commit those changes to git
  - finally it will push those changes to the master branch, which will make the website live.

Since we generated some files and deployed, now is a good time to add all the changes to git, commit them, then push them up to Github. But we'll need to make sure git has the right repository as it's origin.

```sh
  git add -A
  git commit -m "adds my first blog post and deployment"
  git push origin source
```
  - This will
    - add all the changes and commit them
    - add the ssh url of the repo you made to git so it sends your changes to the right place
    - ensures your branch is set as the main branch
    - push the project up to Github where it will live

##BONUS
  If you want to further customize your octopress blog check out this [post](http://tsiege.github.io/blog/2014/04/27/tips-on-setting-up-octopress/) I made to do just that.
