# Accessing ArgoCD Interface

This guide will walk you through the steps to install Argo CD and access its user interface using a set of commands. Argo CD is a declarative GitOps continuous delivery tool for Kubernetes.

Please make sure you have `kubectl` installed and configured to connect to your Kubernetes cluster before proceeding.

## Step 1: Install Argo CD

Install Argo CD by following the appropriate installation method for your environment. You can refer to the official Argo CD documentation for detailed instructions: [Argo CD Installation Guide](https://argoproj.github.io/argo-cd/getting_started/).

## Step 2: Access the Argo CD API Server via Port Forwarding

To access the Argo CD user interface, you need to set up port forwarding to the Argo CD API server. Execute the following command in your terminal:

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

This command forwards local port 8080 to the Argo CD API server on port 443.

## Step 3: Get Password for ARGO CD User Interface

To retrieve the password for the Argo CD user interface, execute the following command:

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

This command retrieves the password stored in the `argocd-initial-admin-secret` secret and decodes it using base64. The password will be displayed in your terminal.

## Step 4: Sign In to the Argo CD User Interface

Open a web browser and navigate to [http://localhost:8080](http://localhost:8080) to access the Argo CD user interface.

Use the following credentials to sign in:

- Username: `admin`
- Password: [password obtained from the previous step]

Replace `[password obtained from the previous step]` with the output from Step 3, which corresponds to the decoded password.

Once you have successfully signed in, you can begin using the Argo CD user interface to manage your deployments and GitOps workflows.

**Note:** Keep in mind that the port forwarding and Argo CD user interface access are only available while the port-forwarding command from Step 2 is running. If you close the command, you will lose access to the user interface until you set up port forwarding again.

## Demo

![Argo CD Demo](../data/argocd-login.gif)

That's it! You have now accessed the Argo CD user interface and can start leveraging its features for continuous delivery in your Kubernetes cluster.
