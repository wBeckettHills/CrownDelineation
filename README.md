# Crown Delineation

A repository to collect information, templates, and best practices about delineating tree crowns in remote sensing imagery.<br clear="left"> <img style="float: left; padding: 2px 2px 2px 2px;" width="30%" src=imgs/cover_shot.png>  <img style="float: right; padding: 2px 2px 2px 2px;" width="32%" src=imgs/cover_shot_crowns.png>

<br clear="right">

## Intro
The most important information in remote sensing research is extracted from the canopy to be used to create spatial models. Field sampling, data entry, and canopy delineation tasks are the most time consuming, repetitive, skill-oriented, and, yet, still remain to be the most critical part of data collection and processing a remote sensing lab produces.

Your skills are an important part of this lab's ability to produce good science. The canopy is *hard* to define, being efficient is a skill set that is only learned through experience.  Do your best and ask a lot of questions.

The overall goal of this guide is to go over canopy crown tracing. To break it down, we need to know some basics of the sampling, which is presented as a set of prompts and questions to help guide yourself to the final outcomes needed.

### Background
It starts with leaf and plot sampling in the field, then later determining and digitizing those precise locations in the imagery is how the leaf chemistry is translated into pixels. The canopy was measured in a particular way based on the remote sensing product(s) going to be used for the research questions. There should be a modicum of notes/protocol, plot photos, and digital files available to help, in addition to the imagery itself, which should all be leveraged to ensure the best attempt goes into finding and tracing each canopy. Get to know the project and work toward creating an organized set of spatial files and supporting information that cohesively provides enough background and context to get started.

#### Project Design
The research intends to use remote sensing products, and this is a basic place to start to understand what the final goals will be and how the researchers plan to extract the pixel values. There are far more research designs than the basic example here that supports the goal of this guide focused on crowns. This is intended to serve as a simple question or prompt highlighting how project design is incorporated into the digitization of the sample plots.

```Single Crown > Pixel Resolution``` or ```Single Crown < Pixel Resolution``` ? 
1. If the outcome is to use imagery with 1-4m pixels (or less), it is essentially a "CANOPY" design, because the size of an individual tree is big enough and pixels are small enough that the single canopy will cover multiple pixels. This is when tree canopies need to be carefully traced, which is what this guide covers.

2. For imagery with larger pixels, especially ranges of 20-30m from space-borne instruments, sampling becomes more of a "PLOT" design. A single pixel in these products possibly include multiple trees / shrubs, or other landscape features, mixed together. This guide does not cover plots of this size, as it is generally an extraction from a point with less emphasis on how to properly find and delineate a single tree.


#### Registration 
Before discussing imagery, this is a short section to present the concept of image registration early. All remote sensing products are imperfectly collected and it is up to the research team to carefully piece it all together into a tidy stack with as much geometric accuracy as possible.

Any products used for tracing should ideally be co-registered (one image registered to another means shifting one to match the other). The concept of being successfully registered means that when flipping from image to image, a building or a tree is aligned with itself and not shifting slightly across the products. If they are not, it is more critical that the work is done carefully to ensure errors are not inserted. It is fine to use other images that are not perfectly co-registered to develop a better context of the digital canopy, just take care to ensure that this is only used as an aid.

#### Reference Image
Since tree canopies being traced become uniquely geo-registered to that single image in time, it is important to identify a good, clear image early on as the ```reference``` or ```ref``` image (older terminology may refer to this as the master or main image). Other common terms may be ```basemap``` or ```base mosaic```. Regardless of whether products are co-registered together ahead of time, the identity of this image should be highlighted accordingly. 

All tracing and finalizing of point / polygon placement is ultimately completed back on the ```ref``` image. It is absolutely critical that this concept is followed closely.

#### Remote Sensing Data
This is a short list of remote sensing products and field data the lab commonly uses or has available for ```CANOPY``` designs. Work with the researchers on the project to know what is actually available to use.

