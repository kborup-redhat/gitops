#GitOps app of apps

This repo were a demonstration of how to do a APP or APPS test. 

It encapsulate the application in a way so it can only access the repositories that has been defined for each application. 

Applications are controlled from the environments directory

To use fork the repo, and create a file for each application you would like to have running. 

In the file change the following lines:

* repoURL: Url to your own repo cotaining the code


Under helm we have all the helm values required for the setup. 

```
    helm:
      values: |-
# This is the name of the namespaces you will create and the different objects
        environmentName: testapp123
# This is the name of the label that get created on all objects as a owner
        customerName: testcustomer
# This is a base64 encrypted string containing a dockerconfig in the json format in case all namespaces has to pull from a locked repo (dont save this in public)
        dockerFile: ".dockerconfigjson: ewogICAiYXV0aHMiOnsKICAgICAgImNsb3VkLm9wZW5zaGlmdC5jb20iOnsKICAgICAgICAgImF1dGgiOiJiM0JsYj0iLAogICAgICAgICAiZW1haWwiOiJ5b3VAZXhhbXBsZS5jb20iCiAgICAgIH0sCiAgICAgICJxdWF5LmlvIjp7CiAgICAgICAgICJhdXRoIjoiYjNCbGI9IiwKICAgICAgICAgImVtYWlsIjoieW91QGV4YW1wbGUuY29tIgogICAgICB9LAogICAgICAicXVheS5pby9yZXBvc2l0b3J5LW1haW4iOnsKICAgICAgICAgImF1dGgiOiJiM0JsYj0iLAogICAgICAgICAiZW1haWwiOiJ5b3VAZXhhbXBsZS5jb20iCiAgICAgIH0KICAgfQp9Cg=="
# This is the name of the group that will be admins for all namespaces.       
        groupNameAdmin: gruppenavn1
# This is the Postfixes of all namespaces that will be created add more or less if you want it in a different way. 
        namespacePostfixes:
          - dev
          - test
          - prod
# This is the name of the application
        applicationName: funtest
# This is the repo name for the app of app application containing a helm chart. 
        gitrepoName: https://github.com/kborup-redhat/funtest.git
# Path to the gitrepo path
        gitrepoPath: funtest
```

Ithe bootstrap directory change the repoURL to match your deployment in the file app-argocd-app.yaml. 
Now  run it ```oc create -f app-argocd-app.yaml``` and watch things popup in argo, if  you run with my repo you can see a httpd application spinning up. 

Have fun and use at own risk. 

