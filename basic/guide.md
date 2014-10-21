#Guide
Guide is responsible for axes look and feel, color, size and other aesthetic parameters.

Guide can accept following params:

TODO: examples with real charts

##Axis
x or y describe axis view
```javascript
  var guide = {
        x:{
           label: { text: 'Count', padding: 36 }
        }
  }
```

##Coordinate grid
If you want draw coordinate grid, you can set *showGridLines*:
```javascript
   var guide = {
        showGridLines:'xy' //show vertical and horizontal line
   }
   //show only x coordinate line
    var guide = {
           showGridLines:'x' //show vertical line
    }
    //or only y
    var guide = {
           showGridLines:'y' //show horizontal line
    }
```

##Color
See [encoding](../advanced/encoding.md#custom-colors-for-encoding-color-value) section.
