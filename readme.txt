SimpleDynProp sample Readme.txt

 (C) Copyright 2023 by Autodesk, Inc.

 Implementation showing IDynamicProperty, ICategorizedProperty, IEnumProperty 

Contents:
=========

1. Abstract
2. Build Instructions
3. How it works, What it shows
4. Revision History

1.Abstract
==========

This sample shows how to create dynamic properties in the Object Property Manager of AutoCAD.

2. Build Instructions
=====================

1. Load SimpleDynProps.vcxproj into Visual Studio 2022 or later.
2. Add ObjectARX SDK include and library paths to the project settings.
3. Ensure that the project is set to build for the desired platform (x64).
4. Build the project (Build/Build SimpleDynProps.arx).


3. How it works, What it shows
==============================

OPM can show so-called dynamic properties in addition to the "static" properties of
an object. Dynamic properties can be used for many different purposes. In this example,
we have three properties that show three values stored in an AcDbXrecord that resides
in the extension dictionary of an entity.

The following figure shows this scenario:

AcDbEntity
|_AcDbDictionary
       |_AcDbXrecord (double, double, long)

Dynamic properties are COM objects that implement at least the IDynamicProperty interface.
(There are other interfaces that can flavor how the dynamic property is shown in OPM.)

Since the sample has to implement a COM object, it uses ATL (Microsoft Active Template
Library) to simplify the process. 

The sample currently shows three properties:
1. A simple property (SimpleProperty.h, SimpleProperty.cpp). This implements
   IDyanamicProperty alone.
2. A categorized property (CategorizedProperty.h, CategorizedProperty.cpp).
   This implements IDynamicProperty and ICategorizeProperties.
3. An enumerated property (Enumproperty.h, EnumProperty.cpp). This implements
   IDynamicProperty, ICategorizeProperties and IEnumProperty.

Since the OPM is a modeless user interface, the sample shows the document locking step
necessary to access the drawing.

Here are the steps to try the sample:
1. Load SimpleDynProps.arx.
2. Bring up OPM (modify command).
3. Draw any entity.
4. Use the assigndata command to assign the xrecord to the entity.
5. Click on the entity to see its properties.
6. Change the values in the xrecord through the dynamic properties.


