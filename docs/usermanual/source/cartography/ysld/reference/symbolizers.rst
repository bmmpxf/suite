.. _cartography.ysld.reference.symbolizers:

Symbolizers
===========

The basic unit of visualization is the Symbolizer. There are five types of symbolizer:

* Point Symbolizer
* Line Symbolizer
* Polygon Symbolizer
* Raster Symbolizer
* Text Symbolizer

Symbolizers are contained inside :ref:`Rules <cartography.ysld.reference.rules>`. A Rule can contain one or many symbolizers. 

.. note:: The most common use case for multiple symbolizers is a geometry (Point/Line/Polygon) Symbolizer to draw the features plus a Text Symbolizer for labeling these features.

.. warning:: ADD FIGURE

It is common to match the symbolizer with the type of geometries contained in the layer, but this is not required. The following table illustrates what will happen when a geometry symbolizer is matched up with another type of geometry.

**Matching symbolizers and geometries**

.. list-table::
   :class: non-responsive
   :header-rows: 1
   :stub-columns: 1

   * - 
     - Points
     - Lines
     - Polygon
   * - Point Symbolizer
     - **Points**
     - Centroid of the lines
     - Centroid of the polygons
   * - Line Symbolizer
     - ?
     - **Lines**
     - Outline (stroke) of the polygons
   * - Polygon Symbolizer
     - ?
     - ?
     - **Polygons**


Point Symbolizer
----------------

The point symbolizer is used to style point features or centroids of non-point features.

The full syntax of a point symbolizer is::

  symbolizers:
  - point:
      graphic: 
        <graphic_options>
      symbols:
      - external:
          url: <text>
          format: <text>
      - mark:
          shape: <shape>
          fill-color: <color>
          fill-opacity: <expression>
          fill-graphic: 
            <graphic_options>
          stroke-color: <color>
          stroke-width: <expression>
          stroke-opacity: <expression>
          stroke-linejoin: <expression>
          stroke-linecap: <expression>
          stroke-dasharray: <float[]>
          stroke-dashoffset: <expression>
          stroke-graphic-fill: 
            <graphic_options>
          stroke-graphic-stroke: 
            <graphic_options>
      size: <expression>
      anchor: <tuple>
      displacement: <tuple>
      opacity: <expression>
      rotation: <expression>
      options: <options>
      gap: <expression>
      initial-gap: <expression>

.. warning:: VERIFY THIS

where:

.. include:: include/stroke.txt

.. include:: include/fill.txt

.. list-table::
   :class: non-responsive
   :header-rows: 1
   :stub-columns: 1
   :widths: 20 10 50 20

   * - Property
     - Required?
     - Description
     - Default value
   * - ``shape``
     - No
     - The shape of the mark. Options are ``square``, ``circle``, ``triangle``, ``cross``, ``x``, and ``star``. 
     - ``square``
   * - ``size``
     - No
     - The size of the mark in pixels. If the aspect ratio of the mark is not 1:1 (square), will apply to the *height* of the graphic only, with the width scaled proportionally.
     - 16
   * - ``anchor``
     - No
     - ???
     - ???
   * - ``displacement``
     - No
     - DIDN'T WORK
     - ???
   * - ``opacity``
     - No
     - DIDN'T WORK
     - ???
   * - ``rotation``
     - No
     - Value (in degrees) or rotation of the mark. Larger values increase counter-clockwise rotation. A value of ``180`` will make the mark upside-down.
     - ``0``
   * - ``options``
     - No
     - ???
     - ???
   * - ``gap``
     - No
     - ???
     - ???
   * - ``initial-gap``
     - No
     - ???
     - ???
   * - ANYTHING ELSE?
     - No
     - ???
     - ???


.. include:: include/graphic.txt


Line Symbolizer
---------------

The line symbolizer is used to style linear features. It is in some ways the simplest of the symbolizers because it only contains facilities for the stroke (outline) of a feature, and not the fill (inside) of a feature.

The full syntax of a line symbolizer is:

::

  symbolizers:
  - line:
      stroke-color: <color>
      stroke-width: <expression>
      stroke-opacity: <expression>
      stroke-linejoin: <expression>
      stroke-linecap: <expression>
      stroke-dasharray: <float[]>
      stroke-dashoffset: <expression>
      stroke-graphic-fill: 
        <graphic_options>
      stroke-graphic-stroke: 
        <graphic_options>
      offset: <expression>
      geometry: <expression>
      options: <options>

.. warning::

   * What about UOM?
   * What does "expression" mean? 
   * What about offset/geometry/options
   * What is stroke-graphic-?

where:

.. include:: include/stroke.txt

.. list-table::
   :class: non-responsive
   :header-rows: 1
   :stub-columns: 1
   :widths: 20 10 50 20

   * - Property
     - Required?
     - Description
     - Default value
   * - ``offset``
     - No
     - ???
     - ???
   * - ``geometry``
     - No
     - ???
     - ???
   * - ``options``
     - No
     - ???
     - ???
   * - ANYTHING ELSE?
     - No
     - ???
     - ???

