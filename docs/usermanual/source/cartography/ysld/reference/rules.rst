.. _cartography.ysld.reference.rules:

Rules
=====

A rule is a **collection of styling directives**, primarily consisting of :ref:`symbolizers <cartography.ysld.reference.symbolizers>` combined with optional conditional statements.

* **If a conditional statement exists** in a rule, then the styling directives will only be carried out **if the conditional returns true**. Otherwise, the rule will be skipped.
* **If no conditional statement exists** in a rule, then the styling directive will **always be carried out**.

.. warning:: FIGURE NEEDED

The types of conditional statements available to rules are:

* :ref:`Filters <cartography.ysld.reference.filters>` for attribute-based rendering
* :ref:`Scale <cartography.ysld.reference.scale>` for scale-based rendering

Rules are contained within :ref:`feature styles <cartography.ysld.reference.featurestyles>`. There is no limit on the number of rules that can be created, and there is no restriction that all rules must be mutually exclusive (as in, some rules may apply to the same features).

Syntax
------

The following is the basic syntax of a Rule. Note that the contents of the block are not all expanded; see the other sections for the relevant syntax.

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
   :class: non-responsive
   :header-rows: 1
   :stub-columns: 1
   :widths: 20 10 70

   * - Property
     - Required?
     - Description
   * - ``name``
     - No
     - Internal reference to the rule. It is recommended that the value be lower case and contain no spaces.
   * - ``title``
     - No
     - Human-readable description of what the rule accomplishes.
   * - ``filter``
     - No
     - :ref:`Filter <cartography.ysld.reference.filters>` expression which will need to evaluate to be true for the symbolizer(s) to be applied.
   * - ``else``
     - No
     - TBD
   * - ``scale``
     - No
     - :ref:`Scale <cartography.ysld.reference.scale>` boundaries showing at what scales (related to zoom levels) the rule will be applied.
   * - ``symbolizers``
     - Yes
     - Block containing one or more :ref:`symbolizers <cartography.ysld.reference.symbolizers>`. These contain the actual visualization directives. If the filter returns true and the view is with the scale boundaries, these symbolizers will be applied.

.. warning:: WHAT IS ELSE/BOOL?

.. warning:: ANYTHING ELSE?
