
# Schema

This directory defines the formal structure of the hdf5-neuro-ml data model.

## Purpose

- Ensure consistency across datasets
- Enable validation of files
- Facilitate interoperability

## Components

- Root metadata schema
- Channel definitions
- Signal attributes
- Processing levels

## Example Fields

### Root Attributes
- subject_id
- recording_start_time
- sampling_reference

### Signal Attributes
- sampling_rate
- unit
- channel_name
- modality

## Future Work

- JSON schema definitions
- Validation tools
- Automatic schema checking
