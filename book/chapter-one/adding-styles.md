# Adding styles to your components

Up to now we've added a component but without any classes or styles. 

Naturally one way is to write into our component the classes we want. This makes sense for static classes, that is, classes that won't change. Something like:

```js
var Comment = React.createClass({
          render: function(){
              return (
                  <div class="well" id="comment-2">
                    <h1>This is totes a comment!</h1>
                    <p class="lead">by Andrew Duckworth</p>
                  </div>
              );
          }
      });
```
Here we've added in the ```.well``` class on the ```<div>``` and ```.lead``` class on our paragraph. But for an interactive app, we may want to be able to update classes and styles on the fly.

Let's learn how to add some style to our components. We'll do this three ways:

1. Inline aka 1997
2. Through creating a variable per line of CSS
3. Through the use of a JavaScript object

Create a file called something like ```hello-styles.html```. Inside that file the following:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello React Styles!</title>
    <script src="/react-et-al/build/react-with-addons.js"></script>
    <script src="/react-et-al/build/JSXTransformer.js"></script>
    <style>
      .important {
        
        color: blue;
        
      }
      
      .flipping-awesome-guy {
        
        text-transform: uppercase;
        
      }
    </style>
  </head>
  <body>
    <div id="comments"></div>
    <script type="text/jsx">
    
      var commentStyles = {
      
        //inline method, notice it uses JavaScript syntax for CSS
        color: 'pink',
        fontSize: '15px'
      
      };
    
      var Comment = React.createClass({
          render: function(){
              
              // manual class way
              var yourClassName = 'important';
              
              // class in an object way
              var classObjectWay = React.addons.classSet;
              var classes = classObjectWay({
                'flipping-awesome-guy': true,
                'dull': this.props.isDull
              });
          
              return (
                  <div id="comment-3">
                    <h1 style={commentStyles}>Oh man, this is well styled</h1>
                    <p className={yourClassName}><span className={classes}>by Andrew Duckworth</span></p>
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

Quite a bit of code there and a few major things to cover.

One of the important things is that we have added some amazing styles to the code itself. Feel free to add.

The second important one is the use of the ```react-with-addons.js``` version of React.js instead of the vanilla JS. As you might have guessed, we use an addon.

Make sure you link to the addons file correctly and have some styles to call. Let's go through how to add classes to React.js strategy by strategy.

## adding styles inline

To add styles inline we create a variable and an object in which we add the styles. We create the CSS using the JavaScript names - like you would in jQuery - so instead of ```font-size``` is it ```fontSize```.

So, in our example we created our inline styles like this:

```js
var commentStyles = {
      
        //inline method
        color: 'pink',
        fontSize: "15px"
      
      };
```

To get this into the Comment we add it into the HTML template, within the render function like so:

```js
var Comment = React.createClass({
          render: function(){
          
            // Other code removed for clarity
              
              return (
                  <div id="comment-3">
                    <h1 style={commentStyles}>Oh man, this is well styled</h1>
                    // ...
                  </div>
              );
          }
      });
```

As you can see, we write the html style attribute and inject into that, via a moustache ```{}```, the variable ```commentStyles```.

This way is pretty nice in terms of writing the CSS in a variable/object, but it isn't great in terms of the final markup.

## Adding classes one variable at a time

The second way of adding a class is to add the desired class to your application through a single class variable declaration.

In this example you create a variable and assign to it a string with your class attached like so:

```js
var yourClassName = 'important';
```

You then inject that into your component by setting ```className``` to your variable within a single set of moustaches as below:

```js
var Comment = React.createClass({
          render: function(){
              
              var yourClassName = 'important';
          
              return (
                  <div id="comment-3">
                    // ...
                    <p className={yourClassName}>by Andrew Duckworth</p>
                  </div>
              );
          }
      });
```

The benefit of this is we have class based styles inside our components now. This method covers a lot of use cases. 

> You can also load up your variable with a whole raft of classes. It is essentially just a string that you are injecting into the class attribute. So, if you are leaning on the Bootstrap framework your button variable could look like:
> ```js
> var bootstrapButtonClass = "btn btn-primary btn-lg";
> ```

You can also add additional conditions. Here is an example of that:

```js
var Comment = React.createClass({
          render: function(){
              
              // Other code removed for clarity
              
              if (authorIsTotesMegaCool) {
              
                  // note the space infront of the new class
                  yourClassName += ' totally-mega-important';
              }
          
             // etc. ...           
           
          }
      });
```

Now, if we build in some functionality where we can set certain conditions we can add some extra classes to our original string and they will render into our HTML.

However, there are issues using this method as different scenarios (active, alerts etc. etc.) may require a dedicated variable. This could make our components a little bit messy.

That is, if we have a small app where there are a few conditions (if condition A etc.) for a component this isn't too much of an issue and is managable. If we have numerous components all with seperate, complicated conditions to which CSS class should be used however, this method can get a little brittle and repetative - nevermind complicated to read and debug. 

There is another way of adding classes which modularizes the CSS classes we want to add.

## Adding classes through a class object

In order to add classes through a class object you need to include an additional plugin.

To do so with the react.js starter pack we include the following line:

```
<script src="/react-et-al/build/react-with-addons.js"></script>
```

> As of React 0.14 this is no longer true.
> You must now include https://github.com/JedWatson/classnames
> Add this in, and instead of ```classSet``` use ```classNames()```
> In the code for this chapter you can just include ```the classNames.js``` file.
> In production apps, install via NPM etc.

This is instead of just ```react.js```.

With our plugins included with can now leverage the ```React.addons.classSet``` functionality.

We start by declaring a variable to the ```classSet()``` function like so:

```js
var classObjectWay = React.addons.classSet;
```

We can then use ```classObjectWay``` to create an object with all of our potential values in one place.

```js
// class in an object way
              var classObjectWay = React.addons.classSet;
              var classes = classObjectWay({
                'flipping-awesome-guy': true,
                'not-getting-added': false, // Anything false doesn't get added
                'dull': this.props.isDull // don't worry if this is confusing. We'll cover props later. Essentially you can add classes if your element is indicted as dull or whatever you want to set. Like above, this relates to false and dull is not added
              });
```

So within the ```classObjectWay({})``` object we declared you can set CSS classes that will be assigned if the value on the right is true or false. If they are true, they get added. If they aren't, they don't.

As you may be able to imagine, this allows us to declare in one place all of the various states and their corresponding CSS classes for alerts.

Another benefit of this method is reduced lines of conditionals like ```if(this.props.isDull){ ... }``` and the lack of repliance on adding strings togther (as with the previous method).

An issue of course is that we are now relying on a plugin. This is a trade-off you'll have to consider if you choose this method.

If you ran this example you may have also noticed that we get the following warning from our browser

```
Warning: React.addons.classSet will be deprecated in a future version. See http://fb.me/react-addons-classset
```

In the future the ```classSet()``` plugin will be removed completely from the plugin bundle. This is not to say the plugin is completely depreciated, but rather that it has a new home.

The new home for the ```classSet()``` plugin is here: [https://github.com/JedWatson/classnames](https://github.com/JedWatson/classnames) 

### Further resources

[Documentation on adding classes](https://facebook.github.io/react/docs/class-name-manipulation.html)
[Documentation on adding styles inline](http://facebook.github.io/react/tips/inline-styles.html)