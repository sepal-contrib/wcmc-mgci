QGIS-MGCI :sub:`beta`
======================

A QGIS-based workflow to support the computation of SDG Indicator 15.4.2 – Mountain Green Cover Index.

.. contents:: **Table of Contents**

General Information
-------------------

About QGIS-MGCI :sub:`beta`
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This geospatial workflow was developed by the UN Environment Programme World Conservation Monitoring Centre (UNEP-WCMC) in collaboration with the Food and Agriculture Organization (FAO) of the United Nations to support member countries to compute and report against SDG Indicator 15.4.2.

This geospatial workflow has been developed to be run on QGIS 3.16.11, a free and open-source geographic information system licensed under the GNU General Public License. QGIS is an official project of the Open Source Geospatial Foundation (OSGeo). It runs on Linux, Unix, Mac OSX, Windows and Android and supports numerous vector, raster, and database formats and functionalities. To run this workflow, you will also need to have R Software 4.4.1.

The QGIS-MGCI :sub:`beta` workflow is in a beta stage and therefore it is still under development. Please contact the QGIS-MGCI :sub:`beta` development team with any comments or suggestions.

If you have specific bugs to report or improvements to the tool that you would like to suggest, please use the `GitHub’s issue tracker
<https://github.com/dfguerrerom/wcmc-mgci/issues>`_ of the QGIS-MGCI :sub:`beta` module and do follow the `contribution guidelines
<https://github.com/dfguerrerom/wcmc-mgci/blob/master/CONTRIBUTE.md>`_.

Authors 
^^^^^^^

QGIS-MGCI :sub:`beta` has been developed by the UN Environment Programme World Conservation Monitoring Centre (UNEP-WCMC) in collaboration with the Food and Agriculture Organization (FAO) of the United Nations. Contributors to QGIS-MGCI :sub:`beta` and its documentation include Corinna Ravilious, Vignesh Kamath Cannanure, Boipelo Tshwene-Mauchaza, Cristina Telhado and Valerie Kapos. 

License
^^^^^^^
The QGIS-MGCI :sub:`beta` workflow and its documentation is made available under the terms of the `Creative Commons Attribution 4.0 International License (CC BY 4.0) <https://creativecommons.org/licenses/by/4.0/>`_ .

Background
^^^^^^^^^^

SDG Indicator 15.4.2 – Mountain Green Cover Index (MGCI) is one of the two indicators under SDG Target 15.4, which aims to:

"*ensure the conservation of mountain ecosystems, including their biodiversity, to enhance their capacity to provide benefits which are essential for sustainable development*".

The Food and Agriculture Organization (FAO) of the United Nations is the custodian agency of this indicator. The Mountain Green Cover Index (MGCI) is designed to measure the extent and the changes of green vegetation in mountain areas to monitor progress towards SDG Target 15.4.

The MGCI is defined as the ratio of the mountain green cover area to the total mountain area:

.. math::
    
    MGCI = (Mountain Green Cover Area)/(Total Mountain Area)

Where: 

- **Mountain Green Cover Area**: sum of mountain area (km :sup:`2`) covered by cropland, grassland, forestland, shrubland and wetland, as defined based on the IPCC classification (Penman et al. 2003). This component is calculated from the vegetation descriptor layer. 
- **Total Mountain Area**: total area (Km2) of mountains. In both the numerator and denominator, mountain area is defined according to Kapos et al. 2000. This component is calculated from the mountain description layer.
- **Vegetation descriptor layer**: The vegetation descriptor layer categorizes land cover into green and non-green areas. Green vegetation includes both natural vegetation and vegetation resulting from anthropic activity (e.g. crops, afforestation, etc.). Non-green areas include very sparsely vegetated areas, bare land, water, permanent ice/snow and urban areas. The vegetation description layer is derived from a land cover map, where land cover categories are classified into IPCC categories and then in green/non-green areas. 
- **Mountain descriptor layer**:  The mountain descriptor layer consists in a map of mountain classes following the UNEP-WCMC classification (Kapos et al. 2000). The UNEP-WCMC classification classifies the world mountain areas according altitude, slope and elevation range into the following categories.

  .. _mountain_classes:
  .. csv-table:: Mountain classes
     :header: "UNEP-WCMC Mountain Class", "Description"
     :widths: auto
     :align: center
  
     "1","Elevation > 4.500 meters"
     "2","Elevation 3.500–4.500 meters"
     "3","Elevation 2.500–3.500 meters"
     "4","Elevation 1.500–2.500 meters and slope >= 2"
     "5","Elevation 1.000–1.500 meters and slope >= 5 or local elevation range (LER 7 kilometer radius) > 300 meters"
     "6","Elevation 300–1.000 meters and local elevation range (7 kilometer radius) > 300 meters"

The QGIS-MGCI :sub:`beta` workflow allows the user to compute each of these description layers to then calculate MGCI values for any given area. The results of this analysis can be exported to a set of standardized reporting tables where MGCI values are disaggregated by mountain class and IPCC land category, as specified in the metadata of SDG Indicator 15.4.2.

References
^^^^^^^^^^

- Kapos, V., Rhind, J., Edwards, M., Prince, M., & Ravilious, C. (2000). Developing a map of the world’s mountain forests. In M. F. Price , & N. Butt (Eds.),?Forests in Sustainable Mountain Development: A State-of-Knowledge Report for 2000?(pp. 4-9). Wallingford: CAB International.? 
- Penman, J., Gytarsky, M., Hiraishi, T., Krug, T., Kruger, D., Pipatti, R., Buendia, L., Miwa, K., Ngara, T., Tanabe, K. (2003). Good Practice Guidance for Land Use, Land-use Change and Forestry. Good Practice Guidance for Land Use, Land-use Change and Forestry. 

Before using QGIS-MGCI :sub:`beta`
-----------------------------------

To run this workflow you will need have QGIS 3.16.11 and R Software 4.4.1. installed in your computer. 

We suggest users use the Long-Term Release version of QGIS to
undertake their analysis as this is most stable versions and users are
less likely to incur technical difficulties and bugs.

There are various installers depending on your operating system but for
most users we recommend the QGIS Standalone Installer. Full instructions
are on their website
https://qgis.org/en/site/forusers/download.html

Whilst the MGCI analysis runs entirely within the QGIS interface, users
wishing to use QGIS for the MGCI analysis are also required to install R
software. R scripts can be run from within the QGIS
interface and an R script will be only be used for calculating real
surface area during the MGCI calculation. Real surface area can be
calculated using one of the ready to use SAGA tools in the processing
toolbox, however after initial testing we found the results differed
from the GEE and R methods and therefore due to the need for consistency
between calculation methods for this SDG indicator, the best and easiest
method was to integrate the ‘surfaceArea’ function from package ‘sp in R
software.

Once QGIS and R are both correctly installed users will need to install
the following plugins:

1. **Processing R Provider:** This plugin essentially allows R scripts
   to be used directly within the QGIS processing toolbox with the
   simple addition of some QGIS header information placed at the top of
   the script to making the R script behave exactly like other
   processing tools in the QGIS processing toolbox. The header
   information allows graphical fields to be set in the processing
   dialogue window when running the tool e.g. the input raster, a
   specific field or the location and name of an output raster. Some
   header information is used to tell QGIS to either pass information to
   R and from QGIS about the tool to enable the R processing to happen
   within the QGIS interface.

-  From the QGIS Menu Toolbar click on **Plugins>>Manage and Install
   Plugins**

   |image9|

-  From the Plugin dialogue window search for **processing R**

   |image10|

-  Click **Install Plugin** and then **Close**

Once installed R will appear as a processing tool in the processing
toolbox and an R Scripts button in the Processing Toolbox Menu.

|image12|
   
Users may find that the R scripts button is missing at this stage.

-  Click the arrow next to the **R** Tools to expand the R toolset.

The toolset should look similar to the below with a few example scripts.

|image13|

and the processing Toolbox Menu should look like this with the missing R scripts button |image14|

|image15|

-  From the QGIS main menu click on **settings>>
   options>>processing>>providers**

-  expand **R** to see the R setting

   |image16|

If you operating system is 64 bit, tick **Use 64bit version**

-  Check the **R folder** is pointing to the correct location (where it
   is installed on your computer)

-  Click okay

-  Save the QGIS project and re-open to activate the changes.

You should now see that the R script button has appeared on the
processing toolbox menu

|image17|

Next add additional resources to the R processing toolbox

-  To add other R resources click on **plugins>>resource
   sharing>>resource sharing**

   |image18|

-  Click on **All Collections** on the left hand panel and click **QGIS
   R script collection (QGIS Official Repository)** then click
   **Install**

   |image19|

A wider collection of scripts should now be present in the R-scripts
collection. These are not required for MGCI but useful for R-Integration
with QGIS.


**Resource sharing plugin:** This plugin is a useful R related
plugin (which is not essential for the MGCI but useful for users
wishing to integrate R with QGIS).

Once the resource sharing plugin is installed some scripts should
also be visible. They are grouped into several categories as in the
screengrab below.

|image30|

For further information see the following sections of the QGIS user
manual at

-  https://docs.qgis.org/3.16/en/docs/user_manual/processing/3rdParty.html#r-scripts

-  https://docs.qgis.org/3.16/en/docs/user\_manual/processing/3rdParty.html#index-5

Introduction
------------

This tutorial explains in detail how to implement the QGIS-MGCI :sub:`beta` workflow step-by-step using Costa Rica as an example. It uses the 90m resolution Digital ELevation Model (DEM) from Copernicus `(COP-DEM_GLO-90) <https://spacedata.copernicus.eu/web/cscda/dataset-details?articleId=394198>`_ to create the mountain descriptor layer and land cover datasets from the  `European Space Agency (ESA) Climate Change Initiative (CCI) land cover datasets <https://maps.elie.ucl.ac.be/CCI/viewer/>`_ to create the vegetation descriptor layer. If using QGIS-MGCI for official purposes, it is recommended that users use nationally appropriate data sources if available. 

The tutorial outlines in detail the steps all the tools used for
individual steps in the processing toolbox as well as providing a custom
toolbox to group and run the steps to help speed up the analysis and
allow for easier repeat processing.

|imagetoolbox|

For each step or group of steps, the tutorial
follow the structure of a detailed description of the exact steps that are running within the toolbox tool followed by the
equivalent processing steps in the MGCI toolbox.

Initial set-up
------------------------------------------

Users will need to download the MGCI_Beta_Toolbox and set of templates and style files from `the MGCI repository <https://github.com/dfguerrerom/wcmc-mgci>`_.

|imagerepository1|

Once downloaded users need to navidate to the ****sources>>qgis>>QGIS_models folder*** and copy the the models and scripts in relevant QGIS folders. Guidance is provided below.

|imagerepository2|


The QGIS R-script ***MGCI_QGIS_rsa_v2.rsx*** for real surface Area will need to be placed in R scripts folder and the ***MGCI_v02beta*** folder placed in the Models folder.
You can find the location in QGIS under **Settings>>Options**. The other style and template files can be stored in your own project working location.

|imagesettings|

We suggest users create a folder for working in the following strucure

|imagerepository3|

Check that the ***MGCI_v02beta*** toolbox is visible in the ***processing toolbox***. It is from here that you will run the tools if you choose to use the MGCI toolbox rather than the manual steps.

|toolbox_access|

Check that your R installation is correctly installed by running the real surface area script with the small test sample data included in the 
MGCI repository download.

-  Add ***aoiDEM_testing_sample1.tif*** to you QGIS project
   
   |image25|

-  Double click on *** Tool C1. Generate Real Surface Area raster from DEM *** and save to a temportary output
   
   |image27|

-  Change the symbology of the output dataset to orange. 
   
   |image28|

You should see that the real surface area output is one cell less than the input dataset as the RSA requires the surrounding pixels for it's calculations.

|image29|

***If the script runs and produces the outputs above your R integration with QGIS has been set up correctly. If the script fails or does not produce the output please revisit the sections in this guidance to check that you have installed R correctly and pointed your QGIS to the relvant folder.***

Define projection and generate an AOI
-------------------------------------
The first step is to define an Area of Interest (AOI) for the analysis. This should go beyond the country
bundary as outlined in the **Defining analysis environments** section of the tutorial.

