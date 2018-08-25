Let's create a stacked area chart to compare how *effort* change over *date* across *teams*.

``` javascript
new Taucharts.Chart({
    type: 'stacked-area',
    x: 'date',
    y: 'effort',
    color: 'team',
    data: [
        {team: 'Alpha', date: '2015-07-15', effort: 400},
        {team: 'Beta',  date: '2015-07-15', effort: 100},
        {team: 'Gamma', date: '2015-07-15', effort: 300},
        {team: 'Alpha', date: '2015-07-16', effort: 200},
        {team: 'Beta',  date: '2015-07-16', effort: 200},
        {team: 'Gamma', date: '2015-07-16', effort: 100},
        ...
    ]
}).renderTo('#target');
```
[Example](https://jsfiddle.net/taucharts/mymLjpyj/363/)

#### guide.showAnchors
Defines when to show anchors:
* `hover` (default) - anchor will appear when user points a cursor over it.
* `always` - anchors will always be visible.
* `never` - anchors will not be displayed.

```javascript
new Taucharts.Chart({
  ...
  guide: {
    showAnchors: 'always'
  }
})
```

#### guide.interpolate
Areas can be represented with polygons, smooth curves or steps:
* `linear` - default polyline.
* `smooth` - smooth curve, suits for interpolating math data.
* `smooth-keep-extremum` - curve which doesn't exceed point values, suites for business data.
* `step`, `step-before`, `step-after` - connects points using steps.

```javascript
new Taucharts.Chart({
  ...
  guide: {
    interpolate: 'smooth-keep-extremum'
  }
})
```

[Example](https://jsfiddle.net/taucharts/mymLjpyj/364/)