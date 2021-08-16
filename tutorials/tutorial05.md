---
layout: page
title: Tutorial 5A
order: 8
---

# Mapping Remotely - A 

## Multispectral satellite imagery 

This portion of the tutorial will introduce you to multispectral satellite imagery, and to the process of visualizing phenomena through 'false color composites'. As an introduction we will create false color composites using Landsat satellite imagery of Puerto Rico captured just before and after [Hurricane Maria](https://en.wikipedia.org/wiki/Hurricane_Maria) (on September 17 2017 and October 3 2017).

After completing this exercise you will:
* have familiarity with basic characteristics of multispectral satellite imagery
* learned how to acquire Landsat satellite imagery through the U.S. Geological Survey
* created a false color composite from multispectral Landsat dataset

## Some Background on Working with Landsat Satellite Imagery

**Multispectral** satellite imagery refers to a type of data that records specific wavelength ranges in the electromagnetic spectrum. In the case of the Landsat program, the Landsat Satellite has sensors that are able to detect light waves beyond the [visible light spectrum](https://en.wikipedia.org/wiki/Visible_spectrum) (both near infrared as well as ultra violet frequencies). Specific frequency ranges are each recorded in a distinct **band**.

A single Landsat 'image' is actually composed of multiple bands. Each band is an individual **raster** dataset where the value of each pixel corresponds to the wavelength of reflected light captured by the satellite. These datasets are stored as individual `.tif` files which appear as monochromatic images when we load them in QGIS individually.

For example the image below shows band 5 from a Landsat 8 satellite image captured of the western portion of Puerto Rico on October 3, 2017:
![satellite12a]

This image shows wavelengths along the electromagnetic spectrum as well as the ranges that are captured by each Landsat band.  
![spectrum]

The field of remote sensing science is dedicated, in part, to understanding the different 'spectral signatures' of features on the earth's surface. In other words, what frequencies of light in the electromagnetic spectrum do various types of vegetation reflect? Do certain types of man-made surfaces reflect more ultra violet light? Does healthy vegetation reflect greater or less light in the near infrared range than vegetation in drought conditions?

From the answers to these questions researchers study topics like landscape change, [ecological vulnerability](https://landsat.visibleearth.nasa.gov/view.php?id=88873), and large scale [urban development](https://www.wired.com/2012/07/landsat-city-change/).

One of the ways that remote sensing scientists study these 'spectral signatures' is through creating color composite images using multiple of the monochromatic bands from multispectral imagery. This is a method by which each band is assigned a color (red, green, or blue) and its values are mapped onto an RGB color scale. We can make color composites that approximate a 'natural color' image of the earth's surface. Or we can combine different frequency ranges from the electro magnetic spectrum into **false color composites** to reveal different phenomena on the ground.
Below shows natural color and 'near infrared' false color composite images:
![compare]

[This introduction](https://appliedsciences.nasa.gov/join-mission/training/english/arset-fundamentals-remote-sensing) to remote sensing from NASA provides a good entry point to further information on many of these concepts.

Students in this course might be interested in using Landsat satellite imagery as a base map for other analysis, or as an illustration of change over time in a particular area. 

The Landsat satellite circles the globe on a 16 day cycle. [This page](https://landsat.usgs.gov/landsat_acq) from the USGS is helpful for identifying the days of coverage for a particular area. From it we can see that the western portion of Puerto Rico is falls between two paths of the landsat's orbit: the western portion of the island is captured on Day 1 of the cycle, and the easter portion is captured on the 10th day of the cycle.

For a history of the Landsat Satellite program please see NASA's website [here](https://landsat.gsfc.nasa.gov/about/history/)

This exercise will walk through how to create false color composites using multiple landsat bands IN QGIS and also how to download Landsat data from USGS. 

### Downloading Landsat satellite images

Landsat satellite data is freely available and can be downloaded via a number of different websites. We will be using the USGS website: [EarthExplorer](https://earthexplorer.usgs.gov/)

These are instructions for how to download Landsat satellite imagery via USGS for future reference, and for use in the assignment. For this tutorial landsat scenes were already provided to you, so scroll down to the next section.  

1. Select `Register` and then follow steps to **Register for an EarthExplorer account**
2. Use the map to zoom in to your area of interest 
3. In the `Coordinates` box select the `Use Map` button. Coordinates around the area you are viewing will populate into this menu.
![coordinates]
4. Select the date range you are interested 
5. Click through to `Data Sets`
6. In the `Data Sets` menu open the nested section for `Landsat` and then for `Landsat Collection 1 Level-1`
7. Check the box next to `Landsat 8 OLI/TIRS c1 Level-1`
![datasets]
8. Select `Additional Criteria` we will not make any selections here in this exercise, but note for future reference that you can use this to search only for images with less than a certain percentage of cloud cover.
9. Select `Results`. You should see a number of images for specified dates and paths. Here you can view the footprint of each image. As well as select images for download.

10. Find the images you are interested in downloading.
  
11. Click on the download icon (looks like a hard drive and a green arrow) for the first image.
12. In the Download Options menu that will open, select `Level -1 GeoTIFF Data Product`. This is the data set that will include all of the Landsat 8 multispectral bands discussed previously.

![download]

13. a zip files will download, unzip it, and save in the working directory you are using for your project.

## Creating False Color Composites

We will use a tool called the "Semi-Automatic Classification Plugin" (SCP) to assist us with creating composite images from the bands of the Landsat images we just downloaded. This plugin has been developed by Luca Congedo and is released under the "Creative Commons Attribution-ShareAlike 4.0 International License." It is an example of the kind of open source tools being developed by the QGIS community.

Full documentation as well as related resources for this set of tools can be found [here](https://fromgistors.blogspot.com/p/semi-automatic-classification-plugin.html).

The SCP plugin provides a number of tools related to satellite image processing and analysis.

### Install the Semi-Automatic Classification Plugin

Navigate to the `Plugins>Manage and Install Plugins` from your menu bar.

Search for and install the `Semi-Automatic Classification Plugin`

When the plugin has finished installing make sure the check box next to the plugin's name is checked and select `Close`.
![install]

A new toolbar and dock should have been added to your QGIS window. The are highlighted below in magenta. If these did not open for you, right click anywhere inside one of the grey toolbars surrounding the map canvas and select `SCP Dock` in the panels section, and `SCP Tools` and `SCP toolbar` in the toolbars section.  

![dock]

### Load Landsat data and create a "Band Set" 

Open the Semi Automatic Classification Plugin menu by clicking the icon circled in yellow above. 
![Preprocessing]

Click on the `Open a file` button (circled above) and navigate to the directory containing the Landsat bands you want to work with for this example it is `Shared_data`>`raster`>`landsat`. And then first choose the folder containing the October 3 Landsat image bundle `LC08_L1TP_005047_20171003_20171014_01_T1`).

Select bands 2-7 in the folder (all of the files with a .tif ending) And click Open.  

You should just have bands 2, 3, 4, 5, 6, 7 in this list. Make sure you have no other bands.

Select `Landsat 8` for the Quick Wavelength settings. This automatically loads in information about the wavelengths of electromagnetic spectrum captured by each landsat band.

Your dialog box options should look like this:

![Bandlist]

Close the SCP menu. 

Then locate the `RGB` option in the SCP Working toolbar. 
![RGB]

This tool tells the program which band it should map to the red, green, or blue band of a standard RBG image. Setting band 3 and Red, band 2, as Blue, and band 1 as Green will show a `natural color` image whose colors are similar to what we are familiar with. This combination is similar to what we see with the naked eye because it uses the bands that capture electromagnetic wavelengths in the visible light spectrum.

Note: to make the image appear more saturated zoom in to a bright-ish area of the image and then click the `Local cumulative cut stretch` button (circled in yellow above)

Further information about band combinations and the kinds of phenomena they make visible can be found [here](/methods-in-spatial-research-sp2021/tutorials/assets/resources/LandsatBandInformation_Berkeley.pdf). Take a look through this document and try out combinations that are interesting to you.

A color composite using `3-2-1` for a 'natural color' image:  

![natural]

The combination of bands `4-5-3` is particularly well suited for looking at land/water boundaries as well as levels of water saturation.

![435]

Or to view a 'near infrared' image set the RGB band values to `4-3-2`. This type of 'false color composite' image is similar to infrared aerial photography and highlights vegetation in shades of red. Try these and others.

![infrared]

### Export false color composites 
To export a false color composite as a GeoTiff image (that freezes the given false color composite you've chosen) right click on the `virtual band set` in the layers menu. Select `save as` and choose `rendered image` as your output mode, and select a location and file name to save the image. This false color composite is now saved, you no longer have access to the raw data of each of the Landsat bands that originally comprised it but you can work with it as a base map or for other uses or bring it into a different program.

If you'd like you can repeat the steps above on the second Landsat image bundle we downloaded to compare false color composites before and after Hurricane Maria to see the visible flooding.

### Take it further: supervised classification

Beyond false color composites researchers use the spectral signatures for different features of the earths surface to classify land use and land cover and a variety of other phenomena. The [USGS for example](https://www.usgs.gov/core-science-systems/science-analytics-and-synthesis/gap/science/land-cover) produces and maintains data on land use and land cover which it creates using Landsat and other remotely sensed data.  

You can create your specific land use classifications using something called supervised classification. This is beyond the required scope of this assignment but if you are interested in going further please follow the instructions for using the SCP for creating your own land use classification contained in this external tutorial produced by the Applied Remote Sensing Training Program at NASA[here](https://appliedsciences.nasa.gov/join-mission/training/english/arset-land-cover-classification-satellite-imagery)

## Tutorial Deliverable

Upload a screenshot of your false color composite to Canvas.
---
Tutorial by Dare Brawley, Spring 2021


[satellite12a]: /methods-in-spatial-research-sp2021/tutorials/assets/tutorial05/satellite12.png
[spectrum]: /methods-in-spatial-research-sp2021/tutorials/assets/tutorial05/Landsat8_SpectralBands.jpg
[compare]: /methods-in-spatial-research-sp2021/tutorials/assets/tutorial05/satellite13.png
[coordinates]: /methods-in-spatial-research-sp2021/tutorials/assets/tutorial05/satellite001.png
[datasets]: /methods-in-spatial-research-sp2021/tutorials/assets/tutorial05/satellite002.png
[install]: /methods-in-spatial-research-sp2021/tutorials/assets/tutorial05/Satellite01.png
[dock]: /methods-in-spatial-research-sp2021/tutorials/assets/tutorial05/satellite02.png
[Preprocessing]: /methods-in-spatial-research-sp2021/tutorials/assets/tutorial05/satellite04.png
[Bandlist]: /methods-in-spatial-research-sp2021/tutorials/assets/tutorial05/satellite06.png


[RGB]: /methods-in-spatial-research-sp2021/tutorials/assets/tutorial05/satellite05.png
[natural]: /methods-in-spatial-research-sp2021/tutorials/assets/tutorial05/satellite09.png
[435]: /methods-in-spatial-research-sp2021/tutorials/assets/tutorial05/satellite14.png
[infrared]: /methods-in-spatial-research-sp2021/tutorials/assets/tutorial05/satellite10.png
[download]: /methods-in-spatial-research-sp2021/tutorials/assets/tutorial05/satellite003.png