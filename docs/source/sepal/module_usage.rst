The SEPAL interface and the SEPAL-SDG 15.4.2
============================================

New SEPAL users are recommended to look over the interface and familiarize themselves with the SEPAL interface, main tools, functionalities and workflows. A detailed description of the features can be consulted in the `SEPAL documentation <https://docs.sepal.io/en/latest/setup/presentation.html#sepal-interface>`_.


Accessing SEPAL-SDG 15.4.2 
----------------------------

To open the SEPAL-SDG 15.4.2 module, click on the **apps tab** and search for the SDG 15.4.2 module among the apps, alternatively, you can type in the search box "SDG 15.4.2". Click on the app drawer and wait a few minutes for the module to load. 
  
.. image:: ../_static/sepal/updates_26/finding_sepal.png
   :align: center
   :width: 1350
   :alt: Accessing_module

The module's interface is divided into two main sections as shown below:

.. image:: ../_static/sepal/updates_26/sepal_main_interface.png
   :align: center
   :width: 1350
   :alt: Accessing_module

- **Process steps**: Located on the top left of the interface, the process steps contain the processing steps to run the module: 1. Area of Interest; 2. Land cover dataset; 3. Indicator settings; 4. Results and Export from task. Each step opens in a window. Use **Next** and **Back** at the bottom of the window to move between the steps, and **Close** to go back to the map.

- **Help links**: Located at the bottom left of the interface, they open the source code (the module was developed under a MIT license, which means that the module is freely accessible, and the code is hosted publicly in GitHub), this documentation, and the bug report page (report of unexpected results or behavior).

- **Results panel**: The chart icon on the right side of the map opens the results panel. More on the results will be elaborated in future sections.

- **Notifications**: The module shows its messages as notifications. Error notifications stay on the screen until you click them. The clock icon at the bottom right of the map shows the previous notifications.


Personalising SEPAL-SDG 15.4.2 
--------------------------------

SEPAL-SDG 15.4.2 allows users to personalize its appearance to suit their preferences.

**Theme customisation:**
Users can choose between an automatic, a dark or a light theme. The automatic theme follows the settings of your computer. To change the theme, click the theme icon, located at the bottom left panel, below the help links. Each click selects the next theme, and the change applies immediately.

.. image:: ../_static/sepal/updates_26/Theme_customization.png
   :align: center
   :width: 900
   :alt: Module_personalization


**Language selection:**

SEPAL-SDG 15.4.2 is available in English, French and Spanish. To change the language, click the language button (**EN**) at the bottom left panel, next to the theme icon, and select a language. The module changes the language immediately.

.. image:: ../_static/sepal/updates_26/language_selection.png
   :align: center
   :width: 400
   :alt: Language selection

.. note:: The reporting tables, the default names of the exported layers and their metadata stay in English in all languages, as SDG reporting requires.



Calculating SDG Indicator 15.4.2
--------------------------------

Conceptual framework
^^^^^^^^^^^^^^^^^^^^
This section covers the  rationale behind SDG Indicator 15.4.2 computation. Simply put,the indicator monitors mountain ecosystem health by assessing changes in green cover and land cover across mountain bioclimatic belts using four key inputs: land cover data, a digital elevation model, a mountain area map, and a national administrative boundary layer.

Overview of Sub-Indicator 15.4.2a : Mountain Green Cover Index (MGCI)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Sub-indicator 15.4.2a, Mountain Green Cover Index (MGCI)**, is designed to measure the extent and changes of green cover - i.e. forest, shrubs, trees, pasture land, cropland, etc. – in mountain areas. MGCI is defined as the percentage of green cover over the total surface of the mountain area of a given country and for given reporting year. The aim of the index is to monitor the evolution of the green cover and thus assess the status of conservation of mountain ecosystems. 

.. math::

   MGCI = \frac{\text{Mountain Green Cover Area}_n}{\text{Total Mountain Area}} \times 100

Where: 

- **Mountain Green Cover Area n** = Sum of areas (in km2) covered by (1) tree-covered areas, (2) croplands,(3) grasslands, (4) shrub-covered areas and (5) shrubs and/or herbaceous vegetation, aquatic or regularly flooded classes in the reporting period n 
- **Total mountain area** = Total area of mountains (in km2). In both the numerator and denominator, mountain area is defined according to UNEP-WCMC (2002).

