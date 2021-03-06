# Stacks

## Custom Multi-Container Stack for NPM

This custom stack is intended for use in the DO500 course offered by Red Hat Training. The materials are available on GitHub. Since the technology is constantly changing this stack should fall out of date quickly.

This stack can be added through the swagger spec in the codeready application. The [raw config file](do500-raw-config.json) is a json file that can be deployed to Codeready. It contains yaml files for Kubernetes objects, commands that can be run to pull in and run the course work, the dev machines with the required components, the servers for the routes and the volume need for mongo. 

A shell script is provided to add the [raw config file](do500-raw-config.json). Modify the environment variables.

An ansible playbook is also provided in the same manner as the shell script if your more into that.

The tech stack included in this stack is NPM, Ansible, Mongo DB and the OC client. 

For reference the do500-stack.yml and Dockerfile files are included in this repo

## Workspace

Once the stack is added to Codeready, create a new workspace through the UI choosing the new stack you previously created (Npm Ansible Mongo). Accept all the defaults. When the workspace is up and running, do the following steps

1. Run the command `init-api` (it is completed with a `done` message)
2. Run the command `init-fe` (it is completed with a `done` message)
3. Replace the contents of the todolist-fe/vue.config.js file with the following

```
module.exports = {
  lintOnSave: false,
  devServer: {
    disableHostCheck: true
  }
};
```
3. Run the command `fe-fix-api-url` (it is completed with a `done` message)
4. Run the command `api-start`
5. run the command `fe-start` 
6. The fe-start command should print a preview URL. Click on that URL to navigate to the application. Verify that the TODOs are populate with values from mongo by clicking on the TOOOs link and verify that a TODO is displayed that mentions learning about mongo. If true, the set up has been successful.
