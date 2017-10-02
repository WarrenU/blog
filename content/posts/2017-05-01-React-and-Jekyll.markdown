---
title:  "Using React and Webpack with Jekyll"
date:   2017-05-01 1:19:42 -0800
---

This post is going to go over the steps I made to integrate React into this website.
The main technologies of interest are Jekyll, React, and Webpack.

Firstly add to your gitignore:
 * public  
 * src/assets/bundle.js  
 * node_modules  
Also install:
 * npm
 * node
On ubuntu it is as easy as:
{% highlight ruby %}
sudo apt-get update
sudo apt-get install node
sudo apt-get install npm
{% endhighlight %}

Warning: I did run into a problem where I had to set up a symlink for nodejs to read for /node:
run the command (if you cannot find node) A safe way to confirm this would be to cd /usr/bin/ -ls -al  
you'll be able to see if you have a nodejs folder but no node folder:
{% highlight ruby %}
"ln -s /usr/bin/nodejs /usr/bin/node"
{% endhighlight %}


*1. Let's work on our project's structure. I'm assuming you have a standard jekyll site built with standard directories setup.
    Create a folder named "public" in your Jekyll App's directory.    
    * This will be the spot your Jekyll project will build to.

*2. Add to the _config.yml a signal to have it read src from your public folder:
    * destination: public  
      source: src
    By default jekyll reads from the root directory to build but since we will be calling webpack to build our bundle js dependency. This is where all of our components get written to. (public)

*3. Add a Webpack Folder
    * This is for development. Webpack will pick up entry.js and compile it into our bundle.js file for Jekyll to utilize.

*4. Configure webpack by creating a file: webpack.config.js
    * For the output file configuration, if you are using webpack 2.0+ you need to give the output path an absolute path. That is why we use require('path')
      You should make a folder src/assets/js in preparation for when you run webpack.
    {% highlight ruby %}
    const path = require('path');
    module.exports = {
      entry: './webpack/entry.js',
      output: {
        path: path.resolve(__dirname, 'src/assets/js'),
        filename: 'bundle.js'
      },
      module: {
      loaders: [
        {
          test: /\.jsx?$/,
          exclude: /(node_modules)/,
          loader: 'babel-loader',
          query: {
            presets: ['react', 'es2015']
          }
        }
        ]
      }
    };{% endhighlight %}

*5. In your config.yml set node_modules to be ignored, this is what my excludes are. The reasoning for this is to prevent a lot of clutter entering your project when you are likely not using it:
    {% highlight ruby %}
     exclude:
      - Gemfile
      - Gemfile.lock
      -'node_modules'{% endhighlight %}

*6. Add bundlejs as a source to the bottom of your page. The DOM needs to be fully loaded before importing the script.
    If there is a different way to do this or if you have more information let me know! As of right now I found best results by putting my src in the footer of my site at the end:
    {% highlight ruby %}<script type="text/javascript" src="/assets/js/bundle.js" charset="utf-8"></script>{% endhighlight %}

*7. Next install loaders and libraries used to compile and run es6 React(This will add in devdependencies to your package.json file.):
    {% highlight ruby %}
    npm install webpack babel-core babel-loader babel-preset-es2015\
     babel-preset-reactreact react-addons-update react-dom\
      --save-dev{% endhighlight %}  

*8. Prepare for simple react component!:  
    create a components folder in webpack and also a Hello.js file:
    {% highlight ruby %}
    webpack/components/Hello.js{% endhighlight %}

*9. Setup Hello.js
    {% highlight ruby %}
    import React from 'react';

    export default class App extends React.Component {
      render() {
        return (
         <div style="textAlign:center;">
            <h1>Hello World (First React Component May 2)</h1>
          </div>);
      }
    }{% endhighlight %}

*10. entry.js
    {% highlight ruby %}
    import React from 'react';
    import ReactDOM from 'react-dom';
    import App from './components/Hello.js';

    ReactDOM.render(<App />, document.getElementById('root'));{% endhighlight %}

*11. Add a div with id root and make sure bundle js is imported in your footer and you will see your react component load in and say whatever you put in your h1 tag ex:

<div id="root"></div>

*12. Right now the component above is getting an element with ID root and rendering through the ReactDom our component named App which is declared in Hello.js


  <script type="text/javascript" src="/assets/js/bundle.js" charset="utf-8"></script>
