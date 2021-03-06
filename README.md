# Cast React + Hogan

## What is this?

I began separating out the components of the Cast application so that I could create a PDF Service against it. For the UI I implemented both React and Hogan: React as a simple Redux app, and Hogan using some components I had begun in the current Cast app.

The API is meant to be a stand-alone server, with some MVC components as an interface to the database. Those MVC components (and the data layer itself) were also meant to be extracted into a stand-alone layer.

The React application is isomorphic.

The Hogan application implements some components for the PDF Service: `express-hogan-cache` is a lightweight view engine which implements `hogan-cache`. The latter reads Hogan templates from the file system, compiles them, then caches them. Since one of the advertised benefits of Hogan over Mustache is its compiled templates, it seemed remiss to implement Hogan and then expect the application to read and compile them with every request. Instead, `hogan-cache` accepts an object which defines the required templates, and that object can be given to the mechanism per request, or at application start. Together with the `make-face` package this should take care of being able to generate PDF headers and footers based on configuration. What remains is to stitch these components together.

Lastly, I'll note that I also ensured that the React application was isomorphic because that meets another requirement for a PDF Service: to produce a document from its rendered HTML. Again, what remains is to stitch these components together.

But, for the time being, here is **Cast React + Hogan**.

## Prerequisites

A copy of the Cast database.

## Installation

```
npm install
```

## Running

React Promise middleware depends on configuration declared in the `.env` file at the application root (alongside `app.js`). Invoking `npm start` runs Gulp which creates the client `config.js` file, and then bundles it with the React application. 

That configuration (and the API server itself) are prerequisites for the React application. You can change the configuration of the API server by modifying the content of the `.env` file.

To run Gulp and start the application with the default settings, at the command line type:


```
npm start
```

To run Gulp and start the application, then watch for changes on the file system, at the command line type:


```
npm run dev
```

UNLESS YOU ARE RUNNING IN DEV YOU PROBABLY DO NOT WANT THE DEFAULT SETTINGS.

### What do you want to do?

> "I want to build the application without starting the servers"

To build the application without starting the servers, run Gulp. At the command line type:

```
gulp start
```

### What else do you want to do?

> "I want to start the servers without building the application"

To start the API, at the command line type:

```
node app
```

To start both the API and the React UI, instead type:

```
node app --react [port]
```

*Where [port] is the port number for the React server.*

To start the API and the Hogan UI, instead type:

```
node app --hogan [port]
```

*Where [port] is the port number for the Hogan server.*

To start the API and both the React and Hogan UIs:

```
node app --react [port] --hogan [port]
```

*Where [port] is the port number for the React and Hogan servers.*

### Anything else?

> "I want to change the configuration of the API"

Open the `.env` file in your preferred editor, change the declaration values, then close the file. Remember to save. Then, build and start.