TopoJSON
TopoJSON is an extension of GeoJSON that encodes topology. Rather than representing geometries discretely, geometries in TopoJSON files are stitched together from shared line segments called arcs. This technique is similar to Matt Bloch’s MapShaper and the Arc/Info Export format, .e00.

TopoJSON eliminates redundancy, allowing related geometries to be stored efficiently in the same file. For example, the shared boundary between California and Nevada is represented only once, rather than being duplicated for both states. A single TopoJSON file can contain multiple feature collections without duplication, such as states and counties. Or, a TopoJSON file can efficiently represent both polygons (for fill) and boundaries (for stroke) as two feature collections that share the same arc mesh. See How To Infer Topology for a visual explanation of how TopoJSON works.

To further reduce file size, TopoJSON can use quantized delta-encoding for integer coordinates. This is similar to rounding coordinate values (e.g., LilJSON), but with greater efficiency and control over loss of information. And like GeoJSON, TopoJSON files are easily modified in a text editor and amenable to gzip compression.

As a result, TopoJSON is substantially more compact than GeoJSON, frequently offering a reduction of 80% or more even without simplification. Yet encoding topology also has numerous useful applications for maps and visualization above! It allows topology-preserving shape simplification, which ensures that adjacent features remain connected after simplification; this applies even across feature collections, such as simultaneous consistent simplification of state and county boundaries. Topology can also be used for Dorling or hexagonal cartograms, as well as other techniques that need shared boundary information such as automatic map coloring.

Installing
If you use NPM, npm install topojson. Otherwise, download the latest release. You can also load directly from d3js.org as a standalone library. AMD, CommonJS, and vanilla environments are supported. In vanilla, a topojson global is exported:

<script src="https://d3js.org/topojson.v2.min.js"></script>
<script>

var topology = topojson.topology({foo: geojson});

</script>
Try topojson in your browser.

API Reference
Generation (topojson-server)
topojson.topology - convert GeoJSON to TopoJSON.
Simplification (topojson-simplify)
topojson.presimplify - prepare TopoJSON for simplification.
topojson.simplify - simplify geometry by removing coordinates.
topojson.quantile - compute a simplification threshold.
topojson.filter - remove rings from a topology.
topojson.filterAttached - remove detached rings.
topojson.filterWeight - remove small rings.
topojson.planarRingArea - compute the planar area of a ring.
topojson.planarTriangleArea - compute the planar area of a triangle.
topojson.sphericalRingArea - compute the spherical area of a ring.
topojson.sphericalTriangleArea - compute the spherical area of a triangle.
Manipulation (topojson-client)
topojson.feature - convert TopoJSON to GeoJSON.
topojson.merge - merge TopoJSON geometry and convert to GeoJSON polygons.
topojson.mergeArcs - merge TopoJSON geometry to form polygons.
topojson.mesh - mesh TopoJSON geometry and convert to GeoJSON lines.
topojson.meshArcs - mesh TopoJSON geometry to form lines.
topojson.neighbors - compute adjacent features.
topojson.bbox - compute the bounding box of a topology.
topojson.quantize - round coordinates, reducing precision.
topojson.transform - remove delta-encoding and apply a transform.
topojson.untransform - apply delta-encoding and remove a transform.
Command-Line Reference
geo2topo - convert GeoJSON to TopoJSON.
toposimplify - simplify TopoJSON, removing coordinates.
topo2geo - convert TopoJSON to GeoJSON.
topomerge - merge TopoJSON geometry, and optionally filter.
topoquantize - round TopoJSON, reducing precision.
