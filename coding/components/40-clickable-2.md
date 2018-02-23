## Creating and Adding a New Object

Not only can components change an HTML element that use them, they can also interact with other HTML elements -- 
and even create new HTML elements. In this last exercise, we learn how to create a new HTML element.

You've already learned how to make something that bugs you shrink when you click on it. But if it really does bug you you less, you want to do more. You want  to shrink it a little more each time you click on it.   You also want to celebrate your little victory. And what better way to celebrate a little than by adding a small turquoise ball to the screen?

Here's the script:

```js
AFRAME.registerComponent('could-bug-me-less', {
init: function () {
    var el = this.el; 
    var score = 10;
    var scene = document.querySelector('a-scene');

    // Text isn't clickable out-of-the-box; we need to add a geometry component, such as a plane
    el.setAttribute('geometry', "height:auto;primitive:plane;width:4");
    el.setAttribute('material', 'opacity: 0');      


    el.addEventListener('click', function () {

        // Make the text a little smaller and a little less visible (i.e., less opaque)
        score = score - 1;
        el.object3D.scale.set(0.1 * score, 0.1 * score, 1);   
        el.setAttribute('opacity', 0.05 * score);

        // Add a little ball in a randomly chosen location
        var ball = document.createElement('a-sphere');
        ball.setAttribute('color', 'turquoise');
        ball.setAttribute('radius', '0.05');
        ball.setAttribute('position', {x: Math.random(),  y: 2.4 - Math.random() * 1.5, 
                                        z: -1.5 + Math.random()});
        scene.appendChild(ball);
    });
}
});
```

Let's break it down. First, we will register the component and add 3 variables.

```js
      AFRAME.registerComponent('could-bug-me-less', {
        init: function () {
            var el = this.el; 
            var score = 10;
            var scene = document.querySelector('a-scene');
```
- **el**: let's us access the text element
- **score**: keep track of the bugs-me-less score, which starts at 10 -- fully bugging you

The last variable, scene, does a little magic. It looks through the A-Frame page and finds the A-Frame scene. As you may remember, the scene is like a scene in a movie: it organizes all the action. Every HTML element that's going to show up on the screen has to be inside the a-scene. We are going to use this in just a minute to add a turquoise  ball to the scene.

Next, just like we did in the last lesson, we need to add some lines of code that make the text clickable:

```js
el.setAttribute('geometry', "height:auto;primitive:plane;width:4");
el.setAttribute('material', 'opacity: 0');      
```

And just like we did in the last lesson, we tell it that if the user clicks on the text, here's the function it should run:

```js
el.addEventListener('click', function () {
```

If the user clicks on the text, we want to do 2 things. First, we want to decrease the score by 1
and then make the text a little smaller and a little less visible/opaque:

```js
score = score - 1;
el.object3D.scale.set(0.1 * score, 0.1 * score, 1);   
el.setAttribute('opacity', 0.05 * score);
```

Then we want to add our cheery little turquoise ball. To do that, first we create an A-Frame sphere element:

```js
var ball = document.createElement('a-sphere');
```

Now we need to pretty it up:
```js
ball.setAttribute('color', 'turquoise');
ball.setAttribute('radius', '0.05');
ball.setAttribute('position', {x: Math.random(),  y: 2.4 - Math.random() * 1.5, 
                                z: -1.5 + Math.random()});
```

The first 2 lines make it turquoise and give it a radius of 0.5. The last line uses a little bit of high school math
to  randomly position the ball on the screen.  Math.random() gives us a random number between 0 and 1. To get a better feel for what this math is doing, play around with it; try changing the numbers and see what impact it has on the turquoise balls.

The last thing we need to do is to add our turquoise ball to the scene:

```js
scene.appendChild(ball);
```

And that's it!  Before you move on to the next lesson, go to [Glitch]() and see the component in action. Then try tweaking the code. 

Once you've played around with the code and have gotten comfortable with what you've learned so far, should definitely check out the A-Frame  [documentation](https://aframe.io/docs/0.7.0/introduction/writing-a-component.html) on creating components; there are lots more tricks to learn!