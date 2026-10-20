# easter_eggs_exist_in_public_neuraldata

1. The Problem
Public neural data archives (DANDI, OpenNeuro, DABI) host recordings that are distributed as "de-identified." The de-identification procedures focus on stripping explicit identifiers: names, dates of birth, contact information. The assumption is that once these fields are removed, the recording is anonymous.

This project tests that assumption for the NWB format, which is the mandatory container format for electrophysiology data on DANDI. The NWB schema is self-describing and schema-enforced: it requires structured metadata (subject_id, session_start_time, device metadata, age, sex, genotype) and it stores neural signals alongside behavioral time series and trial structure. The question is whether the combination of these channels — metadata, neural signal, behavioral annotations — constitutes a de facto identifier that survives anonymization.

This is not a hypothetical. The neural privacy literature has established:

EEG carries individually distinctive "brainprint" signatures (within-dataset identification).

Cross-modal biometric fusion (EEG + keystroke) achieves high authentication accuracy in paired, within-session settings.

Consumer behavioral biometrics (typing rhythm, gait, speech prosody) are individually distinctive.

HDF5 user-defined metadata is identified by the HDF Group as a privacy-sensitive asset class.

What has not been established:

Whether invasive NWB recordings carry a stable behavioral signature across sessions.

Whether that signature is linkable to a separate consumer biometric dataset (unpaired, cross-dataset).

Whether NWB metadata on public archives constitutes a singling-out risk.

The graded privacy risk profile (singling out vs. linkage vs. attribute inference) for this modality pair.

2. Research Questions
The project is structured as a graded sequence. Each claim is weaker than the one below it, and each is independently testable and publishable.

RQ1 (Metadata audit): What identifying information exists in NWB metadata on DANDI, and what fraction of dandisets are metadata singletons?

RQ2 (Signal singling out): Are NWB records distinguishable from one another based on their neural-behavioral signal content alone, with metadata stripped?

RQ3 (Attribute inference): Can behavioral attributes (e.g., reaction-time profile, movement kinematics, trial-by-trial variability) be predicted from the neural signal?

RQ4 (Cross-dataset linkage): Can an anonymized NWB record be linked to the same subject's record in a separate consumer behavioral biometric dataset using a shared latent representation?

RQ1 is deterministic and near-certain to produce a result. RQ4 is the highest-risk, highest-reward claim and is the primary scientific contribution.

3. What Is Novel
Component	Existing Work	This Project
Neural privacy	EEG brainprints, EEG foundation-model leakage audits	Invasive NWB recordings; graded claim structure
Cross-modal biometrics	Paired, within-session EEG-keystroke authentication	Unpaired, cross-dataset linkage; NWB as source
Metadata privacy	HDF5 metadata sensitivity (general)	NWB-specific field inventory on a public archive
Behavioral signature	Keystroke, gait, speech individually distinctive	Whether the same signature appears in neural data
The novelty is not in any single technique. The alignment machinery (CCA, PNBA, CANDY), the SAE variants (TopK, ReLU, archetypal, group-sparse), and the LLM interpretation pipelines all exist. The novelty is in the question: does the behavioral signature in anonymized neural data survive anonymization, and is it linkable across modalities and datasets?

4. Data Sources
Source	Format	Role	Notes
DANDI	NWB (mandatory)	Primary for RQ1, RQ2	Schema-enforced metadata; variable behavioral annotation coverage
OpenNeuro	BIDS	Candidate for RQ3, RQ4	Task-structured; standardized event files; EEG/MEG/fMRI/iEEG
DABI	BIDS + NWB	Candidate	Human iEEG focus
Consumer biometric datasets	Various	Required for RQ4	Keystroke dynamics, gait, speech rhythm; subject overlap is the binding constraint
Binding constraint: RQ4 requires paired or linkable data — the same subject must appear in both a neural dataset and a behavioral biometric dataset. Whether such overlap exists is an open empirical question and must be resolved before RQ4 is attempted.

work in progress! (˶ᵔ ᵕ ᵔ˶) (@ easter_eggs_in_neuraldata)
