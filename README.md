# aap-insights

## requirements

Install requirements

``` shell

ansible-galaxy install -r collections/requirements.yml

```

Follow the instructions in the documentation to create the `tower_cli.cfg` file.

See: https://console.redhat.com/ansible/automation-hub/repo/published/ansible/controller/docs/

``` shell

sudo dnf install -y automation-controller-cli.x86_64

```
awx login -k --conf.host https://100.123.152.33 --conf.username <USER_NAME> --conf.password <PASSWORD>


## monitoring

## tests

### create content

1. create credential
2. create project
3. create inventory
4. create jobtemplate

### execute

1. execute jobtemplate