Overview of Sub-Indicator 15.4.2b : Proportion of degraded mountain land
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**Sub-indicator 15.4.2b, Proportion of degraded mountain land**, is designed to monitor the extent of degraded mountain land as a result of land cover change in a given country and for given reporting year. Similarly to sub-indicator "trends in land cover" under SDG Indicator 15.3.1 (Sims et al. 2021), mountain ecosystem degradation and recovery is assessed based on the definition of land cover type transitions that constitute degradation, as either improving, stable or degraded. The indicator adopts the definition of degradation established by the Intergovernmental Science-Policy Platform on Biodiversity and Ecosystem Services (IPBES) in its computation.

.. math::

   \text{Proportion of Degraded Mountain Land} = \frac{\text{Degraded Mountain Area}_n}{\text{Total Mountain Area}} \times 100

Where:

- **Degraded mountain area n** = Total degraded mountain area (in km2) in the reporting period n. This is, the sum of the areas where land cover change is considered to constitute degradation from the baseline period. Degraded mountain land will be assessed based on the land cover transition matrix in Annex 1.
- **Total mountain area** = Total area of mountains (in km2). In both the numerator and denominator, mountain area is defined according to UNEP-WCMC (2002).

**Disaggregation:**

Both of these sub-indicators are disaggregated by mountain bioclimatic belts as defined by Körner et al. (2011). In addition, land cover in sub-indicator 15.4.2a is
disaggregated into the 10 SEEA classes based on UN Statistical Division (2014).  Those values are reported both as proportions (percent) and area (in square kilometres)

More detailed information on the overall conceptual framework of the indicator is available in the `indicator's metadata <https://unstats.un.org/sdgs/metadata/files/Metadata-15-04-02.pdf>`_.


**To illustrate, we will compute SDG 15.4.2 using Nepal as an example. Throughout the tutorial, we will assume all the default options and datasets available in the application.**


Defining the Area of Interest (AoI)
-----------------------------------

The calculation of the SDG 15.4.2 is restricted to a specific area of interest defined by the user. In this first step, you will have the option to choose between a predefined list of administrative layers or to use a custom dataset to delineate the computational area.

**1. Click on 1. Area of Interest in the process steps to define your AOI.** 

A pop-up will display the following available options to set your AOI: 

- Administrative definitions
- Custom layers

.. image:: ../_static/sepal/updates_26/Aoi_selector.png
   :align: center
   :width: 600
   :alt: Defining_AOI


**2. The Administrative definitions option presents the default administrative boundary dataset (GAUL,2015). Users have three scale options to choose from ; Country/Province, Admin level 1 (provinces, states or regions) and Admin level 2 (district, counties or municipalities ).To define the Area of Interest using this option, :**

- Select **Country/Province** under Administrative definitions.
- In the dropdown list, select the country or territory to calculate SDG Indicator 15.4.2. In this example, we will select Nepal, as shown below.

.. image:: ../_static/sepal/updates_26/aoi_method_countries.png
   :align: center
   :width: 600
   :alt: selecting_nepal


- Clicking on **Select AOI** will display your selection on the map area alongside a corresponding legend.The algorithm automatically generates a legend based on the four mountain bioclimatic belt classes and the area for each as defined in the global mountain map developed by FAO to compute this indicator. Click **Close** to see the map, or **Next** to go to the land cover dataset step. You can hide the bioclimatic belts and show them again in the Results panel (see :ref:`Visualising the results through the Results Panel <ResultsPanel>`).

.. image:: ../_static/sepal/updates_26/AOI_displayed.png
   :align: center
   :width: 600
   :alt: displaying_AOI

.. warning:: The  administrative boundaries available SEPAL-SDG 15.4.2 are extracted from the FAO Global Administrative Unit Layers (GAUL,2015) dataset. The designations employed in the presentation of material on this map do not imply the expression of any opinion whatsoever on the part of the United Nations Secretariat concerning the legal status of any country, territory, city or area or of its authorities, or concerning the delimitation of its frontiers or boundaries. 


