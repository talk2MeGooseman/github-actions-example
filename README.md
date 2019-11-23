# Creating a "Hello World" JavaScript Github Action

This will be a simple walkthrough creating your very first JavaScript Github Action. This repository was created on Stream during the [Talk Github Actions with guest Banjamin Lannon](https://www.twitch.tv/videos/511958691) stream. If you would to watch our conversatoin of follow along at the end of the stream when making this project you can watch the linked video.

## Getting Started

- Use an existing repository or make a brand new repository
> You can run the Github Action from the repository it lives in or run it from another repositories action.
- Create a `.github` folder and the root of your directory
- Create a `actions` folder inside of `.github` folder

## Creating our JavaScript Action
Now we have basic folder structure. Lets make our first JavaScript Github Action.

- Create a `test-action` folder inside of the previously created `actions` folder.
- Inside of `test-action` initalize a npm package by running
```bash
npm init -y
```
- Now create a `index.js` file
> This index.js file will contain the logic we will run for our Github Action
- Open up `index.js` and lets add a simple Hello World
```javascript
// Inside of index.js
console.log('Hello World!)
```
- Create an `action.yml` file inside `test-action` folder
> This is a special file for Github Actions, it helps tell Github information about your action and how to run it
- Insert the following into `action.yml` the following:
```yaml
name: Hello-World
description: Example hello world running JavaScript Github Action
runs:
  using: node12 # Runtime Environment 
  main: index.js # Script to run, path is relative
```
- Make sure everything is saved, commit the code, and push it to your Github repository

## Creating your Github Action Workflow
Next we need to create a Github Action Workflow that will run our brand new JavaScript "Hello World" Github Action. This can be done one of two ways.

1. On Github.com in your repostory page directly
1. Locally be manually creating the dependent folder and files
> Doing it manually is a little more work since on Github.com you can start with using the template bolierplate.

I will going through Method 1. Once were done with Method 1, it will be easy to say how to do it manually.

### Creating your Workflow on Github.com
 - Navigate to your repository homepage on Github
 - On the top bar next to `Pull Requests` click on `▶️ Actions`
 > When you dont have any Github Action Workflows for your repository you will see a "Getting Started" kind of page. It will suggest Github Actions you can start with based off the main language of your repository.
 - Ignore the suggestiong and click on `Setup and workflow yourself` button located on the right side of the page.
 > You will be taken to the standard Github file create/edit screen with a TWIST (very twisty)! On the right margin you will have a WYSIWYG sort of thing to fill in Github Actions that might be of use. This will be attempty to make a `main.yml` file inside of `.github/workflow/`.
 
 > This YAML file will run an entire workflow, excuting our desired Github Actions or commands.
 - In our `main.yml` put the following in:
 ```yaml
 name: CI # Name of our workflow 

on: [push] # Repository event that will trigger the workflow

jobs:
  build:

    runs-on: ubuntu-latest # Environment job will run in 

    steps: # Each action/command to run
    - uses: actions/checkout@v1 # Helps check out the repo code
    - uses: ./.github/actions/test-action # Tell it to run out JS Action
```
- Commit the file on Github
> Since we just made our workflow file and it triggers on `push`. Github should actually attempt to run our workflow and trigger our JavaScript action. Let's go check it out!

## Checking Executed Workflows
- On the top bar next to `Pull Requests` click on `▶️ Actions`
> This page will look completely different since that last time we visited it. Since we now have a workflow, it will display the history of our workflow runs.

> In the table for `All Workflows` you shoudl see a job called `CI` that is currently running or has completed (depending on how fast you got to this page after committing the workflow.
- Click on name `CI` to view the workflow details.
> You will see a UI displaying the various steps your workflow went through during is execution process.
- Click on `Run /./.github/actions/test-action` if its not already expanded.
> If the step has completed executing it will be expanded showing you what is going on during that step. If it has been completed it will be collapsed.
- You should see our console log of `Hello World!`

Congratulations you just made your on JavaScript Github Action and Workflow to run it!!!!!

## Support Using Packages in JavaScript Actions
Doing a plain console log is nice and all but its looking kinda plain. Lets spice it up a little by giving the "Hello World" some flair. By using `Boxen` package to put our "Hello World" in a nice box to make it feel more official.

But in order to support running 3rd party packages, our JavaScript Github Action must be bundled together with its dependency (just like if we were deploying a front end app).

- Install `boxen` inside `test-action` folder using the terminal:
```bash
npm i boxen
```
- Update `index.js` to use `boxen`:
```javascript
// In index.js
const boxen = require('boxen');
 
console.log(boxen('HELLO WORLD!!', {padding: 1}));
```
- Check everything so far is working by running `index.js` with node in the terminal
```bash
node index.js

# Should output:
┌───────────────────┐
│                   │
│   HELLO WORLD!!   │
│                   │
└───────────────────┘
```

