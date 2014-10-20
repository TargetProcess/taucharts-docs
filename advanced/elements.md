For creating composite cart you can use small elements [line](#line), [interval](#interval), [point](#point).

Example [jsBin](http://jsbin.com/hogoci/20/embed?,output)
##Line
Line element draws line and has following view
```javascript
   var line = {
        'ELEMENTS.LINE':{
                x:'dimensionX,
                y:'dimensionY'
                color:'dimensionForGrouping'
        }
   }
```
Property color use for groping your data. For example if you have data like
```javascript
  var data = [
          {x:1, y:1, name:'firstLine'},
          {x:5, y:19, name: 'secondLine'},
          {x:14, y:3, name:'firstLine'},
          {x:6, y:1, name: 'secondLine'},
      ];
```
and you will create graphic with params
```javascript
   var lineElement = {
           unit: {
               type: 'COORDS.RECT',
               x:'x',
               y:'y',
            guide: {
                   showGridLines: 'xy',
                   padding: { l:56, b:46, r:8, t:8 },
                   x: {padding: 8, label: 'x'},
                   y: {padding: 8, label: 'Y'}
               },
               unit: [{
                   type:'ELEMENT.LINE',
                   x:'x',
                   y:'y',
                   color:'name'
               }]
           }
       };

       new tauChart.Plot({
                       data: data,
                       spec: lineElement
                   }).renderTo('#line-element');
```
you will get result
[jsBin](http://jsbin.com/hogoci/19/embed?output)
