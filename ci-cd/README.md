# CI/CD

This project is an example of how to build a CI / CD environment in OpenShift. It will create 3 projects: CI/CD, DEV and DEMO. The CI/CD environment will deploy Jenkins, Nexus and Sonarqube along with related Postgres databases. The buid and deployment is coordinated with the OpenShift Applier (originally version v2.0.3). For more information on how the environment and applier work see this repository: https://github.com/rht-labs/labs-ci-cd.

## What's Happening, Where Are These Artificats Coming From?

This repository pulls in other repos and artifacts to get all pieces running. This repo is really just coordinating it all

### Jenkins

Jenkins is being built via [S2I](https://github.com/openshift/source-to-image) from the (rht-labs project| https://github.com/rht-labs/labs-ci-cd.git). Look in the s2i-config/jenkins-master folder and check out the README.md for set up. A lot of the deployment configuration is set in the init.groovy.d. The base Jenkins images is pulled from the version provided by OpenShift and is intergrated into the auth system.

Three Jenkins slaves are added for: Ansible, Maven and Node. The repo for the quickstarts is found [here](https://github.com/redhat-cop/containers-quickstarts.git).

### Nexus

Often used for Maven builds to speed up the builds and to stored artifacts. This is a pull from docker hub. There is some sugar provided by rht-labs that adds an applier post-action to add additional repos to the application. 

### Sonaqube

This a docker build. Sonarqube has not published a container yet for it's latest community version (7.3). It is built with [this repo](https://github.com/mcanoy/sonarqube.git) as the base image. Then a build with the additions from rht-labs is added. This build is in flux so the repo is [here](https://github.com/mcanoy/labs-ci-cd/tree/sonar-build). Using version (7.3) allows better typescript analysis. The labs addition includes the latest typescript plugin and some integration features.

## Usage

Bring in the applier (run just once):

```
ansible-galaxy install -r requirements.yml --roles-path=roles
```

## Permissions and Projects

This creates the projects in this example. This also gives Jenkins permission to make changes in the other projects.

```
ansible-playbook apply.yml -i inventory/ -e target=bootstrap
```

## CI / CD Tools

Here's the meat of it. This creates all the builds and deployments needed for this example.

```
ansible-playbook apply.yml -i inventory/ -e target=tools
```

## Sensitive Data

This will run sensistive data (secrets). Generally, these files would not be checked in here

```
ansible-playbook apply.yml -i inventory/ -e target=sensitive-data
```

## Filtering and Substituting

Sometimes we like to make in-line changes. Sometimes we like to run only parts of the playbook. Here's how: we're using ansible's `-e` switch. 

To run only select parts of the playbook provide a comma seperated list of tags in the filter_tag parameter

```
ansible-playbook apply.yml -i inventory/ -e target=tools -e "filter_tags=sonarqube"
```
To change a variable in the apply.yml file provide the value like so:

```
ansible-playbook apply.yml -i inventory/ -e target=tools -e "ci_cd_namespace=my-ci-cd"
```