**Using Custom Geometries**

**3. The Custom layers option allows users to use their own national administrative boundary layers.** The boundary layer must be a vector file (for example a shapefile or GeoJSON) uploaded to Google Earth Engine (GEE) as an asset to be used. To define the AOI using this method;

- Choose **GEE Asset Name** as your AOI selection method.
- Copy the **Asset ID** in GEE and paste under "Select an asset", or select the asset in the dropdown list.
- In **Column**, keep "All features" to use the whole asset, or select a column and a value to use only some features. Then click **Select AOI**.

.. image:: ../_static/sepal/updates_26/aoi_method_gee.png
   :align: center
   :width: 600
   :alt: Defining AOI using GEE Asset



Land Cover Dataset 
-------------------

This section of the documentation covers the configuration of the land cover dataset for the computation of SDG Indicator 15.4.2.


Defining your land cover dataset 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

**1. Click on the Land cover dataset in the process steps located in the left panel to open the land cover dataset selector, as shown below:**

.. image:: ../_static/sepal/updates_26/landcover_questionnaire.png
   :align: center
   :width: 700
   :alt: land cover module


**2. The panel presents two questions. The second question depends on the answer to the first one:**

**Would you like to select or reclassify a land use/land cover map?**

- Select **Yes** to use national land cover maps to compute both sub-indicators.
- Select **No**  to use the default global land cover time series .

If you select **No**, the second question is **Would you like to change the default land cover transition matrix?**

- Select **Yes** to modify the default land cover transition matrix to compute sub-indicator B.
- Select **No** to use the default transition matrix (UN-SEEA classes derived).

If you select **Yes**, the second question is **Do you need to reclassify the selected land use/cover map to UN-SEEA classification?**

- Select **Yes** to reclassify the classes of your land cover map for each sub-indicator, and to upload a custom transition matrix.
- Select **No** if your land cover map already uses the UN-SEEA classification. The module then uses the default transition matrix.

Then click **Set up land cover** to open the land cover settings. In this window, click **Validate & close** to keep your settings, or **Close** to discard the changes.

We will look at each scenario individually:

Using the Default Land cover Maps
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When custom national land cover maps are not available, national agencies can use the default land cover dataset available in SEPAL-SDG 15.4.2.

After clicking on **No** to the first question,you have a choice to modify the land cover transition matrix or use the default one.If using the default one, click **No** to the transition matrix question and proceed to the :ref:`Defining the Indicator Settings Chapter <Indicator Settings>`. The default dataset is ready to use: you do not need to open the land cover settings.

In the case where national agencies want to modify the land cover transition matrix,the process is described :ref:`here <Defaultlccustommatrix>`.

Using Custom Land cover maps
~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Select **Yes** to the first question, answer the reclassification question, and then click on **Set up land cover** .

- This opens a new pop-up window that allows you to select your land cover maps as a GEE asset (remember that they must be stored as a `GEE image collection <https://developers.google.com/earth-engine/guides/ic_creating>`_ to be imported.Individual images will not be recognized by the app). Use the bottom arrow to choose your asset or copy/paste it directly from GEE. If you reclassify your map, click on **Get classes** to read the land cover classes of the collection. If you do not reclassify it, the module reads the collection when you select it.

.. image:: ../_static/sepal/updates_26/custom_lc_selection.png
   :width: 700
   :alt: custom_landcover map

.. note:: Choosing Yes in the first question and No in the second, will have the model assume that the selected land cover map is already classified according to the UN-SEEA classification and it will use the default transition matrix. In some cases, national authorities might opt to use the default land cover map but still define a custom transition matrix to capture local degradation characteristics. More on this will be described in the next section.

.. image:: ../_static/sepal/updates_26/custom_lc_default_reclass.png
   :width: 700
   :alt: custom_landcover_default_transition.


**3. For the case of Nepal, we will use the default land cover map and transition matrix. Therefore, we select** **No** **to both questions, then click on** **Next** **to proceed to the indicator settings.**


Reclassifying the land cover map legend for sub-Indicator A computation.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. important:: The UN-SEEA land cover classification is the default classification scheme adopted for this sub-indicator. National agencies must adapt their land cover classes to match the UN-SEEA one for sub-indicator A computation.


