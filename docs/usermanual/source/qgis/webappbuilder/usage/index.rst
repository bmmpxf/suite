.. _qgis.webappbuilder.usage:

Usage
=====

The page will detail how to use the Web App Builder. For more information, please see the :ref:`qgis.webappbuilder.tutorials`.

The Web App Builder is started from the :menuselection:`Plugins --> Boundless --> Web App Builder` menu.

.. figure:: img/menu.png

   Menu to launch the Web App Builder

Once launched, the main dialog looks like this:

.. figure:: img/maindialog.png

   Main dialog

**To create a web app, define its characteristics using the tabs in the dialog and then press the Create App button.**

Below is a description of each tab and its contents.

Description
-----------

The elements in the Description tab control the basic structure of the app page.

Set the title of the project in the :guilabel:`App Title` box. In case you want to add a logo along with your title, enter the path to the logo image file in the :guilabel:`Logo image` box.

From the available themes, select the one you want to use for your app. A theme defines how the elements of the web app (map, widgets, menus, etc.) will appear visually.

There are three themes: Basic, Fullscreen, and Tabbed.

Themes have predefined settings, but these can be modified. This is mainly done by modifying the CSS styles that constitute the theme. Clicking the :guilabel:`Configure theme` button will open the dialog shown below:

.. figure:: img/configuretheme.png

   Configure theme

Click a category in the list in the upper part of the dialog, and its corresponding CSS will be shown in the lower part. Edit the CSS code and click :guilabel:`OK` to save your changes. 

.. note:: These changes will be saved only for the current project. Subsequent web apps will default to the original CSS.

QGIS Layers
-----------

This tab is where you can select the layers from your existing QGIS project that you would like to add to your web app.

.. figure:: img/qgislayers.png

   QGIS Layers tab

Every layer in every group in the QGIS project will be listed in this tab. For each layer, there are several options depending on the type of layer.

* A check box with the name of the layer controls whether the layer will be added to the app or not.
* Another check box controls whether the layer will be visible when the app is loaded.

The following is a description of the different options that you might find for each type of layer, and how the app builder deals with each layer type.

Vector layer
~~~~~~~~~~~~

For each vector layer, the following options are available:

* :guilabel:`Info popup content`. Using this option, you can specify the content of the popup for features in the layer. Click the :guilabel:`Edit` link to open the popup editor.

  .. figure:: img/popupeditor.png

     Popup editor

  Type the expression to use. For adding the value of a given attribute of the future, enter the attribute name between brackets. Formatting is supported, since the content of the field is assumed to be HTML code and will be treated as such. Images can also be included this way.

* :guilabel:`Connect to this layer using`: Determines how to create the data source that will be used by the app. It has the following options:

  * :guilabel:`GeoServer -> WFS`: The data will be published to GeoServer and then the app will connect to it as a WFS service. Styling will be done client side by the app itself.

  * :guilabel:`GeoServer -> WMS`: The data will be published to GeoServer and then the app will connect to it as a WMS service. Styling will be done server side by GeoServer.

  * :guilabel:`GeoServer -> PostGIS -> WFS`: The data will be imported into PostGIS and then a store will be created in GeoServer to consume that data from the PostGIS database. The app will connect to it as a WFS service. Styling will be done client side by the app itself.

  * :guilabel:`GeoServer -> PostGIS -> WMS`: The data will be imported into PostGIS and then a store will be created in GeoServer to consume that data from the PostGIS database. The app will connect to it as a WMS service. Styling will be done server side by GeoServer.

  * :guilabel:`Use file directly`: PostGIS and GeoServer will not be used. The layer will be exported to a GeoJSON file and the app will use it directly. The file will be saved in the output folder in which the app itself will be created.

* :guilabel:`Allow selection on this layer`. If this check box is selected, the user will be able to select the features in this layer using any of the available selection tools (if added as a control). If you want to create charts based on the features of a given layer, you should allow selection on it.

* :guilabel:`Cluster points`. Check this option to have your point features clustered. Only available with point geometries.

* :guilabel:`Cluster distance`. Specify the distance to use for clustering. Only available with point geometries.

Raster layers
~~~~~~~~~~~~~

For each raster layer, the following options are available:

