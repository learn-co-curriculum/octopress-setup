We're setting up octopress to power our student code blogs and also as a test of our environment. So even if you don't plan on blogging on octopress cause you already got a tumblr or wordpress you use, you must setup octopress.

## Cloning Octopress

Go into your code directory and:

```
git clone git://github.com/imathis/octopress.git flatiron-student-003.github.io
```

This will clone the octopress source into a directory that is named based on your githubusername and then the github.io address. So for example, flatiron-student-003.github.io.

## Installing Octopress

From within the directory you just made, do:

```
bundle install
```

Which will install all the gems you need for octopress.

Then `rake install` which will setup octopress.

## Hosting Octopress on Github

So there are two concerns we want to deal with next, having a repository to store our blog posts in so that they are under version control and backed up and having a place to host our blog. Fortunately, github will deal with both of those concerns.

### A Little on Github Pages

[Github Pages](http://pages.github.com/) is a service that will allow you to use github to host static HTML websites. It works in a sort of weird way. User Pages live in a special repository dedicated to only the Pages files. This repository uses the account name, for example flatiron-student-003/flatiron-student-003.github.io where `flatiron-student-003` is the github user name.

- This repository must use the username/username.github.io naming scheme.
- Content from the `master` branch will be used to build and publish the Pages. Because of this, the master branch cannot contain the source code for our blog, but rather `master` ** can only contain statically generated HTML.**

So we need to create a [new Github repository](https://github.com/repositories/new) and name the repository with your user name `username.github.com` (in this example `flatiron-student-003.github.io`.

Github Pages for users uses the master branch like the public directory on a web server, serving up the files at your Pages url `http://username.github.com`.

As a result, you'll want to work on the source for your blog in the `source` branch and commit *the generated content* to the `master` branch. Octopress has a configuration task that helps you set all this up. Make sure you are in your octopress directory.

``` sh
rake setup_github_pages
```
This will:

1. Ask you for your Github Pages repository url.
2. Rename the remote pointing to imathis/octopress from 'origin' to 'octopress'
3. Add your Github Pages repository as the default origin remote.
4. Switch the active branch from master to source.
5. Configure your blog's url according to your repository.
6. Setup a master branch in the _deploy directory for deployment.

Next run:

```sh
rake generate
rake deploy
```

This will generate your blog, copy the generated files into `_deploy/`, add them to git, commit and push them up to the master branch. In a few seconds you should get an email
from Github telling you that your commit has been received and will be published on your site.

**Don't forget** to commit the source for your blog.

```sh
git add .
git commit -m 'your message'
git push origin source
```

**Note:** With new repositories, Github sets the default branch based on the branch you push first, and it looks there for the generated site content.
If you're having trouble getting Github to publish your site, go to the admin panel for your repository and make sure that the master branch is the default branch.

## Starting Octopress Locally

From within your octopress directory, run

```
rake preview
```

That starts a local server that will allow you to preview your blog as you write. Open browser and go to [localhost:4000](http://localhost:4000). Pay attention to the output of rake preview, it should read and make it clear that the server started. You should see an empty octopress blog in your browser.

## Write Your Hello World

Read the [Octopress Bloggin Guide](http://octopress.org/docs/blogging/)

```
rake new_post["hello world"]
```

Write a help world post and then deploy to github pages and you should be able to see your live site.

*Note:* Always make sure you are working out of the `source` branch, never `master`. `master` is perishable.

After you write your post in the `source` directory, do:

```
rake generate
rake deploy
```

you should be able to go to username.github.io and see your posts.

And finally, commit your blog via:

```sh
git add .
git commit -m 'your message'
git push origin source
```