Reclassification can be done in two different ways; By manually assigning your source and target land classes or by uploading a reclassification matrix.

Using a reclassification matrix
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. _reclass_table:

  .. tip:: What is a reclassification matrix table?

     A reclassification matrix is a comma-separated values (CSV) file used to reclassify old pixel values into new ones. The CSV file only has to contain two values per line, the first one refers to the `from` value, while the second is the `target` value, just as it is described in the following table: 

      .. csv-table:: Reclassification table example
         :header: "Origin class", "Target class"
         :widths: auto
         :align: center

         "311", "1"
         "111", "5"
         "...","..."
         "511", "4"




Uploading a reclassification matrix
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

- To upload a custom reclassification matrix, click on the arrow icon :guilabel:`⬆`  in the top right corner of the reclassification table (see the image below). In the **Load remapping table** window, click **Filename** and select your file.
- The table must be in :code:`.csv`, indicating the SEEA land cover equivalent to your land cover classes .Remember the table must already be uploaded in your SEPAL environment. To learn how to do that, please see the `how to exchange files in SEPAL <https://docs.sepal.io/en/latest/setup/filezilla.html#exchange-files-with-sepal>`_. 


.. tip:: The target values must match the UN-SEEA classes codes for sub-indicator A (click on the info button at the top of the table for information on how the SEEA classes are coded).


.. image:: ../_static/sepal/updates_26/reclassify_sub_a.png
   :align: center
   :width: 700
   :alt: reclassifying subA


- Clicking on **Load** will automatically reclassify your land cover legend.

**In certain cases, certain land cover classes might be classified as No Data, Missing Values or Unclassified .In such cases leaving the classes blank will be interpreted as 0 values by SEPAL-SDG 15.4.2 and consequently not included in the computation. Note: Any values left blank will be interpreted as 0**.

.. important:: For ease and comparability when developing a reclassification matrix, the development team have created a template countries can modify for their use. The template can be found in the :ref:`Annex section <Annex>`.


Manually Reclassifying the land classes 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- Directly specify the reclassification rules by matching each land cover class (original class column) to its SEEA equivalent (destination class column), as shown below. Click the information icon in the upper right of the tools ribbon to reference the UN-SEEA classes if needed. The message next to the table title shows how many classes you have classified.
- Select the :guilabel:`💾` button located at the top of the table to save the table within SEPAL for future calculation.

.. image:: ../_static/sepal/custom_reclassification_sub_a.PNG
   :align: center
   :width: 1000
   :alt: Manual reclassification.

For our example, we will reclassify Nepal’s national land cover class using the following guide:

.. image:: ../_static/sepal/nepal_classification_guide.png
   :align: center
   :width: 700
   :alt: Reclassifation table_NEPAL

-Once all land classes have been reclassified, click on **Reclassify Land Cover for Subindicator B** (step 3 of the window) to proceed.

Reclassifying your land cover map legend for sub-Indicator B computation.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
This step allows you to reclassify the legend of your land cover map for computing Sub-Indicator B. 

.. note:: In contrast to sub-indicator A, national authorities have the liberty to use alternative land cover legends in the place of the default 10 UN-SEEA classes. Consequently ,the UN-SEEA legend can be adapted to the national context to ensure that it adequately captures the key degradation and improvement transitions identified in the country . For instance, a given country may decide to differentiate "natural forests" from "tree plantations" in sub-indicator B.

For this reason, this step allows users to apply a new reclassification, or alternatively, use the same reclassification rules defined in Sub-Indicator A. In the latter case,you can access the reclassification matrix you created and saved earlier by clicking the upload button and choosing the file. For both cases, the land cover reclassification rules must be a :code:`.CSV` file, following the same method as in the prior step. To use your own legend for sub-indicator B, click the table icon (**Import target land cover classes**) and select a file with your target classes.


.. image:: ../_static/sepal/updates_26/reclassify_sub_b.png
   :align: center
   :width: 900
   :alt: reclassifying sub_b


Check the :ref:`Annex <Annex>` for a template that can be modified for your land cover legend.


