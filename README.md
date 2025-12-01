# finops-with-gitops

## Utilizing GitOps with FinOps

1. Implementing cost monitoring tools
2. Enforcing budget policies
3. Optimizing resource allocation
4. Streamlining financial operations

## OpenCost with GitOps

```
.
├── applicationsets
│   └── optimization
│       └── opencost-applicationset.yaml
├── cluster
│   ├── in-cluster-austria
│   │   └── optimization
│   │       └── opencost
│   │           └── values.yaml
│   ├── in-cluster-germany
│   │   └── optimization
│   │       └── opencost
│   │           └── values.yaml
│   └── in-cluster-ireland
│       └── optimization
│           └── opencost
│               └── values.yaml
└── optimization
    └── opencost
        ├── Chart.yaml
        └── values.yaml
```

## KubeCost with GitOps

I will show you how to set an alert via the UI, configure a budget with an alert via the UI, and how to set it up through the values.yaml in the Helm Chart for deployment via tools like Argo CD.
Let's consider a straightforward use case:

```
• Project Budget: $100 per month for Project X.
• Cluster Budget: $500 per month for the entire cluster.
• Notification: If any budget is exceeded, a notification should be sent to the FinOps team members.
```

The goal of the FinOps team is not only to track the project but also to respond promptly when costs are too high, understand these costs, and identify cost drivers without needing to be Kubernetes experts.

### Setup Alert in the Kubecost UI

To set up alerts in the Kubecost UI, follow these steps:

```
1. Navigate to the Alerts Section: Open the Kubecost UI and go to the Alerts section.
2. Create a New Alert: Click on the "+ Create Alert" button.
3. Configure Alert Parameters: Select the type of alert you want to set up (e.g., budget, efficiency). Define the parameters such as the time window, aggregation level, filter criteria, and threshold.
4. Set Notification Channels: Specify the notification channels, such as email, Slack, or Microsoft Teams, by providing the necessary webhook URLs and email addresses.
5. Save the Alert: Review the configuration and save the alert.
```

Here is an example of how you can set up an alert for a alerts in the Kubecost UI:
![Setup Alert in the Kubecost UI](docs/images/kubecost_ui_setup_alert.gif)

### Setup Budget + Alert in the Kubecost UI

To set up a budget with an alert in the Kubecost UI:

```
1. Navigate to the Budgets Section: Open the Kubecost UI and go to the Budgets section.
2. Create a New Budget: Click on the "+ Create Budget" button.
3. Define Budget Parameters: Enter the budget amount, select the time window (e.g., daily, weekly, monthly), and choose the aggregation level (e.g., namespace, cluster).
4. Add Alert for the Budget: Link the budget to an alert by configuring the alert settings. Specify the threshold at which the alert should trigger.
5. Set Notification Channels: Provide email addresses and webhook URLs for Slack or Microsoft Teams to receive notifications.
6. Save the Budget and Alert: Review the setup and save both the budget and the alert.
```

Here is an example of how you can set up an alert for a budget + alert in the Kubecost UI:
![Setup Alert in the Kubecost UI](docs/images/kubecost_ui_budget_setup_alert.gif)

### Setup Alert over values.yaml

```
---
alerts:
  - type: budget
    threshold: 100
    window: 30d
    aggregation: namespace
    filter: project-x
    ownerContact:
      - owner@example.com
    slackWebhookUrl: [slackWebhookUrl]
    msTeamsWebhookUrl: [msTeamsWebhookUrl]
  - type: budget
    threshold: 500
    window: 30d
    aggregation: cluster
    filter: cluster-one
```
