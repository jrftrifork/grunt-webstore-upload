# grunt-webstore-upload

> Automate uploading process of the new versions of Chrome Extension or App to Chrome Webstore

## Getting Started
This plugin requires Grunt.

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-webstore-upload --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-webstore-upload');
```

## The "webstore_upload" task

### Overview
Read more about great ability to automate this task here: [Chrome Web Store Publish API](http://developer.chrome.com/webstore/using_webstore_api).
In your project's Gruntfile, add a section named `webstore_upload` to the data object passed into `grunt.initConfig()`.
#### Please noty, that you have to upload your extension first time manually, and then provide appID to update ( see below ). Also please make sure, that your draft ready to be published, ie all required fields was populated

```js
grunt.initConfig({
    webstore_upload: {
        //any browser path. Escape backslashes!
        "browser_path": browserPath, 

        "accounts": {
            "default": { //account under this section will be used by default
                publish: true, //publish item right after uploading. default false
                client_id: "ie204es2mninvnb.apps.googleusercontent.com",
                client_secret: "LEJDeBHfS"
            },
            "new_account": { 
                publish: true, //publish item right after uploading. default false
                client_id: "kie204es2mninvnb.apps.googleusercontent.com",
                client_secret: "EbDeHfShcj"
            }
        },
        "extensions": {
            "extension1": {
                //required
                appID: "jcbeonnlikcefedeaijjln",
                //required, we can use dir name and upload most recent zip file
                zip: "test/files/test1.zip"      
            },
            "extension2": {
                account: "new_account",
                //will rewrite values from 'account' section
                publish: false, 
                appID: "jcbeonnlplijjln",
                zip: "test/files/test2.zip"
            }
        }
    }
})
```

### Configuration

#### browser_path
Path to Browser executed file

Type: `String`

Required

#### accounts
List of the accounts (see *Accounts* section for details).

Type: `Object`

Required

#### extensions
List of the extension (see *Extensions* section for details).

Type: `Object`

Required

### Accounts
Since Google allows only 20 extensions under one account, you can create multiple records here.
It is object with arbitrary meaningful accounts names as a keys (see example above).
Special account named `default` will be used by defaults.

#### publish
Make item available at Chrome Webstore or not

Type: `Boolean`

Default value: `false`

Optional

#### client_id
[How to get it](http://developer.chrome.com/webstore/using_webstore_api#beforeyoubegin)
Client ID to access to Chrome Console API

Type: `String`

Required

#### client_secret
[How to get it](http://developer.chrome.com/webstore/using_webstore_api#beforeyoubegin)
Client Secret to access to Chrome Console API

Type: `String`

Required


### Extensions
It is object with arbitrary meaningful extensions names as a keys (see example above).

#### appID
Extension id or Application id at Chrome Webstore

Type: `String`

Required

#### zip
Path to zip file. Upload most recent zip file in case of path is directory

Type: `String`

Required

#### publish
Make item available at Chrome Webstore or not. 
This option under `extensions` will rewrite `publish` under related `account` section.

Type: `Boolean`

Default value: `false`

Optional

#### account
Name of the account, that we should use to upload extension. If ommited, `default` account will be used.

Type: `String`

Default value: `default`

Optional

### Migrating from < 0.7 versions
In order to move your existing config to new version, do following steps:
- Create new keys in config `accounts`, `extensions`  
- Move `browser_path` from `options` to top level
- Move `publish`, `client_id`, `client_secret` from `options` to `default` account
- Move all exntentions to `extension` section.
- Move `publish`, `zip`, `appID` from `options` of the extension to one level up
- Ask me, if something still broken :P

### Workflow
Read more about [Chrome Web Store Publish API](http://developer.chrome.com/webstore/using_webstore_api) and how to get Client ID and Client secret
+ execute `grunt webstore_upload` or `grunt webstore_upload:target` in order to upload zip files
+ browser should be opened
+ confirm privileges in browser ( we have to manually do this )
+ wait until uploading will be finished


## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).

## Release History
0.7.0 Allowed multiple accounts. Async multiple uploading. Redo configuration style.

0.5.1 Fix problem with path

0.5.0 Initial commit

## License
Copyright (c) 2014 Anton Sivolapov. Licensed under the MIT license.