Uploading a transition matrix for computing Sub-Indicator B
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. important:: **This step should only be completed if you have provided different land cover reclassification rules for Sub-Indicator B in the prior step.** 

The next step is to upload a land cover transition matrix, defining the transitions between the land cover classes .We will consider the transitions to be either **degraded**, **stable** or **improved**, consistent to the legend you have provided in the prior step. This will allow SEPAL-SDG 15.4.2 to compute this sub-indicator in the next processing steps. 

As mentioned earlier, the transition file should have been previously uploaded in the SEPAL environment as a csv file, containing the following columns: **from_code**, **to_code** and **impact_code** .The column names must match exactly. (indication of change between the land cover classes). The file must contain all the possible transitions between your classes.

In step 4 of the window (**Transition matrix**), click **Select a file** and choose your transition file. Then click **Validate & close**.

Check the :ref:`Annex <Annex>` for the transition matrix template.

.. image:: ../_static/sepal/transition_file.PNG
   :align: center
   :width: 700
   :alt: Transition matrix

.. _Defaultlccustommatrix:


Modifying the default transition matrix for use with global land cover data
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

SEPAL-SDG 15.4.2 allows users to modify the default land cover transition matrix without providing a custom land cover map. This enables national authorities to adapt the transition matrix to their local context, better capturing the main land degradation processes occurring in the country while continuing to use the default global land cover data.


- This can be done by selecting **No** to the first question  and **Yes** to the second question of the land cover dataset questionnaire, and then clicking on **Set up land cover**.

.. image:: ../_static/sepal/updates_26/default_lc_custom_matrix.png
   :align: center
   :width: 900
   :alt: Reclassify table

- This will open a pop-up window. Click on **Transition matrix** (step 2 of the window) to see the default land cover transitions matrix, showing improvements (I) in green, degradation (D) in red, and stable transitions (S) in yellow. The matrix can be directly modified by clicking on each cell and changing the sign of the transition. The broom icon resets the matrix to the default values.

.. image:: ../_static/sepal/updates_26/modifying_transition_matrix.png
   :align: center
   :width: 900
   :alt: Reclassify table

- Once finished, click **Validate & close** to keep your changes (**Close** discards them). Then click **Next** to move to the next processing step: **Indicators Settings.**

.. warning::
   Adapting the default land cover transition matrix when using the default global land cover data should be carefully considered. Decisions about which land cover transitions are linked to a degradation or an improvement process in the context of sub-indicator B should be made taking into account the expected change in biodiversity and the mountain ecosystem functions or services that are considered desirable in a local or national context. For these reasons, FAO recommends to consider as degradation all land cover transitions that involve changes from natural land cover types (such as forests, shrublands, grasslands, wetlands) to anthropogenic land cover types (artificial surfaces, cropland, pastures, plantation forests, etc.) as a general rule, given that land use change is known to be the primary driver of biodiversity loss (IPBES, 2019).


.. _Indicator Settings:

Indicators Settings
-------------------

Once the area of interest, land cover data, reclassification rules, and transition matrix have been configured,  click the **Indicator Settings**  in the process steps to set the parameters required for the computation of both sub-indicators.

.. image:: ../_static/sepal/updates_26/indicator_settings.png
   :align: center
   :width: 900
   :alt: Reclassify table


From here on, we will cover the sub-indicators individually.

Defining parameters for Sub-indicator A: Mountain Green Cover Index
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
**1. Click on the add layer icon (highlighted in red) to define the computational years**

.. image:: ../_static/sepal/updates_26/subA_add_layer_icon.png
   :align: center
   :width: 800
   :alt: Indicator settings

**2. In the pop-up window, link each land cover map — whether default or custom — to its corresponding reference year. You can report on one or multiple years. To add additional reporting years, click the + button** 

.. image:: ../_static/sepal/updates_26/sub_a_defining_years.png
   :align: center
   :width: 500
   :alt: Defining computational years


.. note::  The reporting years for sub-indicator A are every five years from the baseline i.e. 2000, 2005, 2010, 2015 and subsequently every three years (2018, 2021, 2024,...).If your custom national land cover maps are not annually updated and do not exactly match the reporting years — for example, if you have a land cover map for 2004 instead of 2005 — the tool will automatically interpolate values for the missing reporting years based on the available land cover data.


