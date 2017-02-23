# CBSI Revenue Report Automation for Adsense

This project automatically extracts reports from a Google Adsense account, configures the data, and uploads it to a specified Google Sheet.

It is currently configured to pull data from the following Adsense accounts
- Cbsnews
- Cnet_newsletters (CNET)
- cnet_newsletters_test (Deals Now)

to the following Google Sheet,
https://docs.google.com/spreadsheets/d/1WeXQ8YD2lfkvQHRCeYTggC1K27YdKu6fQ_yyvJCwuTo/edit#gid=0



## Getting Started
#### Running locally
- [ ] Import secret files to root level
- [ ] Install dependencies
- [ ] Run Program

#### Running remotely
- [ ]  Convert to AWS Lambda Function
- [ ] Upload to AWS console

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
Compress the project to a .zip file.
**Make sure you are compressing**
### Installing

A step by step series of examples that tell you have to get a development env running

Say what the step will be

```
Give the example
```

And repeat

```
until finished
```

End with an example of getting some data out of the system or using it for a little demo

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags).

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details
