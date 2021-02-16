.. _sec:units.intro:

Introduction
============

.. rubric:: Units are common

Measurement plays a central role in observations of the real world. Most
observed quantities are measured in some unit (e.g. dollar, hour, meter,
etc.), and the magnitude of the unit influences the mental picture that
you may have of an object (e.g. ounce, kilogram, ton, etc.). When you
combine such objects in a numerical relationship, the corresponding
units must be *commensurable*. Without such consistency, the
mathematical relationships become meaningless.

.. rubric:: Why units in models

There are several good reasons to track units throughout a model. The
explicit mentioning of units can enhance the readability of a model,
which is especially helpful when others read and/or maintain your model.
Units provide the AIMMS compiler with additional checking power to find
errors in model formulations. Finally, through the use of units you can
let AIMMS perform the job of unit conversion and scaling.

.. rubric:: Standard units

The model editor in AIMMS will give you access to a large number of
quantities and units, and in particular to those of the International
System of Units (referred to as SI from the French "Systeme
Internationale"). The SI system is an improved metric system adopted by
the Eleventh General Conference of Weights and Measures in 1960. The
entire SI system of measurement is constructed from the atomic base
units associated with the following nine basic quantities.

.. _table:units.si-basic:

.. table:: Basic SI quantities and their base units

	================== ================ =========
	Quantity           Atomic Base Unit Text
	================== ================ =========
	length             m                meter
	mass               kg               kilogram
	time               s                second
	temperature        K                kelvin
	amount of mass     mol              mole
	electric current   A                ampere
	luminous intensity cd               candela
	angle              rad              radian
	solid angle        sr               steradian
	================== ================ =========

.. rubric:: Derived quantities and units

All quantities which are not one of the nine basic SI quantities are
called *derived* quantities. Each such quantity has a derived base unit
which can be expressed in terms of the atomic base units of the basic SI
quantities. Optionally, a compound unit symbol can be associated with
such a derived base unit, like the symbol ``N`` for the unit
``kg*m/s^2``. The following table illustrates some of the more
well-known derived quantities and their corresponding derived base
units. Note that five of them have an associated compound unit symbol.
Many other derived quantities are available in AIMMS.

.. _table:units.si-derived:

.. table:: Selected derived SI quantities and their base units

   ================ ================= ========================
   Quantity         Derived Base Unit Text
   ================ ================= ========================
   area             ``m``             square meter
   volume           ``m``             cubic meter
   force            ``N = kg*m/s``    newton
   pressure         ``Pa = kg/m*s``   pascal
   energy           ``J = kg*m/s``    joule
   power            ``W = kg*m/s``    watt
   charge           ``C = A*s``       coulomb
   density          ``kg/m``          kilogram per cubic meter
   velocity         ``m/s``           meter per second
   angular velocity ``rad/s``         radian per second
   ================ ================= ========================

.. rubric:: Related units

Aside from the base unit that must be associated with every quantity, it
is also possible to specify a number of *related* units. Related units
are those units that can be expressed in terms of their base unit by
means of a linear relationship. A typical example is the unit ``km``
which is related to the base unit ``m`` by means of the linear
relationship :math:`x` ``km = 1000*x m``. Similarly, the unit ``degC``
(degree Celsius) is related to the base unit ``K`` through the formula
:math:`x` ``degC = (x + 273.15) K``.

.. rubric:: Standard unit prefix notation

Frequently, related units are a multiple of their own base unit, which
is reflected through a prefix notation that indicates the level of
scaling. :ref:`this table <table:units.unit-mult>` shows the standard SI prefix
symbols and their corresponding scaling factor. Familiar examples are
``kton``, ``MHz``, ``kJ``, etc. Note that any prefix can be applied to
any base unit except the kilogram. The kilogram takes prefixes as if the
base unit were the gram.

.. _table:units.unit-mult:

.. table:: Prefixes of the International System

	=============== ===== ====== ================ ===== ======
	Factor          Name  Symbol Factor           Name  Symbol 
	=============== ===== ====== ================ ===== ======
	:math:`10^1`    deca  da     :math:`10^{-1}`  deci  d
	:math:`10^2`    hecto h      :math:`10^{-2}`  centi c
	:math:`10^3`    kilo  k      :math:`10^{-3}`  milli m
	:math:`10^6`    mega  M      :math:`10^{-6}`  micro mu
	:math:`10^9`    giga  G      :math:`10^{-9}`  nano  n
	:math:`10^{12}` tera  T      :math:`10^{-12}` pico  p
	:math:`10^{15}` peta  P      :math:`10^{-15}` femto f
	:math:`10^{18}` exa   E      :math:`10^{-18}` atto  a
	:math:`10^{21}` zetta Z      :math:`10^{-21}` zepto z
	:math:`10^{24}` yotta Y      :math:`10^{-24}` yocto y
	=============== ===== ====== ================ ===== ======

.. rubric:: Flexible specification

To give you maximum freedom to choose your own quantities, units and
naming conventions, AIMMS is not exclusively committed to any particular
standard. However, you are encouraged to use the standard SI units and
prefix symbols to make your model as readable and maintainable as
possible.

.. rubric:: Summary of terminology

Thus far you have encountered *basic* quantities
(:ref:`this table <table:units.si-basic>`) and *derived* quantities
(:ref:`this table <table:units.si-derived>`). Each quantity has a *base* unit. The
base unit of a basic quantity is defined through a unit symbol, referred
to as an *atomic* unit. All other base units are *derived* base units.
Such units are defined through an expression in terms of other base
units, which can eventually be translated into an expression of atomic
base units. You have the option to associate a unit symbol with any
derived base unit, which is referred to as a *compound* unit symbol.
Whenever you have associated a unit symbol with the base unit of either
a basic or derived quantity, you are also allowed to specify one or more
*related* unit symbols by specifying the corresponding linear
relationship.