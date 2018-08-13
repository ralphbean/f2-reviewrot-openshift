An openshift deployment of review-rot

https://github.com/nirzari/review-rot/pull/44

---

# Steps for initial project creation in OpenShift

First log in using the appropriate `oc login` command, then select or create
the OpenShift project that you will use.

## Creating the secrets

```
oc create secret generic f2-reviewrot-frontend \
--from-literal=WebHookSecretKey=$(openssl rand -base64 12)
```

```
oc create secret generic f2-reviewrot-backend \
--from-literal=WebHookSecretKey=$(openssl rand -base64 12) \
--from-literal=github-token=${GITHUB_TOKEN} \
--from-literal=gitlab-token=${GITLAB_TOKEN}
```

## Create the config

```
oc create configmap f2-reviewrot-config --from-file=./configuration.yaml
```

## Upload the template

```
oc create -f openshift-template.yaml
```

## Process the template

Specify the argument for the hostname to be used to access the frontend UI.

```
oc process f2-reviewrot-template -p FRONTEND_HOSTNAME=${FRONTEND_HOSTNAME} | \
oc apply -f -
```

# Steps for updating the project

## Updating the config

This is the most common update workflow and is performed when a change to
the ReviewRot config is necessary.

First delete the old config:

```
oc delete configmap/f2-reviewrot-config
```

Then recreate the new one:

```
oc create configmap f2-reviewrot-config --from-file=./configuration.yaml
```

The new config will be used when the cronjob gets run next.

## Updating the OpenShift template

First delete the old template

```
oc delete template/f2-reviewrot-template
```

Then recreate it with the new version

```
oc process f2-reviewrot-template | oc apply -f -
```