**3. Click OK. The list of reporting years will now be listed at the bottom of the sub-indicator A box. Click Close to discard the changes.**

.. image:: ../_static/sepal/updates_26/sub_indicator_interpolation.png
   :align: center
   :width: 500
   :alt: Interpolation
 

Defining parameters for Sub-Indicator B: Proportion of Degraded Mountain Land.
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Unlike sub-indicator A, sub-indicator B first calculates the extent of degraded mountain land during the baseline period 2000–2015. This baseline sets the benchmark against which land degradation is measured and monitored every three years from 2015 onwards. In each subsequent reporting period (2018, 2021, 2024, ...), newly degraded land is added to the baseline estimate to track the cumulative extent of land cover degradation over time. For this reason, the tool automatically applies 2000–2015 as the baseline period.

**1. Define the land cover maps for the baseline years 2000 and 2015 by linking each of the land maps to their corresponding reference year. If your custom national land cover maps do not exactly match the baseline reporting years, select the map whose reference year is closest to the required reporting year. For example, a land cover map for 1998 could be used for the reporting year 2000.**


**2. Then define the land cover maps for each of the reporting years and click** **OK** **to save them.**

.. image:: ../_static/sepal/updates_26/sub_b_indicator_settings.png
   :align: center
   :width: 550
   :alt: Reclassify table


Calculation of SDG Indicator 15.4.2
-----------------------------------
Once the parameters of each sub-indicator are set, the tool is now ready to run as shown below:

.. image:: ../_static/sepal/updates_26/indicator_settings_defined.png
   :align: center
   :width: 1300
   :alt: Sub-indicator computations.

.. tip::

   By default, SEPAL-SDG 15.4.2 calculates indicator values assuming planimetric area methods. To calculate indicator values using the real surface area method (a method that takes into account the third dimension of mountain surfaces through the use of digital elevation models and is known to derive closer estimates of the real surface area of mountain regions), click on "Use Real Surface Area" in the Advanced options . Additionally, users can direct computation in Earth Engine (Run in EE background) or modify the processing scale by defining them in the Advanced Options as well. In **Process scale**, "Native" uses the resolution of the land cover data. You can also select 100, 300, 500 or 1000 m, or type a custom value up to 1500 m. A coarser scale makes the process faster, but less accurate.

   .. image:: ../_static/sepal/updates_26/advanced_options.png
      :align: center
      :width: 400
      :alt: Sub-indicator computations.

**1. Click on** **Calculate Indicator** **to initiate the computation.**

**2. Once completed, the module should display the following:**

.. image:: ../_static/sepal/updates_26/computation_success.png
   :align: center
   :width: 1300
   :alt: Reclassify table

.. tip::

   SEPAL-SDG 15.4.2 calculates the indicator values assuming planimetric area methods by default. To calculate indicator values using the real surface area method (a method that takes into account the third dimension of mountain surfaces through the use of digital elevation models and is known to derive closer estimates of the real surface area of mountain regions), click on **Use Real Surface Area**


3. The entire analysis is done in real time. To export the results, click **Export Reporting Tables**, a message will appear indicating the location of the exported files once complete (:code:`module_results/sdg_indicators/15.4.2/reports/SDG1542_<country code>`). Click **Click to download** in the message to download the tables to your computer.

.. image:: ../_static/sepal/updates_26/exporting_reporting_tables.png
   :align: center
   :width: 800
   :alt:  Exporting Reporting table

Calculation from Task
^^^^^^^^^^^^^^^^^^^^^
As explained in earlier sections, SEPAL runs on Google Earth Engine (GEE), and as a result, the computation of SDG Indicator 15.4.2 is subject to GEE resource limitations. One such limitation is the computation timeout (see `computation time out <https://developers.google.com/earth-engine/guides/debugging#timed-out>`_),whereby any computation that takes more than five minutes will throw an exception. To overcome this, the process will be automatically executed as a GEE task —an operation capable of running beyond the standard timeout limit. If the computation is submitted as a task, a message similar to the one shown in the image below will appear.

.. image:: ../_static/sepal/updates_26/processing_indicators_progress.png
   :align: center
   :width: 1200
   :alt: Calculation from Task Notification

