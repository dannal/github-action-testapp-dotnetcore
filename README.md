# GitHub Actions test app (.NET Core)

A simple application to test and try App Service's integration with GitHub Actions.


PS script from CLI to setup webapp/github integration when deployment tab in portal does not work

#!/bin/bash

gitrepo=https://github.com/dannal/github-action-testapp-dotnetcore
token=755be4323ee924ba9288946f2bbabdb66cd3f756
webappname=zerohero1
rg=zero_to_hero1

# Create a resource group.
az group create --location australiasoutheast --name zero_to_hero1

# Create an App Service plan in `FREE` tier.
az appservice plan create --name $webappname --resource-group $rg --sku S1

# Create a web app.
az webapp create --name $webappname --resource-group $rg --plan $webappname

# Configure continuous deployment from GitHub. 
# --git-token parameter is required only once per Azure account (Azure remembers token).
az webapp deployment source config --name $webappname --resource-group $rg --repo-url $gitrepo --branch master --git-token $token

# Copy the result of the following command into a browser to see the web app.
echo http://$webappname.azurewebsites.net
