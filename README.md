API Chaining
API Chaining is a design pattern that allows multiple API calls to be combined into a single request, streamlining interactions and reducing the overhead of multiple network requests. This approach is particularly useful in scenarios where sequential API calls are necessary, as it enhances performance and simplifies client-server communication.

Features
Sequential API Calls: Chain multiple API calls in a defined sequence within a single request.
Reduced Latency: Minimize the delay associated with multiple network round-trips by consolidating requests.
Simplified Client Logic: Offload complex API interaction logic from the client to the server, leading to cleaner client-side code.
Installation
To integrate API Chaining into your project, you can install the package via npm:

bash
npm install api-chain
This will add the api-chain module to your project's dependencies.

Usage
Below is an example demonstrating how to set up and use API Chaining in a Node.js environment:

javascript
// Import the api-chain module
const api = require('api-chain');

// Define your API by passing methods to create
const fs = api.create({
  read: require('fs').readFile,
  toString: function (data, next) {
    next(null, data.toString());
  },
  view: function (contents) {
    console.log(contents);
  }
});

// Use the chainable 'fs' API as created above
fs.read('./example.txt')
  .toString()
  .view();
In this example, the fs object is enhanced with chainable methods that allow for reading a file, converting its contents to a string, and then viewing the contents—all in a streamlined, sequential manner.

Options
API Chaining provides several configurable options to tailor its behavior:

onError: A function called when an error is emitted, unless the error method is overwritten.
throwErrors: A boolean indicating whether to throw unhandled errors (ignored if onError exists). Default is true.
continueErrors: A boolean indicating whether to resume execution of commands after errors occur. Default is false.
These options can be set to customize error handling and control flow according to your application's requirements.

Built-in Chainable Methods
API Chaining includes several built-in methods to enhance control flow:

api.wait(n): Pauses execution flow for n milliseconds.
api.until(fn): Waits until the callback function fn returns true before continuing execution.
api.chain(fn): Adds a callback function to be executed next in the control flow stack.
These methods provide flexibility in managing asynchronous operations within your API chains.

Immediate Methods
The following methods execute immediately (rather than within the control flow) and always return the API object:

api.setOption(option, value): Sets a specific option to the given value.
api.setOptions(options): Sets multiple options at once based on a collection of key/value pairs.
These immediate methods allow for dynamic configuration of the API chaining behavior.

Testing
To test your API chains, ensure that the development dependencies are installed. Navigate to the directory where api-chain is installed and run:

bash
npm install
After the installation of dependencies is complete, execute:

bash
npm test
This will launch the test runner, allowing you to verify the functionality of your API chains.

License
This project is licensed under the MIT License. For more details, refer to the license.txt file included in the repository.
