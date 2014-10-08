.. _cartography.ysld.reference.rules:

Rules
=====

A rule is a collection of styling directives (:ref:`symbolizers <cartography.ysld.reference.symbolizers>` combined with an optional conditional statement.

* If a conditional statement exists in a rule, then the styling directives will only be carried out (drawn) if the conditional returns true. Otherwise, the rule will be skipped.
* If no conditional statement exists in a rule, then the styling directive will always be carried out.

.. warning:: FIGURE NEEDED

The types of conditional statements available to rules are:

* :ref:`Filters <cartography.ysld.reference.filters>` for attribute-based rendering
* :ref:`Scale <cartography.ysld.reference.scale>` for scale-based rendering

Rules are contained within :ref:`Feature Styles <cartography.ysld.reference.featurestyles>`. There is no limit on the number of rules that be created, and there is no restriction that all rules must be mutually exclusive (as in, some rules may apply to the same features). 

The structure of a rule is:

* Rule
  * Filter(s)
  * Scale(s)
  * Symbolizer(s)

Syntax
------

The following is the basic syntax of a Rule. Note that the contents of the block are not all expanded; see the other sections for the relevant syntax.

.. warning:: WHAT IS ELSE/BOOL?

::

     rules:
     - name: <text>
       title: <text>
       filter: <filter>
       else: <boolean>
       scale: (<min>,<max>)
       symbolizers:
       - <symbolizer>
         <symbolizer>
         ...

where:

.. list-table::
   :header-rows: 1
   :stub-columns: 1

   * - Property
     - Required?
     - Description
   * - ``name``
     - No
     - Internal reference to the Rule. It is recommended that the value be lower case and contain no spaces.
   * - ``title``
     - No
     - Human-readable description of what the rule accomplishes.
   * - ``filter``
     - No
     - :ref:`Filter <cartography.ysld.reference.filters>` expression which will need to be evaluated to be true for the symbolizer(s) to be applied.
   * - ``else``
     - No
     - TBD
   * - ``scale``
     - No
     - :ref:`Scale <cartography.ysld.reference.scale>` boundaries showing at what scales (related to zoom levels) the rule will be applied.
   * - ``symbolizers``
     - Yes
     - Block containing one or more :ref:`symbolizers <cartography.ysld.reference.symbolizers>`. These contain the actual visualization directives. If the filter returns true and the view is with the scale boundaries, these symbolizers will be applied.

