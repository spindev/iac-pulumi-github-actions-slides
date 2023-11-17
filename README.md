# General
In this repo you can find my slides for my talk "IaC with Pulumi and GitHub Actions". Next to the slides there are all my commands I used for the demos.

# Prerequisites
- [Pulumi CLI](https://www.pulumi.com/docs/get-started/install/) installed
- [GitHub CLI](https://cli.github.com/) installed
- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) installed
- [OICD between GitHub Actions and Azure](https://learn.microsoft.com/en-us/entra/workload-id/workload-identity-federation-create-trust?pivots=identity-wif-apps-methods-azp#configure-a-federated-identity-credential-on-an-app)

# Demos
Here are the commands for the Demos of my Talk "IaC with Pulumi and GitHub Actions".

## Static Website on Azure with C#

Go to a specific folder and type in the following commands:

```bash
# Create a new folder
mkdir pulumi-demo
```
```bash
# Change into the newly created folder
cd pulumi-demo
```
```bash
# Navigate through the assistant and select "static-website-azure-csharp Azure"
pulumi new
```
```bash
# Create a git repository within the current directory
git init
```
```bash
# Go through the assistant to create a new repository on GitHub
gh repo create
```

```bash
# Add the files to the staging area, make a first commit and push it to GitHub
git add . 
git commit -m "intial commit"
git push -u origin main
```
```bash
# Login into Azure
az login
``````
```bash
# Run Pulumi up, to create the infrastructure. It will use your Default subscription
pulumi up
```

Add something to the ./www/index.html

```bash
# Run pulumi up again, to see what is happening
pulumi up
````

## Create new GitHub Actions worfklow
Make sure OICD is set up correctly and you have access to the values for the secrets.

```bash
# Create a new workflow file under .github/workflows
mkdir .github
mkdir .github/workflows
touch .github/workflows/deploy.yml
```` 

```yaml
name: Deploy to Azure

on: push

permissions:
  id-token: write

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          show-progress: false
      - name: Azure Login
        uses: azure/login@v1
        with:
          client-id: ${{ secrets.AZURE_CLIENT_ID }}
          tenant-id: ${{ secrets.AZURE_TENANT_ID }}
          subscription-id: ${{ secrets.AZURE_SUBSCRIPTION_ID }} 
      - name: Pulumi up
        uses: pulumi/actions@v4
        with:
          command: up
          stack-name: dev
        env:
          PULUMI_ACCESS_TOKEN: ${{ secrets.PULUMI_ACCESS_TOKEN }}
          ARM_USE_OIDC: true
          ARM_CLIENT_ID: ${{ secrets.AZURE_CLIENT_ID }}
          ARM_TENANT_ID: ${{ secrets.AZURE_TENANT_ID }}
          ARM_SUBSCRIPTION_ID: ${{ secrets.AZURE_SUBSCRIPTION_ID }} 
```

Full working backup can be found over [here](https://github.com/spindev/pulumi-demo-backup).

## Advanced Pulumi & GitHub Actions example
[Go over here](https://github.com/spindev/iac-pulumi-github-actions).
