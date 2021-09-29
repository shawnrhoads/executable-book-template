# Preprocessing

Here is a description of the data preprocessing steps in a Markdown file.

## fMRIPrep

All preprocessing was implemented using **fMRIPrep** (Esteban et al., 2018), which includes anatomical T1-weighted brain extraction, anatomical surface extraction, head-motion estimation and correction, susceptibility-derived distortion estimation and unwarping, intrasubject registration, and spatial normalization (intersubject registration). All volumes were registered to the MNI (Montreal Neurological Institute) standard template. Automatic removal of motion artifacts using independent component analysis (ICA-AROMA) was performed on the preprocessed BOLD time series in MNI space and the resulting data was smoothed using a 6.0 mm^3 FWHM Gaussian kernel and the time series was scaled within voxels to represent percent signal change.

We used the following `bash` command with `singularity` to run `fmriprep`:
```
SUBID=1234
singularity run --bind /mnt:/mnt --cleanenv /mnt/data/singularity/fmriprep-20.2.3.simg /mnt/data/study/subjects /mnt/data/study/subjects/derivatives participant \
--work-dir /mnt/data/study/fmriprep-20.2.3_work \
--participant_label $SUBID \
--bold2t1w-dof 9 \
--output-spaces T1w:res-native MNI152NLin2009cAsym:res-native MNI152NLin6Asym:res-2 fsaverage:res-native \
--skull-strip-t1w force \
--ignore slicetiming \
--use-aroma \
--dummy-scans 0 \
--fs-license-file /mnt/data/freesurfer/license.txt \
--no-submm-recon \
--write-graph \
--fd-spike-threshold 0.5 \
--random-seed 2021
```

## First-Level Analysis

We then ran the resulting preprocessed data through a first-level GLM. We used the following `bash` command with `AFNI` to run `3dDeconvolve`:

```
subject_id=123
task_id=faces
3dDeconvolve \
    -input /mnt/data/study/firstlevel_glm/${subject_id}/preproc/${subject_id}_task-${task_id}_run-*_space-MNI152NLin6Asym_desc-smoothAROMAnonaggr_scaled.nii.gz \
    -mask /mnt/data/study/code/modeling/MNI152-graymatter-thr50-2mm.nii.gz \
    -polort A \
    -num_stimts 10 \
    -stim_times 1 /mnt/data/study/code/modeling/events/${subject_id}/${subject_id}_task-${task_id}_timing-condition_A.txt 'BLOCK(0.5,1)' -stim_label 1 condition_A \
    -stim_times 2 /mnt/data/study/code/modeling/events/${subject_id}/${subject_id}_task-${task_id}_timing-condition_B.txt 'BLOCK(0.5,1)' -stim_label 2 condition_B \
    -stim_file 3 "/mnt/data/study/code/modeling/events/${subject_id}/${subject_id}_task-${task_id}_confounds.txt[0]" -stim_base 3 -stim_label 12 csf \
    -stim_file 4 "/mnt/data/study/code/modeling/events/${subject_id}/${subject_id}_task-${task_id}_confounds.txt[1]" -stim_base 4 -stim_label 13 white_matter \
    -stim_file 5 "/mnt/data/study/code/modeling/events/${subject_id}/${subject_id}_task-${task_id}_confounds.txt[2]" -stim_base 5 -stim_label 14 rot_x \
    -stim_file 6 "/mnt/data/study/code/modeling/events/${subject_id}/${subject_id}_task-${task_id}_confounds.txt[3]" -stim_base 6 -stim_label 15 rot_y \
    -stim_file 7 "/mnt/data/study/code/modeling/events/${subject_id}/${subject_id}_task-${task_id}_confounds.txt[4]" -stim_base 7 -stim_label 16 rot_z \
    -stim_file 8 "/mnt/data/study/code/modeling/events/${subject_id}/${subject_id}_task-${task_id}_confounds.txt[5]" -stim_base 8 -stim_label 17 trans_x \
    -stim_file 9 "/mnt/data/study/code/modeling/events/${subject_id}/${subject_id}_task-${task_id}_confounds.txt[6]" -stim_base 9 -stim_label 18 trans_y \
    -stim_file 10 "/mnt/data/study/code/modeling/events/${subject_id}/${subject_id}_task-${task_id}_confounds.txt[7]" -stim_base 10 -stim_label 19 trans_z \
    -tout \
    -stim_times_subtract 1.25 \
    -x1D /mnt/data/study/firstlevel_glm/${subject_id}_task-${task_id}.xmat.1D \
    -censor /mnt/data/study/code/modeling/events/${subject_id}/trial_type/${subject_id}_task-${task_id}_outliers.txt \
    -bucket /mnt/data/study/firstlevel_glm/${subject_id}_stats.nii.gz
```