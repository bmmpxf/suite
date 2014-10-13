.. _cartography.ysld.reference.variables:

Variables
=========

Variables in YSLD that allow for a certain directive or block of directives to be defined by name and later reused. This can greatly simplify the styling document.

The two most-common use cases for using variables are:

* To create a more-friendly name for a value (such as using ``orange`` instead of ``#ff8000``)
* To define a block of directives to remove redundant content and to decrease file length

.. warning:: ANYTHING ELSE?

It is customary, but not required, to place all definitions at the very top of the YSLD file, above all :ref:`header information <cartography.ysld.reference.structure>`:ref:`feature styles <cartography.ysld.reference.featurestyles>`, or :ref:`rules <cartography.ysld.reference.rules>`.

Syntax
------

Single value
^^^^^^^^^^^^

The syntax for defining a variable as a single value is::

  define: &variable <value>

where:

.. list-table::
   :class: non-responsive
   :header-rows: 1
   :stub-columns: 1
   :widths: 20 10 50 20

   * - Attribute
     - Required?
     - Description
     - Default value
   * - ``define``
     - Yes
     - Starts the definition block.
     - N/A
   * - ``&variable``
     - Yes
     - The name of the variable being defined. The ``&``, while required, is not part of the variable name.
     - N/A
   * - ``<value>``
     - Yes
     - A single value, such as ``512`` or ``#dd0000``
     - N/A

The syntax for using this variable is to prepend the variable name with a ``*``::

  <directive>: *variable

This variable can be used in any place where its type is expected.

Directive block
^^^^^^^^^^^^^^^

The syntax for defining a variable as a content block is::

  define: &varblock
    <directive>: <value>
    <directive>: <value>
    <directive>: <value>
    ...
    <block>:
    - <directive>: <value>
      <directive>: <value>
    ...

Any number of directives or blocks of directives can be inside the definition block. Moreover, any type of directive that is valid YSLD can be included in the definition, so long as the content block could be substituted for the variable without modification.

.. warning:: NESTED BLOCKS POSSIBLE?

The syntax for using this variable, once again, is to prepend the variable name with a ``>>: *``::

  <block>:
  - <directive>: <value>  
    >>: *varblock

The line that contains the variable will be replaced with the contents of the definition.

