Backbone.GoogleChart
====================

Google Charts support for your Backbone app.

## What?
`Backbone.GoogleChart` is basically a `Backbone.View` that wraps the GoogleChart API in a "backbone" style

## Dependencies
- [Backbone.js](http://backbonejs.org/)
- [Google Visualization](https://developers.google.com/chart/)

## What's included?
- CoffeeScript impl of Backbone.GoogleChart under `src/backbone/GoggleChart.coffee`
- CoffeeScript compiled JavaScript under `lib/backbone/GoogleChart.js`

## Usage
load Google API ( place it under the `head` section )
```html
<script src='http://www.google.com/jsapi' type='text/javascript'></script>
```
load `Backbone.GoogleChart`

```html
<script src='/my/path/to/GoogleChart.js' type='text/javascript'></script>
```

initialize new `Backbone.GoogleChart` object
```javascript
// https://developers.google.com/chart/interactive/docs/reference#chartwrapperobject
// default `Backbone.View` options ( such as `id`, `className` etc...) can also be passed
columnChart = new Backbone.GoogleChart({
  chartType: 'ColumnChart',
  dataTable: [['Germany', 'USA', 'Brazil', 'Canada', 'France', 'RU'],
              [700, 300, 400, 500, 600, 800]],
  options: {'title': 'Countries'},
});
```

draw it by adding it to the DOM
```javascript
$('body').append( columnChart.render().el );
```

## Events
to bind to events
```javascript
var chart = new Backbone.GoogleChart({
    chartType: 'ColumnChart',
    dataTable: [['Germany', 'USA', 'Brazil', 'Canada', 'France', 'RU'],
                [700, 300, 400, 500, 600, 800]],
    options: {'title': 'Countries'}
});

chart.on("ready",function(chartObject) {
  alert(""+ chartObject + " is ready");
});

$('body').append( chart.render().el );

chart.on("select",function(chartObject) {
  alert("Someone clicked on column " + chartObject.getSelection()[0].column);
});

chart.on("error",function(chartObject) {
  console.log("Oops!");
});

```

## Formatters
use the built-in generic formatter
```javascript
var myFormatter = function(text) {
  return text + "$"
};

var chart = new Backbone.GoogleChart({
  formatter: { 
    callback: myFormatter,
    columns: [1,3,5]
  },
  chartType: 'ColumnChart',
  dataTable: [['Germany', 'USA', 'Brazil', 'Canada', 'France', 'RU'],
              [700, 300, 400, 500, 600, 800]],
  options: {'title': 'Countries'}
});

$('body').append( chart.render().el );
```

use the `beforeDraw` callback
```javascript
var chart = new Backbone.GoogleChart({
  beforeDraw: function( chart, options) {
    var formatter = new google.visualization.NumberFormat({
      prefix: '$', negativeColor: 'red'
    });
    
    // format column 1,3,5
    formatter.format(options.dataTable,1);  
    formatter.format(options.dataTable,3);
    formatter.format(options.dataTable,5);
  },
  chartType: 'ColumnChart',
  dataTable: [['Germany', 'USA', 'Brazil', 'Canada', 'France', 'RU'],
              [700, 300, 400, 500, 600, 800]],
  options: {'title': 'Countries'}
});

$('body').append( chart.render().el );
```

the hard way
```javascript
google.load('visualization', '1',{ packages: ['corechart'], callback: function() {
  var data = google.visualization.arrayToDataTable([
    ['Task', 'Hours per Day'],
    ['Work',     11],
    ['Eat',      2],
    ['Commute',  2],
    ['Watch TV', 2],
    ['Sleep',    7]
  ]);
  
  var formatter = new google.visualization.NumberFormat(
    {prefix: '$', negativeColor: 'red', negativeParens: true
  });
  
  formatter.format(data,1); // format column 1
  
  var chart = new Backbone.GoogleChart({
    chartType: 'ColumnChart',
    dataTable: data,
    options: {'title': 'Countries'}
  });
  
  $('body').append( chart.render().el );
  
}});

```

