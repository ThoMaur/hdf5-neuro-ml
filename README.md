# hdf5-neuro-ml

An HDF5-based standard for multimodal neurophysiology time-series data, optimized for machine learning and clinical interoperability.

## Motivation

Current neurophysiology data formats are fragmented across clinical and research domains.
This project aims to bridge the gap between clinical interoperability (e.g. DICOM EEG) and machine learning workflows.

## Features

- Multimodal time-series support (EEG, NIRS, NOL, TOF, vital parameters)
- Unified time reference
- Separation of raw signals and derived indices
- Efficient chunked storage (HDF5)
- ML-ready data access

## Structure

- SPEC/ → Core specification
- SCHEMA/ → Data schema definitions
- EXAMPLES/ → Example datasets
- MAPPINGS/ → Interoperability mappings

## Status

Draft – under active development

## Citation

DOI will be added after first Zenodo release.
