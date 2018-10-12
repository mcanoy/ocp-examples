# C/CD

This repository is based on the Red Hat Open Innovation Labs CI/CD repository see https://github.com/rht-labs/labs-ci-cd for usage and help

```
ansible-galaxy install -r requirements.yml --roles-path=roles
```

## Permissions and Projects

```
ansible-playbook apply.yml -i inventory/ -e target=bootstrap
```

## CI / CD Tools

```
ansible-playbook apply.yml -i inventory/ -e target=tools
```

## Sensitive Data

This will run sensistive data. Generally, these files will not be checked in here


```
ansible-playbook apply.yml -i inventory/ -e target=sensitive-data
```

To override ansibl variables use the -e switch to change the value.

```
ansible-playbook apply.yml -i inventory/ -e target=tools -e "ci_cd_namespace=tmp_project"
```
