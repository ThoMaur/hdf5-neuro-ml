# Specification

## Scope

This specification defines the structure of the hdf5-neuro-ml standard for multimodal neurophysiology time-series data.

The standard is designed for:

- High-resolution EEG data
- Multimodal intraoperative monitoring
- Machine learning workflows
- Long-duration recordings

## Design Principles

### 1. Unified Time Model
All data streams share a common time reference to ensure precise synchronization across modalities.

### 2. Separation of Data Types
- Raw biosignals are stored separately from derived indices
- Device-specific outputs are clearly labeled

### 3. Multimodal Support
The model supports simultaneous acquisition of multiple data sources with different sampling rates.

### 4. ML-Oriented Structure
Data is structured for:
- Efficient slicing
- Batch processing
- Feature extraction

### 5. Interoperability
The standard enables mapping to and from:
- DICOM EEG
- EDF / EDF+
- BrainVision formats

## Data Hierarchy (Conceptual)

/ (root)
├── metadata/
├── signals/
│   ├── eeg/
│   ├── nirs/
│   ├── vital/
├── derived/
│   ├── indices/
│   ├── features/
├── events/
├── annotations/

## Future Extensions

- Real-time streaming support
- Standardized feature representations
- Integration with ML pipelines
