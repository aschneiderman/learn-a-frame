## Interacting with the User, Part 1: Clicking

So far, if the user wants to change one of the items to show that it bugs are less than it used to, she had to go into the HTML and change it. But what we really want is to let her change an item's status by clicking on it.

The first thing we need to do is to add some HTML tells A-Frame we want to be able to click on objects:

```HTML
      <a-camera mouse-cursor >
        <a-cursor color="green"></a-cursor>
      </a-camera>
```

In this case, we told A-Frame that it should create a small green circle, or cursor, on the screen. When the user wants to click an item, they move the cursor on top of that item and then click it.

Next we need to add our new attribute, could-bug-me-less, to each of the items that bug us:

```HTML
      <a-text value="The News"                 could-bug-me-less  position="-1.1 2 -1.5"   color="red" font="kelsonsans"></a-text>
```

Now to make the magic happen. First, we change the name of the component should and could-bug-me-less:

```JavaScript
      AFRAME.registerComponent('could-bug-me-less', {
```

Why? To show you one more time that component names aren't magical; you can use whatever name you want so long as you use the same name in the HTML as you did when you register the component.

Now we need to do something that's a little odd.

 It turns out that A-Frame knows that boxes and spheres and planes are clickable. But for some reason, it doesn't know that text is clickable because -- for reasons I don't understand --  it doesn't treat text as a 3 dimensional object. To fix that, we need to add a "geometry" component to each text item that we want to make clickable. The easiest way to do this is to add a plane component to it. But we don't want users to see the plane; we need to make it invisible. Here's how we do it:

```JavaScript
            // Text isn't clickable out-of-the-box; we need to add a geometry component, such as a plane
            el.setAttribute('geometry', "height:auto;primitive:plane;width:4");
            el.setAttribute('material', 'opacity: 0');      // Make the plane invisible
```            

(is this weird? Yes it is. But don't sweat it; almost every computer language/framework has a few corners that are a little weird)

Okay, on to the main event: making sure the script knows what to do if the user clicks on the text.

```JavaScript
            el.addEventListener('click', function () {
                el.setAttribute('opacity', 0.2);
                el.object3D.scale.set(0.9, 0.9, 0.9);    
            });
```

 First, we add an "event listener" to the text element. Essentially, this tells the text, if the user clicks on the text, here's the function you should run. What the function tells it to do is to make the text much less transparent by setting the opacity to 0.2 and to scale the object to 0.9 or 90% of its size. You'll notice that just like we did with init, we use an "anonymous function"; since we are only using this function once is no reason to give it a name and define it separately.

And that's it! To see it in action, you can check it out on [Glitch](
) and cries [tweaking the code](
); also check it out on its [GitHub](https://mr4all.github.io/learning-a-frame/coding/components/code/30-clickable.html) page, where you can also view the [source code](https://github.com/mr4all/learning-a-frame/blob/master/coding/components/code/30-clickable.html).