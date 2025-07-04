
# Dart Interops (Read-Only)

This package is a **read-only** collection of Dart interop bindings generated from TypeScript `.d.ts` files using [Dartify](https://github.com/brianmondi/dartify). It is intended as a published output for use in Dart and Flutter projects that require seamless interoperability with JavaScript libraries.

**Note:** This repository does **not** accept contributions. All Dart files in this package are generated automatically by Dartify. To request changes or new interops, please open an issue or contribute to the [Dartify](https://github.com/brianmondi/dartify) tool itself.

## Features

- Provides Dart bindings for JavaScript libraries via auto-generated interop code.
- Enables type-safe access to JavaScript APIs from Dart.
- All code is generated from TypeScript definition files (`.d.ts`).
- No manual edits—ensures consistency with upstream JavaScript libraries.

## Getting started

Add this package as a dependency in your `pubspec.yaml`:

```yaml
dependencies:
  dart_interops:
    git:
      url: https://github.com/bryanbill/dart_interops.git
```

Or use the published version from pub.dev if available.

Import the relevant interop files in your Dart code as needed.

## Usage

```dart
import 'dart:js_interop';

import 'package:dart_interops/openlayers/ol.dart' hide Tile;
import 'package:dart_interops/openlayers/ol/geom/point.dart';
import 'package:dart_interops/openlayers/ol/source/source.dart';


void main() {
  // Create View
  final viewOptions =
      {
            'center': Point([0, 0].jsify() as JSObject).getCoordinates(),
            'zoom': 2,
          }.jsify()
          as JSObject;
  final view = View(viewOptions);

  // Create Tile Layer with OSM Source
  final tileLayerOptions =
      {
            'source': XYZ(
              {
                    // set mt3 google street map
                    'url':
                        'https://mt3.google.com/vt/lyrs=m@221&x={x}&y={y}&z={z}',
                    'attributions': 'Google Maps',
                    'crossOrigin': 'anonymous',
                    'tileSize': 256,
                  }.jsify()
                  as JSObject,
            ),
          }.jsify()
          as JSObject;
  final tileLayer = Tile(tileLayerOptions);

  // Create Map
  final mapOptions =
      {
            'target': 'map',
            'layers': [tileLayer].jsify(),
            'view': view,
          }.jsify()
          as JSObject;
  final map = Map(mapOptions);
}

```

See the `/lib` directory for available interop modules.

## Additional information

- **Read-only:** This package is not intended for direct contribution. All changes must be made via the Dartify tool.
- **Issues:** For bug reports or feature requests, please open an issue in the [Dartify repository](https://github.com/brianmondi/dartify).
- **More info:** See the Dartify documentation for details on generating your own interops.
