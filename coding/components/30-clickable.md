## Changing the Text If the User Clicks on It

So far, if the user wants to change one of the items to show that it bugs her less than it used to, she had to go into the HTML and change it. But what we really want is to let her change an item's status by clicking on it.

The first thing we need to do is to add some HTML to tell A-Frame we want to be able to click on objects:

```html
<a-camera mouse-cursor >
      <a-cursor color="green"></a-cursor>
</a-camera>
```

This code says to create a small green circle, or cursor, on the screen. When the user wants to click an item, they move the cursor on top of that item and then click it.

Next we need to add our new attribute, could-bug-me-less, to each of the items that bug us:

```html
<a-text value="Waking up Early"          could-bug-me-less  position="-1.1 1.0 -1.5" color="red" font="kelsonsans"></a-text>
<a-text value="The News"                 could-bug-me-less  position="-1.1 2 -1.5"   color="red" font="kelsonsans"></a-text>
<a-text value="My Knees"                 could-bug-me-less  position="-1.1 1.5 -1.5" color="red" font="kelsonsans"></a-text>
```

Now to make the magic happen. First, we change the name of the component to could-bug-me-less:

```js
AFRAME.registerComponent('could-bug-me-less', {
```

As you can see, component names aren't magical; you can use whatever name you want so long as you use the same name in the HTML as you did when you register the component.

Now we need to do something that's a little odd.

 It turns out that A-Frame knows that boxes and spheres and planes are clickable. But for some reason, it doesn't know that text is clickable because -- for reasons I don't understand --  it doesn't treat text as a 3 dimensional object. To fix that, we need to add a "geometry" component to each text item that we want to make clickable. The easiest way to do this is to add a plane component to it. But we don't want users to see the plane, so we need to make it invisible. Here's how we do it:

```js
el.setAttribute('geometry', "height:auto;primitive:plane;width:4");
el.setAttribute('material', 'opacity: 0');      // Make the plane invisible
```            

Is this weird? Yes, but don't sweat it. Almost every framework has a few corners that are a little weird.

Okay, on to the main event: making sure the script knows what to do if the user clicks on the text.

```js
el.addEventListener('click', function () {
      el.setAttribute('opacity', 0.2);
      el.object3D.scale.set(0.9, 0.9, 0.9);    
});
```

First, we add an "event listener" to the text element. This tells the text, if the user clicks on the text, here's the function you should run. 

Just like when we register the component, instead of creating a separate function and then calling it, we will do it all in one shot by using an anonymous function.

What should do when a user clicks on the text?

- Make the text much less transparent by setting the opacity to 0.2 
- Scale the object to 0.9 or 90% of its size. .

And that's it! Before you move on to the next lesson, go to [Glitch]() and see the component in action. Then try tweaking the code. 

Up Next: [Adding an Object](30-clickable-2.html)