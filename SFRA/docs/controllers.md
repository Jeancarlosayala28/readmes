## Controllers ##  

The controllers are one of the most important parts of the proyect, with the controllers we can
define routes and the template that we want to see in that route, we can even send
information that we want to use in the template or add some validations if we user forms.

In this document you will learn how can extend the controllers, how you can add diferents
validations in the forms and how you can create your own controller with a template and
update the template if you want to use ajax.


### Table of contents  ###
1. [Controllers](#controllers)  
2. [Extend Controllers](#extend-controllers)  
    
    2.1 [Routes](#routes)

    2.2 [Replace](#replace)

    2.3 [Append](#append)

    2.4 [Prepend](#prepend) 

### Extend Controllers ###

Somethimes we need to extend the controllers when we want to validate a 
new fields in an existing form or when we need to add more attributes in 
our products.

<a name='routes'></a>
We can start with an existing controller for example `Product` controller. Into
the folder _Controllers_ we can see diferents files with diferents names, but we
need the file `Product.js`, we can use the tool [File Utils](https://marketplace.visualstudio.com/items?itemName=sleistner.vscode-fileutils).

With this tool we can duplicate the File in our custom cartridge,
you only need to check the route and change it if is necesary.

Once that you do that we need to check what route we need to extend,
in this case we use the route `Show`, we can remove the other routes and
we need to follow the next structure to extend the controller:

~~~javascript
'use strict'

const server = require('server')

//We need to use server.extend whenever we extend a controller
server.extend(module.superModule)
~~~

We have three options to extend the controllers:
  
  * Replace
  * Prepend
  * Append

<a name='replace'></a>

`Replace` is used when you want to completely replace a route,
for example change the logic in the route.

~~~javascript
server.replace('Show', server.middleware.get, (req, res, next) => {
  var attributes = {}
  
  res.render('myNewTemplate', {attributes: attributes});
  next();
})

module.exports = server.exports();
~~~

<a name='append'></a>

`Append` modifies the `Show` route by appending middleware that adds 
properties to the `viewData` object for rendering. Using `server.append`
causes a route to execute both the original middleware chain and any additional steps.

~~~javascript
server.append('Show', (req, res, next) => {
  const viewData = res.getViewData();

  //you can join into the viewData.product and add an extra section in this case reviews.
  viewData.product.reviews = 'Excelent product';

  //You can create even your custom attributes for example

  viewData.customData = 'custom information'

  /* 
    Somethimes you need to create an object if you want to do the same action as viewData.product
    because, if you try with a custom that is not exist for example viewData.customData.info
    you can receive an error, so you need to follow the next structure.
  */
  
  viewData.customData = {
    info: ''
  };

  //Now you can access into the info data in customData
  viewData.customData.info = 'The product has six items';

  res.setViewData(viewData);

  next();
})

module.exports = server.exports();
~~~

<a name='prepend'></a>

`Prepend` is very similar then `append`, the unique difference is prepend is
executed before than the other methods and the principal controller (`replace` and `append`).
Suppose that you need to get an information before that your main controller, you can get the 
information first using `prepend`

~~~javascript
var COHelpers = require("*/cartridge/scripts/checkout/checkoutHelpers")
var BasketMgr = require('dw/order/BasketMgr');

server.prepend('Show', (req,res,next) => {
  const viewData = res.getViewData();
  const currentBasket = BasketMgr.getCurrentBasket();

  viewData.shippingMethod = 'pickup';

  COHelpers.copyShippingAddressToShipment(
      viewData,
      currentBasket.defaultShipment
  );

  next();
})

module.exports = server.exports();
~~~