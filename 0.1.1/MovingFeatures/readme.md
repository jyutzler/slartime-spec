This directory is an attempt to encode the sample GML in Section 10 of Moving_Features_Encoding_Part_I_XML_Core_0.5.0.doc as [GeoJSON-LD](https://github.com/geojson/geojson-ld/blob/master/time.md). 
It is a straight conversion - I have made no attempt to optimize.
The file(s) should create reasonable results in the [JSON-LD Playground](http://json-ld.org/playground/).

There are a number of caveats:
   * GeoJSON-LD is not a stable specification. It is subject to change without notice.
   * The temporal elements [might not even be in the 1.0 release](https://github.com/geojson/geojson-ld/issues/22) due to some [lingering issues](https://github.com/geojson/geojson-ld/issues/23).
   * If I am reading the spec right, there is no way to specify the enumerations within the file itself - basically the whole `<mf:header>` section.
   * There are timestamps that are not ISO8601 strings (10, 150, 190). Is this deliberate?
   * The CRS has been switched to CRS84 in order to support the GeoJSON requirement for coordinates to be in (LON,LAT) order.
   * Since the feature IDs are not IRIs, the JSON-LD Playground turns them into IRIs. (See [this comment](https://github.com/geojson/geojson-ld/issues/21#issuecomment-48546076)).
   