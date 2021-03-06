# landpatch

Code for downloading & visualizing [Landsat 8](http://www.nasa.gov/mission_pages/landsat/main/) raster
images.

## collection

This plays against two different APIs for the same thing: Google does a mirror
of Landsat 8 imagery that you can access with [gsutil](https://developers.google.com/storage/docs/gsutil):

```
gsutil ls -R "gs://earthengine-public/landsat/L8/**" > scenes-all
```

This just lists and dumps all of the URLs, which include IDs.

Then you can download them with `collect-web.js`, which is a nodejs script
that scrapes metadata from nasa.gov and then downloads, resizes, and tweaks
thumbnail images. This process avoids touching the huge raw GeoTIFF images
in favor of thumbnails.

Then `meta.js` generates a big file that just lists all of the available images.
The image filenames are chosen to expose metadata - they include the bounding
box & collection date of each image.

## display

Then, the web interface is simple - a basic equirectangular projection implemented
with 'just Canvas', using [momentjs](http://momentjs.com/) for time parsing.
