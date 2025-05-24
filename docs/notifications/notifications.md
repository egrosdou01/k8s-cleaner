---
title: k8s-cleaner - Kubernetes Controller that identifies, removes, or updates stale/orphaned or unhealthy resources
description: Welcome to the k8s-cleaner notifications page
tags:
    - Kubernetes
    - Controller
    - Kubernetes Resources
    - Identify
    - Update
    - Remove
authors:
    - Eleni Grosdouli
---

## Introduction to Notifications

Notifications is an easy way of k8s-cleaner to keep users in the loop about relevant updates. Each notification contains a list of successfully deleted or modified resources by the k8s-cleaner.

The below notifications are available.
- **Slack**
- **Webex**
- **Discord**
- **Telegram**
- **Teams**
- **SMTP**
- **Kubernetes Event**

## Slack Notifications Example

### Kubernetes Secret

To allow the k8s-cleaner to write messages or upload files to a channel, we need to create a Kubernetes secret

```bash
$ kubectl create secret generic slack --from-literal=SLACK_TOKEN=<YOUR TOKEN> --from-literal=SLACK_CHANNEL_ID=<YOUR CHANNEL ID>
```


!!! example "Slack Notifications Defintion"

    ```yaml
    ---
    apiVersion: apps.projectsveltos.io/v1alpha1
    kind: Cleaner
    metadata:
      name: cleaner-with-slack-notifications
    spec:
      schedule: "0 * * * *"
      action: Delete # Delete matching resources
      resourcePolicySet:
        resourceSelectors:
        - namespace: test
          kind: Deployment
          group: "apps"
          version: v1
      notifications:
      - name: slack
        type: Slack
        notificationRef:
          apiVersion: v1
          kind: Secret
          name: slack
          namespace: default
    ```

Anytime this Cleaner instance is processed, a Slack message is sent containing all the resources that were deleted by k8s-cleaner.

## Webex Notifications Example

### Kubernetes Secret

To allow the k8s-cleaner to write messages or upload files to a channel, we need to create a Kubernetes secret

```bash
$ kubectl create secret generic webex --from-literal=WEBEX_TOKEN=<YOUR TOKEN> --from-literal=WEBEX_ROOM_ID=<YOUR WEBEX CHANNEL ID>
```


!!! example "Webex Notifications Defintion"

    ```yaml
    ---
    apiVersion: apps.projectsveltos.io/v1alpha1
    kind: Cleaner
    metadata:
      name: cleaner-with-webex-notifications
    spec:
      schedule: "0 * * * *"
      action: Delete # Delete matching resources
      resourcePolicySet:
        resourceSelectors:
        - namespace: test
          kind: Deployment
          group: "apps"
          version: v1
      notifications:
      - name: webex
        type: Webex
        notificationRef:
          apiVersion: v1
          kind: Secret
          name: webex
          namespace: default
    ```

## Discord Notifications Example

### Kubernetes Secret

To allow the k8s-cleaner to write messages or upload files to a channel, we need to create a Kubernetes secret

```bash
$ kubectl create secret generic discord --from-literal=DISCORD_TOKEN=<YOUR TOKEN> --from-literal=DISCORD_CHANNEL_ID=<YOUR DISCORD CHANNEL ID>
```


!!! example "Discord Notifications Defintion"

    ```yaml
    ---
    apiVersion: apps.projectsveltos.io/v1alpha1
    kind: Cleaner
    metadata:
      name: cleaner-with-discord-notifications
    spec:
      schedule: "0 * * * *"
      action: Delete # Delete matching resources
      resourcePolicySet:
        resourceSelectors:
        - namespace: test
          kind: Deployment
          group: "apps"
          version: v1
      notifications:
      - name: discord
        type: Discord
        notificationRef:
          apiVersion: v1
          kind: Secret
          name: discord
          namespace: default
    ```

## Telegram Notifications Example

### Kubernetes Secret

To allow the k8s-cleaner to write messages or upload files to a group, we need to create a Kubernetes secret

```bash
$ kubectl create secret generic telegram --from-literal=TELEGRAM_TOKEN=<YOUR TOKEN> --from-literal=TELEGRAM_CHAT_ID=<YOUR TELEGRAM CHAT ID>
```


