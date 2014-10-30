#Elements
Elements can be used for creating composite chart, you can use small elements [point](#point), [line](#line), [interval](#interval) and draw them on a single plot.

For example:

```javascript
var data = [
        {x:1, y:1, name:'firstLine'},
        {x:5, y:19, name: 'secondLine'},
        {x:14, y:3, name:'firstLine'},
        {x:6, y:1, name: 'secondLine'},
    ];
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
            },{
                type:'ELEMENT.POINT',
                x:'x',
                y:'y',
                color:'x'
            }]
        }
    };

    var s = new tauChart.Plot(
            {
                data: data,
                spec: lineElement
            }).renderTo('#line-element');
```
[jsBin](http://jsbin.com/hogoci/20/embed?,output)
##Point
Point element draws a point. It has the following parameters:

```javascript
   var line = {
        'ELEMENT.POINT':{
                x:'dimensionX', //x axis
                y:'dimensionY' //y axis
                size:'dimensionSize' //point diameter
                color:'dimensionForGrouping' //point color
        }
   }
```
Point diameter can be set via  [encoding](../advanced/encoding.md#size).

Point color can be set via  [encoding](../advanced/encoding.md#custom-colors-for-encoding-color-value#custom-colors-for-encoding-color-value).

##Line
Line element draws a line, obviously:

```javascript
   var line = {
        'ELEMENT.LINE':{
                x:'dimensionX',
                y:'dimensionY'
                color:'dimensionForGrouping'
        }
   }
```

*Color* property groups data into several lines of different colors. For example, if you have data like:

```javascript
  var data = [
          {x:1, y:1, name:'firstLine'},
          {x:5, y:19, name: 'secondLine'},
          {x:14, y:3, name:'firstLine'},
          {x:6, y:1, name: 'secondLine'},
      ];
```
and you create a chart with parameters:

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
the result is two lines:

[jsBin](http://jsbin.com/hogoci/19/embed?output)

##Interval

Draws a bar.

```javascript
var intervalElement = {
    unit: {
        type: 'COORDS.RECT',
        x: 'date',
        y: 'count',
        guide: {
            showGridLines: 'xy',
            padding: {
                l: 56,
                b: 46,
                r: 8,
                t: 8
            },
            y: {
                padding: 8,
                label: 'Count of completed entities'
            }
        },
        unit: [{
            type: 'ELEMENT.INTERVAL'
        }]
    }
};

var bar = new tauChart.Plot({
    data: defData,
    spec: intervalElement
}).renderTo('#interval-element');
```
[jsBin](http://jsbin.com/hogoci/31/embed?output)

*Color* property groups data into several bars of different colors. For example, if you have data like:
```javascript
    ar data = [{
        "team": "d",
        "cycleTime": 2,
        "effort": 2,
        "count": 15,
        "priority": "low"
    }, {
        "team": "d",
        "cycleTime": 3,
        "effort": 3,
        "count": 9,
        "priority": "medium"
    }, {
        "team": "d",
        "cycleTime": 3,
        "effort": 3,
        "count": 1,
        "priority": "medium"
    }, {
        "team": "d",
        "cycleTime": 4,
        "effort": 4,
        "count": 3,
        "priority": "high"
    }, {
        "team": "l",
        "cycleTime": 3,
        "effort": 2,
        "count": 5,
        "priority": "low"
    }, {
        "team": "l",
        "cycleTime": 4,
        "effort": 3,
        "count": 3,
        "priority": "medium"
    }, {
        "team": "l",
        "cycleTime": 5,
        "effort": 4,
        "count": 4,
        "priority": "high"
    }, {
        "team": "k",
        "cycleTime": 3,
        "effort": 5,
        "count": 5,
        "priority": "low"
    }, {
        "team": "k",
        "cycleTime": 4,
        "effort": 6,
        "count": 8,
        "priority": "medium"
    }, {
        "team": "k",
        "cycleTime": 5,
        "effort": 8,
        "count": 4,
        "priority": "high"
    }];
```
and you create a chart with parameters:
```javascript
var intervalElement = {
    unit: {
        type: 'COORDS.RECT',
        x: 'team',
        y: 'count',
        guide: {
            showGridLines: 'xy',
            padding: {
                l: 56,
                b: 46,
                r: 8,
                t: 8
            },
            y: {
                padding: 8,
                label: 'Count of completed entities'
            }
        },
        unit: [{
            type: 'ELEMENT.INTERVAL',
            color: 'priority'
        }]
    }
};

var bar = new tauChart.Plot({
    data: data,
    spec: intervalElement
}).renderTo('#interval-element');
```
[jsBin](http://jsbin.com/hogoci/43/embed?output)
if you wont create horizontal interval you should set flip property to true
```javascript
var intervalElement = {
    unit: {
        type: 'COORDS.RECT',
        x: 'count',
        y: 'team',
        guide: {
            showGridLines: 'xy',
            padding: {
                l: 56,
                b: 46,
                r: 8,
                t: 8
            },
            y: {
                padding: 8,
                label: 'Count of completed entities'
            }
        },
        unit: [{
            type: 'ELEMENT.INTERVAL',
            color:'priority',
            flip:true
        }]
    }
};

var bar = new tauChart.Plot({
    data: data,
    spec: intervalElement
}).renderTo('#interval-element');
```
[jsBin](http://jsbin.com/hogoci/44/embed?output)