* :guilabel:`Connect to this layer using`. Determines how to create the data source that will be used by the app. It has the following options.

  * :guilabel:`GeoServer -> WMS`: The layer will be published to GeoServer and then the app will connect to it as a WMS service. Styling will be done server side by GeoServer.

  * :guilabel:`Use file directly`: PostGIS and GeoServer will not be used. The layer will be exported to an image file and the app will use it directly. The file will be saved in the output folder in which the app itself will be created.

WMS/WFS layers
~~~~~~~~~~~~~~

For WFS and WMS, you will find most of the same options for vector and raster layers, except for the *Connect to this layer using* option, as the original service will always be used.

Handling projections
~~~~~~~~~~~~~~~~~~~~

All layers will be automatically reprojected into the projection of the map to be created (by default, EPSG:3857) if needed. You can use input layers from any CRS.

Remote services such as WMS or WFS are an exception to this, as they must use the projection used in the web app. If a layer that is based on a remote service is added to the web map and uses a CRS other than the one specified, a warning will be shown and the application will not be created.

Other layers
------------

This tab allows you to add other layers to your application. You can select or deselect these layers by clicking the buttons. 

.. figure:: img/otherlayers.png

   Other layers tab with "Open topo map" selected

You can select from a list of **Base Layers**, which will be displayed below your layers and **Overlays**, which can be shown along side of your layers.

Base Layers contain the data such as roads and topography, while Overlays are additional layers that would serve as additional information (such as place labels), all based on available web services.

.. note:: Selecting Base Layers or Overlays is entirely optional.

Base Layers will be added to a group named "Base layers" in the app, which by default is set as the bottom layer.

.. figure:: img/baselayersselector.png

   Base layers in a web app


Controls
--------

The Controls tab allows you to select extra elements that you would like to add to your web app. These can be OpenLayers controls that act on the map and appear in it, or other elements that may or may not be directly related to the map data. Their place in the app and their appearance is controlled by the theme.

.. figure:: img/controls.png

   Controls tab

Some controls can be configured. This is done by right-clicking their corresponding button and selecting the :guilabel:`Configure` option.

.. figure:: img/controlcontext.png

   Configuring a control

You can find a detailed description of all available controls on the :ref:`controls` page.

Deploy
------

The Deploy tab is used to specify where your data will be stored. It has two groups: :guilabel:`PostGIS` and :guilabel:`GeoServer`, and contains connection information on how to store data to each. They are used only if your data configuration uses PostGIS or GeoServer (as explained in the *Layers* section).

.. figure:: img/deploy.png

   Deploy tab

Settings
--------

The Settings tab shows additional configuration for the application:

.. figure:: img/settings.png

   Settings

.. list-table::
   :header-rows: 1
   :stub-columns: 1
   :widths: 20 80
   :class: non-responsive

   * - Setting
     - Description
   * - App view CRS
     - The CRS of the finished map. Default is ``EPSG:3857`` (Web Mercator)
   * - Extent
     - The extent of the map. There are two options: :guilabel:`Canvas extent`, which is the current state of the QGIS canvas, or :guilabel:`Fit to Layers extent`, which will calculate the extent based on the union of all the layers in the project.
   * - Highlight features on hover
     - When selected, features will glow when the mouse rolls over them.
   * - Max zoom level
     - Maximum zoom level available in the web app, as related to the CRS.
   * - Min zoom level
     - Minimum zoom level available in the web app, as related to the CRS.
   * - Precision for GeoJSON export
     - Number of decimal places to use when exporting features using GeoJSON. Higher numbers increase accuracy but also data size. Default is 2.
   * - Restrict to extent
     - Do not allow the map to be panned outside of the extent.
   * - Show popups on hover
     - When selected, a feature's popup will be shown when the mouse rolls over the feature. Otherwise the feature will need to be clicked for the popup to display.
   * - Style for highlighted features
     - Allows customizing the way that features will look when highlighted. Clicking :guilabel:`Edit` will bring up a box with a CSS style, which can be customized.
   * - Style for selected features
     - Allows customizing the way that features will look when selected. Clicking :guilabel:`Edit` will bring up a box with a CSS style, which can be customized.
   * - Use layer scale dependent visibility
     - If defined in the QGIS rendering properties, layers will only be visible in the map when they are within the defined scale range.
   * - Zoom level when zooming to point feature
     - If a single feature is selected in the attributes table in the web app, and the :guilabel:`Zoom to selected` button is clicked, the map zoom will be set to this zoom level.

