# SimpleDynProp

(C) Copyright 2023 by Autodesk, Inc.

## Overview
SimpleDynProp is a sample implementation demonstrating the use of `IDynamicProperty`, `ICategorizedProperty`, and `IEnumProperty` to create dynamic properties in the Object Property Manager (OPM) of AutoCAD.

## Contents
- [Abstract](#abstract)
- [Build Instructions](#build-instructions)
- [How It Works](#how-it-works)

## Abstract
This sample illustrates how to define dynamic properties for objects in AutoCAD’s Object Property Manager (OPM). Dynamic properties provide additional attributes beyond the static properties of an object, making them useful for customization and extended metadata storage.

## Build Instructions
1. Open `SimpleDynProps.vcxproj` in Visual Studio 2022 or later.
2. Configure the project to include ObjectARX SDK paths (both include and library directories).
3. Ensure the target platform is set to **x64**.
4. Build the project via **Build > Build SimpleDynProps.arx**.

## How It Works
### Dynamic Properties in OPM
The OPM displays both static and dynamic properties for objects. Dynamic properties allow for additional, programmable attributes stored in an `AcDbXrecord` within the extension dictionary of an entity.

The following structure represents this hierarchy:
```
AcDbEntity
    ├── AcDbDictionary
          ├── AcDbXrecord (double, double, long)
```

### COM-based Dynamic Properties
Dynamic properties are implemented as COM objects that must at least support the `IDynamicProperty` interface. Additional interfaces refine how the properties appear in OPM. This sample leverages **ATL (Active Template Library)** to simplify COM implementation.

### Implemented Properties
This sample demonstrates three types of dynamic properties:
1. **Simple Property** (`SimpleProperty.h`, `SimpleProperty.cpp`)
   - Implements `IDynamicProperty`.
2. **Categorized Property** (`CategorizedProperty.h`, `CategorizedProperty.cpp`)
   - Implements `IDynamicProperty` and `ICategorizeProperties`.
3. **Enumerated Property** (`EnumProperty.h`, `EnumProperty.cpp`)
   - Implements `IDynamicProperty`, `ICategorizeProperties`, and `IEnumProperty`.

### Document Locking in OPM
Since OPM is a modeless interface, document locking is required to access and modify drawing objects safely.

### Usage Instructions
1. Load `SimpleDynProps.arx` in AutoCAD.
2. Open the Object Property Manager (use the `modify` command).
3. Draw any entity.
4. Use the `assigndata` command to assign an `AcDbXrecord` to the entity.
5. Click on the entity to view its dynamic properties.
6. Modify the values directly in OPM to update the `Xrecord` data.

This sample provides a foundation for extending object properties dynamically in AutoCAD, allowing developers to customize behavior and metadata efficiently.

