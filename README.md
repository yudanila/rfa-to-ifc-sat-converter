# RFA to IFC/SAT Converter

A Revit plugin for batch conversion of RFA family files to IFC and SAT formats with parameter mapping for BIM/CAD workflows.

## Overview

This project is focused on automating the conversion of Revit family files into exchange formats that can be used in downstream BIM/CAD systems.

The plugin is designed for Revit 2020 and provides a simplified workflow for converting RFA files into IFC or SAT while preparing family parameters for further use in engineering software.

## Problem

Manual conversion of Revit families is repetitive, time-consuming and prone to errors.

Typical issues include:

* manual opening of each RFA file;
* inconsistent IFC export settings;
* missing or unused parameters;
* repeated preparation of family data;
* lack of a clear mapping between Revit parameters and downstream BIM/CAD requirements.

## Solution

The plugin automates the conversion process and prepares structured parameter data for exchange workflows.

## Features

* Batch processing of RFA files
* RFA to IFC conversion
* RFA to SAT conversion
* IFC version selection
* Parameter mapping workflow
* Excel-based parameter export for SAT workflows
* Filtering of unused family parameters
* Simplified user interface for selecting conversion mode and folders

## Screenshots

### RFA Converter button in Revit

![RFA Converter button](docs/images/01-rfa-converter-button.png)

### Export mode selection

![Export mode selection](docs/images/02-export-mode-selection.png)

### IFC version selection

![IFC version selection](docs/images/03-ifc-version-selection.png)

### Model Studio parameter remapping

![Model Studio parameter remapping](docs/images/04-model-studio-remapping.png)

### Exported SAT and IFC files

![Exported SAT and IFC files](docs/images/05-result-sat-ifc.png)

### IFC batch export result

![IFC batch export result](docs/images/06-batch-result.png)

### SAT export with parameter tables

![SAT export with parameter tables](docs/images/07-sat-and-parameters.png)

### Parameter table

![Parameter table](docs/images/08-parameter-table.png)

### Source folder selection

![Source folder selection](docs/images/09-batch-folder-selection.png)

### Output folder selection

![Output folder selection](docs/images/10-output-folder-selection.png)

### Batch processing summary

![Batch processing summary](docs/images/11-batch-processing-result.png)

## Tech stack

* C#
* .NET Framework
* Autodesk Revit 2020 API
* IFC export workflow
* SAT export workflow
* Excel-based parameter mapping

## Current status

Prototype / in development.

The project is being developed as a practical BIM/CAD automation tool for engineering workflows.

## Planned improvements

* Cleaner parameter mapping workflow
* Improved error handling
* Minimal logging mode
* More stable batch conversion
* Documentation and usage examples

## Notes

The public repository contains project documentation and portfolio materials.
Source code may be published later after cleanup and removal of internal or sensitive data.
