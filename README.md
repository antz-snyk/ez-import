# Snyk-EZ
snyk-api-import the easy way (Github version)

*An opinionated way to quickly import repos from one Github org to one Snyk org; snyk-api-import utility is capable of a lot more, check out the main [url](https://github.com/snyk-tech-services/snyk-api-import) for more info*

---
## Set up

*prereqs: jq, maybe npm*

1. Install [snyk-api-import](https://github.com/snyk-tech-services/snyk-api-import) tool
   - Easiest way: `npm install snyk-api-import@latest -g`
2. Clone this repo: `git clone https://github.com/antz-snyk/snyk-ez.git`
   - Navigate into it: `cd snyk-ez`
3. Get your [Github Org name](https://github.com/settings/organizations), put that org name in snyk-orgs.json file
   - Ensure the Github user you log in with is connected to a Github Organization
   - Create Var --> `export GITHUB-ORG-NAME=<your GH organization name>`
   - Write this Var to snyk-orgs.json file --> `cat <<< $(jq '.orgData[].name=env.GITHUB-ORG-NAME' snyk-orgs.json) > snyk-orgs.json`
4. Make a new [Github Auth token](https://github.com/settings/tokens)
   - Again, ensure token is created with a Github user connected to a Github org
   - Ensure token is created with all of the repo permissions
   - Create Var --> `export GITHUB_TOKEN=<your Github token>`
5. 