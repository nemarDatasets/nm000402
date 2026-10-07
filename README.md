# Multi-Expert Seizure Annotation (spontaneous and stimulation-induced seizures in SEEG)

## Overview
Automated seizure detection and localization from intracranial EEG requires validated benchmark datasets with expert annotations, yet existing open datasets lack multi-expert consensus annotations and exclude stimulation-induced seizures. We present stereotactic EEG recordings from 78 seizures (44 spontaneous, 34 stimulation-induced) across 29 patients (19 from the University of Pennsylvania, 10 from the Children’s Hospital of Philadelphia) with drug-resistant epilepsy. Three or five board-certified epileptologists independently annotated each seizure for onset time, onset channels, and channels seizing at 10 seconds post-onset using a standardized protocol. All data follow Brain Imaging Data Structure (BIDS) standards and include electrode localizations, patient demographics, and clinical outcomes. This dataset enables the validation of seizure onset and spread detection and localization against human expert performance and supports comparative analysis of seizure networks across spontaneous and stimulation-induced seizures.

This NEMAR dataset redistributes Pennsieve Discover dataset 530, version 3 (doi:10.26275/dely-fzwx, published 2026-07-29 by
Penn CNT; licence on the record: "Creative Commons Attribution"; licence in the authors' dataset_description.json:
"CC-BY 4.0"). The release was already organised in BIDS by the authors (MNE-BIDS 0.17.0). Contents: 29 participants,
78 SEEG seizure recordings (EDF), 6.8 h in total, sampled at 512-2048 Hz.

## Contents
- `sub-<HUP|CHOP>###/ses-postimplant/ieeg/`: one EDF per seizure, with `_channels.tsv`, `_events.tsv/json` and `_ieeg.json`.
  The task label encodes the seizure type and the approximate onset time in seconds from the start of the implant recording,
  as named by the authors (`task-ictal<onset>`: spontaneous seizure; `task-stim<onset>`: stimulation-induced seizure).
- `participants.tsv/json`: age, sex, mesial-temporal epilepsy, unifocal, lesional, Engel outcome, follow-up, disease
  duration, age at onset, number of seizures and number of stimulation-induced seizures (definitions in participants.json).
- `annotations.tsv/json`: the multi-expert annotations, one row per seizure: per-clinician unequivocal electrographic onset
  (UEO) time, UEO channels, channels seizing 10 s after onset, the consensus values, stimulation parameters, semiology,
  LVFA at onset (column definitions in annotations.json). Listed in `.bidsignore` because BIDS has no slot for
  dataset-level annotation tables.
- `sub-*/ses-postimplant/ieeg/*_space-Other_electrodes.tsv/.json` + `_coordsystem.json`: BIDS electrode files generated from the authors' tables (HUP: native-space mm coordinates; CHOP: voxel indices only, units n/a). Column `label` renamed `name`, `size` = n/a, other columns kept.
- `derivatives/electrode-localization/`: the authors' per-subject electrode localisation tables (HUP: native mm, tkrRAS and voxel
  coordinates with DK ROI; CHOP: voxel coordinates, tissue class, DK ROI), moved byte-identically from the release's non-BIDS `sub-*/derivatives/` folders
  (mapping in `sourcedata/pennsieve-530-v3/moved_files.tsv`).
- `sourcedata/pennsieve-530-v3/`: the Pennsieve record files (readme.md, manifest.json, changelog.md, banner.jpg), the
  release's original `README` and `dataset_description.json`, the Pennsieve file listing with checksums, and our download
  verification (every file matched the Pennsieve SHA-256).

## Changes made for NEMAR
No signal file (EDF), channels, events or ieeg sidecar was modified. Changes:
- the authors' electrode tables were moved byte-identically to `derivatives/electrode-localization/` (see above), and BIDS
  `_space-Other_electrodes.tsv/.json` + `_coordsystem.json` were generated from them (HUP: native-space mm coordinates;
  CHOP: voxel indices only, units n/a; `label` renamed `name`, `size` = n/a; the authors' `matter` Levels map moved into the
  column Description because the values use other spellings such as 'grey');
- `participants.json` `outcome`: the integer Levels map was moved into the Description (values are Engel subclasses such as
  1.1, which the validator rejects against integer levels); participants.tsv values unchanged;
- `dataset_description.json`: License written as SPDX `CC-BY-4.0`, Authors taken from the Pennsieve record's contributor
  list, Pennsieve DOI added to ReferencesAndLinks and HowToAcknowledge;
- this README replaces the release README (kept verbatim below and in sourcedata).

## Privacy
EDF headers carry no patient information (patient field `X X X X`, start date 01.01.85 set by the authors); scans.tsv
acq_time is `n/a`. Subject labels are the authors' study codes. Clinician names are replaced by `Clin #` in the release.

## Ethics approval
From the authors' dataset_description.json (EthicsApprovals): "University of Pennsylvania Human Research Protections
Program, Institutional Review Boards (Protocol 703979, 811097, and/or 821778)".

## Funding
As listed by the authors in dataset_description.json (Funding).

## How to cite
Cite the dataset (doi:10.26275/dely-fzwx) and the manuscript https://doi.org/10.64898/2026.01.15.26344025.

## Licence
Creative Commons Attribution 4.0 (CC-BY-4.0), as released by the authors.

## Original release README
﻿References
----------
Appelhoff, S., Sanderson, M., Brooks, T., Vliet, M., Quentin, R., Holdgraf, C., Chaumon, M., Mikulan, E., Tavabi, K., Höchenberger, R., Welke, D., Brunner, C., Rockhill, A., Larson, E., Gramfort, A. and Jas, M. (2019). MNE-BIDS: Organizing electrophysiological data into the BIDS format and facilitating their analysis. Journal of Open Source Software 4: (1896).https://doi.org/10.21105/joss.01896

Holdgraf, C., Appelhoff, S., Bickel, S., Bouchard, K., D'Ambrosio, S., David, O., … Hermes, D. (2019). iEEG-BIDS, extending the Brain Imaging Data Structure specification to human intracranial electrophysiology. Scientific Data, 6, 102. https://doi.org/10.1038/s41597-019-0105-7
