# Japan Atlas TopoJSON
An easy way to access Japanese geospatial boundary data at the national, prefectural, and municipal levels. 
The data is taken from the [Geospatial Information Authority of Japan's "Global Map Japan" published in 2016](http://www.gsi.go.jp/kankyochiri/gm_japan_e.html).
## Usage
jpn-atlas is delivered in [TopoJSON](https://github.com/topojson/topojson) file format and made for SVG and Canvas coordinate systems (with the 'y' axis being reversed).
Because of this, it is convenient to use jpn-atlas to load Japanese geospatial data into a browser application without having to download, convert, simplify, and clean the data yourself, jpn-atlas has already done this for you.
The easiest way to get the jpn-atlas data is via [unpkg](https://unpkg.com/jpn-atlas/), but you can also install it via [npm](https://www.npmjs.com/package/jpn-atlas) for yourself.
Either of these methods, among others, will allow you to access the boundary data:

In-browser SVG via [unpkg](https://unpkg.com/jpn-atlas@1.0.0/), displayed using [d3-geo](https://github.com/d3/d3-geo):

```html
<!DOCTYPE html>
<svg width="850" height="680" fill="none" stroke="#000" stroke-linejoin="round" stroke-linecap="round"></svg>
<script src="https://d3js.org/d3.v4.min.js"></script>
<script src="https://unpkg.com/topojson-client@3"></script>
<script>

var svg = d3.select("svg");

var path = d3.geoPath();

d3.json("https://unpkg.com/jpn-atlas@1/japan.json", function(error, japan) {
  if (error) throw error;

  svg.append("path")
      .attr("stroke", "#aaa")
      .attr("stroke-width", 0.5)
      .attr("d", path(topojson.mesh(japan, japan.objects.municipalities, function(a, b) { return a !== b && (a.id / 1000 | 0) === (b.id / 1000 | 0); })));

  svg.append("path")
      .attr("stroke-width", 0.5)
      .attr("d", path(topojson.mesh(japan, japan.objects.prefectures, function(a, b) { return a !== b; })));

  svg.append("path")
      .attr("stroke-width", 0.5)
      .attr("d", path(topojson.feature(japan, japan.objects.country)));
});

</script>
```

In-browser Canvas via [unpkg](https://unpkg.com/jpn-atlas@1.0.0/), displayed using [d3-geo](https://github.com/d3/d3-geo):

```html
<!DOCTYPE html>
nvas width="850" height="680"></canvas>
<script src="https://d3js.org/d3.v4.min.js"></script>
<script src="https://unpkg.com/topojson-client@3"></script>
<script>

var context = d3.select("canvas").node().getContext("2d"),
    path = d3.geoPath().context(context);

d3.json("https://unpkg.com/jpn-atlas@1/japan/japan.json", function(error, japan) {
  if (error) throw error;

  context.beginPath();
  path(topojson.mesh(japan));
  context.stroke();
});

</script>
```

## File Reference

<a href="#japan/japan.json" name="japan.json">#</a> <b>japan.json</b> [<>](https://unpkg.com/jpn-atlas@1/japan/japan.json "Source")
