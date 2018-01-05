# di-container
Dependency Injection Container for Node.js based on book: 
Node.js Design Patterns - Second Edition
by Luciano Mammino; Mario Casciaro

## Installation

`$ npm install di-containerx`

## Usage

- To register named dependencies: `diContainer.register(<name>,<dependency>)`
- To register named factories: `diContainer.factory(<name>,<factory>)`
- Obtain instance from dependency container: `diContainer.get(<name>)`


### Example

```js
/* lib/main.js */
var main = function(async,path){

    var removeFile = function(callback){
        var path = path.resolve(__dirname);
        var work = [...];//validation,folder existance check
        async.waterfall(work,(err) => {
            if(err) return callback(err);

            callback(null);
        });
    };

    return {
        removeFile: removeFile
    }
};

module.exports = main;

/* index.js */
const diContainer = require('di-containerx')();

diContainer.register('path', require('path'));
diContainer.register('async', require('async'));
diContainer.factory('main', require('./lib/main'));

const main = diContainer.get('main');
main.removeFile((err) => {
    if(err) {
        console.log(err);
        return;
    }

    console.log("Working!");
});

```

# License

[MIT](LICENSE)
