## Using Parameters

In the last exercise, we learned how to add a "bugs-me-less" attribute. But suppose we wanted a little more control. Instead of bugs-me-less, we could give the item that bugs you a bugs-me-score between 1 and 10:

  ```HTML
         <a-text value="The News" bugs-me-score="3"  position="-1.1 2 -1.5"   color="red" font="kelsonsans"></a-text>
        <a-text value="My Knees" bugs-me-score= "8" position="-1.1 1.5 -1.5" color="red" font="kelsonsans"></a-text>
  ```

To make that work, we will create a bugs-me-score component. 

```js
    <script>
      AFRAME.registerComponent('bugs-me-score', {
        schema: {default: 10},
        init: function () {
            var el = this.el;
            var score = this.data;
            el.setAttribute('opacity', 0.05 * score);
            if (score < 4) {
              el.object3D.scale.set(0.7, 0.7, 1);   
            } else {
              el.object3D.scale.set(0.9, 0.9, 1);   
            };
        }
      });
    </script>
```

If you want to change its name from bugs-me-less to bugs-me-score, all you need to do is change the name you use in registerComponent.
  
```js
      AFRAME.registerComponent('bugs-me-score', {
 ```

To let A-Frame know that it should expect to be passed a score, we create what's called a schema.     
 ```Javascript
        schema: {default: 10},
 ```

This schema tells it that it should expect to be passed one value and that if it isn't passed a value, the default score should be 10. You can also pass more than one value; see the [component documentation](https://aframe.io/docs/0.7.0/introduction/writing-a-component.html).

In the last lesson, we learned that we could use this.el to get HTML element/tag that was using the component. To get the component's value, use this.data
```Javascript  
            var score = this.data;
```
   
Then we change the opacity/transparency of the text to score times .05

```Javascript          
            el.setAttribute('opacity', 0.05 * score);
```

We didn't have to store this.data in a variable called score. We could have used it directly            
  
```Javascript          
            el.setAttribute('opacity', 0.05 *this.data);
```

But by using a variable called score, easier for someone reading the script to understand what were doing.

This script uses one more trick: if. In addition to making the text more opaque/transparent, we also want to make it smaller. But we only want to make it a little smaller; if we multiplied the text's scale by the score, it would quickly get so tiny we wouldn't be able to see it. So instead we tell it that if the score is less than 4, set the scale to 0.7 or 70% of its original size; otherwise, sent the scale to 0.9 or 90% of its original size.
  
```Javascript
            if (score < 4) {
              el.object3D.scale.set(0.7, 0.7, 0.7);   
            } else {
              el.object3D.scale.set(0.9, 0.9, 0.9);   
            };
        
And then we're set!
