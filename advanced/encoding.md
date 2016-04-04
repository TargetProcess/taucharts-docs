##Custom colors for encoding color value

The Taucharts color scale behaves differently for a measure and nominal variables.

### Color gradient
A brewer for measure variable is defined using array of color codes. These colors define a continues color gradient.

[Color Gradient Example](https://jsfiddle.net/ojb039vr/2/)


### Nominal color scale
A brewer for nominal variable can be defined in several ways using color codes or CSS classes and handled as a discrete set of colors.

There are 2 ways to define color brewer for nominal color scale:
* array
* object

#### Array

If you want to use custom colors - enumerate classes / codes in an array.

```javascript
var chart = new tauCharts.Chart({
    type: 'bar',
    x: 'month',
    y: 'count',
    color: 'team',
    guide:{
        color:{
            // using CSS classes
            brewer:['myColorCssClass1', 'myColorCssClass2', 'myColorCssClass3']
            // using color codes
            brewer:['#0000FF', 'rgb(0, 255, 0)', '#0000FF']
            // choose more appropriate way
        }
    }
});
```
NOTE: make sure corresponding classes (like *"myColorCssClass2"*) are defined in CSS files on the page.

#### Object

Sometimes there is a strong need to explicitly link some category to a color.

For example, all points with 'NewTeam' team should be *red*. Use **object** notation to define *color / value* mapping:

```javascript
var chart = new tauCharts.Chart({
    type: 'bar',
    x: 'month',
    y: 'count',
    color: 'team',
    guide:{
        color:{
            // using CSS classes
            brewer:{
                NewTeam:'css-red',
                Alaska:'css-blue',
                oldTeam:'css-black'
            }
            // using color codes
            brewer:{
                NewTeam:'#ff0000',       // red
                Alaska:'rgb(0, 0, 255)', // blue
                oldTeam:'#000'           // black
            }
            // choose more appropriate way
        }
    }
});
```

[Example](https://jsfiddle.net/tcw7rna4/)

#### Custom colors with *Cynthia Brewer*
You can set custom colors to encode color value or use bundles from a nice categorical color scales by [Cynthia Brewer](http://colorbrewer2.org/).
If you want to use color brewer, you should include the following code into your pages:

```HTML
 <link href="path_to_tauCharts/css/colorbrewer.css" rel="stylesheet"/>
 <script src="path_to_tauCharts/src/addons/color-brewer.js"></script>
```
and define color brewer like below
```javascript
{
    ...
    color: 'team',
    guide:{
        color:{
            brewer:tauBrewer('YlGnBu',9)
        }
    }
}
```