 
  ```Javascript
         <a-text value="The News" bugs-me-score="3"  position="-1.1 2 -1.5"   color="red" font="kelsonsans"></a-text>
        <a-text value="My Knees" bugs-me-score= "8" position="-1.1 1.5 -1.5" color="red" font="kelsonsans"></a-text>
  ```Javascript
 
 ```Javascript
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
     ```Javascript
    
    
    
    
        
        
        
        
        
   
    ```Javascript
      AFRAME.registerComponent('bugs-me-score', {
        schema: {default: 10},
 ```Javascript
 
 [more than one value](https://aframe.io/docs/0.7.0/introduction/writing-a-component.html)

 ```Javascript  
            var score = this.data;
   ```Javascript
   
   ```Javascript          
            el.setAttribute('opacity', 0.05 * score);
    ```Javascript
            
  
  
   ```Javascript
            if (score < 4) {
              el.object3D.scale.set(0.7, 0.7, 1);   
            } else {
              el.object3D.scale.set(0.9, 0.9, 1);   
            };
        
        
        
   
