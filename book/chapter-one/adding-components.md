# React.js components

We've just built a really simple thing. But you've not yet seen anything great about React.js.

Let's use a core element of React.js called "components".

Components are essentially the HTML that you render when you call ```React.render()```. You did this in the last example but placed the HTML you wanted rendering into the function call.

This time, we'll create a custom component in its own variable that we can call.

Create a file called something like ```hello-components.html```. Inside that file write:


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

Inside this file we've created a component using the ```createClass``` function and then rendered that by calling it within ```React.render();``` which will render the comment. 

Let's go through the file bit by bit:

1. Like before, we included the react.js and JSXtranformer.js files
2. we set up the same div with the id of comments
3. we create a variable of ```Comment``` to the value of ```React.createClass({});```
4. Inside that we create a function that returns our HTML template with a comment
5. We ensure the world gets to see our comment by calling the Comment variable inside a custom HTML tag called ```<Comment/>``` inside the ```React.render();``` function.
6. As before the ```React.render();``` function injects our HTML into an element we selected, in this case the one with an ID of comments. Unlike before of course, this time we created a custom component (or element) and injected that in

>> You have to enclose the element like ```<Comment/>```. This is because it is like an XML tag. You can enclose things in ```<Comment></Comment>```. [For reference see the documentation](http://facebook.github.io/react/tips/self-closing-tag.html)

### Further resources

[]() 