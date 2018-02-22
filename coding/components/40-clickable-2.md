## Interacting with the User, Part 2: Creating a New Object

Not only can components change an HTML element that use them, they can also interact with other HTML elements -- 
and even create new HTML elements. In this last exercise, we learn how to create a new HTML element.

You've already learned how to make something that bugs you shrink when you click on it. But if it really does bug you you less, you want to do more. You want  to shrink it a little more each time you click on it.   You also want to celebrate your little victory. And what better way to celebrate a little than by adding a small turquoise ball to the screen?

First, we will register the component and add 3 variables.

```JavaScript
      AFRAME.registerComponent('could-bug-me-less', {
        init: function () {
            var el = this.el; 
            var score = 10;
            var scene = document.querySelector('a-scene');
```
- **el**: let's us access the text element
- **score**: keep track of the bugs-me-less score, which starts at 10 -- fully bugging you

The last variable, scene, does a little magic. It looks through the A-Frame page and finds the A-Frame scene. As you may remember, the scene is like a scene in a movie: it organizes all the action. Every HTML element that's going to show up on the screen has to be inside the a-scene. We are going to use this in just a minute to add a turquoise  ball to the scene.

Next, just like we did in the last exercise, we need to add some line sof code that make the text clickable:

```JavaScript
    // Text isn't clickable out-of-the-box; we need to add a geometry component, such as a plane
    el.setAttribute('geometry', "height:auto;primitive:plane;width:4");
    el.setAttribute('material', 'opacity: 0');      
```

Next, just like we did in the last exercise, we told that if the user clicks on the text, here's the function it should run:

```JavaScript
    el.addEventListener('click', function () {
```

If the user clicks on the text, we want to do 2 things. First, we want to decrease the score by 1
and then make the text a little smaller and a little less visible/opaque:

```JavaScript
    score = score - 1;
    el.object3D.scale.set(0.1 * score, 0.1 * score, 1);   
    el.setAttribute('opacity', 0.05 * score);
```

Then we want to add our cheery little turquoise ball. To do that, first we create an A-Frame sphere element:

```JavaScript
    var ball = document.createElement('a-sphere');
```

Now we need to pretty it up:
```JavaScript
    ball.setAttribute('color', 'turquoise');
    ball.setAttribute('radius', '0.05');
    ball.setAttribute('position', {x: Math.random(),  y: 2.4 - Math.random() * 1.5, 
                                    z: -1.5 + Math.random()});
```

The first 2 lines make it turquoise and give it a radius of 0.5. The last line uses a little bit of high school math
to  randomly position the ball on the screen.  Math.random() gives us a random number between 0 and 1. To get a better feel for what this math is doing, play around with it; try changing the numbers and see what impact it has on the turquoise balls.

The last thing we need to do is to add our turquoise ball to the scene. Here's how:

```JavaScript
    scene.appendChild(ball);
```

And that's it!  To see it in action, you can check it out on [Glitch](
) and cries [tweaking the code](
); also check it out on its [GitHub](https://mr4all.github.io/learning-a-frame/coding/components/code/30-clickable-2.html) page, where you can also view the [source code](https://github.com/mr4all/learning-a-frame/blob/master/coding/components/code/30-clickable-2.html).




    