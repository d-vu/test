# CBSI Revenue Report Automation for Adsense

This project automatically extracts reports from a Google Adsense account, configures the data, and uploads it to a specified Google Sheet.

It is currently configured to pull data from the following Adsense accounts, Cbsnews, Cnet_newsletters (CNET) and cnet_newsletters_test (Deals Now) to the following Google Sheet, https://docs.google.com/spreadsheets/d/1WeXQ8YD2lfkvQHRCeYTggC1K27YdKu6fQ_yyvJCwuTo/edit#gid=0



## Getting Started
#### Running locally
- [ ] Import secret files to root level
- [ ] Install dependencies
- [ ] Run Program

####  Running remotely via uploding to Amazon Web Services
- [ ]  Convert to AWS Lambda Function
- [ ] Upload to AWS console
- [ ] Configuring AWS Cloudwatch to run function periodically

## Running locally
### Import secret files to root level
Import the `adsenseConfig` folder contaning `config.json` and `credentials.json` at the root level.  The expected folder structure is shown below.

```
adsenseConfig
	config.json
	credentials.json
.gitIgnore
node_modules
clearSheet.js
	.
	.
	.  
uploadReport.js

```
###  Install dependencies
- [ ] navigate to the root directory and run `npm install`

###  Run Program
- [ ] Run `node index.js`

##  Running remotely via uploading to Amazon Web Services
```
Be sure to import the folder containing the secret files and download dependencies before continuing.
```

###  Convert to AWS Lambda Function

At the root level of project in the `index.js` file, modify the block of chain promises chain functions so that is is wrapped in function called `exports.handler` shown below

Before
```
getToken('adsenseUser', 'adsense')
	.then(payload => generateReport('afsh', payload))
	...
	.then(payload => sortSheet('cnet', payload))
	.then(() => console.log('Process is complete'))
	.catch(error => console.log('Error occured: ', error))

```
After
```
exports.handler = function(event, context, callback) {
    getToken('adsenseUser', 'adsense')
	    .then(payload => generateReport('afsh', payload))
		...
        .then(payload => sortSheet('cnet', payload))
        .then(() => console.log('Process is complete'))
        .catch(error => console.log('Error occured: ', error))
}
```

###  Upload to AWS console
Compress the project to a .zip file and upload to AWS by following the steps listed in this article.

http://dev.splunk.com/view/event-collector/SP-CAAAE6Z

```
Make sure you are compressing at root level and not a the folder level of the project
```

###   Configuring AWS Cloudwatch to run function periodically

tbd

## Built With

* [Googleapis](https://github.com/google/google-api-nodejs-client) Google's officially supported Node.js client library for accessing Google APIs
* [Dateformat](https://maven.apache.org/) - Format date
* [Request](https://rometools.github.io/rome/) - Handles HTTP requests
