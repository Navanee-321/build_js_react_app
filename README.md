# simple-node-js-react-npm-app

This repository is for the
[Build a Node.js and React app with npm](https://jenkins.io/doc/tutorials/build-a-node-js-and-react-app-with-npm/)
tutorial in the [Jenkins User Documentation](https://jenkins.io/doc/).

The repository contains a simple Node.js and React application which generates
a web page with the content "Welcome to React" and is accompanied by a test to
check that the application renders satisfactorily.

The `jenkins` directory contains an example of the `Jenkinsfile` (i.e. Pipeline)
you'll be creating yourself during the tutorial and the `scripts` subdirectory
contains shell scripts with commands that are executed when Jenkins processes
the "Test" and "Deliver" stages of your Pipeline.



-------------------------------------------------------------------------------------------
Build a Node.js and React app with npm 
Table of Contents
Prerequisites
Fork and clone the sample repository
Start your Jenkins instance
Create your Pipeline project in Jenkins
Create your initial Pipeline as a Jenkinsfile
Add a test stage to your Pipeline
Add a final deliver stage to your Pipeline
Wrapping up
This tutorial shows you how to use Jenkins to orchestrate building a simple Node.js and React application with the Node Package Manager (npm).

If you are a Node.js and React developer who is new to CI/CD concepts, or you might be familiar with these concepts but don’t know how to implement building your application using Jenkins, then this tutorial is for you.

The simple Node.js and React application (which you’ll obtain from a sample repository on GitHub) generates a web page with the content "Welcome to React" and is accompanied by a test to check that the application renders satisfactorily.

Duration: This tutorial takes 20-40 minutes to complete (assuming you’ve already met the prerequisites below). The exact duration will depend on the speed of your machine and whether you’ve already installed docker and docker compose.

You can stop this tutorial at any point in time and continue from where you left off.

Make sure you have Git installed locally.

Prerequisites
For this tutorial, you will require:

A macOS, Linux, Windows, or Chromebook (with Linux) machine with:

2 GB of RAM

2 GB of drive space for Jenkins

The following software installed:

Docker

Docker Compose

Git, and optionally GitHub Desktop.

Fork and clone the sample repository
Obtain the simple "Welcome to React" Node.js and React application from GitHub, by forking the sample repository of the application’s source code into your own GitHub account and then cloning this fork locally.

Ensure you are signed in to your GitHub account. If you don’t yet have a GitHub account, sign up for a free one on the GitHub website.

Fork the simple-node-js-react-npm-app on GitHub into your local GitHub account. If you need help with this process, refer to the Fork A Repo documentation on the GitHub website for more information.

Clone your forked simple-node-js-react-npm-app repository (on GitHub) locally to your machine. To begin this process, do either of the following (where <your-username> is the name of your user account on your operating system):

If you have the GitHub Desktop app installed on your machine:

In GitHub, click the green Clone or download button on your forked repository, then Open in Desktop.

In GitHub Desktop, before clicking Clone on the Clone a Repository dialog box, ensure Local Path for:

macOS is /Users/<your-username>/Documents/GitHub/simple-node-js-react-npm-app

Linux is /home/<your-username>/GitHub/simple-node-js-react-npm-app

Windows is C:\Users\<your-username>\Documents\GitHub\simple-node-js-react-npm-app

Otherwise:

Open up a terminal/command line prompt and cd to the appropriate directory on:

macOS - /Users/<your-username>/Documents/GitHub/

Linux - /home/<your-username>/GitHub/

Windows - C:\Users\<your-username>\Documents\GitHub\ (although use a Git bash command line window as opposed to the usual Microsoft command prompt)

Run the following command to continue/complete cloning your forked repo:
git clone https://github.com/YOUR-GITHUB-ACCOUNT-NAME/simple-node-js-react-npm-app
where YOUR-GITHUB-ACCOUNT-NAME is the name of your GitHub account.

Start your Jenkins instance
Obtain the latest Jenkins instance, customized for this tutorial, by cloning the quickstart-tutorials repository.

After cloning, navigate to the quickstart-tutorials directory and execute the command

docker compose --profile node up -d
to run the example.

Once the containers are running successfully (you can verify this with docker compose ps), the controller can be accessed at http://localhost:8080.

If you are unable to install docker compose on your machine for any reason, you can still run the example in the cloud for free thanks to GitPod. GitPod is free for 50 hours per month. You need to link it to your GitHub account so you can run the example in the cloud. Utilize this link to open a new browser tab with a GitPod workspace where you’ll be able to start the Jenkins instance and run the rest of the tutorial.

Now, log in using the admin username and admin password.

Create your Pipeline project in Jenkins
In Jenkins, select New Item under Dashboard > at the top left.

Enter your new Pipeline project name, such as simple-node-js-react-npm-app, in Enter an item name.

Scroll down if necessary and select Pipeline, then select OK at the end of the page.

(Optional) Enter a Pipeline Description.

Select Pipeline on the left pane.

Select Definition and then choose the Pipeline script from SCM option. This option instructs Jenkins to obtain your Pipeline from the source control management (SCM), which is your forked Git repository.

Choose Git from the options in SCM.

Enter the URL of your repository in Repositories/Repository URL. This URL can be found when selecting the green Code button in the main page of your GitHub repo.

Select Save at the end of the page. You’re now ready to create a Jenkinsfile to check into your locally cloned Git repository.

Create your initial Pipeline as a Jenkinsfile
You’re now ready to create your Pipeline that will automate building your Node.js and React application in Jenkins. Your Pipeline is created as a Jenkinsfile, which is committed to your locally cloned Git repository (simple-node-js-react-npm-app) and then pushed to GitHub.

This is the foundation of "Pipeline-as-Code", which treats the continuous delivery pipeline as a part of the application to be versioned and reviewed like any other code. Read more about Pipeline and what a Jenkinsfile is in the Pipeline and Using a Jenkinsfile sections of the User Handbook.

First, create an initial Pipeline to download a Node Docker image and run it as a Docker container (which will build your simple Node.js and React application). Also add a "Build" stage to the Pipeline that begins orchestrating this whole process.

Using your favorite text editor or IDE, create and save new text file with the name Jenkinsfile at the root of your local simple-node-js-react-npm-app Git repository.

Copy the following Declarative Pipeline code and paste it into your empty Jenkinsfile:

pipeline {
    agent any
    stages {
        stage('Build') { 
            steps {
                sh 'npm install' 
            }
        }
    }
}
Defines a stage (directive) called Build that appears on the Jenkins UI.
This sh step (of the steps section) executes the npm command to ensure that all dependencies required to run your application have been downloaded to the node_modules workspace directory.
Save your edited Jenkinsfile and commit it to your local simple-node-js-react-npm-app Git repository. Within the simple-node-js-react-npm-app directory, run the commands:
git add .
then
git commit -m "Add initial Jenkinsfile"
and finally
git push to push your changes to your forked repository on GitHub, so it can be picked up by Jenkins.

Now select Build Now on the left pane of your Pipeline project in Jenkins. After making a clone of your local simple-node-js-react-npm-app Git repository itself, Jenkins:

Initially queues the project to be run on the agent.

Runs the Build stage defined in the Jenkinsfile on the agent.

During this time, npm downloads and installs many artifacts necessary to build your node/js application, which are ultimately stored in Jenkins' local npm repository.

npm install You can now select #1 to see the details of the build. You will then see how much time the build took waiting in the queue, and how much time it took to run.

Build details

In the left navigation pane, you can select Pipeline Overview to see the stages of the Pipeline.

Pipeline overview

If you select the Build stage, you will see more information about the stage, including the output of the npm command if you select the green npm install section.

Build stage

You can now select simple-node-js-react-npm-app (if that’s the name you chose for your pipeline) on the top left to return to your pipeline main page.

Add a test stage to your Pipeline
Go back to your text editor/IDE and ensure your Jenkinsfile is open.

Copy and paste the following Declarative Pipeline syntax immediately under the Build stage:

        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
so that you end up with:

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') { 
            steps {
                sh './jenkins/scripts/test.sh' 
            }
        }
    }
}
Defines a stage (directive) called Test that appears on the Jenkins UI.
This sh step (of the steps section) runs the shell script test.sh located in the jenkins/scripts directory from the root of the simple-node-js-react-npm-app repository. Explanations about what this script does are covered in the test.sh file itself. As a general principle, it’s a good idea to keep your Pipeline code (i.e. the Jenkinsfile) as tidy as possible and place more complex build scripting steps into separate shell script files like the test.sh file. This ultimately facilitates the maintenance of your Pipeline, especially if it gains more complexity.
Save your edited Jenkinsfile and commit it to your local simple-node-js-react-npm-app Git repository. E.g. Within the simple-node-js-react-npm-app directory, run the commands:
git add .
then
git commit -m "Add 'Test' stage"
and finally
git push to push your changes to your forked repository on GitHub, so it can be picked up by Jenkins.