!!! example "Telegram Notifications Defintion"

    ```yaml
    ---
    apiVersion: apps.projectsveltos.io/v1alpha1
    kind: Cleaner
    metadata:
      name: cleaner-with-telegram-notifications
    spec:
      schedule: "0 * * * *"
      action: Delete # Delete matching resources
      resourcePolicySet:
        resourceSelectors:
        - namespace: test
          kind: Deployment
          group: "apps"
          version: v1
      notifications:
      - name: telegram
        type: Telegram
        notificationRef:
          apiVersion: v1
          kind: Secret
          name: telegram
          namespace: default
    ```

## Teams Notifications Example

### Kubernetes Secret

To allow the k8s-cleaner to write messages or upload files to a channel, we need to create a Kubernetes secret

```bash
$ kubectl create secret generic teams --from-literal=TEAMS_WEBHOOK_URL="<your URL>"
```


!!! example "Teams Notifications Defintion"

    ```yaml
    ---
    apiVersion: apps.projectsveltos.io/v1alpha1
    kind: Cleaner
    metadata:
      name: cleaner-with-teams-notifications
    spec:
      schedule: "0 * * * *"
      action: Delete # Delete matching resources
      resourcePolicySet:
        resourceSelectors:
        - namespace: test
          kind: Deployment
          group: "apps"
          version: v1
      notifications:
      - name: teams
        type: Teams
        notificationRef:
          apiVersion: v1
          kind: Secret
          name: teams
          namespace: default
    ```

## SMTP Notifications Example

### Kubernetes Secret

To allow the k8s-cleaner to send an SMTP email, we need to create a Kubernetes secret:

```bash
$ kubectl create secret generic smtp \
  --from-literal=SMTP_RECIPIENTS=<COMMA-SEPARATED EMAIL ADDRESSES> \
  --from-literal=SMTP_BCC=<OPTIONAL, COMMA-SEPARATED EMAIL ADDRESSES> \
  --from-literal=SMTP_IDENTITY=<OPTIONAL, IDENTITY/USERNAME OF THE SENDER> \
  --from-literal=SMTP_SENDER=<EMAIL ADDRESS> \
  --from-literal=SMTP_PASSWORD=<OPTIONAL, SMTP PASSWORD FOR EMAIL ADDRESS IF APPLICABLE> \
  --from-literal=SMTP_HOST=<SMTP SERVER HOSTNAME> \
  --from-literal=SMTP_PORT=<OPTIONAL, SMTP SERVER PORT, DEFAULTS TO "587">
```


!!! example "SMTP Notifications Definition"

    ```yaml
    ---
    apiVersion: apps.projectsveltos.io/v1alpha1
    kind: Cleaner
    metadata:
      name: cleaner-with-smtp-notifications
    spec:
      schedule: "0 * * * *"
      action: Delete # Delete matching resources
      resourcePolicySet:
        resourceSelectors:
        - namespace: test
          kind: Deployment
          group: "apps"
          version: v1
      notifications:
      - name: smtp
        type: SMTP
        notificationRef:
          apiVersion: v1
          kind: Secret
          name: smtp
          namespace: default
    ```

## Kubernetes Event Notifications Example

To allow the k8s-cleaner to generate a Kubernetes event for each matching resource

!!! example "Kubernetes Event Notifications Definition"

    ```yaml
    ---
    apiVersion: apps.projectsveltos.io/v1alpha1
    kind: Cleaner
    metadata:
      name: cleaner-with-event-notifications
    spec:
      schedule: "0 * * * *"
      action: Scan # Scan matching resources
      resourcePolicySet:
        resourceSelectors:
        - namespace: test
          kind: Deployment
          group: "apps"
          version: v1
      notifications:
      - name: event
        type: Event
    ```

Cleaner will generate a Kubernetes Event for each Deployment matching this Cleaner instance

````
20m (x2 over 56m)   Normal   k8s-cleaner   Deployment/nginx   [ns:nginx] resource matching Cleaner instance cleaner-with-event-notifications (current action Scan)
```