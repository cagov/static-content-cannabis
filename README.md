# Static content repo for cannabis.ca.gov

This is a content repository for https://headless.cannabis.ca.gov.

## How it works
* Content is created in WordPress.
* When posts, pages or media are added, updated or deleted a WordPress Notifications plugin will sent a webhook request to our AWS Lambda function.
* This AWS Lambda function is located at: https://github.com/cagov/cannabis-ca-gov-lambda-sync-github. This is an @architect arc.codes configuration. This is a framework for generating AWS CloudFormation configurations. This allows us to easily versin our build settings. That code is manually updated by a developer with necessary access tokens.
* A POST request to the AWS Lambda endpoint will run the wordpress-to-github scripts.
* This will run through a series of REST API endpoints and sync them to a target branch in github. * We are currently using these branches `main`, `staging` and `main-reduced-content` (debugging).
* Once content is written into the git repo, a series of GitHub workflow actions will run.
1. Version the static content change and submit an auto-merged pull request to this github repo, bumping the package number.
2. Call a workflow action in @cagov/cannabis.ca.gov repo. This will run a workflow that checks out the code, checks for a content update, and trigger the package.json to update, and will save that as a pull request.


## Preview link 
### Published content
* A preview link from the WordPress editor to the headless.cannabis.ca.gov can be accessed in the top admin toolbar. "View Live Site" - this will jump you over to the static build. 
### Pull request link
* When you submit a pull request to @cagov/cannabis.ca.gov, a preview link to your branch will be generated. Please note that this only updates the first time you submit the PR. If you need a fresh preview, close your pull request and open a new release.
### Staged content
* [Not yet released]
### Unpublished content
* Use the Enable Public Preview to generate a link that will expire in one week. This page will not be available on the production site.


## Time to update
* This whole process currently takes about 3 minutes. [Tests are currently disabled because we are revising our QA process.]
* To double check the pipeline
* Watch static-content-cannabis actions and make sure builds are running: https://github.com/cagov/static-content-cannabis/actions (Usually done in about 30-45 seconds. If there are many changes, it can get longer. If it gets stuck, manually/locally run the AWS Lambda service with `npm run start:debug`)
* Watch for updates on @cagov/cannabis.ca.gov: https://github.com/cagov/cannabis.ca.gov/actions



