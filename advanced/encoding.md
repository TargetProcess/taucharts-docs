##Custom colors for encoding color value
You can set custom colors to encode color value or use bundles from a nice categorical color scales by [Cynthia Brewer](http://colorbrewer2.org/).
If you want to use colorbrewer, you should include the following code into your pages:

```HTML
 <link href="path_to_tauCharts/css/colorbrewer.css" rel="stylesheet"/>
 <script src="path_to_tauCharts/src/addons/color-brewer.js"></script>
```
and define color shouldlike this
```javascript
var spec = {
  unit:[{
       type: 'ELEMENT.POINT',
       x: 'month',
       y: 'count',
       color: 'team',
       guide:{
            color:{
                brewer:tauBrewer('YlGnBu',9)
            }
       }
   }]
};
```

If you want use custom colors, just enumerate classes in an array. Obviously, you should define *myColorCssClass1* and other classes in CSS.

```javascript
var spec = {
  unit:[{
       type: 'ELEMENT.POINT',
       x: 'month',
       y: 'count',
       color: 'team',
       guide:{
           color:{
                brewer:['myColorCssClass1','myColorCssClass2','myColorCssClass3']
           }
       }
   }]
};
```
Sometime you want to explicitly link some category to a color. For example, all points with 'NewTeam' team should be red. Here is how you define that using *color* and brewer *attributes*:

```javascript
var spec = {
    unit:[{
        type: 'ELEMENT.POINT',
        x: 'month',
        y: 'count',
        color: 'team',
        guide:{
            color:{
                brewer:{
                    NewTeam:'css-red',
                    Alaska:'css-blue',
                    oldTeam:'css-black'
                }
            }
        }

    }]
};
```

##Size
Size encoding currently applies to point element only. Point diameter depends on the min and max value in a *size* dimension.

```javascript
var spec = {
    unit:[{
        type: 'ELEMENT.POINT',
        x: 'effort',
        y: 'cycleTime',
        size: 'bugsCount'
    }]
};
```

[jsBin example](http://jsbin.com/hogoci/33/embed?output&height=500px)