In Jenkins, go back to Dashboard if necessary, then simple-node-js-react-npm-app and launch another build thanks to Build Now.

After a while, a new column Test appear in the Stage View.

Test stage

You can select*#2* or on the number representing your last build on the left, under Build History. You will then see the details of the build.

If Docker has not restarted since you last ran the Pipeline above, then no npm artifacts are downloaded during the "Build" stage. Therefore, running your Pipeline this subsequent time should be much faster.

You can now select Pipeline Overview to see the stages of the Pipeline.

Pipeline overview

Notice the additional "Test" stage. You can select the "Test" stage checkmark to access the output from that stage.

Test stage output

Add a final deliver stage to your Pipeline
Go back to your text editor/IDE and ensure your Jenkinsfile is open.

Copy and paste the following Declarative Pipeline syntax immediately under the Test stage of your Jenkinsfile:

        stage('Deliver') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Finished using the web site? (Click "Proceed" to continue)'
                sh './jenkins/scripts/kill.sh'
            }
        }
so that you end up with:

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Deliver') { 
            steps {
                sh './jenkins/scripts/deliver.sh' 
                input message: 'Finished using the web site? (Click "Proceed" to continue)' 
                sh './jenkins/scripts/kill.sh' 
            }
        }
    }
}
Defines a new stage called Deliver that appears on the Jenkins UI.
This sh step (of the steps section) runs the shell script deliver.sh located in the jenkins/scripts directory from the root of the simple-node-js-react-npm-app repository. Explanations about what this script does are covered in the deliver.sh file itself.
This input step (provided by the Pipeline: Input Step plugin) pauses the running build and prompts the user (with a custom message) to proceed or abort.
This sh step runs the shell script kill.sh, also located in the jenkins/scripts directory. Explanations about what this script does are covered in the kill.sh file itself.
Save your edited Jenkinsfile and commit it to your local simple-node-js-react-npm-app Git repository. E.g. Within the simple-node-js-react-npm-app directory, run the commands:
git add .
then
git commit -m "Add 'Deliver' stage"
and finally
git push to push your changes to your forked repository on GitHub, so it can be picked up by Jenkins.

