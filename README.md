Backbone.GoogleChart
====================

Google Charts support for your Backbone app.

## What?
`Backbone.GoogleChart` is basically a `Backbone.View` that wraps the Google Chart API

## Dependencies
- [Backbone.js](http://backbonejs.org/)
- [Google Visualization](https://developers.google.com/chart/)

## What's included?
- CoffeeScript impl of Backbone.GoogleChart under `src/backbone/GoggleChart.coffee`
- CoffeeScript compiled JavaScript under `lib/backbone/GoogleChart.js`

## Usage
load google visualization by adding these lines to your `HTML` ( under the `head` section )
```html
<script src='http://www.google.com/jsapi' type='text/javascript'></script>
<script type='text/javascript'>
  google.load('visualization', '1');
</script>
```
load `Backbone.GoogleChart`

```html
<script src='/my/path/to/GoogleChart.js' type='text/javascript'></script>
```

initialize new `Backbone.GoogleChart` object
```javascript
// https://developers.google.com/chart/interactive/docs/reference#chartwrapperobject
googleChartWrapperOptions = {
  chartType: 'ColumnChart',
  dataTable: [['Germany', 'USA', 'Brazil', 'Canada', 'France', 'RU'],
              [700, 300, 400, 500, 600, 800]],
  options: {'title': 'Countries'},
}

columnChart = new Backbone.GoogleChart({chartOptions: googleChartWrapperOptions});
```

draw it by adding it to the DOM
```javascript
$('body').append( columnChart.render().el );
```

Note that in addition to the default `Backbone.View` options ( such as `id`, `className` etc...) [google.visualization.ChartWrapper](https://developers.google.com/chart/interactive/docs/reference#chartwrapperobject) options should also be passed through `chartOptions` when initializing new charts.