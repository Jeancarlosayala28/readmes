<a name="Top"></a>
# SFRA #

### Table of contents ###

1. [SFRA](#sfra)  

    1.1 [The latest version](#the-latest-version)  

    1.2 [Getting Started](#getting-started)  

2. [NPM scripts](#npm-scripts)
    
    2.1 [Compiling your application](#compiling-your-application)
    
This project contains differents cartridges that we use for his functionality. 
Store Front Reference Architecture has a base cartridge (`app_storefront_base`) provided by Commerce Cloud that is never directly customized or edited.

Instead, we can create a new cartridge for customization and we can put it on top of the base cartridge following the next estructure only to custom cartridges [app_custom_proyectname]() for example `app_custom_test`. 
This change is intended to allow for easier adoption of new features and bug fixes.

### The latest version ###

The latest version of SFRA is `6.3.0`

### Getting Started ###

1. Clone this [repository](https://github.com/PuntoCommerce/storefront-reference).

2. Once that you´re located in the project folder need run `npm install` to install all of the local dependencies in the `package.json`

3. Run `npm run compile:js` from the command line that would compile all client-side JS files. Run `npm run compile:scss` and `npm run compile:fonts` that would do the same for css and fonts.
You can also run `npm run build` and it will automatically execute the last commands we mentioned.

4. Create `dw.json` file in the root of the project. Providing a [WebDAV access key from BM](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp?topic=%2Fcom.demandware.dochelp%2Fcontent%2Fb2c_commerce%2Ftopics%2Fadmin%2Fb2c_access_keys_for_business_manager.html) 
in the `password` field is optional, as you will be prompted if it is not provided.
```json
{
    "hostname": "your-sandbox-hostname.demandware.net",
    "username": "AM username like me.myself@company.com",
    "password": "your_webdav_access_key",
    "code-version": "version_to_upload_to"
}
```

5. You need a [propheat](https://marketplace.visualstudio.com/items?itemName=SqrTT.prophet) extention on your visual studio code to 
upload cartridges to the sandbox you specified in `dw.json` file.

6. Add the `app_storefront_base` cartridge and your custom cartridge to your cartridge path in _Administration >  Sites >  Manage Sites > RefArch - Settings_.

7. You should now be ready to navigate to and use your site.

# NPM scripts #
Use the provided NPM scripts to compile and upload changes to your Sandbox.

### Compiling your application ###

Compiles all .scss files into CSS.
~~~bash
npm run compile:scss
~~~

Compiles all .js files and aggregates them.
~~~bash
npm run compile:js
~~~

Copies all needed font files. Usually, this only has to be run once.
~~~bash
npm run compile:fonts
~~~

Compiles all .scss, .js and fonts.
~~~bash
npm run build
~~~

If you are having an issue compiling scss files, try running 'npm rebuild node-sass' from within your local repo.


# Way of work #

We need to have a way of work in our projects from cartridge 
to how to extend a controller.

### Cartridges ###

We allways need to work in our custom cartridge if we want to
extend a controller, helper, template, create a service conection or
even if we need to create a js file. We can use
[File Utils](https://marketplace.visualstudio.com/items?itemName=sleistner.vscode-fileutils)
to duplicate files more easy and fast.

### Extra Files ###

1. [Controllers](docs/controllers.md)

    1.1 [Extend Controllers](docs/controllers.md#extend-controllers)

2. [Helpers](docs/helpers.md)

[Back to the top](#Top)