[article.md](https://github.com/user-attachments/files/29049356/article.md)
# RFA Converter for Revit: Batch Export of RFA Families to IFC and SAT

## Introduction

When working with Revit families, there is often a simple but repetitive task: exporting a family to another format.

For example, a BIM specialist may need to create an IFC file for data exchange with another BIM platform, or export SAT geometry for further use in a CAD environment.

This can be done manually using standard Revit tools, but the process becomes time-consuming when multiple families need to be processed. Each file has to be opened, configured, exported, checked and saved separately.

To simplify this workflow, I developed a small Revit add-in called **RFA Converter**.

The purpose of the tool is to automate the export of Revit `.rfa` family files to **IFC** and **SAT** formats, while also preparing family parameters for downstream BIM/CAD workflows.

![RFA Converter button in Revit](images/01-rfa-converter-button.png)

## Project Goal

The main goal of the project was to reduce repetitive manual operations during the preparation of Revit families for external systems.

The add-in was designed to solve several practical tasks:

- export Revit families to IFC;
- export Revit families to SAT;
- support batch processing of multiple `.rfa` files;
- allow IFC version selection;
- generate parameter tables for SAT export;
- filter out unused or missing parameters;
- optionally remap parameters for Model Studio workflows;
- avoid unnecessary empty files and excessive log output.

The result is not a universal converter for all BIM data, but a focused automation tool for a specific and common interoperability workflow.

## Why This Was Needed

In many BIM/CAD environments, Revit families are not used only inside Revit.

They may need to be transferred to another BIM system, reused in a CAD workflow, converted into neutral geometry, or prepared for a company-specific engineering platform.

A typical manual workflow may look like this:

1. Open a Revit family.
2. Check its parameters.
3. Choose an export format.
4. Configure IFC or SAT settings.
5. Export the file.
6. Save the result to the correct folder.
7. Repeat the same steps for the next family.

This process is repetitive, slow and prone to errors.

The situation becomes even more complicated when parameter mapping is required. Different BIM/CAD systems may use different names for the same object properties. As a result, geometry can be exported successfully, but attribute data may become incomplete or inconvenient for further use.

The **RFA Converter** add-in was created to automate this part of the workflow.

## Main Workflow

After launching the **RFA Converter** command, the user selects one of two export modes:

- **RFA to IFC**
- **RFA to SAT**

![Export mode selection](images/02-export-mode-selection.png)

This approach keeps the interface simple. The user first selects the target export scenario, and only then the add-in shows the settings related to that scenario.

This is more convenient than showing all settings at once, because IFC and SAT workflows require different options.

## RFA to IFC Export

The IFC workflow is used when a Revit family needs to be exported as a BIM object for exchange with another system.

The add-in supports several IFC versions:

- IFC2x3;
- IFC4;
- IFC4.3.

![IFC version selection](images/03-ifc-version-selection.png)

Version selection is important because different receiving systems may support different IFC versions. For example, some older workflows may still require IFC2x3, while newer systems may work better with IFC4.

After selecting the IFC version, the add-in can perform the export using either a standard workflow or a parameter remapping workflow.

## IFC Export With Optional Parameter Remapping

One of the important additions to the plugin is optional parameter remapping for Model Studio workflows.

After the user selects the IFC export mode, the add-in asks whether the parameters should be remapped to Model Studio parameters.

![Model Studio parameter remapping](images/04-model-studio-remapping.png)

The user can choose one of two options:

- remap parameters to Model Studio;
- keep standard IFC/Revit parameters.

This is useful because Revit parameters and target-system parameters may not have the same names. For example, a property may exist in a Revit family under one parameter name, while the receiving system expects a different system parameter.

Without parameter preparation, the exported geometry may be correct, but the attribute structure may be less useful for further processing.

The remapping workflow helps prepare the data before the file is imported into the target CAD/BIM environment.

## Standard IFC Export and IFC Export With Remapping

The add-in supports two IFC export scenarios.

### Standard IFC Export

This mode is used when the goal is to quickly export a Revit family to IFC without additional parameter transformation.

It is suitable for simple exchange tasks where the receiving system does not require a custom parameter structure.

### IFC Export With Parameter Remapping

This mode is used when the exported IFC file must contain parameters prepared for a specific downstream workflow.

In this project, the main target workflow was related to Model Studio, but the same idea can be adapted to other systems where structured parameter mapping is required.

This makes the add-in more flexible. The same tool can be used both for quick export and for more controlled data preparation.

## Export Results

After processing, the add-in saves the exported files to the selected output folder.

The result may include IFC files, SAT files and parameter tables depending on the selected workflow.

![Exported SAT and IFC files](images/05-result-sat-ifc.png)

For IFC batch export, the add-in processes multiple RFA files and saves the resulting IFC files in the target directory.

![IFC batch export result](images/06-batch-result.png)

## Parameter Handling

A key part of the plugin is parameter processing.

During development, one of the issues was that parameter tables could include rows from the mapping file even when those parameters were not actually present in the current family.

This made the exported tables less readable and less useful.

The current logic is more selective: the add-in exports only the parameters that are actually found in the processed family.

This reduces unnecessary data and makes the output easier to use.

If optional ADSK parameters are missing or not filled in, this is not treated as a critical error. The export can still continue. In that case, the geometry is exported, and the missing parameter data is simply skipped.

This behavior is important because not every family contains the same set of parameters. A missing optional parameter should not stop the entire conversion process.

## RFA to SAT Export

The second main workflow is **RFA to SAT**.

SAT export is useful when the main goal is to extract geometry from a Revit family for further CAD processing.

Unlike IFC, SAT is not a BIM format. It stores geometry, but it does not preserve BIM metadata in the same way. Because of this, the add-in exports geometry and parameters separately.

In SAT mode, the add-in creates:

- SAT geometry files;
- parameter tables.

![SAT export with parameter tables](images/07-sat-and-parameters.png)

This makes the SAT workflow suitable for pipelines where geometry and metadata need to be transferred as separate but related outputs.

For example, the SAT file can be used as CAD geometry, while the parameter table can be used as an attribute source for further processing in another system.

## Parameter Table

When exporting to SAT, the add-in generates a parameter table for the processed family.

The table contains only actual parameters found in the family. This avoids large empty tables and makes the exported data easier to inspect.

![Parameter table](images/08-parameter-table.png)

The parameter table can be used as an intermediate data layer between Revit and another BIM/CAD system.

The general idea is:

- geometry is exported through SAT;
- attribute information is exported through a table;
- the target system can then use both sources together.

This approach is especially useful when the receiving software does not directly preserve all Revit family metadata during geometry import.

## Batch Processing

Another important feature is batch processing.

In real projects, it is rarely necessary to convert only one family. More often, there is a folder containing several `.rfa` files that need to be processed using the same export logic.

The add-in allows the user to select a source folder with Revit families.

![Source folder selection](images/09-batch-folder-selection.png)

Then the user selects the output folder where the exported files will be saved.

![Output folder selection](images/10-output-folder-selection.png)

After that, the add-in processes the files sequentially and reports the result.

![Batch processing summary](images/11-batch-processing-result.png)

This reduces manual work and makes the export process more consistent.

## Practical Value

The value of this add-in is not that it performs something impossible with standard Revit tools.

The value is that it removes repetitive manual steps from a common BIM/CAD workflow.

Instead of manually opening and exporting each family, the user can:

1. launch the **RFA Converter** command;
2. choose IFC or SAT export;
3. select the required settings;
4. choose input and output folders;
5. receive the exported files.

This saves time, reduces the chance of mistakes and makes the process more predictable.

## Current Features

The current version of the add-in includes the following features:

- batch processing of Revit `.rfa` files;
- export to IFC;
- export to SAT;
- IFC version selection;
- optional parameter remapping for Model Studio;
- generation of SAT parameter tables;
- filtering of missing or unused parameters;
- cleaner output without unnecessary empty files;
- export continuation when optional parameters are missing.

## Limitations

The add-in does not repair corrupted Revit families.

If a family contains invalid elements, unsupported geometry, or cannot be exported correctly by Revit itself, the result may be affected.

SAT export should also be understood correctly. SAT is a geometry format, not a BIM data format. Because of this, metadata is exported separately as a parameter table.

The connection between SAT geometry and exported parameters must be handled in the target workflow or receiving system.

The add-in was developed and tested for a specific practical workflow, so adaptation may be required for other Revit versions, company standards or downstream BIM/CAD systems.

## Project Status

This project is currently a practical prototype and internal workflow tool.

It was developed to solve a real task related to Revit family export and preparation of geometry and parameter data for downstream engineering software.

The current version demonstrates the core workflow:

- RFA to IFC;
- RFA to SAT;
- batch processing;
- parameter table export;
- optional parameter remapping.

Further development may include improved configuration files, more flexible parameter mapping, support for additional Revit versions and deeper integration with downstream CAD/BIM platforms.

## Conclusion

**RFA Converter** is a small Revit add-in created to automate the export of Revit family files to IFC and SAT formats.

The tool started as a simple export button, but later evolved into a more complete BIM/CAD interoperability workflow.

It helps prepare both geometry and parameter data, supports batch processing and provides optional parameter remapping for Model Studio-related workflows.

The project is a practical example of how a small automation tool can reduce repetitive work in BIM processes and make data exchange between engineering systems more predictable.
