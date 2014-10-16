.. _cartography.ysld.reference.structure:

Structure
=========

The structure of a typical YSLD file is as follows:

* Variable definitions (if any)
* Header
* Feature Style(s)

Regarding Feature Styles and their content:

* A :ref:`feature style <cartography.ysld.reference.featurestyles>` is a block that can contain one or many rules.
* A :ref:`rule <cartography.ysld.reference.rules>` is a directive that can contain one or many :ref:`symbolizers <cartography.ysld.reference.symbolizers>`.
* A rule applies to all features unless made to be selective by the use of a :ref:`filter <cartography.ysld.reference.filters>`.

**The basic unit of a style is the symbolizer.** This contains the actual visualization for individual features.

.. warning:: FIGURE NEEDED

Simple example
--------------

Here is an example if a YSLD containing a single rule inside a single feature style::

   name: 'style_example'
   title: 'An example of YSLD styling'
   abstract: 'Used in the User Manual of OpenGeo Suite'
   feature-styles:
   - rules:
     - name: 'all'
       title: 'Every feature will be styled this way'
       symbolizers:
       - polygon:
         fill-color: '#808080'
         fill-opacity: 0.5
         stroke-color: '#000000'
         stroke-opacity: 0.75

This would style every polygon feature in a given layer with the given RGB color codes (a medium gray for a fill and black for the outline), with the given opacities for both fill and stroke being given in decimals indicating percentage (so 0.5 is 50% opaque).

.. note:: For more details on syntax, please see the section on :ref:`symbolizers <cartography.ysld.reference.symbolizers>`.

Property syntax
---------------

Statements (or directives) in a YSLD styling document are designed as key-value, or property-value pairs of the following form::

   <property>: <value>

The ``<property>`` is a string denoting the property name, while the ``<value>`` can be one of a number of different types depending on context. These different types require slightly different markup, as shown in the following table:

.. list-table::
   :class: non-responsive
   :header-rows: 1
   :stub-columns: 1
   :widths: 10 20 20 50

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
     - Quotes
     - ``'Title'``
     - Spaces, colons, and other special characters are allowed
   * - Color
     - Quotes (hex) / rgb(r,g,b) (Decimal)
     - ``'#808080'`` or ``"#808080"``; ``rgb(255,0,255)``
     - Used when specifying RGB colors. For hex: ``#rrggbb``; for decimal: ``rgb(rrr,ggg,bbb)``
   * - Tuple
     - Parentheses
     - ``(0,15000)``
     - Entries in the the tuple may be left blank to mean unbounded (such as ``(,15000)``)
   * - :ref:`Filter <cartography.ysld.reference.filters>`
     - Brackets for attribute, quotes for attribute value
     - ``[type] = 'road'``
     - Single or double quotes allowed

.. warning:: ANYTHING ELSE?

.. warning:: WHAT SPECIAL CHARACTERS ARE ALLOWED IN A STRING?

.. warning:: WHEN ARE QUOTES REQUIRED?

.. warning:: IS # REQUIRED?


Indentation
-----------

Indentation is very important in YSLD. All directives must be indented to its proper place to ensure proper hierarchy. **Improper indentation will cause a styled to be rendered incorrectly, or not at all.**

For example, when using a polygon symbolizer, there are certain parameters that are contained inside it, such as the color of the fill and stroke. These must be indented such that they are "inside" the polygon block.

In this example, the following markup is **correct**::

       - polygon:
           fill-color: '#808080'
           fill-opacity: 0.5
           stroke-color: '#000000'
           stroke-opacity: 0.75

The parameters inside the polygon (symbolizer) are indented, meaning that they are referencing the symbolizer and are not "outside it."

.. warning:: WHY IS THERE NOT A SECOND DASH?

Compare to the following **incorrect** markup::

       - polygon:
         fill-color: '#808080'
         fill-opacity: 0.5
         stroke-color: '#000000'
         stroke-opacity: 0.75

The parameters that are relevant to the polygon block here need to be contained inside that block. Without the parameters being indented, they are at the same "level" as the polygon block, and so will not be interpreted correctly.

.. note:: Note that the dash (``-``) indicates that a list is beginning, but that is irrelevant to the specifics of the polygon block. If the polygon block were preceded by another symbolizer, it would not have a dash in front of it.

.. note:: For more details on syntax, please see the section on :ref:`symbolizers <cartography.ysld.reference.symbolizers>`.


List syntax
-----------

.. warning:: TBD. TALK ABOUT DASHES.

Comments
--------

Comments are allowed in YSLD, both for descriptive reasons and to remove certain styling directives without deleting them outright. Comments are indicated by a ``#`` as the first non-whitespace character in a line. For example::

  # This is a line symbolizer
  - line:
      stroke-color: #000000
      stroke-width: 2
      #stroke-width: 3

The above would display the lines with width of ``2``; the line showing a width of ``3`` is commented out.

Comment blocks do not exist, so each line of a comment will need to be indicated as such::

  - line:
      stroke-color: #000000
      stroke-width: 2
  #- line:
  #    stroke-color: #ff0000
  #    stroke-width: 3

