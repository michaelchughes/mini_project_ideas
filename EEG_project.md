Short Project: Classification of Epileptic Seizures from Time Series data

Given a dataset of short bursts (~1 second long) of EEG brain recordings, can we distinguish epileptic seizures from other patterns?

In other words, this is a binary classification problem:
* input is a 1D time series
* output is a binary 0/1

Dataset:
-- 500 subjects, each either had seizures (y=1), or some other pattern (y=2,3,4 or 5)
-- Each subject's EEG 1D signal recorded for ~23 seconds at >> 100 Hz
-- Sequences then post-processed into 1 second chunks, each of length 178

Use the "data.csv" file from this URL: https://archive.ics.uci.edu/ml/datasets/Epileptic+Seizure+Recognition

Each row of data.csv corresponds to data for a 1 second chunk:
-- column 1 is a string that indicates the subject and the chunk
         'X21.V1.791' means the 21-st chunk from subject "V1.791"

-- columns 2-178 are the time-series 1D observed data "x"
-- last column is the label "y" (y=1 means seizure, other values mean non-seizure)

Original research paper: http://users.fs.cvut.cz/ivo.bukovsky/PROJEKT/Data/Realna/BIO/EEG/reference/PRE61907.pdf

More information on the dataset:
http://epileptologie-bonn.de/cms/front_content.php?idcat=193&lang=3&changelang=3


High-level questions:
* Can we build a reasonable classifier for this dataset?
* What feature patterns are important for this decision

# Step-by-step approach:

## Week 1) Dataset descriptive stats

Make a plots of the time-series. Compare time-series for:
* "chunks" within a subject 
* chunks from different subjects with the same label
* chunks from different subjects who have seizures vs. not

High-level goal:
* Can you tell the two classes apart? 
* Educated guess: What performance is possible? Perfect classifier?

Make plots of the label frequencies:
* Does each subject have only one label? Or do we have seizure and non-seizure data from the same subject?

## Week 2) Train some baseline classifiers

Come up with an appropriate train/validation/test split. Be sure to put all data that comes from one subject into the same split (e.g. all 23 chunks from subject "xyz" should go to train only, not to train and valid).

Describe your approach, and provide statistics for the train/valid/test splits (how many subjects in each, how many chunks in each, etc).

Next, compute a feature representation of the time-series. Use just simple descriptive statistics of each time-series x_1, x_2, ... x_T, such that the feature vector might be something like:

```
    feature(x) = [mean(x)  var(x)  slope(x)  slope(x[:L/2]) slope(x[L/2:]) ]
```

Train two classifiers: LogisticRegression and ExtraTrees (use sklearn or similar). 

Show confusion matrices on training, validation, and test.

## Future

* Train some time-series aware classifiers (RNNs)