A new file containing the task ID is created and stored in the :code:`module_results/sdg_indicators/15.4.2/tasks` folder. If both sub-indicators run in the background, the module creates one task file for each sub-indicator. This file allows you to track the status of the task at any time. Alternatively, you can monitor progress using the GEE task tracker (shown below), which displays all tasks currently running on the server.

.. image:: ../_static/sepal/updates_26/GEE_calculation_task.png
   :width: 400
   :align: center
   :alt: Computation in GEE


**1. To enable a computation from task; Click the "Export from task" in the process steps.**

We start by locating the tasking file within SEPAL using the navigator, initiated by clicking on the **Select a file** button. The files are in :code:`module_results > sdg_indicators > 15.4.2 > tasks`. When the task is completed in GEE, click the **Download & export tables** button. The module then saves the reporting tables, and the results dashboard shows the results.

.. image:: ../_static/sepal/updates_26/export_from_task.png
   :align: center
   :width: 1000
   :alt: Locating the task file


Visualising the results
-----------------------

SEPAL-SDG 15.4.2 provides two ways to visualise and access the computed results : 

- The exported tables: These provide the full results of the computation in a tabular format.

- Using the results panel that provides a simplified and visual representation of the results.

We will look at these individually.

Exported tables
^^^^^^^^^^^^^^^

Once the computation is complete, the results are automatically saved to the SEPAL workspace. Users can also download the files to their local computers for offline access or external reporting purposes.

**1. To locate the tables within SEPAL, navigate to the Files Tab, located in the left panel. Navigate to module_results > sdg_indicators > 15.4.2 > reports > SDG1542_<country code>, you should see your tables as shown below:**

.. image:: ../_static/sepal/updates_26/exporting_file.png
   :align: center
   :width: 1200
   :alt: Downloading Exported Tables

**2. To download the report from the SEPAL workspace, click on the report to activate the download icon, found in the top left side of the screen.**

**3. Once the report is downloaded, you can visualise the results of the computation as seen below:**

.. image:: ../_static/sepal/results_csv.png
   :align: center
   :width: 700
   :alt: Visualization using the reported tables

.. tip:: The tables follow the standard format for SDG reporting and therefore can be used to report SDG Indicator 15.4.2 values to FAO.


.. _ResultsPanel:

Visualising the results through the Results Panel
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

SEPAL-SDG 15.4.2 also allows users to visualise the computed results directly within the module. Interactive dashboards are generated to display the results for both sub-indicators . Additionally users can show layers on the map  and export needed layers . To navigate the results panel,


**1. Click on "4. Results" in the process steps on the left, or on the chart icon on the right side of the map, to open the Results panel.**

.. image:: ../_static/sepal/updates_26/results_panel.png
   :align: center
   :width: 800
   :alt: Results panel

**2. The "Visualize layers" table lists the computational layers, including the disaggregated land cover maps, with their sub-indicator. To show a layer on the map, click on the eye icon in its row. Click on the icon again to hide the layer. The legend of the layer shows at the bottom of the map.**

The first row is the **Bioclimatic belts** layer, which both sub-indicators use. It is available as soon as you select the area of interest, and it does not need the reporting years. The belts show on the map by default. Hide them to see the other layers better, as in the image below. When you select a new area of interest, the belts show again.

.. image:: ../_static/sepal/updates_26/visualizing_layers_results.png
   :align: center
   :width: 800
   :alt:   Visualizing computational layers

**3. To download a layer, click on the export icon in its row. The Export layers window opens with this layer selected in "Asset". Select the bands and the destination: Earth Engine asset, Google Drive or SEPAL workspace. Then check the name and the scale, and click on "Export".** The export of a land cover or degradation layer also contains a band with the bioclimatic belts. The export of the Bioclimatic belts row contains only the belts.

.. image:: ../_static/sepal/updates_26/exporting_layers.png
   :align: center
   :width: 900
   :alt: Exporting layers

**4.  Click on "Show Dashboard" under Sub-indicator A to display the Mountain Green Cover Index (MGCI) for each reporting year, disaggregated by bioclimatic belts, together with the land cover composition. Select a year at the top of the window, and a bioclimatic belt to see its composition.**

