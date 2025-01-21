# Predict schizophrenia using brain anatomy

Predict schizophrenia from brain grey matter (GM). schizophrenia is associated with diffuse and complex pattern of brain atrophy. We will try to learn a predictor of the clinical status (patient with schizophrenia vs. healthy control) using GM measurements on the brain participants.

## Dataset

There are 410 samples in the training set and 103 samples in the test set.

### Input data

Voxel-based_morphometry [VBM](https://en.wikipedia.org/wiki/Voxel-based_morphometry)
using [cat12](http://www.neuro.uni-jena.de/cat/) software which provides:

- Regions Of Interest (`rois`) of Grey Matter (GM) scaled for the Total
  Intracranial Volume (TIV): `[train|test]_rois.csv` 284 features.

- VBM GM 3D maps or images (`vbm3d`) of [voxels](https://en.wikipedia.org/wiki/Voxel) in the
  [MNI](https://en.wikipedia.org/wiki/Talairach_coordinates) space:
  `[train|test]_vbm.npz` contains 3D images of shapes (121, 145, 121).
  This npz contains the 3D mask and the affine transformation to MNI
  referential. Masking the brain provide *flat* 331 695 input features (voxels)
  for each participant.

By default `problem.get_[train|test]_data()` return the concatenation of 284 ROIs of
Grey Matter (GM) features with 331 695 features (voxels) within a brain mask.
Those two blocks are higly redundant.
To select only on ROIs (`rois`) features do:

```
X[:, :284]
```

To select only on (`vbm`) (voxel with the brain) features do:

```
X[:, 284:]
```

### Target

The target can be found in `[test|train]_participants.csv` files, selecting the
`age` column for regression problem.

## Evaluation metrics

[sklearn metrics](https://scikit-learn.org/stable/modules/model_evaluation.html)

The main Evaluation metrics is the Root-mean-square deviation
[ROC-AUC](https://en.wikipedia.org/wiki/Receiver_operating_characteristic), the Area Under Curve of eceiver operating characteristic curve, or ROC curve

## Links

- [RAMP studio](https://ramp.studio/)
- [RAMP-workflow’s documentation](https://paris-saclay-cds.github.io/ramp-docs/ramp-workflow/)
- [RAMP-workflow’s github](https://github.com/paris-saclay-cds/ramp-workflow)
- [RAMP Kits](https://github.com/ramp-kits)

## Installation

1. Clone the repository to your machine:
   
   ```bash
   git clone https://github.com/salmabens/predict-schizophrenia-from-gray-matter.git
   cd predict-schizophrenia-from-gray-matter
   ```

2. Create a virtual environment:
   #### On Windows:
         
   ```bash
   python -m venv env
   ```
   #### On macOS/Linux:
         
   ```bash
   python3 -m venv env
   ```
3. Activate the virtual environment:

   #### On Windows:
   
   ```bash
   .\env\Scripts\activate
   ```
   #### On macOS/Linux:
   
   ```bash
   source env/bin/activate
   ```

4. Install the dependencies using pip:
   
   ```bash
   pip install -r requirements.txt
   ```
