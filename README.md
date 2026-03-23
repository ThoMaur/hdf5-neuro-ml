# hdf5-neuro-ml

An HDF5-based standard for multimodal neurophysiology time-series data, optimized for machine learning and clinical interoperability.

## Overview

hdf5-neuro-ml is an open standard designed to bridge the gap between clinical neurophysiology data acquisition and machine learning workflows.

It provides a unified, efficient, and extensible structure for storing and analyzing multimodal time-series data, including:

- Electroencephalography (EEG)
- Near-infrared spectroscopy (NIRS)
- Nociception monitoring (NOL)
- Train-of-four (TOF)
- Vital and physiological parameters

## Motivation

Current data formats are fragmented across clinical and research domains:

- Clinical standards (e.g. DICOM EEG) focus on interoperability but are not optimized for machine learning.
- Research formats (e.g. EDF, NWB, BIDS) do not fully address real-time clinical data integration and multimodal intraoperative monitoring.

hdf5-neuro-ml aims to provide a lightweight, ML-ready data model that integrates both worlds.

## Key Features

- Unified time reference across all modalities
- Support for heterogeneous sampling rates
- Separation of raw signals and derived indices
- Efficient chunked storage using HDF5
- Optimized for machine learning pipelines
- Compatible with open-source tools (Python, MATLAB, R, Julia)
- Interoperability pathways to clinical standards (e.g. DICOM EEG)

## Repository Structure

- SPEC/ → Core specification of the standard
- SCHEMA/ → Data model and schema definitions
- EXAMPLES/ → Example datasets and usage
- MAPPINGS/ → Mapping to/from existing standards (DICOM, EDF, etc.)

## Status

Draft – under active development

## Citation

A DOI will be assigned via Zenodo upon first release.

## License

See LICENSE file.
