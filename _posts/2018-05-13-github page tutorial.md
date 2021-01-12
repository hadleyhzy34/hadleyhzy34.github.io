---
layout: post
title: GitHub Pages Tutorial
key: 20180513
tags:
  - front end
---

## Create a repository

Head over to [GitHub](https://github.com/) and [create a new repository](https://github.com/new) named username.github.io, where username is your username(or organization name) on GitHub.

![repository](/../Pic/051301.png "Repository")

If the first part of the repository doesn't exactly match your username, it won't work, so make sure to get it right.
{:.warning}

<!--more-->
## What git client are you using? A terminal

## Clone the repository

Go to the folder where you want to store your project, and clone the new repository

```terminal
~$ git clone https://github.com/username/username.github.io
```

## Hello world
Enter the project folder and add an index.html file

```terminal
~$ cd username.github.io
~$ echo "Hello World" > index.html
```

## Push it
Add, commit, and push your changes:

```terminal
~$ git add --all
~$ git commit -m "Initial commit"
~$ git push -u origin master
```

## ...and you're done!
Fire up a browser and go to [https://username.github.io](https://username.github.io)

