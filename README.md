```
 _     _  _______  _______    __   __  _______  _______    __   __  _______  ___   _  _______  ______   
| | _ | ||       ||  _    |  |  |_|  ||   _   ||       |  |  |_|  ||   _   ||   | | ||       ||    _ |  
| || || ||    ___|| |_|   |  |       ||  |_|  ||    _  |  |       ||  |_|  ||   |_| ||    ___||   | ||  
|       ||   |___ |       |  |       ||       ||   |_| |  |       ||       ||      _||   |___ |   |_||_
|       ||    ___||  _   |   |       ||       ||    ___|  |       ||       ||     |_ |    ___||    __  |
|   _   ||   |___ | |_|   |  | ||_|| ||   _   ||   |      | ||_|| ||   _   ||    _  ||   |___ |   |  | |
|__| |__||_______||_______|  |_|   |_||__| |__||___|      |_|   |_||__| |__||___| |_||_______||___|  |_|
```

We make a lot of maps at the Los Angeles Times. So we made this tool to help us make them faster. It uses Tangram, which was developed by Mapzen. They shut down in early 2018, but tiles are now hosted by [Nextzen](https://www.nextzen.org/). The map uses Natural Earth and OpenStreetMap data to export an image or a vector file.

![#NICAR18](https://user-images.githubusercontent.com/695934/37242701-9ad8c81e-2433-11e8-9ad4-ad2d7646c02f.png)

We need help making this tool better. If you find bugs, [submit an issue](https://github.com/datadesk/web-map-maker/issues). If you can improve our code, please send us a pull request.

## Live preview

[See that here.](http://datadesk.github.io/web-map-maker/)

## Getting started

You don't need much to get up and running. Clone this repo and make a config.js file (we provided a template [here](https://github.com/datadesk/web-map-maker/tree/master/js/config.js-TEMPLATE)). You'll also need to create a config.yaml file and leave it in the main directory.

A Bing API key isn't necessary to use the map maker; only for geocoding and location search. If you don't have a Bing key you can use coordinates in the location search box.

The gutter and columnWidth are the pixel equivelants for the Times' print 6-column layout.

You'll need a (for now) free [Nextzen key](https://developers.nextzen.org/). That key needs to be placed both in the config.js file and the config.yaml file.

Your config.js file should look like this:
```js
var configOptions = {
    'bingAPI': 'Your API here',
    'attribution': 'Your Org name, ',
    'initCoords': [34.0425, -118.24],
    'initZoom': 14,
    'mapzen-api': 'nextzenKEYHERE',
    'columnWidth': 110.45,
    'gutterWidth': 12,
    'styleFile': 'map-styles.yaml'
}
var sizeOptions = {
    'web_large': [1310, 730],
    'web_small': [410, 450],
    'video': [1930, 1080],
    '1-column': [340, 700],
    '2-column': [706, 700],
    '3-column': [1072, 700],
    '4-column': [1438, 700],
    'twitter': [810, 400]
}
```

Your config.yaml file should look like this:
```yaml
global:
    # Sign up for a Mapzen API key to enjoy higher rate limits
    # https://mapzen.com/documentation/overview/#developer-accounts-and-api-keys
    sdk_mapzen_api_key: 'nextzenKEYHERE'
    description: 'This tool uses Microsoft’s geocoder to approximate an address’s location. It also uses data provided by OpenStreetMap (which you can <a href="http://www.openstreetmap.org/" target="_blank">edit here</a>) and Nextzen. Some supervisor, congressional and other GeoJSON boundaries can be found at <a href="http://boundaries.latimes.com/" target="_blank">boundaries.latimes.com</a>. You can draw your own file at <a href="http://geojson.io/" target="_blank">geojson.io</a>. Questions? Contact <a href="mailto:jon@latimes.com">jon@latimes.com</a> or <a href="https://github.com/datadesk/web-map-maker/issues" target="_blank">submit a bug</a> in GitHub.'
```

Then you're ready to run the mapmaker. The easiest way is to fire up a simple python server (obviously you'll need python) with this command:

```sh
python -m SimpleHTTPServer 8000
```

The app will be hosted at `localhost:8000`.

### Final steps on how to configure the look and feel of the map tiles for your own organization

These instructions help you make this map-builder work for your organization while still incorporating updates to the codebase.

1. Copy the [map-styles.yaml](map-styles.yaml) to a new file.
    1. Whatever you name the new file, update your config.js so `'styleFile': 'map-styles.yaml'` points to your new file's name.
1. If you want a different font for the labels on the map, copy [styles/styles-custom-EXAMPLE.css](styles/styles-custom-EXAMPLE.css) to a file named `styles/styles-custom.css` and edit it from there. You may have to add or find the path to your own web font.

## Vector files for print
Because we make maps for web and print, if you select a column size from the drop-down you'll get a map with the column-equivelant for our six-column layout. The vector paths exported from "download vector" can then be converted to CMYK.

You can then run the `vector-map-restyle.jsx` script in Adobe Illustrator to convert all the layers to values of CMYK. Watch a [tutorial here](http://latimes-graphics-media.s3.amazonaws.com/assets/video/map-maker-script-explainer.mp4).

## What you need to know

Because we've developed this as an internal tool for use at the Los Angeles Times, it's  geared toward our use as far as styles and workflow. But it should be customizable and we're open to suggestions that would help make it better for others to use, too.

Chrome and Firefox are supported.

## Make this better

Have any ideas? File an issue, fork this repo, send us a pull request or contact jon@latimes.com with thoughts, concerns or questions.
