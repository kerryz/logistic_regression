# Description
Implements logistic regression to classify a given set of documents as one of two classes: 0 or 1. 

The loss function used is the ordinary least square, from which we derive an update rule that is implemented through stochastic gradient descent. A momentum term is added to avoid local minima. The early stop method is used to detect convergence and prevent overfitting. The system also uses k-fold cross validation for evaluation and will output the average recall, precision and f1 score to terminal.

Optionally, l2-regularization can be added to the calculations by setting the parameter `reg_const` to a non-zero value in `logistic_regression.py`. Currently, the value is set to 0 as initial experiments have shown that it doesn't improve performance on the given dataset for this particular homework assignment.

## Preprocessing
The system uses a bag-of-word approach to classify the documents. Each document is represented as a bag-of-word vector, but since this will generally produce a very sparse vector, only the words (features) with non-zero values are recorded in the feature files. 

Instead of using a simple term frequency approach, inspiration is drawn from the field of information retrieval and each term's [tf-idf](http://en.wikipedia.org/wiki/Tf%E2%80%93idf) value is used instead.

Also, instead of a simple word tokenization performed through `text.split()`, the [Penn Treebank](http://www.nltk.org/api/nltk.tokenize.html#module-nltk.tokenize.treebank) approach is used.

# How to run
Run the following commands in a terminal (note that the package `nltk` is required for preprocessing. However, if you only want to run the logistic regression, `main.py` can be run since the generated data from preprocessing is already included in this package):

	python preprocessing.py
	python main.py

If you want to process other documents than the ones provided in this repository, you can specify that through the command line interface. See the descriptions of `preprocessing.py` and `main.py` for further information.

## Data description

### Directory structure
The given documents should be partitioned into subsets and labeled. The document directory structure should be:

    data_root_dir
    |-- s1
        |-- class0
            |-- file101
            |-- file102
            |-- ...
        |-- class1
            |-- file111
            |-- file112
            |-- ...
    |-- s2
        |-- class0
            |-- file201
            |-- file202
            |-- ...
        |-- class1
            |-- file211
            |-- file212
            |-- ...
    |-- ...

Where `s1`, `s2`, etc. are subsets and the subdirectories `class0` and `class1` contain the documents for class 0 and class 1 respectively.

### File (document) format

* line 1: From (email address)
* line 2: Subject
* rest: Body

Example:

	From: admiral@jhunix.hcf.jhu.edu (Steve C Liu)
	Subject: Re: Bring on the O's

	I heard that Eli is selling the team to a group in Cinninati. This would
	help so that the O's could make some real free agent signings in the 
	offseason.
	...

# Requirements

* nltk
	* only required for preprocessing (Penn Treebank word tokenization)
* numpy
* Python 2.7.3

## nltk
After download, the 'punkt' and 'stopwords' modules are required. To download, open a python shell type

	>>> import nltk
	>>> nltk.download()

Then an installation window appears. Go to the 'Models' tab and select 'punkt' from under the 'Identifier' column. Then click Download and it will install the necessary files. Go to the 'Corpora' tab and download 'stopwords'.

# Results
This is the final output of some test runs using different parameter values:

	learning_rate = 20
	reg_const = 0
	momentum_constant = 0

	========================================
	Averages of 5-fold cross validation
	Recall:    0.969849246231
	Precision: 0.967213866185
	F1 Score:  0.96842753797
	========================================

.

	learning_rate = 1
	reg_const = 0
	momentum_constant = 0.9

	========================================
	Averages of 5-fold cross validation
	Recall:    0.970854271357
	Precision: 0.967131900575
	F1 Score:  0.968943256605
	========================================


# License

MIT License

Copyright (c) Kerry Zhang

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
"Software"), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE
LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION
WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.