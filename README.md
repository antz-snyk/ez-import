# Snyk-EZ
snyk-api-import the easy way (Github version)

*An opinionated way to quickly import repos from one Github org to one Snyk org, using the snyk-api-import utility; this utility is capable of a lot more, check out the [full repo](https://github.com/snyk-tech-services/snyk-api-import) for more info*

---
## Set up

*prereqs: jq, npm*

1. Install [snyk-api-import](https://github.com/snyk-tech-services/snyk-api-import) tool
   - Easiest way: `npm install snyk-api-import@latest -g`
2. Clone this repo: `git clone https://github.com/antz-snyk/snyk-ez.git`
   - Navigate into it: `cd snyk-ez`
3. Get your [GitHub Org name](https://github.com/settings/organizations), put that org name in snyk-orgs.json file
   - Ensure the GitHub user you log in with is connected to a GitHub Organization
   - Create Var --> `export GITHUB_ORG_NAME=<your GH organization name>`
   - Write this Var to snyk-orgs.json file --> `cat <<< $(jq '.orgData[].name=env.GITHUB_ORG_NAME' snyk-orgs.json) > snyk-orgs.json`
4. Make a new [GitHub Auth token](https://github.com/settings/tokens)
   - Again, ensure token is created with a GitHub user connected to a GitHub org
   - Ensure token is created with all of the repo permissions
   - Create Var --> `export GITHUB_TOKEN=<your GitHub token>`
5. Get your [Snyk Org name](https://app.snyk.io/org/importer-org/manage/settings), put that org name in your snyk-orgs.json file
   - Once logged in to Snyk UI, navigate to the desired organization, then to settings (gear icon, upper right)
   - Scroll to Organization ID, copy the ID
   - Create Var --> `export SNYK_ORG_ID=<your Snyk org ID>`
   - Write this Var to the snyk-orgs.json file --> `cat <<< $(jq '.orgData[].orgId=env.SNYK_ORG_ID' snyk-orgs.json) > snyk-orgs.json`
6. Get your [Snyk Integration ID for GitHub](https://app.snyk.io/org/importer-org/manage/integrations/), put that ID in your snyk-orgs.json file
   - Navigate to [Integration settings page](https://app.snyk.io/org/importer-org/manage/integrations) within your Snyk org
   - Scroll to the GitHub and GitHub Enterprise settings; which was used to integrate?
   - Determine the correct integration option (GH or GH Enterprise), then select *Edit settings* for that integration option
   - Scroll to the bottom of the *Edit settings* page, copy the Integration ID
   - Create Var --> `export SNYK_ORG_INT_ID=<your Snyk org integration ID>`

     Write this Var to the snyk-orgs.json file, and delete the alternate option...
       - If you are doing regular GitHub integration: 
            ```
            cat <<< $(jq '.orgData[].integrations.github=env.SNYK_ORG_INT_ID' snyk-orgs.json) > snyk-orgs.json
            cat <<< $(jq 'del(.orgData[].integrations ["github-enterprise"])' snyk-orgs.json) > snyk-orgs.json 
            ```
       - If you are doing GitHub Enterprise integration:
            ```
            cat <<< $(jq 'del(.orgData[].integrations ["github"])' snyk-orgs.json) > snyk-orgs.json
            cat <<< $(jq '.orgData[].integrations.github-enterprise=env.SNYK_ORG_INT_ID' snyk-orgs.json) > snyk-orgs.json
            ```  
     