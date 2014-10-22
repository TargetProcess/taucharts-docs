Let's create a simple line chart. For example, count of entities that were completed by month.

Here is our datasource:

```javascript
var defData = [{
  type:'us', count:0, date:'12-2013'
},{
  type:'us', count:10, date:'01-2014'
},{
  type:'us', count:15, date:'02-2014'
},
...
{
  type:'bug', count:23, date:'05-2014'
}];
```

Red line shows bugs and blue line shows user stories. Colors coding is defined in *guide* property.

```javascript
var chart = new tauChart.Chart({
    guide: {
        padding: {l: 70, t: 10, b: 70, r: 10},
        showGridLines: 'xy',
        color: {
            brewer: { // set color for every 'type' in datasource
                us: 'color-us',
                bug: 'color-bug'
            }
        },
        y: {
            label: {
                text: 'Count of completed entities',
                padding: 50
            }
        },
        x: {
            label: 'Month'
        }
    },
    data: defData,
    type: 'line',
    x: 'date',
    y: 'count',
    color: 'type' // we have two types in datasource, so there will be two lines on the chart
});

chart.renderTo('#line');

```

Use [guide](guide.md) property for visual settings.

[example jsBin](http://jsbin.com/hogoci/29/embed?output&height=500px)
