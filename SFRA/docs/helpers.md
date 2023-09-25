
## Helpers ## 

Helper functions make complicated or repetitive tasks a bit easier, 
and keep your code **DRY** (`Don’t Repeat Yourself`).

### Extend Helpers ### 

**how can the helper be extended?**.
If we have an exist helper in our base cartridge we need to duplicate
this and extend it very similar as a controller.

~~~javascript
'use strict'

//Here we don't use a server as a controller only use module.superModule
const base = module.superModule
~~~

Now, we need to export our base const. we can order our functions in two
ways:

~~~javascript
//First way
base.test = function(){}

module.exports = base;

//Second way
function test(){}

base.test = test;
module.export = base;
~~~