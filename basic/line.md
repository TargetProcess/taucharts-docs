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
var chart = new tauCharts.Chart({
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

[example jsFiddle](http://jsfiddle.net/taucharts/4o4z6fqn/)

Let's consider more complex example of line chart.

Minard's ["Figurative map of the successive losses of men in the French army during the Russian campaign, 1812-1813"](https://en.wikipedia.org/wiki/Charles_Joseph_Minard) is now one of the most famous statistical graphics, thanks to Tufte. Example below demonstrates how to build it using Taucharts:

```javascript
new tauCharts.Chart({
  type: 'line',
  x: 'longitude',
  y: 'latitude',
  text: 'place',
  size: 'survivors', // we use "size" to encode amount of survivors by line width
  split: 'group',
  color: 'direction',
  data: [...]
})
```
[Example](http://jsfiddle.net/0bu5oo8b/)

#### split
By default data chunks for a line chart are split by color parameter. Taucharts gives the **split** parameter as an additional way to split data for lines. It is useful when you need to draw separate lines per *property A* and colorize them (optionally) by another *property B*.

Here is an example:

[Example](http://jsfiddle.net/oqyu0j2n/)