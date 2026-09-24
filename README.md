# Body-shape biometric recognition from silhouettes

Identifying people from their body shape alone, using silhouettes rather than gait dynamics: no deep
learning, just classical computer vision and a nearest-neighbour classifier.

MSc Artificial Intelligence coursework, COMP6211 Biometrics, University of Southampton, spring 2026.

## The data

Silhouettes from the Southampton Gait Database, provided by the module. **Not included here, and the
notebook's outputs are cleared**, because the data is not public and the images show identifiable
people. To run it, put the module's `Biometrics` folder (with its `training` and `test` subfolders)
next to the notebook.

Nine subjects, 88 probe images, evaluated leave-one-sequence-out.

## The pipeline

1. **Silhouette extraction** - HSV masking to separate the subject from the background.
2. **Geometric features** - a width profile taken down the body.
3. **PCA (eigensilhouettes)** - the silhouette space reduced to its main components.
4. **Feature fusion** - geometric plus appearance features.
5. **Nearest-neighbour classifier**, evaluated with leave-one-sequence-out cross-validation.

## Results

| Metric | Score |
|---|---|
| Rank-1 correct classification rate | 35.2% |
| Rank-2 | 62.5% |
| Rank-3 | 79.5% |
| Rank-5 | 94.3% |
| EER | 32.46% |
| AUC | 0.6627 |
| CCR at the EER threshold | 67.50% |

Chance is 11.1% with nine subjects, so rank-1 at 35.2% is about three times chance, and the right
person is in the top three 79.5% of the time. That is the honest summary: body shape alone carries
real identity information, but not enough to identify someone outright. The CMC curve climbs steeply
and then flattens, which says the classifier is usually close even when it is wrong.

## Running it

```bash
pip install -r requirements.txt
jupyter notebook body_shape_biometrics.ipynb
```

## Note

This is my own coursework code, published with my tutor's confirmation that the code I wrote is mine
to share. The assignment brief, the report and the dataset are not included, and the notebook
outputs are cleared.
