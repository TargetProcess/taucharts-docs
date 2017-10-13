# Creating a plugin

A plugin is a function, which returns an object, that can handle chart events, place content into chart panels or execute chart methods.
``` javascript
(function () {
  function ExtraPlugin(settings) {
    return {
        init: function (chart) {},
        destroy: function () {},
        onSpecReady: function () {},
        onRender: function () {}
        ...
    }
  };
  tauCharts.api.plugins.add('extra', ExtraPlugin);
})();

var chart = new tauCharts.Chart({
    ...
    plugins: [
        tauCharts.api.plugins.get('extra')({...})
    ]
});
```

## Examples

- Plugin, which puts custom control into chart's panel and executes chart's methods:
[Example](https://jsfiddle.net/6mdLrj6o/27/)

- Plugin, which draws points over existing chart using filtered data
[Example](https://jsfiddle.net/wyohpa4a/)
