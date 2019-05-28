---
layout: post
title: Deploy React Web App Linux via Azure DevOps
---

Create an empty Web App Linux with App stack Node 10.1

Create React application locally and make sure its running as expected.

    npx create-react-app azurereactsample
    cd azurereactsample
    npm start 

Here is my GitHub sample: [https://github.com/gangularamya/azurereactsample](https://github.com/gangularamya/azurereactsample)

### Steps to create pipeline in Azure DevOps:

- In Azure DevOps create a project and name it.
<figure class="kg-card kg-image-card"><img src="/content/images/2019/02/image-3.png" class="kg-image"></figure>
- Once it is created add pipelines..here I'm adding build pipeline.
- For the first time it will ask you to authorize for GitHub account.
<figure class="kg-card kg-image-card"><img src="/content/images/2019/02/image-4.png" class="kg-image"></figure>
- After picking up the correct repo from GitHub account...by default it will create azure-pipelines.yml file.
- Here I did added PublishBuildArtifact@1 Task.
- I specified PathtoPublish as $(System.DefaultWorkingDirestory)/build. React app generates build folder after compilation.

    # Node.js with React
    # Build a Node.js project that uses React.
    # Add steps that analyze code, save build artifacts, deploy, and more:
    # https://docs.microsoft.com/azure/devops/pipelines/languages/javascript
    
    trigger:
    - master
    
    pool:
      vmImage: 'Ubuntu-16.04'
    
    steps:
    - task: NodeTool@0
      inputs:
        versionSpec: '8.x'
      displayName: 'Install Node.js'
    
    - script: |
        npm install
        npm run build
      displayName: 'npm install and build'
    
    - task: PublishBuildArtifacts@1
      inputs:
        PathtoPublish: '$(System.DefaultWorkingDirectory)/build'

<figure class="kg-card kg-image-card"><img src="/content/images/2019/02/image-5.png" class="kg-image"><figcaption>``</figcaption></figure>
- Add Release step with two tasks Archiving and Deploy Azure App services.
- Specify Root folder or file to archive as below

    $(System.DefaultWorkingDirectory)/_gangularamya.azurereactsample/drop

- Select Archive type as Zip from drop down

    zip

- Archive file to create as 

    $(Build.ArtifactStagingDirectory)/$(Build.BuildId).zip

<figure class="kg-card kg-image-card"><img src="/content/images/2019/02/image-8.png" class="kg-image"></figure>
- Make sure you select App Service type to Web App on Linux
<figure class="kg-card kg-image-card"><img src="/content/images/2019/02/image-9.png" class="kg-image"></figure>
- For React app deployed on Node Base Image..adding express\_static.js gist that points to index.html file.
- Gist: [https://gist.github.com/gangularamya/de1ce2a5921ad0f2bd2339f6c63d77ef](https://gist.github.com/gangularamya/de1ce2a5921ad0f2bd2339f6c63d77ef)
- Add Startup command as

    pm2 start /home/site/wwwroot/express_static.js --no-daemon

- Select Deployment script as 'Inline script' Below is the Inline Script.

    npm i express
    wget -q https://gist.githubusercontent.com/gangularamya/de1ce2a5921ad0f2bd2339f6c63d77ef/raw/5b3e0750430822b83ae97ace7ccaa6b24498738b/express_static.js -O /home/site/wwwroot/express_static.js

<figure class="kg-card kg-image-card"><img src="/content/images/2019/02/image-10.png" class="kg-image"></figure>
- Once build and release tasks are successful. Browse the site.
- Here is my output: [https://azurereactsample.azurewebsites.net/](https://azurereactsample.azurewebsites.net/)
<figure class="kg-card kg-image-card"><img src="/content/images/2019/02/image-13.png" class="kg-image"></figure>