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