##### Base Imagery
The base imagery is primarily ```raster``` form when used. LiDAR ```point clouds``` are also usually turned into a ```raster``` to be used as surface and height models. 

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
The plots in the field are marked with a GPS unit, which is then later used to manually create an adjusted, additional set of point and polygon (```vector```) layers that more accurately locate each sample area in the ```reference``` remote sensing image(s). Collecting good GPS data is not covered in this guide, although having a basic understanding of the principles can offer insight to the reliability of each piece of information you use to build the context and decide on where to trace the canopy.

The final plots being drawn will need to cover the area of the crown that the project research team sampled. The Townsend Lab has some general basic protocol and guidelines used across most projects. Use these as a suggested place to start when discussing this with your project's leader. 

###### Basic Protocol
- The main objective is to focus on "pure" canopy pixels --> target high quality pixels that are the ***best*** representation of that species

<img style="float: center; padding: 10px 2px 10px 2px;" width="250" src=imgs/contours_may.png> <img style="float: center; padding: 10px 2px 10px 2px;" width="250" src=imgs/contours_july.png> <img style="float: center; padding: 10px 2px 10px 2px;" width="250" src=imgs/contours_october.png> <br clear="left">
- Canopy Contours
     - Sunny side of the canopy (southern side in Northern Hemisphere)
     - Reduce shaded side / shadow pixels --> In a time series, the ```ref``` image may have canopy shading, while other flights over the same area later in the year may have the entire canopy illuminated, look ahead to judge across all dates
- Canopy Edges
    - Avoid edges where shadows and thinning leaves
    - If the purpose of a project is to scale data (e.g., turn small pixels into big ones), be aware the canopy polygon may include the edges as fewer pixels define the crown. 
    - Be aware of spectral pollution from adjacent bright, dark, or mixed areas
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
The precision of the units used can range from many meters to a couple centimeters, here are the basic units the lab uses:

```GARMIN```  These smaller units (along with other brand of handheld units) are easier to pack and carry, but the 2-5m error in all three (X,Y,Z) directions means the final points aren't precise enough for canopy delineation and often serve only as a quick way to keep a digital record of the location. There are ways to enhance this in the field if the crew used ```averaging``` setting, but it is generally still not reliable enough for canopies.

```TRIMBLE``` The Geo7x is the current lab model that can be post-processed with accuracies approaching 2cm. It is a single handheld unit (```BASE```) that has an external antenna that is precisely 2m tall. Field conditions can affect the accuracy. Wide open areas can be expected to retain the best (<5cm), while proximal to or beneath a canopy can degrade quickly to 1-2m (or even worse). This accuracy is still close enough to be able to determine a tree stem location to correctly identify the crown. *This is the most trustworthy data to use without a lot of legwork to determine its reliability.*

```EMLID``` Similar to the Trimble, these units can be post-processed to similar precisions of a few centimeters in the open and a couple meters under the canopy. They require two units, a ```BASE``` and ```ROVER```, in order to offer those accuracies, which can make them more cumbersome to deal with. As well, another complicating factor is that the ```BASE``` unit may need 3+ hours to gain an accurate enough fix to be able to correct the ```ROVER```. Therefore, data collected with these units should be carefully scrutinized if they are to be used as high-precision locations. 


Other points to note:

- What CRS was the unit set to while recording locations in the field (this matters!)? They are often set by default to used decimal degrees (lat / long). Ideally they are using the local UTM to the area the unit is collecting. Not much can be done afterwards, just good info to think about.


#### CRS
 It is critical to understand from the very beginning how to handle the coordinate reference system (CRS) for the geospatial files. NEON and ABoVe cover multiple UTM zones, so this can be challenging to ensure you are tracing in the most accurate CRS for that image in the particular region it was imaged. 

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



### Tracing Crowns

ADD MORE HERE ABOUT HOW TO ACTUALLY DO THIS
(linking to other tutorials can help)


