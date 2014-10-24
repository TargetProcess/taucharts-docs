##Custom colors for encoding color value
You can set custom colors for encoding color value or use bundles some fantastic categorical color scales by [Cynthia Brewer](http://colorbrewer2.org/).
If you want use colorbrewer, you should include following code in your pages
```HTML
 <link href="path_to_tauCharts/css/colorbrewer.css" rel="stylesheet"/>
 <script src="path_to_tauCharts/src/addons/color-brewer.js"></script>
```
and for define color should use
```javascript
var spec = {
  unit:[{
       type: 'ELEMENT.POINT',
       x: 'month',
       y: 'count',
       color: 'team'
       guide:{
            color:{
                brewer:tauBrewer('YlGnBu',9)
            }
       }
   }]
};
```
if you want use custom bandles you can define following method
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
or if you want have mapping from your domain
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
                                NewTeam:'myColorCssClass1',
                                Alaska:'myColorCssClass2',
                                oldTeam:'myColorCssClass3'
                            }
            }
        }

    }]
};
```

##Size
Size encoding currently applies only point element.
Point diameter depends on the min and max value in a *size* dimension.

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