**The instructions below show and explain the manaul steps without the MGCI toolbox:**

-  Add a country boundary layer to QGIS **Layer>>Add Layer>>Add Vector
   Layer**

   |image32|

   |image33|
   |image34|

-  Click **Add** and **Close** to close the Data Source Manager: Vector
   dialogue window

-  Right-click on the country boundary layer and click **Zoom to Layer**

*Note that for Costa Rica the country includes Cocos Island to the
southwest of the Costa Rican mainland in the Pacific Ocean.*

In this example the boundary layer is in Geographic coordinate system
(EPSG 4326). At this stage we want to set-up the projection for the main
parts of the MGCI analysis. We therefore want to set the project window
to an equal area projection and physically project the country boundary
to the same projection.

Costa Rica covers more than one UTM Zone so in this example we will
define a custom Lambert Azimuthal Equal Area projection with the central
meridian set to -84 and the latitude of origin to 8.5.

Costa Rica does have a National Projection (see https://epsg.io/5367)
which may be an alternative to the Lambert Azimuthal Equal Area.

If you need to define a custom projection, follow the instructions in Box 1

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **BOX 1: Defining a custom projection**:                                                                                                                  |
|    :name: box-1-defining-a-custom-projection                                                                                                                          |
|                                                                                                                                                                       |
| -  From the main menu click **settings>>custom projections**                                                                                                          |
|                                                                                                                                                                       |
| -  Click the **+** button to a new custom projection                                                                                                                  |
|                                                                                                                                                                       |
| -  Give the custom projection a **name** e.g. in this example **CRI\_LAEQ**                                                                                           |
|                                                                                                                                                                       |
| -  Copy the following projection information into the **parameters** box, changing the lat and lon                                                                    |
|    highlighted in yellow to the centre lat and lon of your country.                                                                                                   |
|                                                                                                                                                                       |
|    PROJCRS["Custom\_Azimuthal\_Azimuthal\_Equal\_Area",                                                                                                               |
|    BASEGEOGCRS["WGS 84",                                                                                                                                              |
|    DATUM["World Geodetic System 1984",                                                                                                                                |
|    ELLIPSOID["WGS 84",6378137,298.257223563,                                                                                                                          |
|    LENGTHUNIT["metre",1],                                                                                                                                             |
|    ID["EPSG",6326]]],                                                                                                                                                 |
|    PRIMEM["Greenwich",0,                                                                                                                                              |
|    ANGLEUNIT["Degree",0.0174532925199433]]],                                                                                                                          |
|    CONVERSION["unnamed",                                                                                                                                              |
|    METHOD["Lambert Azimuthal Equal Area",                                                                                                                             |
|    ID["EPSG",9820]],                                                                                                                                                  |
|    **PARAMETER["Latitude of natural origin",8.5**,                                                                                                                    |
|    ANGLEUNIT["Degree",0.0174532925199433],                                                                                                                            |
|    ID["EPSG",8801]],                                                                                                                                                  |
|    **PARAMETER["Longitude of natural origin",-84**,                                                                                                                   |
|    ANGLEUNIT["Degree",0.0174532925199433],                                                                                                                            |
|    ID["EPSG",8802]],                                                                                                                                                  |
|    PARAMETER["False easting",0,                                                                                                                                       |
|    LENGTHUNIT["metre",1],                                                                                                                                             |
|    ID["EPSG",8806]],                                                                                                                                                  |
|    PARAMETER["False northing",0,                                                                                                                                      |
|    LENGTHUNIT["metre",1],                                                                                                                                             |
|    ID["EPSG",8807]]],                                                                                                                                                 |
|    CS[Cartesian,2],                                                                                                                                                   |
|    AXIS["(E)",east,                                                                                                                                                   |
|    ORDER[1],                                                                                                                                                          |
|    LENGTHUNIT["metre",1,                                                                                                                                              |
|    ID["EPSG",9001]]],                                                                                                                                                 |
|    AXIS["(N)",north,                                                                                                                                                  |
|    ORDER[2],                                                                                                                                                          |
|    LENGTHUNIT["metre",1,                                                                                                                                              |
|    ID["EPSG",9001]]]]                                                                                                                                                 |
|                                                                                                                                                                       |
| -  Click the **Validate** button to check that the parameters are valid and then **OK** to save the custom projection                                                 |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+ 

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **BOX 1: continued**:                                                                                                                                     |
|    :name: box-1-continued                                                                                                                                             |
|                                                                                                                                                                       |
| -  see example below                                                                                                                                                  |
|                                                                                                                                                                       |
|    |image35|                                                                                                                                                          |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+ 

Next change the projection set for the QGIS project to your chosen equal area
projection. In this example it is the custom projection that was defined
in Box 1.

-  Click on the project projection **EPSG: 4326** in the bottom right
   hand corner of your QGIS project

   |image36|

-  In the Project Properties dialogue window search for the chosen
   projection in the **Filter** tab

   |image37|

-  Once located click on the equal area projection to set your QGIS
   project to be displayed in the chosen projection. E.g. in this
   example **CRI\_LEA**

-  Click **Apply** and **OK**

   |image38|

   See that the project now displays the custom projection in the bottom
   right hand corner.

Next use the reproject tool to project the country boundary layer to the
equal area projection

-  In the processing toolbox search for the **Reproject** tool

   |image39|
   
-  Set the Input layer to be the **country boundary**

-  Set the Target CRS to be the **Project CRS** (i.e. to the equal area
   projection)

-  Set the output name to be the same as the input with a suffix to
   indicate the projection e.g. in this example
   **BND\_CTY\_CRI\_ LAEA**
   
   |image40|

Now that the country boundary is in the chosen equal area projection, we
can generate a 10km buffer which we will use as an area of
interest (AOI). As indicated previously, the AOI needs to be larger than
the country boundary to avoid errors during the processing. A distance
of 10km around the country boundary is added to ensure the AOI is large
enough to accommodate the 7km focal range function used in the mountain
descriptor layer generation.

-  In the processing toolbox search for the **buffer tool**

   |imagebuffer|
   
-  Set the buffer **Distance** to **10**

-  Set the buffer **Units** to **Kilometres**

-  Set the **endcap style** to **round** and the **join style** to
   **round**

-  Save the Buffered output to the same name as the input with the
   suffix **\_BUF10**
   
   |image42|

-  Click **Run** to run the tool.

-  If you change the symbology to semi-transparent symbol and draw it over
   the original country boundary you should be able to see the additional
   buffered area.

   |image43|

The output will be used as the Area of Interest (AOI) when preparing
the various layers for the MGCI analysis.

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox A1. Generic: Define projection and generate an AOI**:                                                                                      |
|    :name: toolbox_A1                                                                                                                                                  |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| Before running the tool users do need to create custom projection in their QGIS project                                                                               |
| as indicated in Box 1 outlined in the section above.                                                                                                                  |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below.                                                                                                  |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageA1|

|imageA1_w|   

Preparation of Vegetation descriptor layer
------------------------------------------

The development of vegetation descriptor layer starts with either a
raster or vector landuse landcover (LULC) dataset. Follow either section
5.2.1 if your LULC dataset is a raster data or 5.2.2 if your LULC
dataset is a vector.

Steps when using a raster dataset 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Clip and project LULC raster (FOR REGIONAL/GLOBAL DATASETS ONLY)
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::
To demonstrate the steps for processing a raster LULC dataset we will
use the Global ESA CCI LULC dataset. This dataset is provided in netcdf
(.nc) format. Similarly to Geotiffs, these can be added directly to
QGIS.

-  From the QGIS main toolbar click on **Layer>>Add Layer>>Add Raster
   Layer** to add the LULC file to your QGIS session.

   |image44|

   |image45|

-  Click **Add**

For most formats this will add the LULC dataset to the QGIS session. The
Global ESA CCI LULC netcdf file however contains 7 different layers
(similar to bands in an image) and users need to select the
**lccs\_class** layer.

-  Click **lccs\_class** to select the LULC layer

-  Click **OK** and the LULC layer will be added to your QGIS project

-  Click **Close** to close the Data Source Manager: Raster dialogue
   window

   |image46|

Next check that the LULC layer has correct projection information and
appears in the correct place in the QGIS project.

-  First check that the LULC layer is correctly overlaying the country
   boundary data. If it does not your country boundary and/or your LULC
   layer may be lacking projection information or have the wrong
   projection information.

   |image47|

   QGIS will display a **?** next to the layer if projection information
   is missing.

-  If projection information is missing define the projection using the
   **Define Shapefile projection** tool in the processing toolbox (this
   will permanently attach projection information to the layer)
   alternatively you can just define it within the current QGIS project
   by right clicking on the layer.

   In this example we know the LULC is in Geographic coordinate system
   so we can assign coordinate system EPSG 4326 to the layer

   |image48|

   This layer should now draw correctly on the country boundary.

   If the LULC dataset is a regional or global extent it will need
   projecting and clipping to the AOI.

   In this example we are using a global dataset so we will need to
   follow **step (a) only** to clip the raster and save it in the equal
   area projection. For National datasets already clipped to the country
   boundary follow **step (b) only.**

-  In the processing toolbox search for **Clip**

-  Double click on the **Clip raster by mask layer** under the GDAL
   toolset

   |image49|

-  Select the **LULC dataset** for the **Input Layer**

-  Select the **buffered bounding box layer** for the **Mask Layer**

-  Select the **Project CRS** for the **Target CRS**

-  Tick **Match the extent of the clipped raster to the extent of the
   mask layer**

-  Tick **set the output file resolution**

-  Type the **X and Y resolution in metres** (in this case the
   resolution of the LULC dataset is 300)

-  Tick **Use Input Layer Data Type**

-  Set the output **Clipped (mask)** e.g. to LULC\_clip\_LAEA\_BUF10.tif

   (see screengrab below)

   |image50|
   
   |image51|

-  **Click Run** to run the tool

The new clipped LULC dataset in the equal area projection should be
added should be added to the map canvas\ **.**

-  Right click on the clipped LULC dataset (i.e. in this example the
   LULC\_clip\_LAEA\_BUF10 layer) and click **properties>>Symbology**

   |image52|

-  Change the render type to **Palleted/Unique Values**

-  Click **Classify** and then **OK**

   |image53|

You should now see the unique LULC classes present within the AOI for
the country.

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox A2a. VegetationDescriptor: Clip and project LULC raster (FOR REGIONAL/GLOBAL DATASETS)**:                                                  |
|    :name: toolbox_A2a                                                                                                                                                 |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| Before running the tool users need to check that they know the projection of their LUUC dataset                                                                       |
|                                                                                                                                                                       |
| and it is faling in the correct place geographically, as outlined in the section above.                                                                               |
|                                                                                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below.                                                                                                  |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageA2a| 

|imageA2a_w|   

Project LULC raster (FOR NATIONAL RASTER DATASETS ONLY):
::::::::::::::::::::::::::::::::::::::::::::::::::::::::

-  search for **project** in the processing toolbox.

   |image54|

-  Double click on the GDAL tool **Warp (reproject)**

-  Select the **National** **LULC dataset** for the **Input Layer**

-  Select the **Project CRS** for the **Target CRS**

-  Set the resampling method to **Nearest Neighbour**

-  Set the output resolution (same as the input or the equivalent to the
   input in metres)

-  Set the output **Reprojected** layer name e.g. to
   **National\_LULC\_\_LAEA.tif**

-  Click **Run** to run the tool

   |image55|

The new projected LULC dataset in the equal area projection should be
added should be added to the map canvas\ **.**

-  Right click on the projected LULC dataset and click
   **properties>>Symbology**

-  Change the render type to **Palleted/Unique Values**

-  Click **Classify** and then **OK**
  
   |image56|
  
   |image57|

The layer should now show all the National LULC classes for Costa Rica.

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox A2b. VegetationDescriptor: Project LULC raster (FOR NATIONAL RASTER DATASETS)**:                                                           |
|    :name: toolbox_A2b                                                                                                                                                 |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| Before running the tool users need to check that they know the projection of their LUUC dataset                                                                       |
|                                                                                                                                                                       |
| and it is faling in the correct place geographically as outlined in the section above.                                                                                |
|                                                                                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below.                                                                                                  |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer.                                                                                                                 |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageA2b|

|imageA2b_w|

Steps when using a vector dataset 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Project Vector LULC and convert to raster (FOR NATIONAL VECTOR DATASETS ONLY):
::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

When using a vector LULC dataset the data will also need to be projected
to an equal area projection.

-  If the dataset is not already in an equal area projection, search for **reproject** in the processing toolbox
   
   |image58| 

-  Select the **National** **LULC vector dataset** for the **Input
   Layer**

-  Select the **Project CRS** for the **Target CRS**

-  Set the **reprojected** output layer e.g. **LULC_vector_LAEA.shp**
   
   |image59|
   
-  Click **Run** to run the tool.

The next step is to rasterize the LULC data. When converting it is
important to choose an output resolution that is appropriate for the
scale of the vector dataset. (see Box 2).

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **BOX 2 Conversion between nominal scale and resolution**:                                                                                                |
|    :name: box-2-conversion-between-nominal-scale-and-resolution                                                                                                       |
|                                                                                                                                                                       |
| -  The scale of a vector dataset is usually expressed in a similar way to paper maps, i.e. in a ratio to show the amount of reduction from the real world             |
|    e.g.  1:50,000. A country’s vector LULC map will have been created a particular scale. determined by the Minimum Mapping Unit. i.e. the size of the smallest       |
|    feature. A nominal scale is will have been assigned to the dataset to reflect the scale at which the data were collected and mapped. Conversion to raster requires |
|    this scale to be converted to a resolution, i.e. an appropriate pixel size for the scale of the data.                                                              |
|                                                                                                                                                                       |
|    To calculate map scale there are two parameters:  ground resolution and screen resolution.                                                                         |
|                                                                                                                                                                       |
|    .. math:: scale = 1: (resolution * PPI / 0.0254)  or    resolution = scale * 0.0254/PPI                                                                            |
|                                                                                                                                                                       |
|    **Where**   :                                                                                                                                                      |
|    **resolution** =  ground resolution (the size in (m) that a pixel represents.                                                                                      |
|    **PPI** =  the screen resolution (pixels number that every inch contains on the screen (default 96dpi).                                                            |
|    **0.0254** = (m/inch),  the unit conversion between meter and inches.                                                                                              |
|    **scale** = nominal scale of vector dataset                                                                                                                        |
|                                                                                                                                                                       |
|    some examples are provided in the table below:                                                                                                                     |
|                                                                                                                                                                       |
|    |imagescale_table|                                                                                                                                                 |
|                                                                                                                                                                       |
|    (source: https://enonline.supermap.com/iExpress9D/Appendix/scale.htm)                                                                                              |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+ 


Once the resolution to convert the vector dataset to has been
determined the vector dataset can be converted to Raster.

-  In the processing toolbox search for **Rasterize.**

   |imagerasterize|

-  Double click on the GDAL **Rasterize (vector to raster)** tool

-  Select the **National** **LULC vector dataset in equal area
   projection** for the **Input Layer**

-  Select the **field containing LULC classes** for the **field to use
   for a burn-in value**

-  Set the **output raster size units** as **Georeferenced units**

-  Set both the **Width/ Horizontal resolution and Width/ vertical
   resolution** to the resolution determined by previous step using the
   formula to convert from the nominal

   vector scale (see BOX 2)

-  Set the **output extent** to **Calculate by Layer** and selecting the
   same dataset used for the Input Layer

-  Set the **rasterized** output layer e.g.
   **LULC\_LAEA\_fromvector.tif**
   
   |image61| 

-  Click **Run** to run the tool

The new rasterised LULC dataset in the equal area projection should be
added should be added to the map canvas\ **.**

-  Right click on the projected LULC dataset and click
   **properties>>Symbology**

-  Change the render type to **Palleted/Unique Values**

-  Click **Classify** and then **OK**

   |image62|
   
   |image63|

The layer should now show all the National LULC classes for Costa Rica.

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox A2c. VegetationDescriptor: Project vector LULC and convert to raster (FOR NATIONAL RASTER DATASETS)**:                                     |
|    :name: toolbox_A2c                                                                                                                                                 |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| Before running the tool users need to check that they know the projection of their LUUC dataset and it is faling in the correct place geographically                  |
| as outlined in the section above.                                                                                                                                     |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below.                                                                                                  |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageA2c|  

|imageA2c_w|   

Reclassify to IPCC landcover types
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The next step is to reclassify the LULC map prepared in 5.2.1, 5.2.2 or
5.2.3 into the 6 MGCI vegetation descriptor LULC types.

QGIS provides several tools for reclassification. The easiest one to use
in this instance is the **r.reclass** tool in the GRASS toolset as it
allows the upload of a simple crosswalk textfile containing the input
LULC types on the left and the IPCC reclass values on the right.

-  Create a text file to crosswalk landuse/landcover (LULC) types from
   the ESA CII or National landcover dataset to the 6 IPCC landcover
   classes

   |image64|

-  Search for **reclass** in the processing toolbox
   
   |image65|

-  Double click on **r.reclass**

-  Select the LULC output(from step 5.2.1, 5.2.2 or 5.2.3) as the
   **input raster layer**

-  Set the **GRASS GIS region extent** to be the same as the input layer

-  Set the **Reclassified** output e.g. VegetationDescriptor\_LAEA.tif

   |image66|

-  Click **Run** to run the tool

The new **VegetationDescriptor** layer is added to the map.

Although the reclassification only had 6 output classes the symbology
initially show values 0-255. This is a QGIS visualisation only and you
can see that the actual layer only has 6 values.

-  Right click on the layer **properties>>>Symbology**

-  Change the Render type to **Palleted/Unique values** and click
   **Classify** to see only the classes present in the raster (i.e. the
   1-6 Vegetation descriptor classes).

-  Load the VegetationDescriptor.qml file for quickly assigning the
   colours and labels.

   |image67|

   |image68|
   
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox A3. VegetationDescriptor: Generate Vegetation Descriptor Layer**:                                                                         |
|    :name: toolbox_A3                                                                                                                                                  |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
| Before running the tool users need to check that they know the projection of their LUUC dataset and it is faling in the correct place geographically.                 |
| as outlined in the section above.                                                                                                                                     |
|                                                                                                                                                                       |
| Before running the tool users need to check that they know the projection of their LUUC dataset and it is faling in the correct place geographically                  |
| as outlined in the section above.                                                                                                                                     |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below.                                                                                                  |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageA3|

|imageA3_w| 

Preparation of Mountain descriptor 
----------------------------------

Users should have read the ***Choice of DEM and data access*** section of
***defining analysis environements*** and selected a DEM
for use in the analysis before starting this section as the generation
of the mountain descriptor layer requires a DEM as the input source.

In this tutorial the Copernicus 90m source DEM has been chosen as an
example.

Merging DEM tiles into a single DEM 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The DEM tiles covering the full extent of Costa Rica have been download
from Copernicus using their AWS client. (Instructions for download of
Copernicus data can be found in the Annexes).

-  From the QGIS main toolbar click on **Layer>>Add Layer>>Add Raster
   Layer** to add the DEM tiles to your QGIS session.

   |image69|

-  Click **Open** and then **Add.** The DEM tiles will be added to the QGIS project

   The next step is to merge the DEM tiles into a single raster.
   
-  Search for **Merge** in the processing toolbox window
   
   |image70|
   
-  Double click the **GDAL Merge tool**.
   
-  For the Input layers **select the DEM tiles** covering your area of
   interest
   
   |image71|

-  Tick the DEM tiles to merge and Click **OK** to make the selection
   and return to main **Merge Dialog window**

-  Set the **output data type** to Float32 (same as the input DEM tiles)

-  Set the **Merged** output name e.g. C:/MGCI\_tutorial/
   DEM\_copernicus\_merge.tif
   
   |image72|
   
   |image73|

-  Click **Run** to run the tool

The merged DEM is added to the QGIS project.

|image74|

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox B1. MountainDescriptor: Merging DEM tiles into a single DEM**:                                                                             |
|    :name: toolbox_B1                                                                                                                                                  |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| Before running the tool users need to check that they know the projection of their DEM dataset and it is faling in the correct place geographically                   |
|                                                                                                                                                                       |
| as outlined in the section above.                                                                                                                                     |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below.                                                                                                  |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageB1|

|imageB1_w|

Clip and project merged DEM
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The DEM tiles are likely to cover a much wider area than the country
being analysed therefore it is important to crop the extent to minimise
processing time. As indicated previously,  the country boundary is
not used to clip the dataset directly as the various calculations during
the generation of the mountain descriptor layer require neighbouring
pixels to be analyses therefore the buffered AOI which you have already generated 
should be used.

-  search for **project** in the processing toolbox.

   |image54|

-  Double click on the GDAL tool **Warp (reproject)**

-  Select the **merged DEM dataset** for the **Input Layer**

-  Select the **Project CRS** for the **Target CRS**

-  Set the resampling method to **bilinear**

-  Set NoData value for output bands to **-9999**

-  Set the output **Reprojected** layer name e.g. to
   **DEM_MERGE_LAEA.tif**

-  Click **Run** to run the tool
   
   |image75|

The new DEM dataset in the equal area projection should be added
should be added to the map canvas\ **.**

   |image74a|
   
-  search for **mask** in the processing toolbox.  

-  Double click on the **r.mask.vect** under the GRASS
   toolset

-  Select the **AOI buffered country boundary** for the **Name of vector dataset to use as mask**

-  Select the **Merged DEM in equal area projection r** for the **Name of raster map to which apply the mask**

-  Set the  the **GRASS GIS 7 Region Extent**  to the **AOI buffered country boundary**

-  Set the output **Masked** e.g. to
   DEM_merge_LAEA_AOI.tif
   
-  Click **Run** to run the tool

   |image74b|
   
The new clipped DEM dataset in the equal area projection should be added
should be added to the map canvas\ **.**
    
|image76|

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox B2. MountainDescriptor: Clip and project merged DEM to EQUAL AREA PROJECTION**:                                                            |
|    :name: toolbox_B2                                                                                                                                                  |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageB2| 

|imageB2_w| 

Project merged DEM to Equidistant projection (and generate AOI with tiled approach) 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In this section the projection used for the slope and 7km Local Elevation Range
calculation will differ as it is important to use an equidistant
projection to reduce errors, particularly in slope calculation. An overview of slope
calculation methods is provided in the Dendining analysis environments section 
of the tutorial. 

IF your country falls within **a single UTM Zone only** ***AND*** **you
have used the UTM projection for the previous steps**, or **if the
projection you are using has equidistant properties**, slope can be
generated in the same projection as the rest of the analysis, otherwise
please follow instruction in **BOX 3** for creating a custom equidistant
projection before following the next steps.

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **BOX 3: Defining a custom Azimuthal Equidistant projection**:                                                                                            |
|    :name: box-3-defining-a-custom-azimuthal-equidistant-projection                                                                                                    |
|                                                                                                                                                                       |
| -  From the main menu click **settings>>custom projections**                                                                                                          |
|                                                                                                                                                                       |
| -  Click the **+** button to a new custom projection                                                                                                                  |
|                                                                                                                                                                       |
| -  Give the custom projection a **name** e.g. in this example **CRI\_AZ\_EQUI**                                                                                       |
|                                                                                                                                                                       |
| -  Copy the following projection information into the **parameters** box, changing the lat and lon highlighted in yellow to the centre lat and lon of your country.   |
|                                                                                                                                                                       |
|    PROJCRS["Custom\_Azimuthal\_Equidistant",                                                                                                                          |
|    BASEGEOGCRS["WGS 84",                                                                                                                                              |
|    DATUM["World Geodetic System 1984",                                                                                                                                |
|    ELLIPSOID["WGS 84",6378137,298.257223563,                                                                                                                          |
|    LENGTHUNIT["metre",1],                                                                                                                                             |
|    ID["EPSG",7030]]],                                                                                                                                                 |
|    PRIMEM["Greenwich",0,                                                                                                                                              |
|    ANGLEUNIT["Degree",0.0174532925199433]]],                                                                                                                          |
|    CONVERSION["unnamed",                                                                                                                                              |
|    METHOD["Modified Azimuthal Equidistant",                                                                                                                           |
|    ID["EPSG",9832]],                                                                                                                                                  |
|    **PARAMETER["Latitude of natural origin",8.5**,                                                                                                                    |
|    ANGLEUNIT["Degree",0.0174532925199433],                                                                                                                            |
|    ID["EPSG",8801]],                                                                                                                                                  |
|    **PARAMETER["Longitude of natural origin",-84**,                                                                                                                   |
|    ANGLEUNIT["Degree",0.0174532925199433],                                                                                                                            |
|    ID["EPSG",8802]],                                                                                                                                                  |
|    PARAMETER["False easting",0,                                                                                                                                       |
|    LENGTHUNIT["metre",1],                                                                                                                                             |
|    ID["EPSG",8806]],                                                                                                                                                  |
|    PARAMETER["False northing",0,                                                                                                                                      |
|    LENGTHUNIT["metre",1],                                                                                                                                             |
|    ID["EPSG",8807]]],                                                                                                                                                 |
|    CS[Cartesian,2],                                                                                                                                                   |
|    AXIS["(E)",east,                                                                                                                                                   |
|    ORDER[1],                                                                                                                                                          |
|    LENGTHUNIT["metre",1,                                                                                                                                              |
|    ID["EPSG",9001]]],                                                                                                                                                 |
|    AXIS["(N)",north,                                                                                                                                                  |
|    ORDER[2],                                                                                                                                                          |
|    LENGTHUNIT["metre",1,                                                                                                                                              |
|    ID["EPSG",9001]]]]                                                                                                                                                 |
|                                                                                                                                                                       |
| -  Click the **Validate** button to check that the parameters are valid and then **OK** to save the custom projection                                                 |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+


+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **BOX 3: continued**:                                                                                                                                     |
|    :name: box-3-continued                                                                                                                                             |
|                                                                                                                                                                       |
| -  see example below                                                                                                                                                  |
|                                                                                                                                                                       |
|    |image78|                                                                                                                                                          |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+ 

This slope and local elevation range generation can take a long time to run so we will 
generate and AOI split into a chosen number of tiles so uses can choose to run these steps iteratively.

First we need to project the merged DEM to equidistant projection.

-  In the **processing toolbox** search for **reproject** 

   |image54|                                                                                                                                                                  
    
- Double click on the **Warp (reproject)** tool under the **GDAL toolset** 
- Set the Input layer to be the **merged DEM in geographic coordinate system**
    *Note: it is important not to use the one that has already been projected as this can introduce errors into the DEM*
- Set the Source CRS to be **EPSG: 4326 (Geographic)**
- Set the Target CRS to be **your custom equidistant projection** e.g. CRI\_AZ\_EQUI
- Set the resampling method to **bilinear**
- Set the output file resolution to the resolution of the DEM in meters e.g. 90m in this example
- Set the Reprojected output to e.g. **DEM_merge_EQUI.tif**

  |image79|
  
- Click **Run** to run the tool
 
The reprojected layer is added to the QGIS project. 

|reprojequi2|

Next we will extract the extent from the merged DEM in equidistant projection. This generates a polygon layer 
which aligns with the outer cells of the DEM. It also provides a height and width field in the attribute table of the layer
which we can use to split the dataset into a selected number of tiles for iterative processing

-  In the **processing toolbox** search for **Extract layer** 

   |extract_layer_extent|
   
-  Set the **Input Layer ** to **the merged DEM in equidistant projection**
   
   |extract_layer_extent2|
   
- Open the attribute table of the extent layer

  |extent_attr|

- add and calculate an attribute for tile_width by dividing the width field by your number of chosen tiles e.g. in this example we have chosen 6 tiles.
  
  |extent_attr_width|
  
- add and calculate an attribute for tile_width by dividing the height field by your number of chosen tiles e.g. in this example we have chosen 6 tiles.
  
  |extent_attr_height|

-  In the **processing toolbox** search for **Create grid** 

   |creategrid|  

-  Set the **Grid Type** to **Rectangle (polygon)**
-  Set the **Grid extent** to **the merged DEM in equidistant projection**
-  Set the **Grid extent** to **the merged DEM in equidistant projection**
-  Copy the tile_width number from the step above to the **Horizontal spacing** and the tile height to the **Vertical spacing**
-  Copy the cellsize to the **Horizontal overlay** and **Vertical overlay**. 

This will mean that the tiles will overlap by one cell and ensure there are no gaps when the tiles are merged back together
(as the internal tile lines will not match a grid cell line)

-  Set the **Grid CRS** to **your chosen equidistant projection**

   |creategrid2|  
   
-  Click **Run** to run the tool.

The vector grid is added to the QGIS project. 

|creategrid3|  

Next, use the reproject tool to project the country boundary layer to the
equidistant projection

-  In the processing toolbox search for the **Reproject** tool

   |image54|
   
-  Set the Input layer to be the **country boundary**

-  Set the Target CRS to be the **your chosen equidistant CRS** 

-  Set the output name to be the same as the input with a suffix to
   indicate the projection e.g. in this example
   **BND_CTY_CRI_EQUI**
   
   |reprojequi|

Now that the country boundary is in the chosen equidistant projection, we
can generate the 10km buffer which we will use as an area of
interest (AOI). As indicated previously, the AOI needs to be larger than
the country boundary to avoid errors during the processing. A distance
of 10km around the country boundary is added to ensure the AOI is large
enough to accommodate the 7km focal range function used in the mountain
descriptor layer generation.

-  In the processing toolbox search for the **buffer tool**

   |imagebuffer|

-  Set the **Input layer** to **your country boundary in equidistant projection e.g. BND_CTR_EQUI**

-  Set the buffer **Distance** to **10000**

-  Set the buffer **Units** to **meters**

-  Set the **endcap style** to **round** and the **join style** to
   **round**

-  Save the Buffered output to a new name **e.g. BND_BUF_AOI_EQUI**

   |buffequi|

-  Click **Run** to run the tool.

The last step is to intersect the equidistant vector grid with the buffered AOI in equidistant projection.

-  In the **processing toolbox** search for **intersection** 

   |intersection|

-  Set the **Input layer** to **the buffered country boundary in equidistant projection**
-  Set the **Overlay layer** to **the vector grid in equidistant projection**
-  Set the output **Intersection** toe.g. **BND_BUF_AOI_EQUI_tiles.shp**

   |intersection2|
   
The output tiled Area of Interest (AOI) can be used when preparing
the slope and local elevation range datasets.

|intersection3|

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox B3. MountainDescriptor:  Project merged DEM to Equidistant projection (and generate AOI with tiled approach) **:                           |
|    :name: toolbox_B3                                                                                                                                                  |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageB3|

|imageB3_w| 

Generating slope layer from layer DEM
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Slope can now be generated from the merged DEM in equidistant projection. Users should be warned that the slope process can
take some time to process. 

-  In the processing toolbox search for **Slope**
   
   |image80|   
   
-  Double click on the **slope** tool under **Raster analysis** in the
   **GDAL** toolset.

-  *We will use this tool instead of the* *basic QGIS slope tool* *as it
   has an option to compute edges which means it looks at edge pixels
   and no data values*.

-  Set the **Input layer** to be the reprojected DEM i.e. the
   equidistant version unless, as specified above, your country falls
   within a single UTM Zone only *AND* you have used the UTM projection
   for the previous steps, or if the projection you are using has
   equidistant properties e.g. in this example
   **DEM\_copernicus\_merge\_CRI\_AZ\_EQUI.tif** , the projected
   equidistant DEM generated from BOX 3.

-  Tick **compute edges**

-  Set the **Slope** output to e.g.
   **DEM\_copernicus\_merge\_SLOPE\_CRI\_AZ\_EQUI.tif**
   
   |image82|

-  Click **Run** to run the tool
   
If it takes too long uses may wish to use the tiled AOI to clip the merged DEM into smaller chunks using r.mask.cect and 
run the slope tool multiple times for each tile and then merge the slope at the end. 

**NOTE: the MGCI toolbox tools B4a will be far more efficient (as users can choose to iterate automatically through the tiles and produce slope at the same time).**

If you wish to iterate manually. Split the Merged DEM in equidistant projection into tiles as follows:

-  search for **r.mask** in the processing toolbox.  
   
   |rmask|

-  Double click on the **r.mask.vect** under the GRASS
   toolset

-  Select the **AOI tiles layer** for the **Name of vector dataset to use as mask**

-  Select the **Merged DEM in equidistant projection** for the **Name of raster map to which apply the mask**

-  Set the  the **GRASS GIS 7 Region Extent**  to the **AOI tiles layer**

-  Set the output **Masked** e.g. to
   DEM_merge_EQUI_AOI_tiles.tif
   
-  Click **Run** to run the tool

   |manualiterate|

Then repeat the slope process above for each of the tiles.

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox B4a. MountainDescriptor: iterate and  generate slope in equidistant projection**:                                                          |
|    :name: toolbox_B4a                                                                                                                                                 |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| This tool can run generating the slope in one layer or users can click the green iterate button too process the slope in smaller chunks                               |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageB4a|

|imageB4a_w| 

Next, if you haave processed the slope layer chunks use the merge tool to combine the slope tiles into a single layer

-  Search for **Merge** in the processing toolbox window
   
   |image70|
   
-  Double click the **GDAL Merge tool**.
   
-  For the Input layers select all of the SLOPE tiles. Tick the SLOPE tiles to merge and Click **OK** to make the selection
   and return to the main **Merge Dialog window**

-  Set the **output data type** to Float32 (same as the input slope tiles)
-  Set the **Merged** output name e.g. C:/MGCI\_tutorial/
   SLOPE_merge_EQUI.tif
   
   |mergeslope1| |mergeslope2|

-  Click **Run** to run the tool

You will notice when compared to the output image it no longer looks clipped to the buffer. This is because the no data value in the slope images is set to nan and it was not possible to set the No data value in the merge tool to a non numeric value. You therefore must clip the merged slope layer back to the buffered AOI:

-  search for **r.mask** in the processing toolbox.  

   |rmask|

-  Double click on the **r.mask.vect** under the GRASS
   toolset

-  Select the **AOI tiles layer** for the **Name of vector dataset to use as mask**

-  Select the **merged SLOPE layer in equidistant projection** for the **Name of raster map to which apply the mask**

-  Set the  the **GRASS GIS 7 Region Extent**  to the **AOI tiles layer**

-  Set the output **Masked** e.g. to  **Slope_merge_EQUI_AOI.tif**
   
-  Click **Run** to run the tool

The merged slope is added to the QGIS project. 

|mergedslope| 



+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox B4b. MountainDescriptor: merge slope tiles (run if iteration used in B4a)**:                                                               |
|    :name: toolbox_B4b                                                                                                                                                 |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageB4b|

|imageB4b_w| 

The slope raster can now be projected to the main analysis equal area projection

-  In the **processing toolbox** search for **reproject** 

   |image54|                                                                                                                                                                  
    
- Double click on the **Warp (reproject)** tool under the **GDAL toolset** 
- Set the Input layer to be the **slope layer in equidistant projection**
- Set the Source CRS to be **your equidistant projection**
- Set the Target CRS to be **your equal area projection** e.g. CRI\_AZ\_EQUI
- Set the resampling method to **bilinear**
- Set the output file resolution to the resolution of the slope in meters e.g. 90m in this example
- Set the Reprojected output to e.g. **Slope_AOI_LAEA.tif**
  
  
  
- Click **Run** to run the tool
 
The new **SLOPE dataset in the equal area projection** is now added should be added to the map canvas\ **.**

|slopeinequalarea|



+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox B5. MountainDescriptor: Project SLOPE raster to Equal Area projection**:                                                                   |
|    :name: toolbox_B5                                                                                                                                                  |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageB5|

|imageB5_w| 


Generating 7km local elevation range from DEM
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For UNEP-WCMC mountain classes 5 and 6 a 7km local elevation range (LER7km) is required for
the identification of areas that occur in regions with significant
relief, even though elevations may not be especially high, and
conversely high-elevation areas with little local relief. This local
elevation range is generated by defining a 7km radius of interest around
each grid cell and calculating the difference between the maximum and
minimum values within a neighborhood. In QGIS the focal functions gives the option for calculating the range but only
allow for the specification of the neighborhood size in pixels (i.e.
number of cells) so therefore, when running the next steps the size of
the neighborhhod will be influenced by the cellsize of the DEM.

|image93|

To calculate the neighborhood size for your analysis in pixels divide 7000m by your cellsize and multiply by two. Round to the nearest odd integer.
This is because the neighborhood size in pixels in this tool represents diameter rather than radius. 

This step is very slow and it is recommended that the same tiled approach is used to generate the LER7km layer.

If you wish to iterate manually. Split the Merged DEM in equidistant projection into tiles. If you have used tiles for generating slope you can skip the following r.mask step:

-  search for **r.mask** in the processing toolbox.  
   
   |rmask|

-  Double click on the **r.mask.vect** under the GRASS
   toolset

-  Select the **AOI tiles layer** for the **Name of vector dataset to use as mask**

-  Select the **Merged DEM in equidistant projection** for the **Name of raster map to which apply the mask**

-  Set the  the **GRASS GIS 7 Region Extent**  to the **AOI tiles layer**

-  Set the output **Masked** e.g. to
   DEM_merge_EQUI_AOI_tiles.tif
   
-  Click **Run** to run the tool

   |manualiterate|

Then for each of the tiles run the following steps:

-  In the processing toolbox search for **r.neighbor**.

   |imageneighbors|

-  Double click on the **r.neighbor** tool under the GRASS toolset

-  Select the **Input Raster Layer to** the merged equidistant DEM (or equidistant dem tile is you are running in smaller clumps)

-  Set the **neighborhood operation** to **Range**

-  Set the **neighborhood size to** 155 (e.g. in this example determined by:
   7000/90*2))

-  Set the **GRASS GIS 7 region extent** to the **same as the Input
   Layer specified above**

-  Set the **GRASS GIS 7 cellsize** to the **same as the Input Layer
   specified above**

-  Set the output **Neighbors layer** e.g. to
   LER7km_EQUI

   |image99|
   
  
-  Click **Run** to run the tool
   
 
The LER7km layer (or set of LER7km tiles) in the equidistant projection should have been
added to the map canvas.

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox B6a. MountainDescriptor: generate 7km LER in equidistant projection**:                                                                     |
|    :name: toolbox_B6a                                                                                                                                                 |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
| This tool can run generating the Ler7KM in one layer or users can click the green iterate button too process the ler7KM in smaller chunks                             |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageB6a|

|imageB6a_w|  

Next, if you have processed the LER7km layer in chunks use the merge tool to combine the slope tiles into a single layer

-  Search for **Merge** in the processing toolbox window
   
   |image70|
   
-  Double click the **GDAL Merge tool**.
   
-  For the Input layers select all of the SLOPE tiles. Tick the SLOPE tiles to merge and Click **OK** to make the selection
   and return to the main **Merge Dialog window**

-  Set the **output data type** to Float32 (same as the input slope tiles)
-  Set the **Merged** output name e.g. C:/MGCI\_tutorial/
   LER7km_merge_EQUI.tif
   
   |mergeLER7km_1|

-  Click **Run** to run the tool

You will notice when compared to the output image it no longer looks clipped to the buffer. This is because the no data value in the LER7km images is set to nan and it was not possible to set the No data value in the merge tool to a non numeric value. You therefore must clip the merged LER7km layer back to the buffered AOI:

-  search for **r.mask** in the processing toolbox.  

   |rmask|

-  Double click on the **r.mask.vect** under the GRASS
   toolset

-  Select the **AOI tiles layer** for the **Name of vector dataset to use as mask**

-  Select the **merged LER7km layer in equidistant projection** for the **Name of raster map to which apply the mask**

-  Set the  the **GRASS GIS 7 Region Extent**  to the **AOI tiles layer**

-  Set the output **Masked** e.g. to  **LER7km_merge_EQUI_AOI.tif**
   
-  Click **Run** to run the tool

The merged LER7km is added to the QGIS project. 

|mergedLER7km| 


+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox B6b. MountainDescriptor: merge LER7km tiles (run if iteration used in B6a)**:                                                              |
|    :name: toolbox_B6b                                                                                                                                                 |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageB6b|

|imageB6b_w|  

The LER7km raster can now be projected to the main analysis equal area projection

-  In the **processing toolbox** search for **reproject** 

   |image54|                                                                                                                                                                  
    
- Double click on the **Warp (reproject)** tool under the **GDAL toolset** 
- Set the Input layer to be the **LER7km layer in equidistant projection**
- Set the Source CRS to be **your equidistant projection**
- Set the Target CRS to be **your equal area projection** 
- Set the resampling method to **bilinear**
- Set the output file resolution to the resolution of the LER7km in meters e.g. 90m in this example
- Set the Reprojected output to e.g. **LER7km_AOI_LAEA.tif**
  
  
  
- Click **Run** to run the tool
 
The new **LER7km dataset in the equal area projection** is now added should be added to the map canvas\ **.**

|LER7kminequalarea|

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox B7. MountainDescriptor: Project LER7km raster to Equal Area projection**:                                                                  |
|    :name: toolbox_B7                                                                                                                                                  |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageB7|

|imageB7_w| 


Generating layers for each mountain class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
We now have all the inputs required for generating the mountain classes
for the mountain descriptor layer. We will use the raster calculator to
input the followings expression to generate a raster layer for each
mountain class.

**Mountain Class 1**

"DEM\_copernicus\_merge\_AOI\_LAEA@1" >= 4500

|image101|

**Mountain Class 2**

"DEM\_copernicus\_merge\_AOI\_LAEA@1" >= 3500 AND
"DEM\_copernicus\_merge\_AOI\_LAEA@1" < 4500

|image102|

**Mountain Class 3**

"DEM\_copernicus\_merge\_AOI\_LAEA@1" >= 2500 AND
"DEM\_copernicus\_merge\_AOI\_LAEA@1" < 3500

|image103|

**Mountain Class 4**

"DEM\_copernicus\_merge\_AOI\_LAEA@1" >= 1500 AND
"DEM\_copernicus\_merge\_AOI\_LAEA@1" < 2500 AND
"DEM\_copernicus\_merge\_AOI\_LAEA\_SLOPE@1" >= 2

|image104|

**Mountain Class 5**

("DEM\_copernicus\_merge\_AOI\_LAEA@1" >= 1000 AND
"DEM\_copernicus\_merge\_AOI\_LAEA@1" < 1500 AND
"DEM\_copernicus\_merge\_AOI\_LAEA\_SLOPE@1" >= 5) OR
("DEM\_copernicus\_merge\_AOI\_LAEA@1" >= 1000 AND
"DEM\_copernicus\_merge\_AOI\_LAEA@1" < 1500 AND
"LocalElevationRange7km\_AOI\_LAEA@1" > 300)

|image105|

**Mountain Class 6**

"DEM\_copernicus\_merge\_AOI\_LAEA@1">= 300 AND
"DEM\_copernicus\_merge\_AOI\_LAEA@1" < 1000
AND"LocalElevationRange7km\_AOI\_LAEA@1" > 300

|image106|

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox B8. MountainDescriptor: Generating layers for each Kapos mountain class**:                                                                 |
|    :name: toolbox_B8                                                                                                                                                  |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageB8|

|imageB8_w| 

Generate an interim mountain layer with classes 1-6
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

We can now use the following expression in the raster calculator to add
the different classes into a single map where class 1 has a value of 1,
class2 a value of 2 etc.

"K1\_AOI\_LAEA\_@1" + ("K2\_AOI\_LAEA\_@1"\*2) +
("K3\_AOI\_LAEA\_@1"\*3)+("K4\_AOI\_LAEA\_@1"\*4)
+("K5\_AOI\_LAEA\_@1"\* 5)+("K6\_AOI\_LAEA\_@1"\*6)

|image107|

The first interim dataset K1\_to\_K6\_AOI\_LAEA\_interim.tif of the
mountain descriptor layer should have been added should be added to the
map canvas\ **.**

-  To improve the symbology, right click on the new layer and click
   **properties** and then **symbology**

   |image108|

At the bottom of the layer properties dialogue window click the
**style** button and then load the predefined style file

|image109|

|image110|

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox B9. MountainDescriptor: Generate Mountain Descriptor layer (EXCLUDING isolated pixels from class 7)**:                                     |
|    :name: toolbox_B9                                                                                                                                                  |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageB9| 

|imageB9_w|

Filling isolated pixels within mountain areas and merging into classes 1-6 (****NOTE: This step is still in development****)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The last part of the mountain descriptor layer generation is to identify
isolated ‘non-mountain’ grid cells ( < 25km\ :sup:`2` in size)occurring
in mountain areas i.e, isolated inner basins and plateaus that are
surrounded by mountains but do not themselves meet criteria 1-6.

Once identified these can be reclassified according to the predominant
class among their neighbours.

-  The first step is to generate a raster of all non-mountain areas
   using the following expression in the **Raster Calculator**

   **"K1\_to\_K6\_AOI\_LAEA\_interim@1" = 0**

-  Set the output layer to e.g. **non\_mountain\_areas\_LAEA.tif**

   |image111|

   |image112|

You can see that the resultant non-mountains output dataset has value 1
for nonmountains and 0 for mountains. We need to set the 0 values to no
data.

-  Use the **Raster calculator** again with the following expession.
   This formular will set the 0’s to no data and leave the 1’s remaining
   as 1.

   ("non\_mountain\_areas\_LAEA@1">0)\*( "non\_mountain\_areas\_LAEA@1") /
   (("non\_mountain\_areas\_LAEA@1">0)\*1 +
   ("non\_mountain\_areas\_LAEA@1"<=0)\*0)

   |image113|

   |image114|

We can now use this layer to clump the the pixels into groups of
connected pixels

-  In the **Processing Toolbox** search for **r.clump**

   |image115|

-  Double click on the **r.clumps tool** under the GRASS toolset

-  Select the **Input layer** as the non-mountain dataset with 1’s and
   no data.

-  Set the **Title for output raster map** to **connected\_clumps**

-  Set the **GRASS GIS 7 region extent** to the **same as the Input
   Layer specified above**

-  Set the **GRASS GIS 7 cellsize** to the **same as the Input Layer
   specified above**

-  Set the output **Clumps layer** e.g. to
   non\_mountain\_clumps\_NA\_LAEA.tif

-  Click **Run** to run the tool

   |image116|

You can see that the resultant clumped non-mountains output dataset
which has a different value for each clump.

|image117|

We can now use this clumped layer to select and reclass clumps < 25sqkm
(2500 ha)

-  In the **Processing Toolbox** search for **r.reclass.area**

-  Double click on the **r.reclass.area tool** under the **GRASS
   toolset**

-  Select the **Input layer** as the **non\_mountain\_clumps**

-  Set the **value option that sets the area size limit** to **2500**

-  Set the **Lesser or greater than specified value** to **lesser**

-  Tick **Input map is clumped**

-  Set the **GRASS GIS 7 region extent** to the **same as the Input
   Layer specified above**

-  Set the **GRASS GIS 7 cellsize** to the **same as the Input Layer
   specified above**

-  Set the output **Reclassified** layer e.g. to
   non\_mountain\_clumps\_lt\_25km2\_\_LAEA.tif

-  Click **Run** to run the tool

   |image118|

If we zoom in to look at the output we can see the pixels that are
smaller than 25km2 in purple.

|image119|

We can now use the r.neighbor tool in the GRASS toolst to reclassified
according to the predominant class among their neighbours.

-  In the processing toolbox search for **r.neighbor**.

-  Double click on the **r.neighbor** tool under the GRASS toolset

-  Set the **Input Raster** dataset to the 1-6 interim Kapos map

   e.g. K1\_to\_K6\_AOI\_LAEA\_interim.tif

-  Set the **Raster Layer to select cells which should be processed** to
   **reclassified clumps for the Input Layer e.g.**
   non\_mountain\_clumps\_lt\_25km2\_\_LAEA.tif

-  Set the **neighborhood operation** to **Mode**

-  Set the **neighborhood size to 3** (we set it small for this first
   run so to make a best attempt to correctly recode according to
   closest neighbours)

-  Set the **GRASS GIS 7 region extent** to the **same as the Input
   Layer specified above**

-  Set the **GRASS GIS 7 cellsize** to the **same as the Input Layer
   specified above**

-  Set the output **Neighbors layer** e.g. to

   K1\_to\_K6\_AOI\_LAEA\_interim2.tif

-  Click **Run** to run the tool

   |image120|

Copy the Kapos mountain class symbology to the new
K1\_to\_K6\_AOI\_LAEA\_interim2.tif

-  Right click on the the 1-6 interim Kapos map e.g.
   K1\_to\_K6\_AOI\_LAEA\_interim.tif

-  Click on styles>>copy style

-  Then right click on the new 1-6 interim Kapos plus filled neighbors
   layer e.g. K1\_to\_K6\_AOI\_LAEA\_interim2.tif and paste style

   |image121|

See that the smallest of the identified isolated pixels < 25km2 have
been classified correctly into Kapos classes 1-6 but the larger ones are
still not classified.

|image122|

To rerun again on the new K1\_to\_K6\_AOI\_LAEA\_interim2.tif we first
have to extract the remaining pixels that are still to be reclassified
into a separate raster.

Use the **Raster Calculator** and the following expression to create the
new clumps subset.

"K1\_to\_K6\_AOI\_LAEA\_interim2@1" = 0 AND
"non\_mountain\_clumps\_lt\_25km2\_\_LAEA@1" > 0

|image123|

Use the Raster Calculator again but this time to convert the 0 cells in
the new clumps subset to no data using the following expression:

("non\_mountain\_clumps\_lt\_25km2\_\_LAEA\_subset2@1">0)\*(
"non\_mountain\_clumps\_lt\_25km2\_\_LAEA\_subset2@1") /
(("non\_mountain\_clumps\_lt\_25km2\_\_LAEA\_subset2@1">0)\*1 +
("non\_mountain\_clumps\_lt\_25km2\_\_LAEA\_subset2@1"<=0)\*0)

|image124|

We can then use the r.neighbor again to the remaining identified clumps
that didn’t get picked up first time round. (this time we suggest making
the neighborhood bigger area e.g. in this example we have used the same
number of pixels that was used for the local elevation range function
e.g. for a 90m resolution dataset 55 )

|image125|

Check to see if all pixels have been classified and if not so a further
run on a 3rd clumps subset will be required.

-  Use the **Raster Calculator** and the following expression to create
   the new clumps subset.

   "K1\_to\_K6\_AOI\_LAEA\_interim55@1" = 0 AND
   "non\_mountain\_clumps\_lt\_25km2\_\_LAEA\_subset2@1" > 0

|image126|

Convert the no data values to 0 using the ecxpression:

("non\_mountain\_clumps\_lt\_25km2\_\_LAEA\_subset3@1">0)\*(
"non\_mountain\_clumps\_lt\_25km2\_\_LAEA\_subset3@1") /
(("non\_mountain\_clumps\_lt\_25km2\_\_LAEA\_subset3@1">0)\*1 +
("non\_mountain\_clumps\_lt\_25km2\_\_LAEA\_subset3@1"<=0)\*0)

|image127|

Run the r.neighborhood again to catch the last pixels

|image128|

Select any remaining non-classified pixels using the expression:

"K1\_to\_K6\_AOI\_LAEA\_interim55\_55@1" = 0 AND
"non\_mountain\_clumps\_lt\_25km2\_\_LAEA\_subset3@1" > 0'

|image129|

If the resultant layer has all zeros then all pixels have been
classified

|image130|

|image131|

There is one last step before the Mountain Descriptor layer is complete.

-  Right click on the last K1\_to\_K6\_AOI\_LAEA layer that was
   generated in the previous step.

   See that the Raster is 32 bit floating point raster. We will use the
   GRASS r.reclass tool to convert the dataset to Byte and also embed
   the Kapos class descriptions to the mountain classes. Whilst QGIS
   cannot see it the class description when the file loads GRASS will
   be able to read them when calculating statistics and add the
   descriptions to output CSVs.

We have create a reclass file containing the mountain classes and
descriptions

|image132|

-  Run the **r.reclass** GRASS tool:

-  Set the reclassified output name to be
   **MountainDescriptor\_LAEA.tif**

|image133|

Copy and paste the style from the previous layer to shade and label the
classes in the MountainDescriptor\_LAEA.tif within the QGIS session.

|image134|

The Mountain Descriptor layer is now complete

Generation of Real Surface Area raster
--------------------------------------

The final layer that needs generating is the Real Surface
Area raster from the DEM. The tools should have all been tested to check
your R integration is working in the initial setup.

Refer to the workflow diagram in the overview section for an explaination of the process to calculate the 
real surface area from a DEM. In addition the images below help to explain what is happening for a single DEM pixel (focal cell)
using calculations based on it's surrounding elevation value.

|imagersa1|

|imagersa2|



-  In the processing toolbox expand the R-tools

   |image135|

-  Expand Raster Processing and double-click on Create RSA raster V1

-  Select the projected DEM as the Input Layer

-  Set the cellsize to the resolution of your DEM in metres

-  Set an output name RealSufaceArea\_LAEA.tif

   |image136|

-  Click Run to run the tool

   |image137|
   
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox C1. Generate Real Surface Area raster from DEM**:                                                                                          |
|    :name: toolbox_C1                                                                                                                                                  |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageC1|  

|imageC1_w|

Aggregation to standard resolution and clipping to country
----------------------------------------------------------
Aggregating mountain and RSA rasters to match resolution of vegetation descriptor layer
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Now that we have 3 raster datasets in their native resolutions we need to bring the datasets together and ensure that correct aggregation is undertaken and that the all the layers align to the coarsest resolution layer.   In this example we have the Mountain Descriptor layer and the RealSurfaceArea Rasters at 90m resolution but a VegetationDescriptor layer at 300m resolution. There are various tools that can be used but we have opted for the GRASS tool r.resamp.stats as it allowed for various methods when resampling to a coarser grid.

In the processing toolbox search for ***r.resamp.stats***

|imageresamp|  

We will first aggregate the Real Surface Area raster.

-  Select the **RealSufaceArea_LAEA**  as the **Input Layer**
-  Set the **aggregation method** to **sum**
-  **Tick Weight according to area** (as the documentation suggests it gives a more accurate result)
-  Set the **region extent** to **Calculate from layer>>Vegetation Descriptor_AOI_LAEA**
-  Set the **cellsize** to the the **same resolution as your Vegetation Descriptor layer** e.g. in this example 300m
-  Set the **Resampled Aggregated** layer to a name that distinguishes the resampling of the layer e.g. **RSA_LAEA_AOI_resample_sum_300.tif**
-  Click **Run** to run the tool 

   |image170|  

Next we will  aggregate the mountain descriptor layer.

In the processing toolbox search for ***r.resamp.stats***

|imageresamp|  
 
-  Select the **MountainDescriptor_K1_6** layer  as the **Input Layer** e.g in this example MoutainDescriptor_K1_6_withoutK7.tif
-  This time set the **aggregation method** to **mode** as we want to pick the value that represents the majority of smaller cell values in the coarser cell.
-  **Tick Weight according to area** (as the documentation suggests it gives a more accurate result)
-  Set the **region extent** to **Calculate from layer>>Vegetation Descriptor_AOI_LAEA**
-  Set the **cellsize** to the the **same resolution as your Vegetation Descriptor layer** e.g. in this example 300m
-  Set the **Resampled Aggregated layer** to a name that distinguishes the resampling of the layer e.g. in this example **MoutainDescriptor_K1_6_withoutK7_agg300.tif**

   |image173|  

If the Vegetation Descriptor is coarser resolution use:

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox D1a. Generic: Aggregate to resolution of Vegetation Descriptor**:                                                                          |
|    :name: toolbox_D1a                                                                                                                                                 |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageD1a|
|imageD1a_w|

If the Mountain Descriptor is coarser resolution use:

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox D1b. Generic: Aggregate to resolution of Mountain Descriptor**:                                                                            |
|    :name: toolbox_D1b                                                                                                                                                 |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageD1b|
|imageD1b_w|

Combine mountain and vegetation descriptor layers
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
As the MGCI required disaggregation by both the 6  LULC class and the 6 Mountain Class and the tools within QGIS will only allow a single input for zones, we will combine the two datasets together to form a combined zones dataset.

-  In the **processing toolbox**, search for and double click on the **raster calculator**
-  In the expression window we will sum the two dataset together but in order to distinguish the vegetation class from the mountain call all the vegetation values will be 
   multiplied by 10. This means for example a value of 35 in the output means the pixel has class 3 in the vegetation descriptor layer and class 5 in the Mountain descriptor
   layer.
-  In the expression box formulate the expression e.g.  ("VEGETATION_DESCRIPTOR_AOI_LAEA@1"*10) + "MoutainDescriptor_K1_6_withoutK7_agg300recl@1"
-  Set the Reference layer as the Vegetation Descriptor layer
-  Click **Run** to run the tool

   |image174|
 
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox D2. Generic: Combine mountain and vegetation rasters**:                                                                                    |
|    :name: toolbox_D2                                                                                                                                                  |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageD2|  

|imageD2_w|  

Clip layers to country boundary
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

At this stage we can now clip the final aggregated datasets to the country boundary (remember that up to this point we have used a bounding box of the country boundary buffered out by 10km).

-  In the **processing toolbox** search for **Clip Raster by Mask Layer** 
-  Set the **Input layer** the **aggregated combined vegetation + mountain descriptor layer** e.g. veg10_mountain.tif
-  Set the **mask layer** to the **polygon country boundary in equal area projection** e.g. BND_CTR_LAEA
-  Set the **Source CRS** and the **Target CRS** to be the equal area projection
-  **Tick Match the extent of the clipped raster to the extent of the mask layer**
-  **Tick Keep resolution of input raster**
-  Set the **Clipped (mask) output** to e.g. veg10_mountain_CTRY_clip.tif
-  Click **Run** to run the tool

   |image175|
   
-  Repeat the above step for the resampled RSA raster.

   |image176|
   
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **MGCI Toolbox D3. Generic:  Clip to country boundary**:                                                                                                  |
|    :name: toolbox_D3                                                                                                                                                  |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageD3|  

|imageD3_w|

Computation of Mountain Green Cover Index
-----------------------------------------
Generate Real Surface Area and Planimetric Area Statistics
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The data are now in a consistent format and clipped to the country boundary, so we can now generate the statistics required for the MGCI reporting. As we want to generate disaggregated statistics by LULC class and Mountain Class we will use a zonal statistics tool with the combined Vegetation + mountain  layer as the summary unit and the RSA raster as the summary layer. The Zonal statistics tool will automatically calculate planimetric area in the output.

This output is the main statistics table from the analysis, from which other summary statistics tables will be generated.

-  In the **processing toolbox** search for Zonal Statistics

-  Double click on the **Raster Layer Zonal Statistics** tool
-  Set the **input layer** to the **Aggregated Real Surface Area raster clipped to the country boundary**
-  Set the **zones layer** to the **combined vegetation and mountain layer clipped to the country boundary**
-  Save the **Statistics output to a .csv file** e.g. rsastats.csv

   |image177|
   
The Planimetric area generated in m2 rather than km2 and will be stored in a field called m2

-  In the **processing Toolbox** search for **Rename Field** 
-  Set the field to rename as **m2**
-  Set the **New field name** to **PlanimetricArea_m2**
-  Save the **Renamed output to a .csv file** e.g. MGCI_stats.csv

   |image178|

**Important Note:**
When the statistics .csv files  added to the QGIS project it **does not add it correctly using delimited text** if you are saving to an output file rather than a temporary file. This means that all the fields are viewedas string. Remove the MGCI_stats.csv from the QGIS project and re-add it using Layer>>AddLayer>>Add Delimited Text Layer or save as a temporary layer which you can rightclick on an export later. This applies to each of the next steps.  If you do not to this the following steps run only from the MGCI toolbox will fail to run. 

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **E1. MGCI:  Generate RSA and Planimetric Area Statistics**:                                                                                              |
|    :name: toolbox_D3                                                                                                                                                  |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| **Also note:** The tool in the MGCI toolbox includes the above steps but also does some further refinement to add some additional fields to convert the RSA and       |
| Planimetric Area into km2 and drop any unrequired fields generated by the zonal statistics function. It also joins on some additional fields from a template file     |
|                                                                                                                                                                       |
| MGCI_classes_template.csv                                                                                                                                             |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageE1|

|imageE1_w| 

***The following steps will only be run from the custom MGCI toolbox. We did not feel there was benefit to detailing the many tabular joins required to create the summary tables and standard reporting tables. Users can explore the models in the model designer to explore the steps further.*** 

This last step does the the Mountain Green Cover Index Calculation and outputs the 3 standard reporting tables

Create summary statistics by green cover and Mountain class
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Export to standard reporting table
----------------------------------
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **F1: Formatting Reporting Tables: Planimetric Area**:                                                                                                    |
|    :name: toolbox_F1                                                                                                                                                  |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageF1| 

|imageF1_w| 

+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| .. rubric:: **Formatting Reporting Tables: Real Surface Area**:                                                                                                       |
|    :name: toolbox_F1                                                                                                                                                  |
|                                                                                                                                                                       |
| These steps can be run using a single tool in the MGCI toolbox.                                                                                                       |
|                                                                                                                                                                       |
| In the **custom MGCI toolbox** these step are run by the tool below                                                                                                   |
|                                                                                                                                                                       |
| The workflow steps can be viewed QGIS Model Designer                                                                                                                  |
|                                                                                                                                                                       |
+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------+

|imageF2|

|imageF2_w| 

.. |image0| image:: media_QGIS/image2.png
   :width: 6.26806in
   :height: 3.16875in
.. |image1| image:: media_QGIS/image3.png
   :width: 6.26806in
   :height: 5.06528in
.. |image2| image:: media_QGIS/image4.png
   :width: 6.26806in
   :height: 0.81458in
.. |image3| image:: media_QGIS/image5.png
   :width: 6.26806in
   :height: 1.65347in
.. |image4| image:: media_QGIS/image6.png
   :width: 6.26806in
   :height: 3.97847in
.. |image5| image:: media_QGIS/image7.png
   :width: 5.97917in
   :height: 4.25867in
.. |image6| image:: media_QGIS/image8.png
   :width: 6.03472in
   :height: 4.75909in
.. |image7| image:: media_QGIS/image9.png
   :width: 6.26806in
   :height: 4.46458in
.. |image8| image:: media_QGIS/image10.png
   :width: 6.26806in
   :height: 3.33742in
.. |image9| image:: media_QGIS/image11.png
   :width: 5.52160in
   :height: 0.94805in
.. |image10| image:: media_QGIS/image12.png
   :width: 6.26806in
   :height: 3.70278in
.. |image11| image:: media_QGIS/image13.png
   :width: 4.42770in
   :height: 4.71941in
.. |image12| image:: media_QGIS/image14.png
   :width: 4.42653in
   :height: 4.71816in
.. |image13| image:: media_QGIS/image15.png
   :width: 3.44840in
   :height: 1.83359in
.. |image14| image:: media_QGIS/image16.png
   :width: 0.43750in
   :height: 0.35417in
.. |image15| image:: media_QGIS/image17.png
   :width: 3.21875in
   :height: 1.13542in
.. |image16| image:: media_QGIS/image18.png
   :width: 6.26806in
   :height: 2.56667in
.. |image17| image:: media_QGIS/image19.png
   :width: 2.32263in
   :height: 0.97904in
.. |image18| image:: media_QGIS/image20.png
   :width: 6.26806in
   :height: 3.45417in
.. |image19| image:: media_QGIS/image21.png
   :width: 5.21948in
   :height: 1.75024in
.. |image20| image:: media_QGIS/image22.png
   :width: 1.95347in
   :height: 2.17361in
.. |image21| image:: media_QGIS/image23.png
   :width: 5.10417in
   :height: 1.21875in
.. |image22| image:: media_QGIS/image24.png
   :width: 5.75000in
   :height: 3.93750in
.. |image23| image:: media_QGIS/image25.png
   :width: 0.29861in
   :height: 0.29276in
.. |image24| image:: media_QGIS/image26.png
   :width: 6.26806in
   :height: 3.40417in
.. |image25| image:: media_QGIS/image27.png
   :width: 6.26806in
   :height: 3.59931in
.. |image26| image:: media_QGIS/image28.png
   :width: 3.18056in
   :height: 2.63633in
.. |image27| image:: media_QGIS/image29.png
   :width: 6.26806in
   :height: 2.40000in
.. |image28| image:: media_QGIS/image30.png
   :width: 5.48788in
   :height: 5.13889in
.. |image29| image:: media_QGIS/image31.png
   :width: 5.43750in
   :height: 3.10009in
.. |image30| image:: media_QGIS/image32.png
   :width: 3.37547in
   :height: 4.79234in
.. |image31| image:: media_QGIS/image33.png
   :width: 6.26806in
   :height: 2.66389in
.. |image32| image:: media_QGIS/image34.png
   :width: 900
.. |image33| image:: media_QGIS/image35.png
   :width: 625
.. |image34| image:: media_QGIS/image36.png
   :width: 275
.. |image35| image:: media_QGIS/image37.png
   :width: 900
.. |image36| image:: media_QGIS/image38.png
   :width: 900
.. |image37| image:: media_QGIS/image39.png
   :width: 900
.. |image38| image:: media_QGIS/image40.png
   :width: 900
.. |image39| image:: media_QGIS/image41.png
   :width: 900
   
.. |image40| image:: media_QGIS/image42.png
   :width: 600

.. |image41| image:: media_QGIS/image43.png
   :width: 900
.. |image42| image:: media_QGIS/image44.png
   :width: 900
.. |image43| image:: media_QGIS/image45.png
   :width: 900
.. |image44| image:: media_QGIS/image46.png
   :width: 900
.. |image45| image:: media_QGIS/image47.png
   :width: 900
.. |image46| image:: media_QGIS/image48.png
   :width: 600

.. |image47| image:: media_QGIS/image49.png
   :width: 300

.. |image48| image:: media_QGIS/image50.png
   :width: 900
   
.. |image49| image:: media_QGIS/image51.png
   :width: 300

.. |image50| image:: media_QGIS/image52.png
   :width: 900
.. |image51| image:: media_QGIS/image53.png
   :width: 900
.. |image52| image:: media_QGIS/image54.png
   :width: 900
.. |image53| image:: media_QGIS/image55.png
   :width: 900
   
.. |image54| image:: media_QGIS/image56.png
   :width: 400

.. |image55| image:: media_QGIS/image57.png
   :width: 900
.. |image56| image:: media_QGIS/image58.png
   :width: 900
.. |image57| image:: media_QGIS/image54.png
   :width: 900
   
.. |image58| image:: media_QGIS/image59.png
   :width: 300
   
.. |image59| image:: media_QGIS/image60.png
   :width: 900
.. |image60| image:: media_QGIS/image61.png
   :width: 900
.. |image61| image:: media_QGIS/image62.png
   :width: 900
.. |image62| image:: media_QGIS/image58.png
   :width: 900
.. |image63| image:: media_QGIS/image54.png
   :width: 900
.. |image64| image:: media_QGIS/image63.png
   :width: 900
   
.. |image65| image:: media_QGIS/image64.png
   :width: 300
   
.. |image66| image:: media_QGIS/image65.png
   :width: 900
   
.. |image67| image:: media_QGIS/image66.png
   :width: 900
.. |image68| image:: media_QGIS/image67.png
   :width: 900
   
.. |image69| image:: media_QGIS/image68.png
   :width: 900

.. |image70| image:: media_QGIS/image69.png
   :width: 300

.. |image71| image:: media_QGIS/image70.png
   :width: 600

.. |image72| image:: media_QGIS/image71.png
   :width: 600
   
.. |image73| image:: media_QGIS/image72.png
   :width: 900
.. |image74| image:: media_QGIS/image73.png
   :width: 900
.. |image75| image:: media_QGIS/image74.png
   :width: 900
.. |image74a| image:: media_QGIS/image74a.png
   :width: 900
.. |image74b| image:: media_QGIS/image74b.png
   :width: 900
.. |image76| image:: media_QGIS/image75.png
   :width: 900
.. |image77| image:: media_QGIS/image76.png
   :width: 900
.. |image78| image:: media_QGIS/image77.png
   :width: 900
 
.. |image79| image:: media_QGIS/image78.png
   :width: 900
   
.. |image80| image:: media_QGIS/image79.png
   :width: 300
   
.. |image81| image:: media_QGIS/image80.png
   :width: 900
.. |image82| image:: media_QGIS/image81.png
   :width: 900
.. |image83| image:: media_QGIS/image82.png
   :width: 900
.. |image84| image:: media_QGIS/image83.png
   :width: 200
.. |image85| image:: media_QGIS/image84.png
   :width: 900
.. |image86| image:: media_QGIS/image85.png
   :width: 900
.. |image87| image:: media_QGIS/image86.png
   :width: 900
.. |image88| image:: media_QGIS/image80.png
   :width: 900
.. |image89| image:: media_QGIS/image87.png
   :width: 900
.. |image90| image:: media_QGIS/image88.png
   :width: 900
.. |image91| image:: media_QGIS/image89.png
   :width: 900
.. |image92| image:: media_QGIS/image90.png
   :width: 900
.. |image93| image:: media_QGIS/image91.png
   :width: 200
.. |image94| image:: media_QGIS/image92.png
   :width: 900
.. |image95| image:: media_QGIS/image93.png
   :width: 900
.. |image96| image:: media_QGIS/image94.png
   :width: 300
.. |image97| image:: media_QGIS/image95.png
   :width: 900
.. |image98| image:: media_QGIS/image96.png
   :width: 900
.. |image99| image:: media_QGIS/image97.png
   :width: 900
.. |image100| image:: media_QGIS/image98.png
   :width: 900
.. |image101| image:: media_QGIS/image99.png
   :width: 900
.. |image102| image:: media_QGIS/image100.png
   :width: 900
.. |image103| image:: media_QGIS/image101.png
   :width: 900
.. |image104| image:: media_QGIS/image101.png
   :width: 900
.. |image105| image:: media_QGIS/image102.png
   :width: 900
.. |image106| image:: media_QGIS/image103.png
   :width: 900
.. |image107| image:: media_QGIS/image104.png
   :width: 900
.. |image108| image:: media_QGIS/image105.png
   :width: 900
.. |image109| image:: media_QGIS/image106.png
   :width: 900
.. |image110| image:: media_QGIS/image107.png
   :width: 900
.. |image111| image:: media_QGIS/image108.png
   :width: 900
.. |image112| image:: media_QGIS/image109.png
   :width: 900
.. |image113| image:: media_QGIS/image110.png
   :width: 900
.. |image114| image:: media_QGIS/image111.png
   :width: 900
.. |image115| image:: media_QGIS/image112.png
   :width: 300
.. |image116| image:: media_QGIS/image113.png
   :width: 900
.. |image117| image:: media_QGIS/image114.png
   :width: 900
.. |image118| image:: media_QGIS/image115.png
   :width: 900
.. |image119| image:: media_QGIS/image116.png
   :width: 900
.. |image120| image:: media_QGIS/image117.png
   :width: 900
.. |image121| image:: media_QGIS/image118.png
   :width: 900
.. |image122| image:: media_QGIS/image119.png
   :width: 900
.. |image123| image:: media_QGIS/image120.png
   :width: 900
.. |image124| image:: media_QGIS/image121.png
   :width: 900
.. |image125| image:: media_QGIS/image122.png
   :width: 900
.. |image126| image:: media_QGIS/image123.png
   :width: 900
.. |image127| image:: media_QGIS/image124.png
   :width: 900
.. |image128| image:: media_QGIS/image125.png
   :width: 900
.. |image129| image:: media_QGIS/image126.png
   :width: 900
.. |image130| image:: media_QGIS/image127.png
   :width: 900
.. |image131| image:: media_QGIS/image128.png
   :width: 900
.. |image132| image:: media_QGIS/image129.png
   :width: 900
.. |image133| image:: media_QGIS/image130.png
   :width: 900
.. |image134| image:: media_QGIS/image131.png
   :width: 900
.. |image135| image:: media_QGIS/image132.png
   :width: 300
.. |image136| image:: media_QGIS/image133.png
   :width: 900
.. |image137| image:: media_QGIS/image134.png
   :width: 900
.. |image138| image:: media_QGIS/image135.png
   :width: 900
.. |image139| image:: media_QGIS/image136.png
   :width: 900
.. |image140| image:: media_QGIS/image137.png
   :width: 900
.. |image141| image:: media_QGIS/image138.png
   :width: 900
.. |image142| image:: media_QGIS/image139.png
   :width: 900
.. |image143| image:: media_QGIS/image140.png
   :width: 900
.. |image144| image:: media_QGIS/image141.png
   :width: 900
.. |image145| image:: media_QGIS/image142.png
   :width: 900
.. |image146| image:: media_QGIS/image143.png
   :width: 900
.. |image147| image:: media_QGIS/image144.png
   :width: 900
.. |image148| image:: media_QGIS/image145.png
   :width: 900
.. |image149| image:: media_QGIS/image146.png
   :width: 900
.. |image150| image:: media_QGIS/image147.png
   :width: 900
.. |image151| image:: media_QGIS/image148.png
   :width: 900
.. |image152| image:: media_QGIS/image149.png
   :width: 900
.. |image153| image:: media_QGIS/image150.png
   :width: 900
.. |image154| image:: media_QGIS/image151.png
   :width: 900
.. |image155| image:: media_QGIS/image152.png
   :width: 900
.. |image156| image:: media_QGIS/image153.png
   :width: 900
.. |image157| image:: media_QGIS/image154.png
   :width: 900
.. |image158| image:: media_QGIS/image155.png
   :width: 900
.. |image159| image:: media_QGIS/image156.png
   :width: 900
.. |image160| image:: media_QGIS/image157.png
   :width: 900
.. |image161| image:: media_QGIS/image158.png
   :width: 900
.. |image162| image:: media_QGIS/image159.png
   :width: 900
.. |image163| image:: media_QGIS/image160.png
   :width: 900
.. |image164| image:: media_QGIS/image161.png
   :width: 900
.. |image165| image:: media_QGIS/image162.png
   :width: 900
.. |image166| image:: media_QGIS/image163.png
   :width: 900
.. |image167| image:: media_QGIS/image164.png
   :width: 900
.. |image168| image:: media_QGIS/image165.png
   :width: 900
.. |image169| image:: media_QGIS/image166.png
   :width: 900
.. |imagetoolbox| image:: media_QGIS/Toolbox_images/toolbox.PNG
   :width: 900
.. |image170| image:: media_QGIS/image170.png
   :width: 900
.. |image171| image:: media_QGIS/image171.png
   :width: 900
.. |image172| image:: media_QGIS/i1_aoi_tool.png
   :width: 900
.. |image173| image:: media_QGIS/image173.png
   :width: 900
.. |image173| image:: media_QGIS/image173.png
   :width: 900
.. |image174| image:: media_QGIS/image174.png
   :width: 900
.. |image175| image:: media_QGIS/image175.png
   :width: 900
.. |image176| image:: media_QGIS/image176.png
   :width: 900
.. |image177| image:: media_QGIS/image177.png
   :width: 900
.. |image178| image:: media_QGIS/image178.png
   :width: 900

.. |imageA1| image:: media_QGIS/Toolbox_images/A1.png
   :width: 1100
.. |imageA1_w| image:: media_QGIS/Toolbox_images/A1_w.png
   :width: 600
   
.. |imageA2a| image:: media_QGIS/Toolbox_images/A2a.png
   :width: 1100
    
.. |imageA2a_w| image:: media_QGIS/Toolbox_images/A2a_w.png
   :width: 600
   
.. |imageA2b| image:: media_QGIS/Toolbox_images/A2b.png
   :width: 1100

.. |imageA2b_w| image:: media_QGIS/Toolbox_images/A2b_w.png
   :width: 600
   
.. |imageA2c| image:: media_QGIS/Toolbox_images/A2c.png
   :width: 1100
   
.. |imageA2c_w| image:: media_QGIS/Toolbox_images/A2c_w.png
   :width: 800
   
.. |imageA3| image:: media_QGIS/Toolbox_images/A3.png
   :width: 1100
   
.. |imageA3_w| image:: media_QGIS/Toolbox_images/A3_w.png
   :width: 800
   
.. |imageB1| image:: media_QGIS/Toolbox_images/B1.png
   :width: 1100

.. |imageB1_w| image:: media_QGIS/Toolbox_images/B1_w.png
   :width: 600

.. |imageB2| image:: media_QGIS/Toolbox_images/B2.png
   :width: 1100
 
.. |imageB2_w| image:: media_QGIS/Toolbox_images/B2_w.png
   :width: 600
   
.. |imageB3| image:: media_QGIS/Toolbox_images/B3.png
   :width: 1100
  
.. |imageB3_w| image:: media_QGIS/Toolbox_images/B3_w.png
    :width: 1100
     
.. |imageB4| image:: media_QGIS/Toolbox_images/B4.png
   :width: 1100
 
.. |imageB4_w| image:: media_QGIS/Toolbox_images/B4_w.png
   :width: 600
.. |imageB4a| image:: media_QGIS/Toolbox_images/B4a.png
   :width: 1100
 
.. |imageB4a_w| image:: media_QGIS/Toolbox_images/B4a_w.png
   :width: 800

.. |imageB4b| image:: media_QGIS/Toolbox_images/B4b.png
   :width: 1100
 
.. |imageB4b_w| image:: media_QGIS/Toolbox_images/B4b_w.png
   :width: 800
.. |imageB5| image:: media_QGIS/Toolbox_images/B5.png
    :width: 1100

.. |imageB5_w| image:: media_QGIS/Toolbox_images/B5_w.png
   :width: 600
   
.. |imageB6a| image:: media_QGIS/Toolbox_images/B6a.png
   :width: 1100
   
.. |imageB6a_w| image:: media_QGIS/Toolbox_images/B6a_w.png
   :width: 1100
 
.. |imageB6b| image:: media_QGIS/Toolbox_images/B6b.png
   :width: 1100
   
.. |imageB6b_w| image:: media_QGIS/Toolbox_images/B6b_w.png
   :width: 1100
   
.. |imageB7| image:: media_QGIS/Toolbox_images/B7.png
   :width: 1100
 
.. |imageB7_w| image:: media_QGIS/Toolbox_images/B7_w.png
   :width: 1100


.. |imageB8| image:: media_QGIS/Toolbox_images/B8.png
   :width: 1100
 
.. |imageB8_w| image:: media_QGIS/Toolbox_images/B8_w.png
   :width: 1100

.. |imageB9| image:: media_QGIS/Toolbox_images/B9.png
   :width: 1100
 
.. |imageB9_w| image:: media_QGIS/Toolbox_images/B9_w.png
   :width: 1100
   
   
.. |imageC1| image:: media_QGIS/Toolbox_images/C1.png
   :width: 1100
  
.. |imageC1_w| image:: media_QGIS/Toolbox_images/C1_w.png
   :width: 600

   
.. |imageD1| image:: media_QGIS/Toolbox_images/D1.png
   :width: 1100

.. |imageD1_w| image:: media_QGIS/Toolbox_images/D1_w.png
   :width: 1100

.. |imageD1a| image:: media_QGIS/Toolbox_images/D1a.png
   :width: 1100

.. |imageD1a_w| image:: media_QGIS/Toolbox_images/D1a_w.png
   :width: 1100

.. |imageD1b| image:: media_QGIS/Toolbox_images/D1b.png
   :width: 1100

.. |imageD1b_w| image:: media_QGIS/Toolbox_images/D1b_w.png
   :width: 1100

.. |imageD2| image:: media_QGIS/Toolbox_images/D2.png
   :width: 1100

.. |imageD2_w| image:: media_QGIS/Toolbox_images/D2_w.png
   :width: 600

.. |imageD3| image:: media_QGIS/Toolbox_images/D3.png
   :width: 1100
 
.. |imageD3_w| image:: media_QGIS/Toolbox_images/D3_w.png
   :width: 1100

.. |imageE1| image:: media_QGIS/Toolbox_images/E1.PNG
   :width: 1100
 
.. |imageE1_w| image:: media_QGIS/Toolbox_images/E1_w.PNG
   :width: 1100

.. |imageF1| image:: media_QGIS/Toolbox_images/F1.PNG
   :width: 1100

.. |imageF1_w| image:: media_QGIS/Toolbox_images/F1w.png
   :width: 1100

.. |imageF2| image:: media_QGIS/Toolbox_images/F2.PNG
   :width: 1100

.. |imageF2_w| image:: media_QGIS/Toolbox_images/F2w.png
   :width: 1100
   
.. |toolbox_access| image:: media_QGIS/Toolbox_images/toolbox_access.png
   :width: 600   
   
.. |imagesettings| image:: media_QGIS/settings.png
   :width: 900

.. |imagerepository1| image:: media_QGIS/repository.png
   :width: 900

.. |imagerepository2| image:: media_QGIS/repository2.png
   :width: 600

.. |imagerepository3| image:: media_QGIS/repository3.png
   :width: 900
.. |imagescale_table| image:: media_QGIS/scale_table.png
   :width: 500
.. |imagemin_bou| image:: media_QGIS/min_bou.png
   :width: 400
.. |imagebuffer| image:: media_QGIS/buffer.png
   :width: 400
.. |imagerasterize| image:: media_QGIS/rasterize.png
   :width: 400
.. |imageslopemask| image:: media_QGIS/slopemask.png
   :width: 900
   .. |imageslopemask| image:: media_QGIS/slopemask.png
   :width: 900
.. |extract_layer_extent| image:: media_QGIS/extract_layer_extent.png
   :width: 300
.. |imageneighbors| image:: media_QGIS/neighbors.png
   :width: 400
.. |imagersa1| image:: media_QGIS/rsa1.png
   :width: 900
.. |imagersa2| image:: media_QGIS/rsa2.png
   :width: 900
.. |imageresamp| image:: media_QGIS/resamp.png
   :width: 400
   
.. |extent_attr| image:: media_QGIS/extent_attr.png
   :width: 900
.. |extract_layer_extent2| image:: media_QGIS/extract_layer_extent2.png
   :width: 900
.. |extent_attr_width| image:: media_QGIS/extent_attr_width.png
   :width: 900
.. |extent_attr_height| image:: media_QGIS/extent_attr_height.png
   :width: 900
.. |creategrid| image:: media_QGIS/creategrid.png
   :width: 300
.. |reprojequi| image:: media_QGIS/reprojequi.png
   :width: 900
.. |buffequi| image:: media_QGIS/buffequi.png
   :width: 900
.. |intersection| image:: media_QGIS/intersection.png
   :width: 300
.. |intersection2| image:: media_QGIS/intersection2.png
   :width: 900
.. |intersection3| image:: media_QGIS/intersection3.png
   :width: 900
.. |manualiterate| image:: media_QGIS/manualiterate.png
   :width: 900
.. |reprojequi2| image:: media_QGIS/reprojequi2.png
   :width: 900
.. |creategrid3| image:: media_QGIS/creategrid3.png
   :width: 900
.. |creategrid2| image:: media_QGIS/creategrid2.png
   :width: 900
.. |rmask| image:: media_QGIS/rmask.png
   :width: 300
.. |mergeslope1| image:: media_QGIS/mergeslope1.png
   :width: 900
.. |mergeslope2| image:: media_QGIS/mergeslope2.png
   :width: 900
.. |mergedslope| image:: media_QGIS/mergedslope.png
   :width: 900
.. |slopeinequalarea| image:: media_QGIS/slopeinequalarea.png
   :width: 900
.. |mergedLER7km| image:: media_QGIS/mergedLER7km.png
   :width: 900
.. |mergeLER7km_1| image:: media_QGIS/mergeLER7km_1.png
   :width: 900
.. |LER7kminequalarea| image:: media_QGIS/LER7kminequalarea.png
   :width: 900
   
   



