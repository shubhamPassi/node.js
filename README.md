<!-- @format -->

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

# Learn and understand nodejs

## Table of Contents

- [Learn and understand nodejs](#learn-and-understand-nodejs)

  - [**1.Intro**](#1intro)
    <details>
    <summary>Click to expand!</summary>

    - [Needs to make a web server](#needs-to-make-a-web-server)
    </details>

  - [2.Modules, Export and Require](#2modules-export-and-require)
    <details>
    <summary>Click to expand!</summary>

    - [Common JS Modules](#common-JS-modules)
    - [Function constructor](#function-constructor)
    - [Immediately Invoked Functions Expressions (IIFEs)](#immediately-invoked-functions-expressions-iifes)
    - [How Modules Work](#how-modules-work)
    - [The Path resolving algorithm](#the-path-resolving-algorithm)
    - [The module cache](#the-module-cache)
    - [Module Patterns](#module-patterns)
    - [Module definition patterns](#module-definition-patterns)
      <details>

      - [Named exports](#named-exports)
      - [Exporting a function](#exporting-a-function)
      - [Exporting a constructor](#exporting-a-constructor)
      - [Exporting an instance](#exporting-an-instance)
      </details>

    - [Monkey patching](#monkey-patching)
    - [Wiring Modules](#wiring-modules)
    - [cohesion & coupling](#cohesion-&-coupling)
    - [Stateful & Stateless modules](#Stateful-&-Stateless-modules)
    - [Modules and ES6](#modules-and-es6)
    </details>

  - [3.Events And EventEmitter](#3events-and-eventemitter)
    <details>
    <summary>Click to expand!</summary>

    - [Events](#events)
    - [Our Event Emitter](#our-event-emitter)
    - [Magic String](#magic-string)
    - [Inheriting from event emitter](#inheriting-from-event-emitter)
    - [ES6 Classes](#es6-classes)
    - [Extending the EventEmitter](#extending-the-eventemitter)
    </details>

  - [4.Asyncchronous](#4asyncchronous)
    <details>
    <summary>Click to expand!</summary>

    - [livuv with setInterval or setTimeOut](#livuv-with-setinterval-or-settimeout)
    - [Reactor Pattern](#reactor-pattern)
    - [Event Queue](#event-queue)
    - [Timers queue](#timers-queue)
    - [Immediates Queue](#immediates-queue)
    - [setTimeout vs setImmediate](#settimeout-vs-setimmediate)
    - [Native Promises](#native-promises)
    - [Q and Bluebird](#q-and-bluebird)
    </details>

  - [5. Buffer and Streams](#buffer-and-streams) - [callback function](#callback-function) - [libuv](#libuv) - [Buffer](#buffer) - [Stream](#stream) - [Binary data](#binary-data) - [Character sets](#character-sets) - [Encoding](#encoding)
    <details>
    <summary>Click to expand!</summary>

    - [Buffers](#buffers)
    - [ArrayBuffer](#arraybuffer)
    - [Callbacks](#callbacks)
    - [Files](#files) - [Error First Callback](#error-first-callback)
    - [Streams](#streams) - [Chunk](#chunk)
    - [Pipes](#pipes) - [Method chaining](#method-chaining)
    </details>

  - [6.HTTP](#5http) - [Protocol](#protocol) - [Port](#port) - [HTTP](#http) - [MIME Type](#mime-type) - [http_parser](#httpparser)
    <details>
    <summary>Click to expand!</summary>

    - [HTTP server](#http-server)
    - [Output HTML and Templates](#output-html-and-templates) - [Template](#template)
    - [Streams and Performance](#streams-and-performance) - [API](#api) - [Endpoint](#endpoint)
    - [Outputting a JSON](#outputting-a-json) - [Serialize](#serialize) - [Deserialize](#deserialize)
    - [Routing](#routing)
    </details>

  - [7.NPM](#6npm) - [Semantic Versioning](#semantic-versioning)
    <details>
    <summary>Click to expand!</summary>

    - [Package.json](#packagejson)
    - [Global dependencies](#global-dependencies) - [nodemon](#nodemon)
    </details>

  - [8.Express](#7express) - [Environment variables](#environment-variables) - [Http method (verbs)](#http-method-verbs)
    <details>
    <summary>Click to expand!</summary>

    - [Routes](#routes)
    - [Static Files and Middleware](#static-files-and-middleware) - [Midleware](#midleware)
    - [Templates and Template Engines](#templates-and-template-engines)
    - [Querystring and Post Parameters](#querystring-and-post-parameters)
      - [Querystring](#querystring)
      - [Form Post](#form-post)
      - [Post as json](#post-as-json)
    - [RESTful API and JSON](#restful-api-and-json) - [REST](#rest)
    - [Structuring the Application](#structuring-the-application)

      - [Structuring with Express](#structuring-with-express)
      - [Our own Structure](#our-own-structure)
      </details>

    - [9.MEAN](#8mean) - [DOM](#dom)
      <details>
      <summary>Click to expand!</summary>

      - [Angular](#angular)
      - [Separating Server code from Client code](#separating-server-code-from-client-code)
      </details>

    - [10.Build an app](#9build-an-app)
      <details>
      <summary>Click to expand!</summary>

      - [1. Init](#1-init)
      - [2. Connect to the Database](#2-connect-to-the-database)
      - [3. Adding Data](#3-adding-data)
      - [4. Create the API](#4-create-the-api)
      </details>

    <!-- /TOC -->

  # 1.Intro

  ## Needs to make a web server

  - Better ways to organize our code into reusable pieces
  - Ways to deal with files
  - Ways to deal with databases
  - The ability to communicate over the Internet
  - The ability to accept requests and send responses
  - A way to deal with work that takes long time

  **[⬆ back to top](#table-of-contents)**

  # 2.Modules, Export and Require

  ## Common JS Modules

  CommonJS is a group with the aim to standardize the JavaScript ecosystem, and one of their most popular proposals is called CommonJS modules.

  CommonJS modules - An agreed upon standard for how code modules should be structured.

  **[⬆ back to top](#table-of-contents)**

  ## Function constructor

  A function used to build objects using `new`

  ```javascript
  function Person(firstname, lastname) {
    this.firstname = firstname;
    this.lastname = lastname;
  }

  Person.prototype.greet = function () {
    console.log("Hello, " + this.firstname + " " + this.lastname);
  };

  var john = new Person("John", "Doe");
  john.greet();
  ```

  **[⬆ back to top](#table-of-contents)**

  ## Immediately Invoked Functions Expressions (IIFEs)

  Run the function at the point it is created. Add a `()` after its declaration.

  ```javascript
  var firstname = "Jane";

  (function (lastname) {
    var firstname = "John";
    console.log(firstname);
    console.log(lastname);
  })("Doe");

  console.log(firstname);
  ```

  **[⬆ back to top](#table-of-contents)**

  ## How Modules Work

  When we pass path to require function then nodejs create a function around the content of a module, wraps it into a private scope, and evaluates it.

  ```javascript
  function loadModule(filename, module, require) {
    const wrappedSrc = `(function(module, exports, require) {
                          ${fs.readFileSync(filename, "utf8")}
                        })(module, module.exports, require);`;
    eval(wrappedSrc);
  }
  ```

  **Under the hood**

  1. Resolve Path: A module name is accepted as input, and the very first thing that we do is resolve the full path of the module, **_which we call id_**. This task is delegated to require.resolve(), which implements a specific resolving algorithm.

  2. If the module has already been loaded in the past, it should be available in the cache. In this case, we just return it immediately.

  3. If the module was not loaded yet, we set up the environment for the first load. In particular, we create a module object that contains an exports property initialized with an empty object literal. This property will be used by the code of the module to export any public API.

  4. The module object is cached

  5. The module source code is read from its file and the code is evaluated, as we have seen before. The module exports its public API by manipulating or replacing the module.exports object.

  6. Finally, the content of module.exports, which represents the public API of the module, is returned to the caller.

  ```javascript
  const require = (moduleName) => {
    console.log(`Require invoked for module: ${moduleName}`);
    const id = require.resolve(moduleName); //[step 1]
    if (require.cache[id]) {
      //[step 2]
      return require.cache[id].exports;
    }
    //module metadata
    const module = {
      //[step 3]
      exports: {},
      id: id,
    };
    //Update the cache
    require.cache[id] = module; //[step 4]
    //load the module
    loadModule(id, module, require); //[step 5]
    //return exported variables
    return module.exports; //[step 6]
  };
  require.cache = {};
  require.resolve = (moduleName) => {
    /* resolve a full module id from the moduleName */
  };
  ```

  **[⬆ back to top](#table-of-contents)**

  ## The Path resolving algorithm

  As we saw, the resolve() function takes a module name (which we will call here, moduleName) as input and it returns the full path of the module.

  This path is then used to load its code and also to identify the module uniquely. The resolving algorithm can be divided into the following three major branches:

  The resolving algorithm can be divided into the following three major branches:

  1. File modules: If moduleName starts with / , it is already considered an absolute path to the module and it's returned as it is. If it starts with ./, then moduleName is considered a relative path, which is calculated starting from the requiring module.

  2. Core modules: If moduleName is not prefixed with / or ./, the algorithm will first try to search within the core Node.js modules.

  3. Package modules: If no core module is found matching moduleName, then the search continues by looking for a matching module in the first node_modules directory that is found navigating up in the directory structure starting from the requiring module. The algorithm continues to search for a match by looking into the next node_modules directory up in the directory tree, until it reaches the root of the filesystem.

  **[⬆ back to top](#table-of-contents)**

  ## The module cache

  Each module is only loaded and evaluated the first time it is required, since any subsequent call of require() will simply return the cached version.
  Caching is crucial for performance, but it also has some important functional implications:

  1. It makes it possible to have cycles within module dependencies
  2. It guarantees, to some extent, that the same instance is always returned when requiring the same module from within a given package

  The module cache is exposed via the require.cache variable, so it is possible to directly access it if needed.

  **[⬆ back to top](#table-of-contents)**

  ## Module Patterns

  **The revealing module pattern**
  One of the major problems with JavaScript is the absence of namespacing. Programs that run in the global scope polluting it with data that comes from both internal application code and dependencies. A popular technique to solve this problem is called the revealing module.

  ```javascript
  const module = (() => {
    const privateFoo = () => {...};
    const privateBar = [];
    const exported = {
      publicFoo: () => {...},
      publicBar: () => {...}
    };
    return exported;
  })();
  console.log(module);
  ```

  This pattern leverages a self-invoking function to create a private scope, exporting only the parts that are meant to be public.

  **[⬆ back to top](#table-of-contents)**

  ## Module definition patterns

  ### Named exports

  The most basic method for exposing a public API is using named exports, which consists of assigning all the values we want to make public to properties of the object referenced by exports (or module.exports).

  ```javascript
  //file logger.js
  exports.info = (message) => {
    console.log("info: " + message);
  };
  exports.verbose = (message) => {
    console.log("verbose: " + message);
  };
  ```

  ### Exporting a function

  One of the most popular module definition patterns consists of _reassigning the whole module.exports variable to a function_.

  Its main strength is the fact that it exposes only a single functionality, which provides a clear _entry point for the module_, making it simpler to understand and use; it also honors the principle of small surface area very well.

  This way of defining modules is also known in the community as the _substack pattern_

  ```javascript
  module.exports.verbose = (message) => {
    console.log(`verbose: ${message}`);
  };
  ```

  ### Exporting a constructor

  This pattern we allow the user to create new instances using the constructor, but we also give them the ability to extend its prototype and forge new classes.

  ```javascript
  //file logger.js
  function Logger(name) {
    this.name = name;
  }
  Logger.prototype.log = function (message) {
    console.log(`[${this.name}] ${message}`);
  };
  Logger.prototype.info = function (message) {
    this.log(`info: ${message}`);
  };
  Logger.prototype.verbose = function (message) {
    this.log(`verbose: ${message}`);
  };
  module.exports = Logger;
  ```

  **OR**
  Given that ES2015 classes are just syntactic sugar for prototypes, the usage of this module will be exactly the same as its prototype-based alternative.

  Exporting a constructor or a class still provides a single entry point for the module, but compared to the substack pattern, it exposes a lot more of the module internals; however,on the other hand it allows much more power when it comes to extending its functionality.

  ```javascript
  class Logger {
    constructor(name) {
      this.name = name;
    }
    log(message) {
      console.log(`[${this.name}] ${message}`);
    }
    info(message) {
      this.log(`info: ${message}`);
    }
    verbose(message) {
      this.log(`verbose: ${message}`);
    }
  }
  module.exports = Logger;
  ```

  ### Exporting an instance

  ```javascript
  //file logger.js
  function Logger(name) {
    this.count = 0;
    this.name = name;
  }
  Logger.prototype.log = function (message) {
    this.count++;
    console.log("[" + this.name + "] " + message);
  };
  module.exports = new Logger("DEFAULT");
  ```

  Because the module is cached, every module that requires the logger module will actually always retrieve the same instance of the object, thus sharing its state. This pattern is very much like creating a singleton; however, it does not guarantee the uniqueness of the instance across the entire application,

  ## Monkey patching

  We said a module can modify other modules or objects in the global scope; well, this is called monkey patching.

  **[⬆ back to top](#table-of-contents)**

  ## Wiring Modules

  **The most important patterns related to Wiring Modules**

  1. Hardcoded dependency
  2. Dependency Injection
  3. Service locator
  4. Dependency Injection containers

  In the worst case, the components are so tightly connected together that it becomes impossible to add or change anything without refactoring or even completely rewriting entire parts of the application. This, of course, does not mean that we have to over-engineer our design starting from the very first module, but surely finding a good balance from the fffginning can make a huge difference.

  **[⬆ back to top](#table-of-contents)**

  ### cohesion & coupling

  The two most important properties to balance when building modules are

  1. cohesion: This is a measure of the correlation between the functionalities of a component.

  High cohesion refers to a component that is very well defined. Meaning that it serves only one purpose and it accomplishes that purpose very well. If you have a component that reads from a database, sends an email, prints out documents, then it does not have high cohesion. Each one of those should be separated out into its own component.

  For example, a module that does only one thing, where all its parts contribute to that one single task has a high cohesion.

  By having a component do only one thing you can gain many benefits, such as testing only what you need, separation of concerns, and ease of maintenance.

  A module that contains functions to save any type of object into a database—saveProduct(), saveInvoice(), saveUser(), and so on has a low cohesion.

  2. coupling: : This measures how much a component is dependent on the other
     components of a system.

  Loose coupling refers to how much a component of code knows about the inner workings of another component of code. If it depends on knowing too much about a certain component, then it is considered highly coupled. When a component doesn’t know too much about the inner workings of other components it is considered loosely coupled.

  For example, a module is tightly coupled to another module when it directly reads or modifies the data of the other module.

  - Also, two modules that interact via a global or shared state are tightly coupled.
  - On the other hand, two modules that communicate only via the passing of parameters are loosely coupled.

  The desirable scenario is to have a high cohesion and a loose coupling, which usually results in more understandable, reusable, and extensible modules

  **[⬆ back to top](#table-of-contents)**

  ### Stateful & Stateless modules

  **stateful**: stateful applications require backing storage.
  Stateful applications like the Cassandra, MongoDB and mySQL databases all require some type of persistent storage that will survive service restarts.

  **stateless**: stateless applications don't “store”.

  **Stateful Module** — a module that exposes an instance of some stateful object (db connection, third party service instance, socket and etc).

  When working with stateful module you should have a Singleton pattern to make sure all the other modules that require the stateful module access the same instance.

  **Stateless Module** - a module that exposes stateless entities like classes or utility methods.

  It’s far more important to be careful when working with stateful modules than the stateless ones. While having tight coupling within the stateless modules can be bad for your architecture.

  **[⬆ back to top](#table-of-contents)**

  ### The Singleton pattern in Node.js

  - Exporting an instance using module.exports is already enough to obtain something very similar to the Singleton pattern.

  ```javascript
  //'db.js' module
  module.exports = new Database("my-app-db");
  ```

  Note:

  1. The module is cached using its full path as lookup key, therefore it is guaranteed to be a Singleton only within the current package.

  2. Each package might have its own set of private dependencies inside its node_modules directory, which might result in multiple instances of the same package and therefore of the same module, with the result that our Singleton might not be single anymore.

  for example, the case where the db module is wrapped into a package named mydb.
  Now consider the following package dependency tree:

  ```
  app/
  `-- node_modules
    `-- packageA
      `-- node_modules
          `-- mydb
    `-- packageB
      `-- node_modules
          `-- mydb
  ```

  Both packageA and packageB have a dependency on the mydb package; in turn, the app package, which is our main application, depends on packageA and packageB.
  Both packageA and packageB will actually load two different instances of our pretending Singleton because the mydb module will resolve to a different directory depending on the package it is required from.

  **[⬆ back to top](#table-of-contents)**

  ## Modules and ES6

  **greet.js**

  ```javascript
  export function greet() {
    console.log("Hello");
  }
  ```

  **app.js**

  ```javascript
  import * as greetr from "greet";
  greetr.greet();
  ```

  **[⬆ back to top](#table-of-contents)**

  # 3.Events And EventEmitter

  ## Events

  Something that has happened in our application that we can respond to

  - **System Events**: C++ core (libuv). This events handle by c library libuv.
  - **Custom Events**: Javascript core (Event Emitter)

  **[⬆ back to top](#table-of-contents)**

  ### Our Event Emitter

  **Emitter.js**

  ```javascript
  function Emitter() {
    this.events = {};
  }

  Emitter.prototype.on = function (type, listener) {
    this.events[type] = this.events[type] || [];
    this.events[type].push(listener);
  };

  Emitter.prototype.emit = function (type) {
    if (this.events[type]) {
      this.events[type].forEach(function (listener) {
        listener();
      });
    }
  };

  module.exports = Emitter;
  ```

  **app.js**

  ```javascript
  var Emitter = require("./emitter");

  var emtr = new Emitter();

  emtr.on("greet", function () {
    console.log("Somewhere, someone said hello.");
  });

  emtr.on("greet", function () {
    console.log("A greeting occurred!");
  });

  console.log("Hello!");
  emtr.emit("greet");
  ```

  **[⬆ back to top](#table-of-contents)**

  ### Magic String

  A String that has some special meaning in our code. Bad because of typos.
  Use config files instead.

  ```javascript
  module.exports = {
    events: {
      GREET: "greet",
    },
  };
  ```

  ```javascript
  var Emitter = require("events");
  var eventConfig = require("./config").events;

  var emtr = new Emitter();

  emtr.on(eventConfig.GREET, function () {
    console.log("Somewhere, someone said hello.");
  });

  emtr.on(eventConfig.GREET, function () {
    console.log("A greeting occurred!");
  });

  console.log("Hello!");
  emtr.emit(eventConfig.GREET);
  ```

  **[⬆ back to top](#table-of-contents)**

  ## Inheriting from event emitter

  Set to our object a prototype of the Emitter
  Allow us create objects with the Emitter properties

  ```javascript
  var EventEmitter = require("events");
  var util = require("util");

  function Greetr() {
    // This is call to a "function constructor"
    EventEmitter.call(this); //<-- also called "super constructor"
    this.greeting = "Hello world!";
  }

  util.inherits(Greetr, EventEmitter); //<--

  Greetr.prototype.greet = function (data) {
    console.log(this.greeting + ": " + data);
    this.emit("greet", data);
  };

  var greeter1 = new Greetr();

  greeter1.on("greet", function (data) {
    console.log("Someone greeted!: " + data);
  });

  greeter1.greet("Tony");
  ```

  **[⬆ back to top](#table-of-contents)**

  ## ES6 Classes

  ```javascript
  "use strict"; // like 'lint' for javascript

  class Person {
    constructor(firstname, lastname) {
      this.firstname = firstname;
      this.lastname = lastname;
    }

    greet() {
      console.log("Hello, " + this.firstname + " " + this.lastname);
    }
  }
  ```

  **[⬆ back to top](#table-of-contents)**

  ## Extending the EventEmitter

  ```javascript
  var EventEmitter = require("events");

  class Greetr extends EventEmitter {
    constructor() {
      super();
      this.greeting = "Hello world!";
    }

    greet(data) {
      console.log(`${this.greeting}: ${data}`);
      this.emit("greet", data);
    }
  }
  ```

  **[⬆ back to top](#table-of-contents)**

  # 4.Asyncchronous

  Javascript is synchronous, V8 engine is synchronous
  Node.js is asynchronous

  **Nodejs is separated in two dependencies**
  
  ![Nodejs overview](lib_uv.png)
  
  - v8: An open source JS engine created by google. Its main purpose is to execute JS code outside of the browser

    - V8 compiles JavaScript directly to native machine code using just-in-time compilation before executing it.

    - The compiled code is additionally optimized (and re-optimized) dynamically at runtime, based on heuristics of the code's execution profile. Optimization techniques used include inlining, elision of expensive runtime properties, and inline caching.

  - libuv: A c++ open source project that gives node access to the operating system underline file system, networking and some aspects of concurrency.

  ![Nodejs internals](nodejs-internals.png)

                  <details>

                  <summary>V8 Engine Architecture</summary>

  ![](v8-engine-architecture-1.png)

  ![](v8-engine-architecture.png)

                  </details>

  **Nodejs is javscript runtime**
  Javascript runtime refers to where your javascript code is executed when you run it.

  **Browser**: Javascript engine, web api, callbacks queue, microtask queue and event loop is part of javascript runtime.

  ![](browser-javascript-runtime.png)

  **Nodejs**: Javascript engine, libuv, timer queue, I/O queue, immediate queue, close event queue, nexttick queue, microtask queue and event loop is part of javascript runtime in nodejs.

  ![](nodejs-system-diagram.jpg)

  The event loop is the central part of Libuv and it runs on the main thread. It is a semi-infinite loop. It keeps running until there is still some work to be done (e.g. unexecuted code, active handlers, or requests), and when there is no more work the loop exists (process.exit).

  Nodejs is asynchronous because thing happening between v8 and libuv in parallel.

  **[⬆ back to top](#table-of-contents)**

  ## livuv with setInterval or setTimeOut

  1. Timer callbacks are executed as part of the NodeJS event loop. When you call setTimeout or setInterval, libuv (the C library which implements the NodeJS event loop) creates a timer in a 'min heap' data structure which is called the timers heap. In this data structure, it keeps track of the timestamp that each timer expires at.

  2. At the start of each fresh iteration of the event loop, libuv calls uv\_\_update_time which in turn calls a syscall to get the current time and updates the current loop time up to a millisecond precision.

  3. Right after that step comes the first major phase of the event loop iteration, which is timers phase. At this phase, libuv calls uv_run_timers to process all the callbacks of expired timers. During this phase, libuv traverses the timers heap to identify expired timers based on the 'loop time' it just updated using uv_update_time. Then it invokes the callbacks of all those expired timers.

  ```javascript
  while (r != 0 && loop->stop_flag == 0) {
    uv__update_time(loop);
    uv__run_timers(loop);

    r = uv__loop_alive(loop);
    if (mode == UV_RUN_ONCE || mode == UV_RUN_NOWAIT)
      break;
  }
  ```

  **[⬆ back to top](#table-of-contents)**

  ## Reactor Pattern

  [Reference to this understanding](https://blog.insiderattack.net/event-loop-and-the-big-picture-nodejs-event-loop-part-1-1cb67a182810)

  NodeJS works in an event-driven model that involves an Event Demultiplexer and an Event Queue. All I/O requests will eventually generate an event of completion/failure or any other trigger, which is called an Event.

  These events are processed according to the following algorithm.

  1. Event demultiplexer receives I/O requests and delegates these requests to the appropriate hardware.
  2. Once the I/O request is processed (e.g, data from a file is available to be read, data from a socket is available to be read, etc.), event demultiplexer will then add the registered callback handler for the particular action in a queue to be processed. These callbacks are called events and the queue where events are added is called the Event Queue.
  3. When events are available to be processed in the event queue, they are executed sequentially in the order they were received until the queue is empty.
  4. If there are no events in the event queue or the Event Demultiplexer has no pending requests, the program will complete. Otherwise, the process will continue from the first step.

  ![](reacter-pattern.jpeg)

  Event demultiplexer is not a single component which does all the types of I/O in all the OS platforms.

  The Event queue is not a single queue as displayed here where all the types of events are queued in and dequeued from.

  I/O is not the only event type that is getting queued.

  - As we saw, in the real world it is really difficult to support all the different types of I/O (file I/O, network I/O, DNS, etc.) in all the different types of OS platforms. Some I/O can be performed using native hardware implementations while preserving complete asynchrony, and there are certain I/O types which should be performed in the thread pool so that the asynchronous nature can be guaranteed.

  - To govern this entire process while supporting cross-platform I/O, there should be an abstraction layer that encapsulates these inter-platform and intra-platform complexities and expose a generalized API for the upper layers of Node.

  - I/O is not the only type of tasks performed on the thread pool. There are some Node.js crypto functions such as crypto.pbkdf2, async versions of crypto.randomBytes,crypto.randomFill and async versions of zlib functions which run on the libuv thread pool because they are highly CPU intensive.

  **For Better Understanding of Event Loop working**
  
  [Reference to this understanding](https://medium.com/@vishalkalaskar/we-must-have-come-across-the-terms-callbacks-non-blocking-i-o-and-event-looping-while-927a5e2150c0)

  Here is an attempt to explain!
  
  What is Event Looping?
  
  At start, we will go through concepts of Blocking and Non-Blocking executions, then jumping on to the ‘Event Loops by Reactor Pattern’!

  Consider examples like reading a file into the application, or an http request to a third party api’s. There are two ways we can perform these I/O operations:

  Blocking I/O: Where, application will make a function call and pause its execution at this point until the data is received.

  Non-Blocking I/O: Where, application will make a function call, and, without waiting for the results, continue its execution.
Former is called as ‘Synchronous’, while later is called as Asynchronous’ nature of execution, and NodeJS as you know, is Asynchronous in nature.
So, despite being single-threaded framework, How NodeJS works asynchronously?

  Answer is, **Reactor Pattern** – which is at the heart of NodeJS.

  But, what is Event Looping?
  
  “It is a magical place filled with unicorns and rainbows.“
  To explain this, we will compare two patterns of Event-Driven programming:

  1. **`Busy Waiting`**:
In which, continuous checks on resources is done to see if data is ready for further processing, – called as Active Polling

```javascript
resources = [socketA, socketB, pipeA];
while(!resources.isEmpty()) {
  for(i=0; i < resources.length; i++) {
    resource = resources[i];

    // try to load
    var data = resource.read();
    if( data === NO_DATA_AVAILABLE)
    // there is no data to read at the moment
    continue;

    if( data === RESOURCE_CLOSED )
    // the resource was closed, remove it from list
    resources.remove(i);
    else
    // some data was received, process it
    consumeData( data );
  }
}
```
Though, it is the simple way to implement asynchronous, event-driven behaviour, it’s not efficient. As this process will keep running continuously, it will use the CPU extensively.

2. **`Reactor Pattern`**:
Reactor Pattern is made of following:
**Resources**:
That are shared by multiple applications for I/O operations, generally slower in executions.

**Synchronous Event De-multiplexer / Event Notifier**:
This uses Event Loop for blocking on all resources. When a set of I/O operations completes, the Event De-multiplexer pushes the new events into the Event Queue.

**Event Loop and Event Queue**:
Event Queue queues up the new events occurred along with its event-handler, <event, event-handler> pair.

**Request Handler / Application**:
This is, generally, the application that provides the handler to be executed for registered events on resources.
See below diagram for understanding of Reactor Pattern and the place for Event Loop:

  ![](1_X0m82lpBhRONFvRGCRu84w.jpeg)

  This is what happens in an application using the reactor pattern:

  The **application** generates a new **I/O operation** by submitting a request to the **Event De-multiplexer**. The application also specifies a **handler**, which will be invoked when the operation completes. Submitting a new request to the Event **De-multiplexer is a **non-blocking call** and it immediately returns the control back to the application.

  When a set of I/O operations completes, the **Event De-multiplexer** pushes the new events into the **Event Queue**. At this point, the **Event Loop** iterates over the items of the **Event Queue**. For each **event**, the associated **handler is invoked**. The **handler**, which is part of the **application code**, will give back the control to the Event Loop when its execution completes (5a). 

  However, new asynchronous operations might be requested during the execution of the handler (5b), causing new operations to be inserted in the Event De-multiplexer (1), before the control is given back to the Event Loop. When all the items in the Event Queue are processed, the loop will block again on the Event De-multiplexer which will then trigger another cycle. The asynchronous behavior is now clear. The application expresses the interest to access a resource at one point in time (without blocking) and provides a handler, which will then be invoked at another point in time when the operation completes. This is by far the basics behind asynchronous behavior of Node-JS.

  Now let’s see how libuv is composed. The following diagram is from the official libuv docs and describes how different types of I/O have been handled while exposing a generalized API.

  Libuv and types of input outputs
  ![](libuv-and-types-of-input-outputs.png)

  **Event Demultiplexer is not an atomic entity, but a collection of an I/O processing APIs abstracted by the Libuv and exposed to the upper layers of NodeJS.**

  **[⬆ back to top](#table-of-contents)**

  ## Event Queue

  The event queue is supposed to be a data structure where all the events are getting enqueued and processed by the event loop sequentially until the queue is empty.

  - There are more than one queues in NodeJS where different types of events getting queued in their own queue.

  There are 4 main types of queues that are processed by the native libuv event loop.

  1. **Expired timers and intervals queue** — consists of callbacks of expired timers added using setTimeout or interval functions added using setInterval.

  2. **IO Events Queue** — Completed IO events

  3. **Immediates Queue** — Callbacks added using setImmediate function.

  4. **Close Handlers Queue** — Any close event handlers.

  Besides these 4 main queues, there are additionally 2 interesting queues which I previously mentioned as ‘intermediate queues’ and are processed by Node. **Although these queues are not part of libuv itself but are parts NodeJS.**

  1. **Next Ticks Queue** — Callbacks added using process.nextTick function.

  2. **Other Microtasks Queue** — Includes other microtasks such as resolved promise callbacks.

  ![](queues-in-nodejs-and-livuv.png)

  - As you can see in the following diagram, Node starts the event loop by checking for any expired timers in the timers queue, and go through each queue in each step while maintaining a reference counter of total items to be processed. After processing the close handlers queue, if there are no items to be processed in any queue and there are no pending operations, the loop will exit. The processing of each queue in the event loop can be considered as a phase of the event loop.

  - If there are any items available in the intermediate queues, the event loop will immediately start processing them until the two immediate queues are emptied.

  E.g, The event loop is currently processing the immediates queue which has 5 handlers to be processed. Meanwhile, two handlers are added to the next tick queue. Once the event loop completes 5 handlers in the immediates queue, event loop will detect that there are two items to be processed in the next tick queue before moving to the close handlers queue. It will then execute all the handlers in the next tick queue and then will move to process the close handlers queue.

  - Next tick queue is displayed separately from the other four main queues because it is not natively provided by the libuv, but implemented in Node.

  - Before each phase of the event loop (timers queue, IO events queue, immediates queue, close handlers queue are the four main phases), before moving to the phase, Node checks for the `nextTick` queue for any queued events. If the queue is not empty, Node will start processing the queue immediately **until the queue is empty**, before moving to the main event loop phase.

  - **This introduces a new problem**. Recursively/Repeatedly adding events to the `nextTick` queue using `process.nextTick` function can cause I/O and other queues to starve forever. We can simulate this scenario using the following simple script.

  ```javascript
  const fs = require("fs");

  function addNextTickRecurs(count) {
    let self = this;
    if (self.id === undefined) {
      self.id = 0;
    }

    if (self.id === count) return;

    process.nextTick(() => {
      console.log(`process.nextTick call ${++self.id}`);
      addNextTickRecurs.call(self, count);
    });
  }

  addNextTickRecurs(Infinity);
  setTimeout(console.log.bind(console, "omg! setTimeout was called"), 10);
  setImmediate(console.log.bind(console, "omg! setImmediate also was called"));
  fs.readFile(__filename, () => {
    console.log("omg! file read complete callback was called!");
  });

  console.log("started");
  ```

  You can see the output is an infinite loop of `nextTick` callback calls, and the `setTimeout`, `setImmediate` and `fs.readFile` callbacks were never called because any of the ‘omg!…’ messages were printed in the console.

  ```
    started
  process.nextTick call 1
  process.nextTick call 2
  process.nextTick call 3
  process.nextTick call 4
  process.nextTick call 5
  process.nextTick call 6
  process.nextTick call 7
  process.nextTick call 8
  process.nextTick call 9
  process.nextTick call 10
  process.nextTick call 11
  process.nextTick call 12
  ....
  ```
  
  > Before Node v0.12, there has been a property called process.maxTickDepth which is used as a threshold to the process.nextTick queue length. This could be manually set by the developers so that Node will process no more than maxTickDepth callbacks from the next tick queue at a given point. But this has been removed since Node v0.12 for some reason. Therefore, for newer Node versions, repeatedly adding events to next tick queue is only discouraged.

  **[⬆ back to top](#table-of-contents)**

  #### Timers queue

  When you add a timer using `setTimeout` or an interval using `setInterval`, Node will add the timer to the timers heap, which is a data structure accessed through libuv. At the timers phase of the event loop, Node will check the timers heap for expired timers/intervals and will call their callbacks respectively. If there are more than one timer which were expired (set with the same expiration period), they will be executed in the order they were set.

  When a timer/interval is set with a specific expiration period, it **does not** guarantee that the callback will be called exactly after the expiration period. When the timer callback is called depends on the performance of the system (Node has to check the timer for expiration once before executing the callback, which takes some CPU time) as well as currently running processes in the event loop. Rather, the expiration period will guarantee that the timer callback will not be triggered at least for the given expiration time period. We can simulate this using the following simple program.

  ```javascript
  const start = process.hrtime();

  setTimeout(() => {
    const end = process.hrtime(start);
    console.log(
      `timeout callback executed after ${end[0]}s and ${end[1] / Math.pow(10, 9)}ms`);
  }, 1000);
  ```
  
Above program will start a timer for 1000ms when the program starts and will log how much time it took to execute the callback. If you run this program multiple times, you will notice that it will print a different result each time and it will never print **timeout callback executed after 1s and 0ms**. You will get something like this instead,

  ```
  timeout callback executed after 1s and 0.006058353ms
  timeout callback executed after 1s and 0.004489878ms
  timeout callback executed after 1s and 0.004307132ms
  ...
  ```

  This nature of the timeouts can cause unexpected and unpredictable results when `setTimeout` used along with `setImmediate` which I’ll explain in the next section.

  **[⬆ back to top](#table-of-contents)**

  #### Immediates Queue

  Although the immediates queue is somewhat similar to timeouts on how it behaves, it has some of its own unique characteristics. Unlike timers which we cannot guarantee when its callback gets executed even though the timer expiration period is zero, immediates queue is guaranteed to be processed immediately after the I/O phase of the event loop. Adding an event(function) to the immediates queue can be done using `setImmediate` function as follows:

  ```javascript
  setImmediate(() => {
    console.log("Hi, this is an immediate");
  });
  ```
 **[⬆ back to top](#table-of-contents)**

  #### setTimeout vs setImmediate
  Now, when we look at the event loop diagram at the top of this post, you can see that when the program starts its execution, Node starts processing the timers. And later after processing the I/O, it goes for the immediates queue. Looking at this diagram, we can easily deduce the output of the following program.
  
   **Program 1**

  ```javascript
  setTimeout(function () {
    console.log("setTimeout");
  }, 0);
  setImmediate(function () {
    console.log("setImmediate");
  });
  ```
  
  As you might guess, this program will always print `setTimeout` before `setImmediate` because the expired timer callbacks are processed before immediates. **But the output of this program can never be guaranteed!** If you run this program multiple times, you will get different outputs.
  
  This is because of the interesting fact that NodeJS caps the minimum timeout to `1ms` in order to align with **Chrome’s timers cap**. Due to this cap, even if you set a timer to `0ms` delay, the delay is actually overridden and set to `1ms`.

  At the start of a new iteration of the event loop, NodeJS invokes a system call to get the current clock time. Depending on how busy the CPU is, getting the current clock time may or may not complete within `1ms`. If the clock time is retrieved in less than `1ms`, NodeJS will detect that the timer is not expired, because the timer takes `1ms` to expire. But, if getting the clock time takes more than `1ms`, the timer will be expired by the time the clock time is retrieved. In the case of Node detecting that the timer is not yet expired, Then the event loop will move on to the I/O phase and then to the immediates queue. Then it will see that there is an event in the immediates queue and it will process it. Hence, `setImmediate` preceding the `setTimeout` callback.

  However, in the following program, it is **guaranteed** that the immediate callback will be definitely called before the timer callback.

  **Program 2**

  ```javascript
  const fs = require("fs");

  fs.readFile(__filename, () => {
    setTimeout(() => {
      console.log("timeout");
    }, 0);
    setImmediate(() => {
      console.log("immediate");
    });
  });
  ```

  Let’s see the execution flow of the above program.

  - At the start, this program reads the current file asynchronously using `fs.readFile` function, and it provides a callback to be triggered after the file is read.

  - Then the event loop starts.

  - Once the file is read, it will add the event (a callback to be executed) in the I/O queue in the event loop.

  - Since there are no other events to be processed, Node is waiting for any I/O event. It will then see the file read event in the I/O queue and will execute it.

  - During the execution of the callback, a timer is added to the timers heap and an immediate is added to the immediates queue.

  - Now we know that the event loop is in I/O phase. Since there are no any I/O events to be processed, the event loop will move to the immediates phase where it will see the immediate callback added during the execution of file read callback. Then the immediate callback will be executed.

  - In the next turn of the event loop, it will see the expired timer and it will execute the timer callback.

  **Conclusion**
  So let’s have a look at how these different phases/queues work altogether in the event loop. See the following example.

  ```javascript
  setImmediate(() => console.log("this is set immediate 1"));
  setImmediate(() => console.log("this is set immediate 2"));
  setImmediate(() => console.log("this is set immediate 3"));

  setTimeout(() => console.log("this is set timeout 1"), 0);
  setTimeout(() => {
    console.log("this is set timeout 2");
    process.nextTick(() =>
      console.log("this is process.nextTick added inside setTimeout")
    );
  }, 0);
  setTimeout(() => console.log("this is set timeout 3"), 0);
  setTimeout(() => console.log("this is set timeout 4"), 0);
  setTimeout(() => console.log("this is set timeout 5"), 0);

  process.nextTick(() => console.log("this is process.nextTick 1"));
  process.nextTick(() => {
    process.nextTick(
      console.log.bind(console, "this is the inner next tick inside next tick")
    );
  });
  process.nextTick(() => console.log("this is process.nextTick 2"));
  process.nextTick(() => console.log("this is process.nextTick 3"));
  process.nextTick(() => console.log("this is process.nextTick 4"));
  ```

  After the execution of the above script, the following events are added to the respective event loop queues.
  
  - 3 immediates
  - 5 timer callbacks
  - 5 next tick callbacks

  Let’s now see the execution flow:

  - When the event loop starts, it will notice the next tick queue and will start processing the next tick callbacks. During the execution of the second next tick callback, a new next tick callback is added to the end of the next tick queue and will be executed at the end of the next tick queue.
  - Callbacks of the expired timers will be executed. Inside the execution of the second timer callback, an event is added to the next tick queue.
  - Once callbacks of all the expired timers are executed, the event loop will then see that there is one event in the next tick queue (which was added during the execution of the second timer callback). Then the event loop will execute it.
  - Since there are no I/O events to be processed, the event loop will move to the immediates phase and will process the immediates queue.

  ```
  this is process.nextTick 1
  this is process.nextTick 2
  this is process.nextTick 3
  this is process.nextTick 4
  this is the inner next tick inside next tick
  this is set timeout 1
  this is set timeout 2
  this is set timeout 3
  this is set timeout 4
  this is set timeout 5
  this is process.nextTick added inside setTimeout
  this is set immediate 1
  this is set immediate 2
  this is set immediate 3
  ```

  **[⬆ back to top](#table-of-contents)**

  #### Native Promises

  In the context of native promises, a promise callback is considered as a microtask and queued in a microtask queue which will be processed right after the next tick queue.

  Consider the following example.

  ```javascript
  Promise.resolve().then(() => console.log("promise1 resolved"));
  Promise.resolve().then(() => console.log("promise2 resolved"));
  Promise.resolve().then(() => {
    console.log("promise3 resolved");
    process.nextTick(() =>
      console.log("next tick inside promise resolve handler")
    );
  });
  Promise.resolve().then(() => console.log("promise4 resolved"));
  Promise.resolve().then(() => console.log("promise5 resolved"));
  setImmediate(() => console.log("set immediate1"));
  setImmediate(() => console.log("set immediate2"));

  process.nextTick(() => console.log("next tick1"));
  process.nextTick(() => console.log("next tick2"));
  process.nextTick(() => console.log("next tick3"));

  setTimeout(() => console.log("set timeout"), 0);
  setImmediate(() => console.log("set immediate3"));
  setImmediate(() => console.log("set immediate4"));
  ```

                  <details>
                  <summary>Output</summary>

  ```
  next tick1
  next tick2
  next tick3
  promise1 resolved
  promise2 resolved
  promise3 resolved
  promise4 resolved
  promise5 resolved
  next tick inside promise resolve handler
  set timeout
  set immediate1
  set immediate2
  set immediate3
  set immediate4

  ```

                  </details>

                  <details>
                  <summary>Explaination</summary>

  1. Loop will identify that there are three items in the process.nextTick queue and Node will start processing the nextTick queue until it is exhausted.

  2. Then the loop will check the promises microtask queue and identify there are five items in the promises microtask queue and will start processing the queue.

  3. During the process of promises microtask queue, one item is again added to the process.nextTick queue (‘next tick inside promise resolve handler’).

  4. After promises microtask queue is finished, event loop will again detect that there is one item is in the process.nextTick queue which was added during promises microtask processing. Then node will process the remaining 1 item in the nextTick queue.

  5. Enough of promises and nextTicks. There are no more microtasks left. Then the event loop moves to the first phase, which is the timers phase. At this moment it will see there is an expired timer callback in the timers queue and it will process the callback.

  6. Now that there are no more timer callbacks left, loop will wait for I/O. Since we do not have any pending I/O, the loop will then move on to process setImmediate queue. It will see that there are four items in the immediates queue and will process them until the immediate queue is exhausted.

  7. At last, loop is done with everything…Then the program gracefully exits.

    </details>

  **[⬆ back to top](#table-of-contents)**

  #### Q and Bluebird

  Before JS native promises were implemented in NodeJS, prehistoric people were using libraries such as Q and Bluebird (Pun intended :P). Since these libraries predate native promises, they have different semantics than the native promises.

  **At the time of this writing, Q (v1.5.0) uses process.nextTick queue to schedule callbacks for resolved/rejected promises.**

  **Bluebird, at the time of this writing (v3.5.0) uses setImmediate by default to schedule promise callbacks in recent NodeJS versions.**

  ```javascript
  const Q = require("q");
  const BlueBird = require("bluebird");

  Promise.resolve().then(() => console.log("native promise resolved"));
  BlueBird.resolve().then(() => console.log("bluebird promise resolved"));
  setImmediate(() => console.log("set immediate"));
  Q.resolve().then(() => console.log("q promise resolved"));
  process.nextTick(() => console.log("next tick"));
  setTimeout(() => console.log("set timeout"), 0);
  ```

                  <details>
                  <summary>Output</summary>

  ```
  q promise resolved
  next tick
  native promise resolved
  set timeout
  bluebird promise resolved
  set immediate
  ```

                  </details>

                  <details>
                  <summary>Explaination</summary>

  BlueBird.resolve().then callback has the same semantics as the following setImmediate call. Therefore, bluebird’s callback is scheduled in the same immediates queue before the setImmediate callback. Since Q uses process.nextTick to schedule its resolve/reject callbacks, Q.resolve().then is scheduled in the nextTick queue before the succeeding process.nextTick callback.

                  </details>

  - Please note that although I have used only promise resolve handlers in the above examples, this behavior is identical for promise reject handlers as well. At the end of this article, I’ll present you an example with both resolve and reject handlers

  - Bluebird, however, provides us a choice. We can select our own scheduling mechanism. Does it mean we can instruct bluebird to use process.nextTick instead of setImmediate? Yes it does. Bluebird provides an API method named setScheduler which accepts a function which overrides the default setImmediate scheduler.

  **consider the program and try to findout output of the program**

  ```javascript
  const Q = require("q");
  const BlueBird = require("bluebird");

  Promise.resolve().then(() => console.log("native promise resolved"));
  BlueBird.resolve().then(() => console.log("bluebird promise resolved"));
  setImmediate(() => console.log("set immediate"));
  Q.resolve().then(() => console.log("q promise resolved"));
  process.nextTick(() => console.log("next tick"));
  setTimeout(() => console.log("set timeout"), 0);
  Q.reject().catch(() => console.log("q promise rejected"));
  BlueBird.reject().catch(() => console.log("bluebird promise rejected"));
  Promise.reject().catch(() => console.log("native promise rejected"));
  ```

                <details>
                  <summary>Output</summary>

  ```
  q promise resolved
  q promise rejected
  next tick
  native promise resolved
  native promise rejected
  set timeout
  bluebird promise resolved
  bluebird promise rejected
  set immediate
  ```

                </details>

  **[⬆ back to top](#table-of-contents)**

# Buffer and Streams

#### callback function

A function passed to other function, which invoked in future after complete some task.

#### Buffer

- A Temporary holding spot for data being moved from one place to another. we put data in buffer, then move out and we again move data in buffer and again move out data.

- Intentionally limited in size. so buffer allow us to gather some data and mon=ve it along.

- Generally the data coming and moving through Streams.

#### Stream

A sequence of data made available over time.

Streams are collections of data — just like arrays or strings. The difference is that streams might not be available all at once, and they don’t have to fit in memory.

A stream over a internet might moving at different speed depending upon how fast is your internet but data being moved and passed one computer to another computer or from one processor to another within a computer. And we have this data moving and we processing as we go instead of wait and try to get all the data.
For example watching movie online(where streaming ang processing happening altogether) instead of downloading a movie.

#### Binary data

Data store in binary(sets of 0's and 1's)
Eg: 1010

#### Character sets

A representation of characters as numbers (Unicode, Ascii...)

![](character-set.png)

#### Encoding

How characters are stored in binary (UTF-8).

**Character Encoding means number of bits we are using to represent a number.**

![](character-encoding.png)

Note:

      1. javascript is not good encoding part.

      2. javascript handles unicode okay, translating letters to numbers. But for pure raw binary data, javascript doesn't have much to deal with them.

      3. Node with v8 engine expands the feature of javascript and give us some mechanism to deal with binary data.

**[⬆ back to top](#table-of-contents)**

## Buffers

Needed because javascript was not used to deal with binary data. In ES6 it does using ArrayBuffer.
Pure JavaScript is Unicode friendly but not nice to binary data. When dealing with TCP streams or the file system, it's necessary to handle octet streams. Node has several strategies for manipulating, creating, and consuming octet streams.

Buffer is written in c++ side of the node core. And made available to javascript side.

In Node.js, Buffer is a global object that provides a way to work with different
kinds of binary data. Most APIs in Node core (e.g. http, net, fs) will give you
buffers, and will be able to do their job faster if you give them buffers.

```javascript
var buf = new Buffer("Hello", "utf8");

console.log(buf); //<Buffer 48 65 6c 6c 6f>
console.log(buf.toString()); //Hello
console.log(buf.toJSON()); // { type: 'Buffer', data: [ 72, 101, 108, 108, 111 ] }
console.log(buf[2]); //108

buf.write("wo");
console.log(buf.toString()); // wollo
```

**[⬆ back to top](#table-of-contents)**

## ArrayBuffer

[ArrayBuffer Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Typed_arrays)

```javascript
var buffer = new ArrayBuffer(8);
var view = new Int32Array(buffer);
view[0] = 5;
view[1] = 15;
console.log(view); //Int32Array { '0': 5, '1': 15 }
```

**[⬆ back to top](#table-of-contents)**

## Callbacks

```javascript
function greet(callback) {
  console.log("Hello!");
  var data = {
    name: "John Doe",
  };

  callback(data);
}

greet(function (data) {
  console.log("The callback was invoked!");
  console.log(data);
});

greet(function (data) {
  console.log("A different callback was invoked!");
  console.log(data.name);
});

//Hello!
//The callback was invoked!
//{ name: 'John Doe' }
//Hello!
//A different callback was invoked!
//John Doe
```

**[⬆ back to top](#table-of-contents)**

## Files

```javascript
var fs = require("fs");

//synchronous
var greet = fs.readFileSync(__dirname + "/greet.txt", "utf8");
console.log(greet); //#1

//asynchronous
var greet2 = fs.readFile(
  __dirname + "/greet.txt",
  "utf8",
  function (err, data) {
    console.log(data); //#3
  }
);

console.log("Done!"); //#2
```

Here both method first collect all data in buffer and then start processing or return file. so, node use heap for store buffer memory. By using this method we can be end up with many buffers which can be very large in size.

**[⬆ back to top](#table-of-contents)**

#### Error First Callback

Callbacks take en error object as their first parameter.
The Standard.
null if no error.

**[⬆ back to top](#table-of-contents)**

## Abstract Class

A type of constructor, you never work directly with, but inherit from.

We create new custom objects which inherits from the abstract class.

**[⬆ back to top](#table-of-contents)**

## Streams

A stream is a sequence of pieces of data and data just broken up and known as chunk.

Under the hood, in nodejs, Stream is an abstract(base) class.

![](stream-abstract-class.png)

We work with custom stream. we never touch abstract classes like stream or stream.Readable.

**[⬆ back to top](#table-of-contents)**

#### Chunk

A piece of data being sent through a Stream

- Data is split in 'chunks' and streamed

```javascript
var fs = require("fs");

var readable = fs.createReadStream(__dirname + "/greet.txt", {
  encoding: "utf8",
  highWaterMark: 16 * 1024,
}); // highWaterMark numebr of the buffer

var writable = fs.createWriteStream(__dirname + "/greetcopy.txt");

readable.on("data", function (chunk) {
  // Event emitter, just listenting the event starts the buffer
  console.log(chunk.length);
  // console.log(chunk);
  writable.write(chunk);
});
```

**[⬆ back to top](#table-of-contents)**

## Pipes

Connecting two streams by writing to one stream what is being read from another

- In Node, you pipe from a Readable stream to a writeable stream.

- Read a chunk and pipe it to a writeable stream.

- if start with a stram that is readable, then you move along with streams that both writeable and readable, then can pipe the chunk along a flow of streams and do different things with chunk of data.

- if the writeable stream is also Readable then we can pipe to another writeable stream.

- Pipe can be chained or can be connected if you are sending them to different writable streams.

- Sending data from Readable to writeable stream as each chunk is processed is common.

- Pipe is avaiable on readable stream.

- under the hood pipe takes destination where you want to send this chunk to. This destination should be a writable stream.

- Readable stream can be piped only to a writeable stream.

![](pipes-explained.png)

- zlib => part of node core. used to produce Gzip files. zlib gives transform streams.

```javascript
var fs = require("fs");
var zlib = require("zlib");

var readable = fs.createReadStream(__dirname + "/greet.txt");

var writable = fs.createWriteStream(__dirname + "/greetcopy.txt");

var compressed = fs.createWriteStream(__dirname + "/greet.txt.gz");

var gzip = zlib.createGzip();

readable.pipe(writable); // Same as forehead sample

readable.pipe(gzip).pipe(compressed); // Chain pipes
```

**[⬆ back to top](#table-of-contents)**

#### Method chaining

A Method returns an object so we can keep calling more methods.
When it returns the parent object is called "cascading".

Note:

1. Stream minimize the the buffer size we are working with. Therefore, helping the memory that the application is using.

2. Stream helps in speed of things to occur.

**[⬆ back to top](#table-of-contents)**

# 5.HTTP

#### Protocol

A set of rules two sides agree on the use communicating.
IP : Internet Protocol. Addresses
TCP: Transmission Control Protocol. Send Packets

#### Port

Which program in a computer handles a packet received.

#### HTTP

A set of rules and format for data being transferred on the web
'Hypertext Transfer Protocol' (how the messages are written)

#### MIME Type

A standard for specifying the type of the data being sent

MIME stands for 'Multipurpose Internet Mail Extensions'

Examples: application/json, text/html, image/jpeg
Content-Type: application/json

#### http_parser

C program that parse http requests and responses

## HTTP server

```javascript
var http = require("http");

http
  .createServer(function (req, res) {
    res.writeHead(200, { "Content-Type": "text/plain" });
    res.end("Hello World\n");
  })
  .listen(1337, "127.0.0.1");
```

## Output HTML and Templates

```javascript
var http = require("http");
var fs = require("fs");

http
  .createServer(function (req, res) {
    res.writeHead(200, { "Content-Type": "text/html" });
    var html = fs.readFileSync(__dirname + "/index.htm", "utf8");
    var message = "Hello world...";
    html = html.replace("{Message}", message);
    res.end(html);
  })
  .listen(1337, "127.0.0.1");
```

#### Template

Text designed to be the basis for final text or content after being processed

## Streams and Performance

We can send chunks of data instead all at once using Streams and piping it to the response.
Use it always.

```javascript
var http = require("http");
var fs = require("fs");

http
  .createServer(function (req, res) {
    res.writeHead(200, { "Content-Type": "text/html" });
    fs.createReadStream(__dirname + "/index.htm").pipe(res);
  })
  .listen(1337, "127.0.0.1");
```

#### API

Application Programing Interface.

API is a software intermediary that allows two applications to talk to each other.

In node's field URLs which accept and send only data via HTTP and TCP/IP.

API endpoint are used for get some data and this data can be json or xml etc.

#### Endpoint

One URL in a web API.

An endpoint is any device that is physically available during communication.

## Outputting a JSON

```javascript
var http = require("http");
var fs = require("fs");

http
  .createServer(function (req, res) {
    res.writeHead(200, { "Content-Type": "application/json" });
    var obj = {
      firstname: "John",
      lastname: "Doe",
    };
    res.end(JSON.stringify(obj));
  })
  .listen(1337, "127.0.0.1");
```

#### Serialize

Translating and object into a format that can be stored or transferred.
JSON, CSV, XML are popular.

#### Deserialize

'Deserialize' is the opposite of serialize (converting the format back into an object)

## Routing

Mapping HTTP requests to content.
Get data in the server from parameters in the http call.

```javascript
var http = require("http");
var fs = require("fs");

http
  .createServer(function (req, res) {
    if (req.url === "/") {
      fs.createReadStream(__dirname + "/index.htm").pipe(res);
    } else if (req.url === "/api") {
      res.writeHead(200, { "Content-Type": "application/json" });
      var obj = {
        firstname: "John",
        lastname: "Doe",
      };
      res.end(JSON.stringify(obj));
    } else {
      res.writeHead(404);
      res.end();
    }
  })
  .listen(1337, "127.0.0.1");
```

# 6.NPM

#### Semantic Versioning

MAYOR.MINOR.PATCH

## Package.json

`npm init`
`npm install moment --save` The `--save` writes a reference in package.json

```javascript

  "dependencies": {
    "moment": "^2.13.0" // ^ automatically updates minors ~ updates only patches
  }
```

`npm install` : Once we have the package.json we dont need to copy the modules in a new environment, just calling `npm install` will download everything for us

`require` will look directly in the `node_modules` folder

```javascript
var moment = require("moment");
console.log(moment().format("ddd, hA"));
```

## Global dependencies

Install dependencies that we only need while developing
`npm install jasmine-node --save-dev`
Install globally, if we kwow we will us a package in many apps in our computer
`npm install nodemon -g`
They are stored at `/usr/local/lib/node_modules/npm/node_modules`

#### nodemon

It watches changes in the folder

# 7.Express

```javascript
var express = require("express");
var app = express();

var port = process.env.PORT || 3000;

app.get("/", function (req, res) {
  res.send("<html><head></head><body><h1>Hello world!</h1></body></html>");
});

app.get("/api", function (req, res) {
  res.json({ firstname: "John", lastname: "Doe" });
});

app.listen(port);
```

#### Environment variables

Global variables specific to the environment (server) our code is living in.

#### Http method (verbs)

Specific type of action the request wishes to make.
GET, POST, DELETE...

## Routes

```javascript
app.get("/person/:id", function (req, res) {
  res.send(
    "<html><head></head><body><h1>Person: " +
      req.params.id +
      "</h1></body></html>"
  );
});
```

## Static Files and Middleware

#### Midleware

Code that sit between 2 layers of software.
In Express: sitting between request and response

```javascript
app.use("/assets", express.static(__dirname + "/public"));

app.use("/", function (req, res, next) {
  console.log("Request Url:" + req.url);
  next(); // call the next Middleware
});
app.get("/", function (req, res) {
  res.send(
    "<html><head><link href=assets/style.css type=text/css rel=stylesheet /></head><body><h1>Hello world!</h1></body></html>"
  );
});
```

## Templates and Template Engines

```javascript

  ...

  app.set('view engine', 'ejs');

  app.get('/', function(req, res) {
    res.render('index');
  });

  app.get('/person/:id', function(req, res) {
    res.render('person', { ID: req.params.id });
  });
  ...

```

```html
<html>
  <head>
    <link href="/assets/style.css" type="text/css" rel="stylesheet" />
    // important the / before the path of the css
  </head>
  <body>
    <h1>Person: <%= ID %></h1>
  </body>
</html>
```

## Querystring and Post Parameters

### Querystring

```javascript

  GET /?id=4&page=3 HTTP/1.1
  Host:www.learnweb.net
  Cookie:username=abc:name:Tony
```

```javascript
app.get("/person/:id", function (req, res) {
  res.render("person", { ID: req.params.id, Qstr: req.query.qstr }); //req.query get the querystring
});
```

### Form Post

Data in the body as objects
Use body-parser

```javascript

  POST HTTP/1.1
  Host:www.learnweb.net
  Content-Type:application/x-www-form-urlencoded
  Cookie:num=4;page=3
  username=Tony&password=pwd
```

```javascript
var bodyParser = require("body-parser");
var urlencodedParser = bodyParser.urlencoded({ extended: false });

app.post("/person", urlencodedParser, function (req, res) {
  res.send("Thank you!");
  console.log(req.body.firstname);
  console.log(req.body.lastname);
});
```

```html
<form method="POST" action="/person">
  First name: <input type="text" id="firstname" name="firstname" /><br />
  Last name: <input type="text" id="lastname" name="lastname" /><br />
  <input type="submit" value="Submit" />
</form>
```

### Post as json

Data in the body as json

```javascript

  POST HTTP/1.1
  Host:www.learnweb.net
  Content-Type:application/json
  Cookie:num=4;page=3
  {
    'username'='Tony',
    'password'='pwd'
  }
```

```javascript
var jsonParser = bodyParser.json();

app.post("/personjson", jsonParser, function (req, res) {
  res.send("Thank you for the JSON data!");
  console.log(req.body.firstname);
  console.log(req.body.lastname);
});
```

```html
<script>
  $.ajax({
    type: "POST",
    url: "/personjson",
    data: JSON.stringify({ firstname: "Jane", lastname: "Doe" }),
    dataType: "json",
    contentType: "application/json",
  });
</script>
```

## RESTful API and JSON

#### REST

Representational State Transfer. Which HTTP verbs and URLs do what.

```javascript
app.get("/api/person/:id", function (req, res) {
  // get that data from database
  res.json({ firstname: "John", lastname: "Doe" });
});

app.post("/api/person", jsonParser, function (req, res) {
  // save to the database
});

app.delete("/api/person/:id", function (req, res) {
  // delete from the database
});
```

## Structuring the Application

### Structuring with Express

`install express-generator -g` // do it global
`express <my app name>`// Create the architecture
`cd <my app name>` // go to the app
`npm install` // install the packages

### Our own Structure

Using controllers

**app.js**

```javascript
var express = require("express");
var app = express();

var apiController = require("./controllers/apiController");
var htmlController = require("./controllers/htmlController");

var port = process.env.PORT || 3000;

app.use("/assets", express.static(__dirname + "/public"));

app.set("view engine", "ejs");

app.use("/", function (req, res, next) {
  console.log("Request Url:" + req.url);
  next();
});

htmlController(app);
apiController(app);

app.listen(port);
```

**htmlController**

```javascript
var bodyParser = require("body-parser");

var urlencodedParser = bodyParser.urlencoded({ extended: false });

module.exports = function (app) {
  app.get("/", function (req, res) {
    res.render("index");
  });

  app.get("/person/:id", function (req, res) {
    res.render("person", { ID: req.params.id, Qstr: req.query.qstr });
  });

  app.post("/person", urlencodedParser, function (req, res) {
    res.send("Thank you!");
    console.log(req.body.firstname);
    console.log(req.body.lastname);
  });
};
```

**apiController**

```javascript
module.exports = function (app) {
  app.get("/api/person/:id", function (req, res) {
    // get that data from database
    res.json({ firstname: "John", lastname: "Doe" });
  });

  app.post("/api/person", function (req, res) {
    // save to the database
  });

  app.delete("/api/person/:id", function (req, res) {
    // delete from the database
  });
};
```

# 8.MEAN

#### DOM

Document Object Model
The structure browsers use to store and manage web pages
Browsers give JavaScript the ability to manipulate the DOM

## Angular

**app.js**

```javascript
var express = require("express");
var app = express();

var port = process.env.PORT || 3000;

app.set("view engine", "ejs");
app.use("/assets", express.static(__dirname + "/public"));

app.get("/", function (req, res) {
  res.render("index");
});

app.listen(port);
```

**view/index.ejs**

```html
<html ng-app="TestApp">
  <head>
    <title>The MEAN stack</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.4.5/angular.js"></script>
  </head>
  <body ng-controller="MainController as vm">
    <input type="text" ng-model="vm.message" />
    <br />
    {{ vm.message }}
    <br />
    <ul>
      <li ng-repeat="person in vm.people">{{ person.name }}</li>
    </ul>

    <script src="assets/js/app.js"></script>
  </body>
</html>
```

**public/js/app.js**

```javascript
angular.module("TestApp", []);

angular.module("TestApp").controller("MainController", ctrlFunc);

function ctrlFunc() {
  this.message = "Hello";

  this.people = [
    {
      name: "John Doe",
    },
    {
      name: "Jane Doe",
    },
    {
      name: "Jim Doe",
    },
  ];
}
```

## Separating Server code from Client code

We can set in the server what we show in client
**app.js**

```javascript
var express = require("express");
var app = express();

var port = process.env.PORT || 3000;

var people = [
  {
    name: "John Doe",
  },
  {
    name: "Jane Doe",
  },
  {
    name: "Jim Doe",
  },
];

app.set("view engine", "ejs");
app.use("/assets", express.static(__dirname + "/public"));

app.get("/", function (req, res) {
  res.render("index", { serverPeople: people }); //<--
});

app.listen(port);
```

**view/index.ejs**

```html
<html ng-app="TestApp">
  <head>
    <title>The MEAN stack</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.4.7/angular.js"></script>
  </head>
  <body ng-controller="MainController as vm">
    <ul>
      <li ng-repeat="person in vm.people">{{ person.name }}</li>
    </ul>
    <script>
      var clientPeople = <%- JSON.stringify(serverPeople) %>; //<--
    </script>
    <script src="/assets/js/app.js"></script>
  </body>
</html>
```

**public/js/app.js**

```javascript
angular.module("TestApp", []);

angular.module("TestApp").controller("MainController", ctrlFunc);

function ctrlFunc() {
  this.people = clientPeople;
}
```

# 9.Build an app

## 1. Init

*1 `npm init`
*2 `npm install express --save-dev`
*3 `npm install ejs --save-dev`
*4 `npm install body-parser --save-dev`
\*5 `npm install mongoose --save-dev`

**app.js**

```javascript
var express = require("express");
var app = express();

var port = process.env.PORT || 3000;

app.use("/assets", express.static(__dirname + "/public"));

app.set("view engine", "ejs");

app.listen(port);
```

## 2. Connect to the Database

mLab.com
**config/config.json**

```javascript

  {
    "uname":"test",
    "pwd":"test"
  }
```

**config/index.js**

```javascript
var configValues = require("./config");

module.exports = {
  getDbConnectionString: function () {
    return `mongodb://${configValues.uname}:${configValues.pwd}@ds013212.mlab.com:13212/nodetodo`;
  },
};
```

**models/todoModel.js**

```javascript
var mongoose = require("mongoose");

var Schema = mongoose.Schema;

var todoSchema = new Schema({
  username: String,
  todo: String,
  isDone: Boolean,
  hasAttachment: Boolean,
});

var Todos = mongoose.model("Todos", todoSchema);

module.exports = Todos;
```

**app.js**

```javascript
var express = require("express");
var app = express();
var mongoose = require("mongoose");
var config = require("./config");

var port = process.env.PORT || 3000;

app.use("/assets", express.static(__dirname + "/public"));

app.set("view engine", "ejs");

mongoose.connect(config.getDbConnectionString());

app.listen(port);
```

## 3. Adding Data

**controllers/setupController.js**

```javascript
var Todos = require("../models/todoModel");

module.exports = function (app) {
  app.get("/api/setupTodos", function (req, res) {
    // seed database
    var starterTodos = [
      {
        username: "test",
        todo: "Buy milk",
        isDone: false,
        hasAttachment: false,
      },
      {
        username: "test",
        todo: "Feed dog",
        isDone: false,
        hasAttachment: false,
      },
      {
        username: "test",
        todo: "Learn Node",
        isDone: false,
        hasAttachment: false,
      },
    ];
    Todos.create(starterTodos, function (err, results) {
      res.send(results);
    });
  });
};
```

**app.js**

```javascript
var express = require("express");
var app = express();
var mongoose = require("mongoose");
var config = require("./config");
var setupController = require("./controllers/setupController");

var port = process.env.PORT || 3000;

app.use("/assets", express.static(__dirname + "/public"));

app.set("view engine", "ejs");

mongoose.connect(config.getDbConnectionString());
setupController(app);

app.listen(port);
```

Run
`http://localhost:3000/api/setupTodos`

## 4. Create the API

**controllers/apiController**

```javascript
var Todos = require("../models/todoModel");
var bodyParser = require("body-parser");

module.exports = function (app) {
  app.use(bodyParser.json()); // Middleware
  app.use(bodyParser.urlencoded({ extended: true })); // Middleware

  app.get("/api/todos/:uname", function (req, res) {
    Todos.find({ username: req.params.uname }, function (err, todos) {
      if (err) throw err;

      res.send(todos);
    });
  });

  app.get("/api/todo/:id", function (req, res) {
    Todos.findById({ _id: req.params.id }, function (err, todo) {
      if (err) throw err;

      res.send(todo);
    });
  });

  app.post("/api/todo", function (req, res) {
    if (req.body.id) {
      // if i received an id I know that is an update
      Todos.findByIdAndUpdate(
        req.body.id,
        {
          todo: req.body.todo,
          isDone: req.body.isDone,
          hasAttachment: req.body.hasAttachment,
        },
        function (err, todo) {
          if (err) throw err;

          res.send("Success");
        }
      );
    } else {
      var newTodo = Todos({
        username: "test",
        todo: req.body.todo,
        isDone: req.body.isDone,
        hasAttachment: req.body.hasAttachment,
      });
      newTodo.save(function (err) {
        if (err) throw err;
        res.send("Success");
      });
    }
  });

  app.delete("/api/todo", function (req, res) {
    Todos.findByIdAndRemove(req.body.id, function (err) {
      if (err) throw err;
      res.send("Success");
    });
  });
};
```

**app.js**

```javascript
var express = require("express");
var app = express();
var mongoose = require("mongoose");
var config = require("./config");
var setupController = require("./controllers/setupController");
var apiController = require("./controllers/apiController");

var port = process.env.PORT || 3000;

app.use("/assets", express.static(__dirname + "/public"));

app.set("view engine", "ejs");

mongoose.connect(config.getDbConnectionString());
setupController(app);
apiController(app);

app.listen(port);
```
