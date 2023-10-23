# General
In this repo you can find my slides for my talk "IaC with Pulumi and GitHub Actions". Next to the slides there are all my commands I used for the demos.

## Demo - Creating a new Pulumi project

### Prerequisetes
- [Pulumi CLI](https://www.pulumi.com/docs/get-started/install/) installed
- [GitHub CLI](https://cli.github.com/) installed
- [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) installed

Go to a specific folder and type in the following commands:

```bash
# Create a new folder
mkdir pulumi-example
```
```bash
# Change into the newly created folder
cd pulumi-example
```
```bash
# Navigate through the assistant and select Azure CSharp static website
pulumi new
```
```bash
# Make the folder a git repository
git init
```
```bash
# Go through the assistant to create a new repository on GitHub
gh repo create
```

```bash
# Go through the assistant to create a new repository on GitHub
git add . 
git commit -m "intial commit"
git push -u origin main
```

