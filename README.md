# Crown Delineation

This is a repository to collect information, templates, and best practices about delineating tree crowns in remote sensing imagery.<br clear="left"> <img style="float: left; padding: 2px 2px 2px 2px;" width="40%" src=imgs/cover_shot.png>  <img style="float: right; padding: 2px 2px 2px 2px;" width="43%" src=imgs/cover_shot_crowns.png>
<br clear="right">

## Intro
In remote sensing research, important information is extracted from imagery collected above tree canopies. This information is used to create spatial models that can help us understand what is happening on the ground and predict how it might change. Field sampling, data entry, and canopy delineation tasks are the most time consuming, repetitive, skill-oriented, and, yet, still remain to be the most critical part of data collection and processing a remote sensing lab produces.

Your skills are an important part of this lab's ability to produce good science. The canopy is *hard* to define, being efficient is a skill set that is only learned through experience.  Do your best and ask a lot of questions.

The overall goal of this guide is to go over canopy crown tracing. To break it down, we need to know some basics of the sampling and remote sensing. We introduce several concepts in the first part and then have a training exercise in the second.

### Background
Most of the remote sensing studies in this lab starts with leaf and plot sampling in the field (this is often called "ground-truthing"). The next step is to then determine and digitize the precise locations of those leaves and plots in the imagery. This how leaf chemistry,i.e., the thing we measured on the ground, is translated into pixels. Based on the research questions and remote sensing products being used, the canopy is measured in a particular way. There should be a modicum of notes/protocol, plot photos, and digital files available to help, in addition to the imagery itself, which should all be leveraged to ensure the best attempt goes into finding and tracing each canopy. Get to know the project and work toward creating an organized set of spatial files and supporting information that cohesively provides enough background and context to get started.

#### Project Design
Most research in the lab uses remote sensing products. While there far more research designs than what we can cover in this guide, the following demonstrates an example of possible final goals of the research, which informs how the researchers plan to extract the pixel values. This is intended to serve as a simple question or prompt highlighting how project design is incorporated into the digitization of the sample plots.

```Single Crown > Pixel Resolution``` or ```Single Crown < Pixel Resolution``` ? 
1. If the outcome is to use imagery with 1-4m pixels (or less), it is essentially a "CANOPY" design, because the size of an individual tree is big enough and pixels are small enough that the single canopy will cover multiple pixels. This is when tree canopies need to be carefully traced, which is what this guide covers.

2. For imagery with larger pixels, especially ranges of 20-30m from space-borne instruments, sampling becomes more of a "PLOT" design. A single pixel in these products possibly include multiple trees / shrubs, or other landscape features, mixed together. This guide does not cover plots of this size, as it is generally an extraction from a point with less emphasis on how to properly find and delineate a single tree.


#### Registration 
Before discussing imagery, this is a short section to present the concept of image registration early. All remote sensing products are imperfectly collected and it is up to the research team to carefully piece it all together into a tidy stack with as much geometric accuracy as possible.

Any products used for tracing should ideally be co-registered (one image registered to another means shifting one to match the other). The concept of being successfully registered means that when flipping from image to image, a building or a tree is aligned with itself and not shifting slightly across the products. If they are not, it is more critical that the work is done carefully to ensure errors are not inserted. It is fine to use other images that are not perfectly co-registered to develop a better context of the digital canopy, just take care to ensure that this is only used as an aid.

#### Reference Image
Since tree canopies being traced become uniquely geo-registered to that single image in time, it is important to identify a good, clear image early on as the ```reference``` or ```ref``` image (older terminology may refer to this as the master or main image). Other common terms may be ```basemap``` or ```base mosaic```. Regardless of whether products are co-registered together ahead of time, the identity of this image should be highlighted accordingly. The researcher you are working with will help you identify what this reference image will be for the project at hand. Always make sure you are clear on what reference image you are supposed to be using. It is best to ask first if you are unsure.

All tracing and finalizing of point / polygon placement is ultimately completed back on the ```ref``` image. It is absolutely critical that this concept is followed closely.

