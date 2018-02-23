## Creating a Basic Component

Let's say you made an A-frame page with a list of things that are really bugging you:

```html
<a-scene>
    <a-text value="What's Really Bugging Me"  position="-1.1 2.5 -1.5" color="black" font="kelsonsans"></a-text>
    <a-text value="Waking up Early"           position="-1.1 1.0 -1.5" color="red" font="kelsonsans"></a-text>
    <a-text value="The News"                  position="-1.1 2 -1.5"   color="red" font="kelsonsans"></a-text>
    <a-text value="My Knees"                  position="-1.1 1.5 -1.5" color="red" font="kelsonsans"></a-text>
    <a-sky color="lightyellow"></a-sky>
</a-scene>
```

Before you go any further, see what the [list looks like](https://github.com/mr4all/learn-a-frame/blob/master/coding/components/code/00-whats-bugging-me.html) in VR.

Suppose you want to create an attribute called **bugs-me-less**:

```HTML
    <a-text value="My Knees" bugs-me-less       position="-1.1 1.5 -1.5" color="red" font="kelsonsans"></a-text>
```

If you add bugs-me-less to one of the items in your list, it would make the text a little more transparent/opaque and slightly smaller.

To make the attribute work, you'd need to create a component. Here's how:

```js
<script>
    AFRAME.registerComponent('bugs-me-less', {
    init: function () {
        var el = this.el;                     // el = an HTML element/tag that's using this component
        el.setAttribute('opacity', 0.2);
        el.object3D.scale.set(0.9, 0.9, 1);   // Scale documentation says this is much faster than using setAttribute
    }
    });
</script>
```

Let's break it down.

First we need to create and register our component and give it a name -- in this case bugs-me-less.

```js
AFRAME.registerComponent('bugs-me-less', {
```
Then we need to tell A-Frame what to do when an HTML element uses our attribute. **init**, short for initialize, tells it to run the following function on that HTML element.

```js
init: function () {
```
Normally, when you are going to use a function, first you define it and give it a name, then you call the function by that name whenever you need it. But in this case we are only going to use this function once. So instead of defining it somewhere else in the code and then calling it here, we can define and use it in one shot. And since we aren't using it elsewhere, we don't need to give it a name. This kind of function is known as an "anonymous function."

Inside the function, we are going to do 3 things. First, if we are going to change the look and feel of the text element, we need some way to refer to it.  **this.el** will get us the info we need.

```js
var el = this.el;
```

We could use this.el directly, but the convention in A-Frame is to save it in a variable called el.

Next, we're going to make the text more transparent/opaque. We do it by setting the text **opaque**attribute:

```js
el.setAttribute('opacity', 0.2);

Finally, we will shrink the text slightly by changing the text's scale attribute:

```js
el.object3D.scale.set(0.9, 0.9, 1);
```

Wait, what? Why didn't we just use setAttribute?

Because the [documentation](https://github.com/aframevr/aframe/blob/master/docs/components/scale.md) recommends you don't use setAttribute when you're changing scale:

> For performance and ergonomics, we recommend updating scale directly via the three.js Object3D .scale Vector3 versus via .setAttribute....
>
> [This approach is] faster by skipping .setAttribute overhead and not needing to create an object to set rotation

And what's all this about three.js , object3D, Vector3  etc.?  A-Frame is built on top of a library called three.js. What they're essentially saying is that by directly calling that library, you'll improve performance. It won't make a difference if you're just changing the scale of one text element. But it could definitely make a difference if you're changing a lot of elements down the line, so it's good to get the practice of using it. And if you see it in anybody else's code, now you'll know what it is.

This also brings us to an important lesson. Components look a little weird when you first see them, but once created a couple you'll have used the same pattern over and over so it will become second nature. The hard part isn't the slightly weird JavaScript, it's getting used to all of the libraries you will end up using and dealing with dealing with issues like performance.

And now for the good news: you're done! In just a few lines of code, you have created a component.

Before you move on to the next lesson, go to [Glitch]() and see the component in action. Then try tweaking the code. For example, see what happens if you change the opaqueness or scale.

Up Next: [Using Parameters](20-parameters.html)