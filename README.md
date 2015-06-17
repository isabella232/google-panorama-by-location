# google-panorama-by-location

[![experimental](http://badges.github.io/stability-badges/dist/experimental.svg)](http://github.com/badges/stability-badges)

Gets a Google StreetView Panorama by `[ lat, lng ]`. Also features some Node support.

```js
var panorama = require('google-panorama-by-location')

var location = [ 51.50700703827454, -0.12791916931155356 ]
panorama(location, function (err, result) {
  if (err) throw err
  
  // pano ID
  console.log(result.id)

  // actual latitude, longitude
  console.log(result.latitude)
  console.log(result.longitude)

  // other details from Google API
  console.log(result.copyright)
})
```

In Node, the request uses an undocumented API entry-point, using [nets](https://www.npmjs.com/package/nets). It only provides `{ id, latitude, longitude }`. This is mostly useful for unit testing.

## Usage

[![NPM](https://nodei.co/npm/google-panorama-by-location.png)](https://www.npmjs.com/package/google-panorama-by-location)

#### `panorama(opt, cb)`

Gets the panorama data at the given location, where `opt` can be an array of `[ latitude, longitude ]` or an options object with:

- `location` - the `[ lat, lng ]` array
- `radius` - the radius to search, defaults to 50
- `service` - (browser only) the Google API `StreetViewService` to use, defaults to a new instance

The Node-style callback uses the form `(err, result)`, where `err` will be null if a street view was found. On success, `result` is an object containing:

```js
{
  id: String, // pano ID
  latitude: Number,
  longitude: Number
}
```

In the browser, the `result` object will also contain other details from `StreetViewService`, like `copyright`. 

## node

The [node.js](./node.js) entry point uses [nets](https://github.com/maxogden/nets) to request the JSON, so it works in both Node and the Browser. This means you can require it for quick unit testing in the browser, without bringing in the entire Google Client library. 

```js
var panorama = require('google-panorama-by-location/node')

panorama([ lat, lng ], callback)
```

However, this is not recommended for production, since it uses an undocumented API entry point.

## See Also

- [google-panorama-by-id](https://github.com/Jam3/google-panorama-by-id)
- [google-panorama-equirectangular](https://github.com/mattdesl/google-panorama-equirectangular)

## License

MIT, see [LICENSE.md](http://github.com/Jam3/google-panorama-by-location/blob/master/LICENSE.md) for details.
