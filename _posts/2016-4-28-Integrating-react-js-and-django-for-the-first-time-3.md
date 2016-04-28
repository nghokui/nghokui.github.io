---
layout: post
title: Basic tutorial on setting up a very basic Django and React JS application 3/3
tags: django, react, html, work
---
## 3. Finish our sample React code
Let's start of by doing all the things necessary to get the most basic django server running.
##### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Get our main django project up and running
1. Create a file `app.jsx` in our directory `your_project_name/assets/js/`
```
$ touch assets/js/app.jsx
```
2. Throw the following code into our newly created `app.jsx` file:
```
var React = require('react');
var ReactDOM = require('react-dom');

var App = React.createClass({
  render: function() {
    return <h1>Hello World</h1>;
  }
});

ReactDOM.render(<App/>, document.getElementById('app'));
```
3. Open up `assets/js/index.js` and add the following:
```
var App = require('.app.jsx');
```
There we go! Now our code is all set to go.

## 4. Set up our webpack configuration and bundle our react js code
##### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Set the webpack configuration
1. Open up the file `webpack.config.js` and add the following code
```
var path = require("path")
var webpack = require('webpack')
var BundleTracker = require('webpack-bundle-tracker')
module.exports = {
  context: __dirname,
  entry: './assets/js/index.js', // entry point of our app.; require other js modules and dependencies within it

  // let's set the output to our static folder, so all we need to do is run the webpacker and it should be good to go
  // remember, we made reference to it in our django html code!
  output: {
      path: path.resolve('./your_app_name/static/your_app_name/'),
      filename: "bundle.js",
  },
  plugins: [
    new BundleTracker({filename: './webpack-stats.json'}),
  ],
  module: {
    loaders: [
      { test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: 'babel-loader',
        query:
          {
            presets:['react']
          }
      }, // loader is used to transform JSX into JS
    ],
  },

  resolve: {
    modulesDirectories: ['node_modules', 'bower_components'],
    extensions: ['', '.js', '.jsx']
  },
}
```
Save it!
##### &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Last but not least, compile our bundle.js
```
$ ./node_modules/.bin/webpack --config webpack.config.js
```
You might have to do `\` instead in Windows.

## 4. Let's see if this works!
Run the following
```
$ python manage.py runserver
```
Open up a web browser, navigate to `http://127.0.0.1:8000`, and if you see Hello, World!



SUCCESS!