#### Remote Sensing Data
This is a short list of remote sensing products and field data the lab commonly uses or has available for ```CANOPY``` designs. Work with the researchers on the project to know what is actually available to use.

##### Base Imagery
The base imagery is primarily ```raster``` form when used [See here for a description of raster](https://desktop.arcgis.com/en/arcmap/latest/manage-data/raster-and-images/what-is-raster-data.htm). LiDAR ```point clouds``` are also usually turned into a ```raster``` to be used as surface and height models. See [here](https://oceanservice.noaa.gov/facts/lidar.html) and [here](https://pro.arcgis.com/en/pro-app/latest/help/data/las-dataset/what-is-lidar-.htm) to learn more about LiDAR.

Here are just a few examples of what's most commonly used in the Townsend Lab:
1. Hyperspectral (```raster```)
    1. Sensors -> these would be the main point of the study
        1. NEON (1m)
        2. HySpex (~1m or less)
        3. AVIRIS (~4m)
    2. Useful products can be created for more efficient workflows
        1. Quicklooks - mosaic and/or individual flightlines ```RGB```
        2. 1660nm band mosaic
        3. Multiband custom mosaic (~ 20 selected bands across the wavelength range)
            1. False Color
            2. Veg Indices
2. LiDAR (```LAS / LAZ point clouds``` - cm) -> great ancillary products to help, especially for shadows, gaps, and judging crown edges
    1. Digital Surface Model (```DSM```) for crown shape only
    2. Canopy Height Model (```CHM```) for crown height plus shape
3. Photogrammetry (e.g., structure from motion - cm)
    1. Occasionally a higher resolution mosaic or surface may be available from drone cameras

##### Canopy Points & Polygons
The plots in the field are marked with a GPS unit, which is then later used to manually create an adjusted, additional set of point and polygon (```vector```) layers that more accurately locate each sample area in the ```reference``` remote sensing image(s). See [here](https://docs.qgis.org/2.18/en/docs/gentle_gis_introduction/vector_data.html) to learn more about what vector data is. Collecting good GPS data is not covered in this guide, although having a basic understanding of the principles can offer insight to the reliability of each piece of information you use to build the context and decide on where to trace the canopy.

The final plots being drawn will need to cover the area of the crown that the project research team sampled. The Townsend Lab has some general basic protocol and guidelines used across most projects. Use the section below as a suggested place to start when discussing this with your project's leader. 

###### Basic Protocol
- The main objective is to focus on "pure" canopy pixels --> target high quality pixels that are the ***best*** representation of that species

<img style="float: center; padding: 10px 2px 10px 2px;" width="250" src=imgs/contours_may.png> <img style="float: center; padding: 10px 2px 10px 2px;" width="250" src=imgs/contours_july.png> <img style="float: center; padding: 10px 2px 10px 2px;" width="250" src=imgs/contours_october.png> <br clear="left">
- Canopy Contours
     - Sunny side of the canopy (southern side in Northern Hemisphere)
     - Reduce shaded side / shadow pixels --> In a time series, the ```ref``` image may have canopy shading, while other flights over the same area later in the year may have the entire canopy illuminated, look ahead to judge across all dates
- Canopy Edges
    - Avoid edges where shadows and thinning leaves
    - If the purpose of a project is to scale data (e.g., turn small pixels into big ones), be aware the canopy polygon may include the edges as fewer pixels define the crown. 
    - Be aware of spectral pollution from adjacent bright, dark, or mixed areas. Sometimes these are referred to as adjacency effects.
- Canopy Closure
    - When trees merge, do your best to find the correct tree in earlier / later season imagery before / after the canopy is at peak biomass.
 
<img style="float: center; padding: 10px 2px 10px 2px;" width="250" src=imgs/shading_may.png> <img style="float: center; padding: 10px 2px 10px 2px;" width="250" src=imgs/shading_july.png> <img style="float: center; padding: 10px 2px 10px 2px;" width="250" src=imgs/shading_october.png> <br clear="left">
 
###### Basic Tracing Guidelines
 - EXPECTATIONS
     - Triple-check everything.
     - Take good notes during each session to characterize decisions you made or questions you may have.
     - Use screenshots in a powerpoint to easily and quickly communicate questions or clarifications.
         - Researchers are usually supportive of frequent "Does this look right?" check-ins, especially using an easy visual approach.
     - Go SLOW and build a context for each polygon to clearly understand the digital record of the individual plot you are creating. DO NOT race through and trace haphazardly with little use of extra information beyond the ```ref``` image. A single plot may have cost the lab multiple thousands of dollars to sample. Please take great care to correctly and carefully dedicate equal attention to each plot with patience and a sense of investigation. 
     - The CRS of layers and map documents must match and make sense every step of the way. Avoid letting QGIS or ArcMap reproject on-the-fly to display layers. This often means creating multiple versions of a layer in different CRS to be able to confidently control layer creation.
     - Version polygon / point files at routine intervals during the working process (one per session, one per week, etc) to have an easy way to roll back if errors are discovered.
     - Use temp directories to keep a tidy workspace.
 - FILE NAMES
     - ALWAYS AVOID SPACES IN FILE and DIRECTORY NAMES
     - Use an approved naming convention that is agreed upon ahead of time with the project's leader.
     - Add an underscore with your initials to "own" the files so questions can quickly be routed to the correct person
     - Use underscores, hyphens, and upper and lower case intentionally, consistently, and according to the project leader's preferences. Additionally, names can also have a structure of overview down to details from left to right. For example, using underscores to separate the "sections," and hyphens or ```camelCase``` within the sections, can help break apart names for readability in a way that also helps sorting or programmatically working them in processing scripts. 
         - BIG-PROJECT_sampledate_sample-site_PlotID_details_version
 - DATES
     - All dates should have a consistently followed convention for a project (YYYYMMDD --> 20200531)
 - FORMATS
     - ```GEOJSON``` are acceptable when polygon areas and counts are low, these can be great for versioning and quickly sharing since they are a single file readable in a text editor.
     - ```SHP``` files are preferable for more complex layers covering large areas with thousands of polygons - but because of the extra required ancillary (```shx```, ```dbf```, ```prj``` ) files these can also be a little more problematic to work with when first getting started creating / sharing GIS layers.
 - ATTRIBUTES
     -  ```PlotID``` - bare minimum... there needs to be a way to link the polygon to the ```plot``` or ```sample```
     -  ```TreeTag```  - if there is one, it should likely be included from the beginning
     -  ```UUID``` - if a project is using a database, a unique identifier like this may replace the ```PlotID``` and ```TreeTag``` info 


##### GPS Units
The precision of the GPS units used in a project can range from many meters to a couple centimeters. Here are the basic units the lab uses:

```GARMIN```  These smaller units (along with other brand of handheld units) are easier to pack and carry, but the 2-5m error in all three (X,Y,Z) directions means the final points aren't precise enough for canopy delineation and often serve only as a quick way to keep a digital record of the location. There are ways to enhance this in the field if the crew used ```averaging``` setting, but it is generally still not reliable enough for canopies.

```TRIMBLE``` The Geo7x is the current lab model that can be post-processed with accuracies approaching 2cm. It is a single handheld unit (```BASE```) that has an external antenna that is precisely 2m tall. Field conditions can affect the accuracy. Wide open areas can be expected to retain the best (<5cm), while proximal to or beneath a canopy can degrade quickly to 1-2m (or even worse). This accuracy is still close enough to be able to determine a tree stem location to correctly identify the crown. *This is the most trustworthy data to use without a lot of legwork to determine its reliability.*

```EMLID``` Similar to the Trimble, these units can be post-processed to similar precisions of a few centimeters in the open and a couple meters under the canopy. They require two units, a ```BASE``` and ```ROVER```, in order to offer those accuracies, which can make them more cumbersome to deal with. As well, another complicating factor is that the ```BASE``` unit may need 3+ hours to gain an accurate enough fix to be able to correct the ```ROVER```. Therefore, data collected with these units should be carefully scrutinized if they are to be used as high-precision locations. 


Other points to note:

- What CRS was the unit set to while recording locations in the field (this matters!)? They are often set by default to used decimal degrees (lat / long). Ideally they are using the local UTM to the area the unit is collecting. Not much can be done afterwards, just good info to think about.


#### CRS
 It is critical to understand from the very beginning how to handle the coordinate reference system (CRS) for the geospatial files. NEON and ABoVe cover multiple UTM zones, so this can be challenging to ensure you are tracing in the most accurate CRS for that image in the particular region it was imaged. If you are interested, see [here](https://docs.qgis.org/3.28/en/docs/gentle_gis_introduction/coordinate_reference_systems.html) for a guide that explains projection systems in GIS.

##### UTM vs Lat/Long
UTM zones are commonly used by the lab since the accuracy is sufficient for all the project designs. More accurate CRS may be used for higher-precision work such as surveying, but that level is generally unnecessary for the lab's larger scale work. While Lat / Long is more intuitive and very common, it can be very problematic for accuracies, so avoid this when working on crowns.

```EPSG``` codes are an easy way to define particular CRS, but not the only one. Common EPSG codes used for lab work:
   1. <img align="right" width="150" src=imgs/epsg_32616.png>EPSG 326**15** and 326**16** split Wisconsin (**15**N and **16**N). UTM is in meters - this is often what is used. <br clear="right"> 
   2. <img align="right" width="150" src=imgs/epsg_4326.png> EPSG 4326 - the lat/ or commonly called "WGS 84" projection, e.g., decimal degrees --> 10+ decimal places... or you lose precision!! This is not used for delineation, but will often be encountered as this is a very common format. Reprojecting these files into UTM is ideal. <br clear="right"> 
 
A good place to find projection information using EPSG codes is [spatialregerence.org](https://spatialreference.org). The projection strings or files maintained for each entry offers more advanced handling or troubleshooting.

A nice write up on geographic and projected coordinate systems can be found [here](https://www.esri.com/arcgis-blog/products/arcgis-pro/mapping/gcs_vs_pcs/).

The CRS should be identical across all of your data and project files:
1. ```Map``` document
2. ```Reference``` rasters
3. ```GPS``` points
4. ```Crown``` vector polygon / point layers
5. ```Ancillary``` images, borders, surfaces


## Getting Started
For the first time setup there is a bit more work to orient the entire project and get organized. Planning thoroughly will mean less mistakes and repetition of tasks to make adjustments later. 

### Project directory
Start a working directory dedicated to a single project. Organize files within this directory intentionally using subdirectories that are clear and easy to understand. 

One was can very descriptive:
 - ARB
     + base_mosaic
     + field_datasheet
     + gps_data
     + plot_pictures
     + tree_crowns
     + qgis_maps

Another way is to organize by layer or file's general type / category
 - ARB
     + csv
     + xlsx
     + qgz
     + shp
     + geojson
     + gps
     + tif
     + shp




### Map Document(s)

- Creating two basic documents can help containerize the workflow and be useful to have both open to cross check and organize final layers.
    + Overview Map --> Make one document that organizes the "BIG" picture and pulls together the various ancillary files all into one place. This is also a good repo to export completed versions of polygons from the working document.
    + Working Map --> Use this to keep a very simple set of only necessary files like the ```ref``` image and a couple working drafts of ```vector``` layers. As files are finished, export them out of here to keep it clean and free of junk files.
    + If you have a lot of areas spread out (NEON or ABoVe), consider multiple working map documents and avoid trying to fit everything in one. This allows allows for easier control of varying CRS across regions.
Other notes:
- Be careful of loading too much imagery into a single document
- Keep things organized with groups in the document
- Maintaining a clean directory structure that mimics your map docs will ease transferability and sharing


### Base ```REF``` Imagery


# Crown Delineation Training Exercises

Now that you have some background information, now it is time for you to begin applying these skills. The goals of this exercise is to get you familiar with QGIS, able to open and save GIS data, create and edit canopy delineation polygons, and troubleshoot common problems you may encounter.


## Getting familiar with QGIS

You may have heard of GIS software like ArcMap, GRASS, and QGIS. These programs give a graphical interface to work with spatial data. Our lab often uses QGIS because it is an open-source software that can be used on both Mac and Windows platforms. The general principles translate well across software. 

To familiarize yourself with QGIS, we recommend completing Module 2 of the QGIS tutorial: https://docs.qgis.org/3.28/en/docs/training_manual/basic_map/index.html

## Set up your folders

As mentioned in the Project directory section above, you first need to set up an area on your computer where all of your work will be saved and located. A directory is just a folder on your computer. A "subdirectory"" is a folder within a main folder. As mentioned above, naming folders clearly and descriptively is important so that you and others can easily locate and replicate what you are doing. Again do not use spaces in naming!

Go ahead and set up your directories as follows:
 - ARB
     + base_mosaic
     + gps_data
     + tree_crowns
     + qgis_maps
     
## Opening some data

Download the example dataset. *Put specific instructions here*.  Put the raster file (denoted by a .tif) extension into your base_mosaic folder. Put the vector files (denoted by either the .geojson or .shp) into your tree_crowns folder.

You can open the raster file by navigating to Layer > Add Layer > Add Raster Layer... A pop-up window will appear. Find your file at the top by inserting the file path or hitting the button with the three dots to find the file in your computer. Click the Add button at the bottom right of the popup to add it to the map.

You can do the same for vector data, but instead navigate to Layer > Add Layer > Add Vector Layer...

## Setting up QGIS

*Becket can you put instructions on how to set up the map docs as you suggested?*

## Creating a new polygon layers

You are now going to create your first polygons to delineate a canopy. Navigate to Layer > Create Layer > New Shapefile Layer.

A pop-up should now appear. Name the file and it within your tree_crown folder. Under the "Geometry Type" field select polygon. Check the CRS. Based on the above, which epsg code should you select?

Now you should name some fields. The researcher you are working with will help define these for each specific project. For now lets create three fields, named "Plot", "Species", and "Notes". Each of these will be Type strings. You can reduce the number of characters to 40 and hit the "Add to Fields List Button." Once done, you can hit "OK" at the bottom right.

Click the "Toggle Editing" button (it looks like a yellow pencil) and then click the "Add polygon feature" button. Choose a tree canopy to delineate. Now you can start drawing points that define the polgyon (these are called vertices). Remember the guidelines for canopy delineation above. To stop drawing your polygon, double or right click (depending if you use a mouse or laptop) the last vertex. You will now be prompted to enter the fields that you created earlier.

You've done your first canopy. Congrats! Continue to draw more until you fill the entire image. 

Once you are done editing click the save edit feature. It's recommended you do this often so you do not lose work as you draw.

## Editing an existing polygon layer

Now open the other vector file named *XYZ* that you downloaded (hopefully you put it into to the tree_crown folder). Go to Layer > Add Layer > Add vector layer...  Find where the file is located in the pop up and click Add.

Anytime you are opening new data it's good practice to check the file details. Double or right click the new layer under the Layers panel. Click on Properties and navigate to the Source tab on the left. Uh-oh what is the CRS. Is it the one you should be using?

You may need to project the file to the correct CRS. Note that you typically only want to do this for vector data. Consult the project lead before doing anything to a raster file. To project the current vector file, navigate to Vector > Data Management Tools > Reproject Layer...  Select the correct epsg code to reproject the current layer. Note that most GIS software will do something called on-the-fly projection to properly display data with different projection systems. It's best practice to actually project the data before working with it.

Now that we know the CRS is correct. Let's delineate another canopy and add it to this file. Can figure this out based on the above exercise?


## Common troubleshooting

*Beckett you may have some more ideas here...*

## Closing out and savings

*Beckett, again you probably have a better idea on what ask for here*








