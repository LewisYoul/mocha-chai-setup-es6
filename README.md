# Setting up Mocha and Chai to work with ES6

The aim of this repository is to summarise how to set up a test-framework for an ES6 JavaScript application:

**1 -** Create a new repository

**2 -** Inside that repository run `npm init`, this will create a package.json that will be required when you install node-modules.

**3 -** Install the Mocha testing framework as a dependency using `npm install --save mocha`

**4 -** Add the following code to a new test file at `test/test.js`:

```
var assert = require('assert');
describe('Array', function() {
  describe('#indexOf()', function() {
    it('should return -1 when the value is not present', function() {
      assert.equal([1,2,3].indexOf(4), -1);
    });
  });
});
```

**5 -** It will now be possible to run this test and see it pass by calling Mocha directly from your node_modules folder using `$ ./node_modules/mocha/bin/mocha`.

**6 -** However it would be better if we could just call npm test right? Lets add Mocha to our package.json:
```
"scripts": {
    "test": "mocha"
  }
```

We can now run our tests with `npm test`

**7 -** Now install the assertian library "chai" with `npm install --save chai`

**8 -** Here's where things get interesting. We need to import chai into our test file but we can't do that with ES6 syntax because Mocha gets confused. Therefore we need to install a transpiler. Babel to the rescue! Babel will essentially convert the new ES6 syntax into ES5 syntax that Mocha can read:

```
npm install babel-core --save-dev
npm install babel-preset-es2015 --save-dev
npm install babel-register --save-dev
```
I'd be lying if I said I knew what all of these commands do. They install Babel to transpile ES6 to ES5 essentially. The last thing we need to do is configure npm to know what to execute. Replace the test command in your package.json with this: `"test": "node node_modules/.bin/mocha --require babel-register"`

You will now be able to run `npm test` and your tests will pass. Wizard!

## Useful Websites

Mocha - https://mochajs.org/
Chai - http://chaijs.com/
Babel ES15 Preset - https://babeljs.io/docs/plugins/preset-es2015/
