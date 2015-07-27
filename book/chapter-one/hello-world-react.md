# Howdy React.js

Inside the starter pack you'll find plenty of examples and inside the build directory you'll find several versions of react.js and the JSXTransformer

> JSX is a version of JavaScript combined with XML. The idea of JSX is to make a JavaScript syntax better optimized for rendering HTML inside of JS objects. At first the use of JSX and its XML-nature can be a bit of a put off for JS developers. But, stick with it. It is perfect for creating HTML templates with the added power of JavaScript.

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

> It breaks. Needs to be wrapped by a single overarching element due to its XML nature

Create a second call to ```React.render();```. What happens?

> Overites the first element. See more about ```React.render();``` [here in the offical documentation](http://facebook.github.io/react/docs/top-level-api.html#react.render)

### Further resources

[React.render() API Documentation](http://facebook.github.io/react/docs/top-level-api.html#react.render) 