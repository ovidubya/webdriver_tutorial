# Step 1

## Install NodeJS and npm

[Webdriver.io](http://webdriver.io/) requires  v4+ to run.

Go to [Node.js](https://nodejs.org/) and install either the LTS or current version. 

You should have an updated version of nodejs and npm. Type in your terminal

![Check versions](https://github.com/ovidubya/webdriver_tutorial/blob/master/Step1.gif)

By default, Mac computers will contain versions of node and npm but they are usaully outdated and its good to have the updated version.

# Step 2

## Create Project Directory


![Check versions](./step2.gif)

# Step 3

## Install package.json

package.json is a file that will manage all your projects dependencies and dev dependencies

It also contains lincense and author information, for this example, we will not be providing much information. Just the basics to get us started.

Type in your terminal:
```sh
$ npm init
```
This will bring a prompt on your terminal, you can choose to enter information, I just pressed enter for the default option.

![Install package.json](./step3.gif)


# Step 4

## Install Webdriver.io and chromedriver

Once you have package.json, your ready to install node modules. Type in your terminal

```sh
$ npm install webdriverio --save
$ npm install chromedriver --save
```



The --save means that it will save it in your package.json. You can also type --save-dev. This means that it will install webdriverio as a dev dependency. Dev dependcies do not get included when pushing into production. But since this demo is mainly used for webdriverio, we will not install it as a dev depenedncy.

Install webdriverio
![Install webdriverio](./step4.gif)

Install chromedriver
![Install chromedriver](./step4.1.gif)

After install, your project directory should look something like this:
![folder dir](./step4pic.png)

The node_modules folder is where all your modules live, as you keep installing more modules, your folder grows.

# Step 5 (optional)

## Allow intellij support in your javascript files.

This step is optional.Go to your package.json folder.

You dependecies should look something like this:
```sh
"dependencies": {
    "chromedriver": "^2.34.1",
    "webdriverio": "^4.10.1"
}
```
Add the following to it:
```sh
"dependencies": {
    "chromedriver": "^2.34.1",
    "webdriverio": "^4.10.1",
    "@types/node": "^8.5.2",
    "@types/webdriverio": "^4.8.7"
}
```
@types allows intellij support for webdriverio which is useful to get access to api.

Once you save it your package.json, go back to your terminal and type
```sh
$ npm install
```
![Install chromedriver](./step5.gif)

This command will install any packages that are listed in the package.json file but not in the node_modules folder.

# Step 6

## Configure test envirorment

For this demo, we will only test on our local machine. To test on devices on the clould you will need a subscription from either of these providers:

- browserstack
- saucelabs
- testingbot

For now we will install the modules needed to test on our machine. Make sure you have chrome installed on your computer otherwise, it wont work.

Type in your terminal and follow the same path. To select multiple options, use the space key, then hit enter once your done.

```sh
$ ./node_modules/.bin/wdio
```
![Install wdio conf](./step6.gif)

# Step 7

## Edit the config file

In  your `wdio.conf.js` you will have to make a few edits.

Change the browser to chrome.
```sh
capabilities: [{
    maxInstances: 5,
    browserName: 'chrome'
}],
```
Change the timeout to a big number so that tests never timeout if no user action happens.
```sh
mochaOpts: {
    ui: 'bdd',
    timeout: 99999999
},
```

Since we are not running a suite of tests, we can change it to a single folder and to a single file.
```sh
specs: [
    './test/simpleDemoTest.js'
],
```

After these changes have been made, go to your terminal and create a test folder. You will want to name it the same as the spec property in the wdio.conf.js file. 

![Install wdio conf](./step7.gif)


# Step 8

## Editing the test file

With your favorite editor, open the `simpleDemoTest.js` that you just created.

and type the following
```sh
describe('this is a simple test', function() {
    it('it will do a simple search and click', function(){
        
    });
});
```
Describe takes a String and a function. The string will be the description of what the test is. The It will be a more specfic explantion of what happens during the test. `All tests should be written in this format.`

The goal for the test is to navigate to google and do a search.

Within the it function, type the following code:
```sh
browser.url('https://www.google.com'); //goes to the url
browser.pause(2000); //pauses execution for 2 seconds
browser.setValue('input[name=q]', 'javascript WAT'); 
browser.keys('Enter'); //press the enter key
browser.pause(2000); //pause for 2 seconds
```

So you should have something like this:
```sh
describe('this is a simple test', function() {
    it('it will do a simple search and click', function(){
        browser.url('https://www.google.com'); 
        browser.pause(2000); 
        browser.setValue('input[name=q]', 'javascript WAT'); 
        browser.keys('Enter'); 
        browser.pause(2000); 
    });
});
```
To learn more about the the webdriver api, visit this link: http://webdriver.io/api.html
# Step 8

## Running the test file

To run the test file, type in your console
```sh
$ ./node_modules/.bin/wdio wdio.conf.js
```
The first part `./node_modules/.bin/wdio` uses webdriver, the2nd part `wdio.conf.js` is the config file we want to run.

![Install wdio conf](./step8.gif)

# Step 9

## todo

# Step 10

## todo
