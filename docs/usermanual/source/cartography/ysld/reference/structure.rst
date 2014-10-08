.. _cartography.ysld.reference.structure:

Structure
=========

The structure of a typical YSLD file is as follows:

* Variable definitions (if any)
* Header
* Feature Style(s)

Regarding Feature Styles and their content:

* A Feature Style is a block that can contain one or many Rules
* A Rule is a directive that can contain one or many Symbolizers
* A Rule can be made to be selective by the use of a Filter

The basic unit of a style is the Symbolizer. This contains the actual visualization instructions for individual features.

.. warning:: FIGURE NEEDED

Simple example
--------------

Here is an example if a YSLD containing a single Rule inside a single Feature Style::

   name: 'style_example
   title: An example of YSLD styling
   abstract: Used in the User Manual of OpenGeo Suite
   feature-styles:
   - rules:
     - name: 'all'
       title: 'Every feature will be styled this way'
       symbolizers:
       - point:
         shape: <shape>
         fill-color: '#808080'
         fill-opacity: 0.5
         stroke-color: '#000000'
         stroke-opacity: 0.75

This would style every feature in a given layer with a point with the given RGB color codes (#808080, a medium gray, for a fill, and #000000, black, for the outline), with the given opacities for fill and stroke being given in decimals indicating percentage (so 0.5 is 50% opaque).

Property syntax
---------------

Statements (or directives) in a YSLD styling document are designed as key-value, or property-value pairs (IS THIS RIGHT?) of the following form::

   property: value

The ``property`` is a string denoting the property name, while the ``value`` can be one of a number of different types depending on context. These different types require slightly different markup, as shown in the table below

.. list-table::
   :header-rows: 1
   :stub-columns: 1

   * - Type
     - Syntax
     - Example
     - Notes
   * - Integer
     - Value only
     - ``12``
     - Quotes allowed as well
   * - Float
     - Value only
     - ``0.75``
     - Quotes allowed as well
   * - Text
     - Quotes (single or double)
     - ``'Title'``
     - Spaces, colons, and other special characters are allowed (WHICH AREN'T?) (AND IS THIS TRUE THAT QUOTES ARE REQUIRED?)
   * - Hex value
     - Quotes (single or double)
     - ``'#808080'`` or ``"#808080"``
     - Used when specifying RGB colors (#RRGGBB)
   * - Tuple
     - Parentheses
     - ``(0,15000)``
     - Entries in the the tuple may be left blank to mean unbounded (such as ``(,15000)``)
   * - Filter predicate
     - Brackets for attribute, quotes for attribute value
     - ``[type] = 'road'``
     - Single or double quotes allowed
   * - OTHERS
     - ???
     - ???
     -

List syntax
-----------

TBD.

Indentation
-----------

Indentation is very important in YSLD. All directives must be indented to its proper place to ensure proper heirarchy. **Improper indentation will cause a styled to be rendered incorrectly, or not at all.**

For example, when using a polygon symbolizer (see the section on POLYGON SYMBOLIZERS) there are certain parameters that are contained inside it, such as the color of the fill and stroke. These must be indented such that they are "inside" the polygon block.

In this example, the following markup is **correct**::

       - polygon:
           fill-color: '#808080'
           fill-opacity: 0.5
           stroke-color: '#000000'
           stroke-opacity: 0.75

The parameters inside the polygon (symbolizer) are indented, meaning that they are referencing the symbolizer and are not "outside it."

Compare to the following **incorrect** markup::

       - polygon:
         fill-color: '#808080'
         fill-opacity: 0.5
         stroke-color: '#000000'
         stroke-opacity: 0.75

Note that the dash (``-``) indicates that a list is beginning, but that is irrelevant to the specifics of the polygon block. (If the polygon block was preceded by another symbolizer, it would not have a dash in front of it.) The parameters that are relevant to the polygon block here need to be contained inside that block. Without the parameters being indented, they are at the same "level" as the polygon block, and so will not be interpreted correctly.

TALK MORE ABOUT LISTS AND DASHES


Scratch pad
-----------


::

      - name: MFR-20
        title: 'Residential: Multi-Family 20 Units/Acre'
        filter: zone = 'MFR-20'
        scale: (,140000.0)
        symbolizers:
        - polygon:
            fill-color: '#BD0026'
            fill-opacity: 0.5
      - name: MFR-15
        title: 'Residential: Multi-Family 15 Units/Acre'
        filter: zone = 'MFR-15'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#E31A1C'
            fill-opacity: 0.5
      - name: SFR-10
        title: 'Residential: Single-Family 10 Units/Acre'
        filter: zone = 'SFR-10'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#FC4E2A'
            fill-opacity: 0.5
      - name: SFR-6
        title: 'Residential: Single-Family 6 Units/Acre'
        filter: zone = 'SFR-6'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#FD8D3C'
            fill-opacity: 0.5
      - name: SFR-4
        title: 'Residential: Single-Family 4 Units/Acre'
        filter: zone = 'SFR-4'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#FEB24C'
            fill-opacity: 0.5
      - name: SFR-2
        title: 'Residential: Single-Family 2 Units/Acre'
        filter: zone = 'SFR-2'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#FED976'
            fill-opacity: 0.5
      - name: SFR-00
        title: 'Residential: Single-Family 1 Units/Acre'
        filter: zone = 'SFR-00'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#FFEDA0'
            fill-opacity: 0.5
      - name: C-H
        title: 'Commercial: Heavy'
        filter: zone = 'C-H'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#A50F15'
            fill-opacity: 0.5
      - name: C-R zones
        title: 'Commercial: Regional'
        filter: zone = 'C-R'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#DE2D26'
            fill-opacity: 0.5
      - name: C-C
        title: 'Commercial: Community'
        filter: zone = 'C-C'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#FB6A4A'
            fill-opacity: 0.5
      - name: C-N
        title: 'Commercial: Neighborhood'
        filter: zone = 'C-N'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#FCAE91'
            fill-opacity: 0.5
      - name: C-S/P
        title: 'Commercial: Service/Professional'
        filter: zone = 'C-S/P'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#FEE5D9'
            fill-opacity: 0.5
      - name: I-H
        title: 'Industrial: Heavy'
        filter: zone = 'I-H'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#810F7C'
            fill-opacity: 0.5
      - name: I-G
        title: 'Industrial: General'
        filter: zone = 'I-G'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#8856A7'
            fill-opacity: 0.5
      - name: I-L
        title: 'Industrial: Light'
        filter: zone = 'I-L'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#8C96C6'
            fill-opacity: 0.5
    - name: name
      rules:
      - name: SR-1
        title: 'Suburban: 1 Acre Minimum'
        filter: zone = 'SR-1'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#A50026'
            fill-opacity: 0.5
      - name: SR-2.5
        title: 'Suburban: 2.5 Acre Minimum'
        filter: zone = 'SR-2.5'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#D73027'
            fill-opacity: 0.5
      - name: RR-5
        title: 'Rural: 5 Acre Minimum'
        filter: zone = 'RR-5'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#F46D43'
            fill-opacity: 0.5
      - name: F-5
        title: 'Residential: Farm 5 Acre Minimum'
        filter: zone = 'F-5'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#FDAE61'
            fill-opacity: 0.5
      - name: GC
        title: 'Commercial: General'
        filter: zone = 'GC'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#FEE090'
            fill-opacity: 0.5
      - name: NC
        title: 'Commercial: Neighborhood'
        filter: zone = 'NC'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#FFFFBF'
            fill-opacity: 0.5
      - name: EFU
        title: 'Resource: Exclusive Farm Use'
        filter: zone = 'EFU'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#E0F3F8'
            fill-opacity: 0.5
      - name: OSR
        title: 'Resource: Open Space Reserve'
        filter: zone = 'OSR'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#ABD9E9'
            fill-opacity: 0.5
      - name: GI
        title: 'Industrial: General'
        filter: zone = 'GI'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#74ADD1'
            fill-opacity: 0.5
      - name: LI
        title: 'Industrial: Light'
        filter: zone = 'LI'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#4575B4'
            fill-opacity: 0.5
      - name: AD-MU
        title: 'Industrial: Airport Development-Multi-Use'
        filter: zone = 'AD-MU'
        scale: (,280000.0)
        symbolizers:
        - polygon:
            fill-color: '#313695'
            fill-opacity: 0.5



