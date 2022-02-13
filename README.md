# Snyk-EZ
snyk-api-import the easy way (Github version)

---
1. Clone this repo: `git clone https://github.com/antz-snyk/snyk-ez.git`
    - Navigate into it: `cd snyk-ez`
2. Install [snyk-api-import](https://github.com/snyk-tech-services/snyk-api-import) tool
    - If you have NPM, this method is probably easiest: `npm install snyk-api-import@latest -g`
3. Get your [Github Org name](https://github.com/settings/organizations) (log in as user connected to a GH Organization), make a variable with it
    - Create Var --> `export SCM_ORG_NAME=<source code manager organization name>`
4. Make a new [Github token](https://github.com/settings/tokens)
   - Again, ensure token is created with a GH user connected to a GH Org
   - Ensure token is created with all repo permissions
   - Create Var --> `export GITHUB_TOKEN=<Github token>`
5. 