.. image:: ../_static/sepal/updates_26/Sub_A_Results_dashboard.png
   :align: center
   :width: 900
   :alt: Sub-Indicator A dashboard

**5. Sub-indicator B uses a Sankey diagram to show the transitions between land cover classes, in km2, for each computed year and bioclimatic belt. Hovering over the sankey will display area changes.**

.. image:: ../_static/sepal/updates_26/Sub_B_Results_dashboard.png
   :align: center
   :width: 900
   :alt: Sub-Indicator B dashboard

**6. Click on "Matrix" to show the same transitions as a matrix. The rows are the initial classes and the columns are the final classes. The colours show degradation (red), stable (yellow) and improvement (green) transitions. Hovering over a cell displays its area in km2.**

.. image:: ../_static/sepal/updates_26/Sub_B_Results_matrix.png
   :align: center
   :width: 900
   :alt: Sub-Indicator B transition matrix




  
.. _Annex:

Annex
-----

This section contains supplementary information and resources for an 
enhanced understanding and operationalization of SEPAL-SDG 15.4.2.

Computation Resources: Template Tables
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. tip:: 
   
   All templates contain a README section with instructions.

Template A: Custom Land Cover Reclassification Template
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When computing sub-indicator A using **custom** land cover maps, SEPAL-SDG 15.4.2 requires reclassifying the land cover legend into the 
UN-SEEA classification.

The development team recommends that countries adopt this template to 
reclassify their land cover maps.

.. note::
   
   The origin and target names and codes must be properly defined for 
   the reclassification to work correctly.

The table requires the following fields as columns:

- **from_name**: Name of each land cover class in the custom land cover map.
- **from_code**: Numerical code (pixel value) of each land cover class in 
  the custom land cover map.
- **to_name**: Name of the corresponding UN-SEEA land cover class.
- **to_code**: Numerical code of the corresponding UN-SEEA land cover class.

Download the template here:

.. raw:: html

   <a target="_blank" href="../_static/sepal_tables/Custom_LC_Classification_SubB.csv" download="_static/sepal_tables/Custom_LC_Classification_SubB.csv">Custom_LC_Classification_SubB</a>

Template B: Custom Land Cover Classification Template (Sub-indicator B)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As explained earlier, countries must use the UN-SEEA defined classes in 
sub-indicator A but have more flexibility when defining the classification 
scheme for sub-indicator B.

Countries can choose to use either the UN-SEEA classification legend 
(defined in the earlier step) or the FAO-defined template to develop their 
classification and legend.

Download the template here:

.. raw:: html

   <a target="_blank" href="../_static/sepal_tables/Default_LC_map_reclassification.csv" download="_static/sepal_tables/LC_map_reclassification.csv">LC_map_reclassification</a>

Template C: Transition Matrix
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This template should be used when a custom land classification legend is 
applied in the Sub-Indicator B computation. It enables countries to fully 
capture the transitions occurring in land cover.

.. note::
   
   When adopting this template, remember to fully define the original and 
   resultant classes, the impact, and their subsequent codes so that transitions are correctly captured by SEPAL-SDG 15.4.2.

The following fields must be defined:

- **from_name**: Name of the original land cover class.
- **from_code**: Numerical code (pixel value) of the original land cover class.
- **to_name**: Name of the final land cover class.
- **to_code**: Numerical code (pixel value) of the final land cover class.
- **impact_name**: Expected impact of the land cover transition. Only three 
  values are allowed: *degraded*, *stable*, or *improved*.
- **impact_code**: Numerical code for the expected impact. Only three values 
  are allowed: **1** for degraded, **2** for stable, **3** for improved.

Download the template here:

.. raw:: html

   <a target="_blank" href="../_static/sepal_tables/Transition_Matrix_SubB.csv" download="_static/sepal_tables/Transition_Matrix_SubB.csv">Transition_Matrix_SubB</a>

.. note:: 
   
   SEPAL-SDG 15.4.2 only accepts :code:`.csv` files. Once 
   these templates are modified to meet each country's needs, they must be 
   saved as :code:`.csv` files and imported into the SEPAL environment as
   described in earlier section.
