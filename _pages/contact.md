---
permalink: /contact/
title: "Contact"
excerpt: "Contact me"
author_profile: true
---
Contact information is below, including email and various web services.  This is to make it easy for people to find me when they search for things like "stuart geiger email" and get wrong pages on my site.  Here are some other places on the Internet where I reside.

* E-mail: stuart [at] stuartgeiger.com
* Twitter: [staeiou](http://twitter.com/Staeiou)
* Academia.edu: [RStuartGeiger](http://georgetown.academia.edu/RStuartGeiger)
* Flickr: [staeiou](http://www.flickr.com/photos/Staeiou)
* Google Scholar: [author:geiger-r-stuart](http://scholar.google.com/citations?user=0AvWi3wAAAAJ&hl=en)
* LinkedIn: [rstuartgeiger](http://www.linkedin.com/in/rstuartgeiger)
* Wikipedia: [staeiou](http://en.wikipedia.org/wiki/User:Staeiou)
* UC-Berkeley: [Berkeley Institute for Data Science](https://bids.berkeley.edu/people/r-stuart-geiger), [School of Information](http://www.ischool.berkeley.edu/people/students/rstuartgeiger)

![Pandao editor.md](https://pandao.github.io/editor.md/images/logos/editormd-logo-180x180.png "Pandao editor.md")

## 17 Ways to Be a Raster Master
#### The beautiful thing about rasters is that they’re useful for both visualizing and mathematical analysis.

The beautiful thing about rasters is that they’re useful for both visualizing and mathematical analysis. They’re simple, versatile, and the best way to represent data on a continuous, pixel-by-pixel basis.

Here are a bunch of ways you can work with this data type—and I hope the list inspires you to think of even more possibilities. You’ll see how to restructure rasters to get exactly what you need, exerting specific control over cells, bands, palettes, even the way they’re geocoded. You’ll also see many ways to integrate them, resulting in datasets that are much more rich and illustrative. If you hang around long enough, you might even learn how to use math and expression evaluation to impress your friends.

1. Convert between data formats
![This GeoTIFF has been converted from a layered DWG, creating an image of the vector that better meets structural requirements.](http://cdn.safe.com/wp-content/uploads/2014/07/1-GeoTIFF-raster-300x225.png "This GeoTIFF has been converted from a layered DWG, creating an image of the vector that better meets structural requirements.")
This GeoTIFF has been converted from a layered DWG, creating an image of the vector that better meets structural requirements.

There are a lot of raster formats. I don’t want to embarrass myself by guessing how many (I’ve always been terrible at those Jelly Bean Jar guessing games), but I can tell you that FME works with more than 60 of them. The most popular ones in our usage statistics are GeoTIFF/TIFF and ECW.

To get all the benefits of data integration, it’s often worth converting to another raster format, or translating between raster and vector, or combining rasters with point clouds, databases, CAD, GIS, or any other data type. In a world where data is liquid, it’s suicide to keep information locked in a single format.

2. Change the dimensions

![This is a visual representation of a 25x25 DEM that has been downsampled to 10x10.](http://cdn.safe.com/wp-content/uploads/2014/07/2-resample-dem-300x160.png "This is a visual representation of a 25×25 DEM that has been downsampled to 10×10.")
This is a visual representation of a 25×25 DEM that has been downsampled to 10×10.

Resample the image to your desired row/column dimensions, cell size, or percentage of the original size. Resampling is usually done to generate a smaller image, but it can also be used to make a bigger (though lower quality) one.

Unless you’re looking to make pixel art, you’ll want to get essentially the same representation of a picture (for a color image) or value distribution (for a numeric raster) when downsampling. Useful interpolation methods include nearest neighbor (fast), bicubic (best quality), bilinear (a compromise), and average 4 or 16 (good for numeric rasters like DEMs).

3. Change the coordinate system
Lat/long projections might be the most popular in our usage statistics, but different tasks require different coordinate systems.
Lat/long projections might be the most popular in our usage statistics, but different tasks require different coordinate systems.

Like any worthy, respectable spatial data format, rasters can be georeferenced and can come in a variety of coordinate systems.

If you need to project the graphics onto a map or combine it with other data, you can reproject it to another system. For example, KML requires WGS84 (LL84), while tiles in a Web Map Tile Service are likely in Spherical Mercator.

If you want to get really specific, you can even control your raster’s geocoding. For example, some rasters are embedded with Ground Control Points (GCPs) instead of having geocoding on the corners. You can extract or set the GCPs as needed.

4. Combine tiles into one image
Mosaicking means bringing multiple images together. At Safe, this is our most popular raster transformation.
Mosaicking means bringing multiple images together. At Safe, this is our most popular raster transformation.

Mosaic multiple rasters into a single feature. For example, maybe you need to bring tiles together into a simple overview in a lat/long projection. This would involve a mosaic, resample (#2), and reproject (#3) transformation.

It’s like a puzzle! One where the pieces don’t really fit together!

Yes. About that. Reprojecting can rotate an image slightly, and when this is followed by mosaicking, we often end up with empty black areas in between the pieces. An obsessive-compulsive nightmare. Don’t worry. You can fix it by adding a “nodata” value, so the empty areas become transparent and pick up whatever background is underneath.

This image has been compressed by 75% to make it easier to work with while not compromising the overall quality.
This image has been compressed to make it easier to work with while not reducing quality.

5. Compress raster files
Like putting your raster in Spanx, compressing it makes everything slimmer and trimmer. 75% is a pretty good ratio to use if you want a smaller image that’s quicker to process, but still good quality.

Many formats support compression: JPEG/JPEG2000, ECW, GeoTIFF/TIFF, Oracle Spatial GeoRaster, ArcSDE Raster, Geodatabase Raster, CADRG, and WebP, to name ten.

6. Clip to boundaries
Clipping is essentially a combination of rasters and vectors to produce more useful output. For instance, each of these clipped pieces can be stored in a PostGIS database with its associated metadata.
Clipping is essentially a combination of rasters and vectors to produce more useful output. For instance, each of these clipped pieces can be stored in a PostGIS database with its associated metadata.

Clip an image to keep only the pieces you need, and toss away the parts outside of your defined boundary.

For example, you can merge an ECW of California with a polygon defining the coastline, and clip away the ocean (who needs that big blue wet thing anyway?). The result will be an image of just the state.

If you’re clipping many regions, like park boundaries, you can merge the attributes from the vector features so each clipped piece retains all the properties, like the park name. As mentioned in #4, it’s handy to define the empty pieces as “nodata” so they stay transparent, making it easy to view over a background map.

Check out fme.ly/parks to see a sample HTML catalog of images and metadata.
Check out fme.ly/parks to see a sample HTML catalog of images and metadata.

7. Make a catalog of raster graphics and/or metadata
Consolidate graphics and their properties into a useful place, one you can share with your mom to show her all the cool stuff you do at work.

To see what I mean, check out fme.ly/parks. That’s a catalog of a bunch of clipped images and information on each piece.

The catalog reads the raster as a binary blob from a database that doesn’t support imagery, and then uses some simple HTML to make everything look nice.

This GIF has been tiled, resulting in the same output in many pieces. Note the shadows in this image have been exaggerated so the tiles can be distinguished.
This GIF has been tiled, resulting in the same output in pieces. The shadows have been exaggerated to distinguish the tiles.

8. Split a big image into tiles
Split a raster into a series of tiles. Maybe you want images in a particular size, or maybe you want a particular number. Maybe you need smaller pieces for processing. Maybe you need to load your raster in software that doesn’t support highly compressed wavelengths. Maybe you just like your data in really tiny pieces—like data confetti. I don’t blame you. Confetti is fun.

Whatever your situation, you have a giant image and you want it in smaller pieces. Tile it.

The most commonly used web map tiling scheme is the Google and Bing Maps compatible one. Visit MSDN for more info about this tiling scheme.
The most commonly used web map tiling scheme is the Google and Bing Maps compatible one.

9. Create a web map tile service
Create a series of image tiles that can be utilized by web mapping applications such as Google Maps, Bing Maps, or other Web Map Tile Service.

The imagery in a WMTS is stored in tile sets, so as you zoom, you see different tile sets at different resolutions. You can create a WMTS by reprojecting to spherical mercator (#3), resampling to various resolutions (#2), and splitting into tiles (#8).

10. Texture a geometric surface
This 3D model is the result of a multi-step raster transformation: a JPEG draped onto a TIN surface that was generated from a DEM.
This 3D model is the result of a multi-step raster transformation: a JPEG draped onto a TIN surface that was generated from a DEM.

I feel like no raster has fulfilled its destiny until it’s been used to texture a surface. First, rasters are a 2D representation of a 3D world. Second, 3D models are often plain and textureless. Neither is as helpful as it could be. Draping a raster over a 3D model is often an enlightening integration.

Say you have an Esri Shapefile of contours, and a MrSID orthophoto. You can create a DEM by converting the contours to 3D based on elevation. When generated as a TIN and integrated with the orthophoto, you end up with a much more useful 3D model with a textured surface, like Candy Mountain over there on the right.

Draping a point cloud with RGB and DEM rasters also results in some great surface model transformations (one of our most popular LiDAR processing tasks).

11. Attach an image as an attribute of a feature
Esri ArcGIS supports the ability to add attachments in a Geodatabase feature class.
Esri ArcGIS supports the ability to add attachments in a Geodatabase feature class.

A lot of formats, like Geodatabase or Excel, allow for image attachments.

This is great news for interoperability, because you can make a raster out of anything. Photos, scans, statistical data, charts, illustrations, satellite imagery … One time I demoed an enterprise raster reader/writer using a picture of a pony.

Anything that can go in a raster can also go in a format that supports image attachments.

This 32-bit RGBA PNG has been transformed to have an alpha band so it can represent transparency. This type of “feathering” can be useful when mosaicking.
This 32-bit RGBA PNG has been transformed to have an alpha band so it can represent transparency. This type of “feathering” can be useful when mosaicking.

12. Restructure the bands
Ok, now we’re getting into some more powerful stuff. (Puts on sunglasses.)

If you have multi-band data and you need to convert to a format that doesn’t support it—for example, if you have an intense 8-band format but all you want is an RGB overview—you can remove bands you don’t need.

You can also recode or add bands, for instance to recode from RGB into RGB with transparency, or to remove the alpha band so you end up with plain RGB.

In this example, the user has generated a set of vector polygons based on values in a DEM.
In this example, the user has generated a set of vector polygons based on values in a DEM.

13. Vectorize a raster based on values
One way to convert raster to vector is to create a polygon for each contiguous area of pixels with the same value. We call this classifying a raster.

In the vector image on the right, polygons were generated by rounding off the nearest 25 meters in the elevation model before classifying. NURBS were then made from the polygons, resulting in a vectorized contour map.

Either that, or someone put a rainbow in a blender. I’m not sure.

This Canadian Digital Elevation Data has been hill-shaded then overlaid on a background map.
This Canadian Digital Elevation Data has been hill-shaded then overlaid on a background map.

14. Make the bitmap realistic with hill shading
If you work with elevation data, you’re probably familiar with the plain, black and white graphics where high elevations are white and low elevations are black. Sorry, but even 3D glasses can’t make that stuff look 3D. Trust me, I tried.

Hill shading offers a real-world rendering of what the picture actually looks like. This is particularly useful for visualizing terrain when putting together a cartographic product.

15. Colorize point clouds
This pretty point cloud has been colorized with a raster.
This point cloud has been colorized with a raster.

Datasets are like spices, and until you blend them together you don’t experience the full burst of flavor.

Overlay a point cloud on a georeferenced raster to color the points.

Combining rasters and point clouds makes LiDAR visualization much more eye-pleasing. Check out my blog post on 14 Ways to Take Charge of LiDAR Data to see many ways to integrate point clouds. Some of the most useful, beautiful outputs involve rasters.

These red polygons were overlaid based on algebra performed to identify areas of interest.
These red polygons were overlaid based on algebra performed to identify areas of interest.

16. Pixel by pixel expression evaluation
Perform calculations based on the value of one or more cells. For example, you can calculate the slope or aspect (direction of slope) for each cell, or extract the extents, or detect changes between two inputs.

You could also modify pixel values based on an algorithm. Yes, friends, if these pixels store RGB values, then this is just a fancy way of saying “make your own Valencia or X-Pro II”. Free spork to anyone who uses raster expression evaluation to make their own Instagram filter.

In this example, a GeoTIFF and PNG have been combined by copying cell values from the road image over to the background layer.
A GeoTIFF and PNG have been combined by copying cell values from the road image over to the background layer.

17. Layer rasters by copying cells or using semi-transparency
Combine two rasters to see information from both layers. You can do this by taking only certain pixels from one of the images (e.g. the white and yellow roads), or by adding transparency (#12). An alpha band allows you to smoothly blend the images when overlaying them. Kind of like digital iron-on transfer paper.

 

 

To see how to accomplish all of the above tasks with FME, visit safe.com/raster. I recommend you watch this October 2013 webinar recording for great live demos, including impressive scenarios that combine several data sources (including WMS), advanced transformations, and mathematics. We also have a huge collection of articles in our FME Community to help you accomplish your raster needs.

What kind of translations and transformations do you do with raster data? What do you find the most challenging?
