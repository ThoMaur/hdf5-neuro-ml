# hdf5-neuro-ml: A standard for EEG time-series data in HDF5 optimized for machine learning (Profile 1.2)


hdf5-neuro-ml is an open standard for storing EEG time-series data in HDF5, designed for efficient analysis and direct integration into machine learning workflows.

This repository contains the publication package for the EEG-only profile of the `hdf5-neuro-ml` standard, aligned with the current production implementation in the acquisition pipeline.

## DOI

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19190860.svg)](https://doi.org/10.5281/zenodo.19190860)

## Scope

This release covers **EEG only**. Other modalities are explicitly out of scope for Profile 1.2.

## Normative specification

The specification in `SPEC/HDF5_NEURO_ML_STANDARD.md` is normative.  
All compliant implementations MUST follow this specification.

## Repository contents

| Path | Description |
|------|-------------|
| `SPEC/HDF5_NEURO_ML_STANDARD.md` | Full normative specification |
| `SCHEMA/HDF5_NEURO_ML_root_metadata.schema.json` | JSON Schema for root metadata |
| `EXAMPLES/` | Real and synthetic EEG example files |
| `MAPPINGS/README.md` | Placeholder for interoperability mappings |
| `HDF5_STRUCTURE_PROFILE_1_2.txt` | ASCII tree of the current pipeline implementation |
| `CHANGELOG.md` | Version history |
| `LICENSE` | License for this package |
| `CITATION.cff` | Citation metadata |
| `.zenodo.json` | Zenodo metadata for DOI registration |
| `ZENODO_CHECKLIST.md` | Pre-release checklist |
| `requirements.txt` | Python dependencies for example generation |

## Current implementation status

Profile 1.2 represents the current production implementation used in the data acquisition pipeline.

## Minimal valid file

A minimal valid file MUST contain:

- root attributes as defined in the schema
- `/time/timestamps`
- at least one `/signals/channel_k` dataset
- equal length across timestamps and all signal datasets

## How to cite

After publication on Zenodo, the version-specific DOI SHOULD be used for citation and reproducibility.

## License

This package is released under CC BY 4.0 unless otherwise noted.


DOI trigger v1.2.2.