.. include:: include/graphic.txt

Polygon Symbolizer
------------------

The polygon symbolizer styles polygon (2-dimensional) features. It contains facilities for the stroke (outline) of a feature, as well as the fill (inside) of a feature. 

The full syntax of a polygon symbolizer is::

  symbolizers:
  - polygon:
      fill-color: <color>
      fill-opacity: <expression>
      fill-graphic: 
        <graphic_options>
      stroke-color: <color>
      stroke-width: <expression>
      stroke-opacity: <expression>
      stroke-linejoin: <expression>
      stroke-linecap: <expression>
      stroke-dasharray: <float[]>
      stroke-dashoffset: <expression>
      stroke-graphic-fill: 
        <graphic_options>
      stroke-graphic-stroke: 
        <graphic_options>
      offset: <expression>
      geometry: <expression>
      options: <options>

.. warning:: VERIFY THAT THERE AREN'T OTHER OPTIONS

where:

.. include:: include/stroke.txt

.. include:: include/fill.txt

.. list-table::
   :class: non-responsive
   :header-rows: 1
   :stub-columns: 1
   :widths: 20 10 50 20

   * - Property
     - Required?
     - Description
     - Default value
   * - ``offset``
     - No
     - ???
     - ???
   * - ``displacement``
     - No
     - ???
     - ???
   * - ANYTHING ELSE?
     - No
     - ???
     - ???

.. include:: include/graphic.txt

Raster Symbolizer
-----------------

The raster symbolizer styles raster (coverage) layers. A raster is an array of information with each cell in the array containing one or more values, stored as "bands".

The full syntax of a raster symbolizer is::

  symbolizers:
  - raster:
      opacity: 1.0
      color-map:
        type: ramp
        entries: []
      contrast-enhancement: {}

.. warning:: WHAT ELSE?

.. warning:: HOW TO PICK OUT BANDS?

where:

.. list-table::
   :class: non-responsive
   :header-rows: 1
   :stub-columns: 1
   :widths: 20 10 50 20

   * - Property
     - Required?
     - Description
     - Default value
   * - ``opacity``
     - No
     - Opacity of the display. Valid values are a decimal between ``0`` (completely transparent) and ``1`` (completely opaque).
     - ``1``
   * - ``color-map``
     - No
     - Creates a mapping of colors to grid values.
     - ???
   * - ``type``
     - No
     - Type of color mapping. Default is ``ramp``, which creates a smooth gradient between values. OTHER OPTIONS? SYTNAX?
     - ???
   * - ``entries``
     - No
     - Values for the color mapping. SYTNAX?
     - ???
   * - ``contrast-enhancement``
     - No
     - ???
     - ???
   * - ANYTHING ELSE?
     - No
     - ???
     - ???

Text Symbolizer
---------------

The text symbolizer styles labels of vector features.

The full syntax of a text symbolizer is::

  symbolizers:
  - text:
      label: <expression>
      font-family: <expression>
      font-size: <expression>
      font-style: <expression>
      font-weight: <expression>
      placement:
        type: point|line
        offset: <expression>
        anchor: <tuple>
        displacement: <tuple>
        rotation: <expression>

.. warning::

   UNSURE ABOUT THESE::

      <<: *fill
      <<: *symbolizer
      <<: *graphic

.. warning:: WHAT ABOUT THE VENDOR OPTIONS?

where:

.. list-table::
   :class: non-responsive
   :header-rows: 1
   :stub-columns: 1
   :widths: 20 10 50 20

   * - Property
     - Required?
     - Description
     - Default value
   * - ``label``
     - Yes REALLY?
     - The text to display. Often taken from an attribute (``[type]``) but any valid expression that constructs a string will do.
     - N/A
   * - ``font-family``
     - No
     - The type of font to be used for the label. Options are system dependent, but usually include SOMETHING.
     - ???
   * - ``font-size``
     - No
     - The size of the font.
     - ???
   * - ``font-style``
     - No
     - The style of the font. Options are ``normal``, ``italic``, and ``oblique``.
     - ``normal``
   * - ``font-weight``
     - No
     - The weight of the font. Options are ``normal`` and ``bold``.
     - ``normal``
   * - ``placement``
     - No
     - The family of options that determine where the label is to be drawn relative to its feature
     - N/A
   * - ``type``
     - Yes REALLY?
     - Determines whether the label is to be drawn derived from a ``point`` or a ``line``.
     - ???
   * - ``offset``
     - No
     - ???
     - ???
   * - ``anchor``
     - No
     - ???
     - ???
   * - ``displacement``
     - No
     - ???
     - ???
   * - ``rotation``
     - No
     - ???
     - ???
   * - ANYTHING ELSE?
     - No
     - ???
     - ???
