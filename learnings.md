# Learning React.js

React.js is a javascript framework created by Facebook and the team at Instagram. 

It focuses on creating "Views" and as such doesn't try to replicate the entirety of an MVC framework on the "front-end".

## Getting React.js

The first thing you have to do is download their starter pack. This is easily achieved by "wget-ing" the pack:

```shell
wget http://facebook.github.io/react/downloads/react-0.13.3.zip
```

>> Copying this will get the pack version 0.13.3, so when that is no longer the latest, find the version number you need

You can then unzip the file and either browse the examples or use the code to create your own. 

To unzip and delete the zip file in one line, you can do something like this:

```shell
unzip react-0.13.3.zip && rm react-0.13.3.zip
```

## Putting React into your HTML

Inside the starter pack you'll find plenty of examples and inside the build directory you'll find several versions of react.js and the JSXTransformer

>> JSX is a version of JavaScript combined with XML. The idea of JSX is to make a JavaScript syntax better optimized for rendering HTML inside of JS objects.

To get a handle on getting used to React.js, let's use these files but in our own html file.

Create a file called something dull like ```hello-world.html```. Inside that file write:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello World React!</title>
    <script src="/react-0.13.3/build/react.js"></script>
    <script src="/react-0.13.3/build/JSXTransformer.js"></script>
  </head>
  <body>
    <div id="comments"></div>
    <script type="text/jsx">
      React.render(
        <div id="comment-1">
          <h1>Hello, world!</h1>
          <p>by Andrew Duckworth</p>
        </div>,
        document.getElementById('comments')
      );
    </script>
  </body>
</html>
```

Few things going on here, let's explain.

1. The "src" of your ```react.js``` and ```JSXTransformer.js``` files should point to wherever your build files are.
2. the ```<div id="comment"></div>``` gives us an ID to inject our comment into
3. The ```<script type="text/jsx"></script>``` indicates to react.js that we are using the jsx syntax (and not JavaScript)
4. Inside the script tag is the call to the ```React.render();``` function.
5. Inside the function, on two lines seperated by a comma write the HTML we want to inject and then where we want to inject the HTML

Open up your browser. You should see the stunning comment. If you find any errors, investigate and solve.

A couple of things to try. Remove the ```<div id="comment-1"></div>```. What happens?

>> It breaks. Needs to be wrapped by a single overarching element due to its XML nature

Create a second call to ```React.render();```. What happens?

>> Overites the first element. See more about ```React.render();``` [here in the offical documentation](http://facebook.github.io/react/docs/top-level-api.html#react.render)


## Using React.js Components

We've just built a really simple thing. But you've not yet seen anything great about React.js.

Let's use a core element of React.js called "components".

Components are essentially the HTML that you render when you call ```React.render()```. You did this in the last example but placed the HTML you wanted rendering into the function call.

This time, we'll create a custom component in its own variable that we can call.


```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello React Components!</title>
    <script src="/react-et-al/build/react.js"></script>
    <script src="/react-et-al/build/JSXTransformer.js"></script>
  </head>
  <body>
    <div id="comments"></div>
    <script type="text/jsx">
      var Comment = React.createClass({
          render: function(){
              return (
                  <div id="comment-2">
                    <h1>This is totes a comment!</h1>
                    <p>by Andrew Duckworth</p>
                  </div>
              );
          }
      });
      
      React.render(
          <Comment/>,
          document.getElementById('comments')
      );
    </script>
  </body>
</html>
```

>> You have to enclose the element like ```<Comment/>```. This is because it is like an XML tag. You can enclose things in ```<Comment></Comment>```.