In Jenkins, sign in if necessary, go back to the Dashboard and then navigate to simple-node-js-react-npm-app. Alternatively, you can go directly to simple-node-js-react-npm-app depending on where you’re starting from.

Select Build Now on the left. You should see after a while a new column Deliver appear in the Stage View.

Deliver stage

Select #3 or on the number representing your last build on the left, under Build History. Select Pipeline Overview to see the stages of the Pipeline.

Pipeline overview

Select the Deliver stage.+ You will then see a green part displaying ./jenkins/scripts/deliver.sh, which represents the successful execution of the deliver.sh script.

Deliver stage pauses for user input

Ensure you are viewing the "Deliver" stage (click it if necessary), then click the green ./jenkins/scripts/deliver.sh step to expand its content and scroll down until you see the http://localhost:3000 link.

Deliver stage output only

Click the http://localhost:3000 link to view your Node.js and React application running (in development mode) in a new web browser tab. You should see a page/site with the title Welcome to React on it.

When you are finished viewing the page/site, select the #3 link at the top of the page, or the number that represents your last build. On the left, look for Paused for Input. You should see two buttons, Proceed and Abort. Select the Process link to complete the Pipeline’s execution.

Deliver stage runs successfully You can now select simple-node-js-react-npm-app on the top left, and then on Stages at the left. It will list your previous Pipeline runs in reverse chronological order.

All previous runs displayed

Wrapping up
Well done! You’ve just used Jenkins to build a simple Node.js and React application with npm!

The "Build", "Test" and "Deliver" stages you created above are the basis for building more complex Node.js and React applications in Jenkins, as well as Node.js and React applications that integrate with other technology stacks.

Because Jenkins is extremely extensible, it can be modified and configured to handle practically any aspect of build orchestration and automation.

To learn more about what Jenkins can do, check out:

The Tutorials overview page for other introductory tutorials.

The User Handbook for more detailed information about using Jenkins, such as Pipelines (in particular Pipeline syntax) and the Blue Ocean interface.

The Jenkins blog for the latest events, other tutorials and updates.
 
