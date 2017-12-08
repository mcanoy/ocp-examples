# Hubot Jenkins Slack Integration

This examples shows how to integrate slack with Jenkins. It requires an OpenShift environment (see MiniShift for local development) and Ansible (originally tested with version 2.4)

To run this app:

1. Configure your slack workspace by adding the Hubot app
2. Clone this repository
3. cd to hubot-slack/
4. update `params/hubot/build-deploy`. Change the value of the key HUBOT_SLACK_TOKEN to your slack integration token with the value from step 1.
5. (optional: by default Jenkins will post to a channel called `jenkins`) Update the default Jenkins room in `params/jenkins/deploy`
6. invite the bot you created to the default slack channel
7. Run the ansible prequisite step 
 ```
ansible-galaxy install --roles-path . -r casl-ansible.yml
 ```
8. Run the playbook
 ```
ansible-playbook --connection=local -i inventory casl-ansible/playbooks/openshift-cluster-seed.yml
 ```

 The result of this should deploy a hubot app, a jenkins app and a sample pipeline in an OCP project called hubot. The sample pipeline should run automatically once Jenkins and Hubot are running. A message should be posted in the default slack channel with instructions on how to respond.