# Helm Chart for Chatbot Service

This Helm chart is designed to deploy **Chatbot Service** using ArgoCD for GitOps-style continuous delivery. The chart supports various configurations to ensure smooth deployment and management of your application on Kubernetes.

---

## Prerequisites

### Infrastructure Requirements
- A running Kubernetes cluster (v1.20+ recommended)
- Persistent Volume provisioner (if storage is required)

### Tools
- Helm 3.x
- ArgoCD installed and configured on the cluster

---

## Repository Setup for ArgoCD

To deploy this Helm chart using ArgoCD:

### Add Your Git Repository to ArgoCD
1. Access the ArgoCD UI or CLI.
2. Add your Helm chart repository to ArgoCD:
    ```bash
    argocd repo add [REPO_URL] --username [USERNAME] --password [PASSWORD]
    ```
3. Verify the repository has been added:
    ```bash
    argocd repo list
    ```
---


## Updating the Helm Chart
If you modify the Helm chart, follow these steps to ensure the updates are applied correctly:

1. Package the Helm Chart
Run the following command to package the chart into a .tgz file:

    ```bash
    helm package [CHART_DIRECTORY]
    ```
    - Example:
        ```bash
        helm package chatbot
        ```
        This will create a file like chatbot-0.1.0.tgz (version depends on Chart.yaml).

2. Update the Repository Index
After packaging the chart, update the repository index:

    ```bash
    helm repo index .
    ```
    This will update or create the index.yaml file in your repository.

3. Commit and Push Changes
Commit the .tgz file and index.yaml file to the repository:

    ```bash
    git add [CHART_NAME]-[VERSION].tgz index.yaml
    git commit -m "Update Helm chart to version [VERSION]"
    git push origin [branch-name]
    ```

4. Sync Changes with ArgoCD
Trigger a manual sync to apply the updated chart:

    ```bash
    argocd app sync [APPLICATION_NAME]
    ```

