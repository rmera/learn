# Gradient-boosting learning for multi-class classification.

## Important note: 

There is a bug in the regular gradient boosting implementation. Please dont' use it as long as this note is up. The XGBoost implementation is not affected.

## Introduction

chemLearn is a simple library that implements simple versions of gradient boosting
and [XGBoost](https://github.com/dmlc/xgboost) ([reference](https://arxiv.org/abs/1603.02754)) for classification, in pure Go. 

The goal is for chemLearn to become a part of goChem when its mature enough, hence the name. Still, there is nothing specific about Chemistry in the library.

# Features

* Simple implementation and data format. It's quite easy for any program to put the data into chemLearn's "Databunch" format.

* The library is pure Go, so there are no runtime dependencies. There is only one compilation-time dependency (the [Gonum library](www.gonum.org)).

* The library can serialize models in JSON format, and recover them. 

* Some facilities, such as cross-validation and file-reading (a _very_ naive/incomplete)
reader for the libSVM format), are provided.

* The cross-validation grid search for the hyperparameters can run in parallel



Both the regular gradient-boosting as well as the xgboost implementations are close ports/translations from the following Python implementations:

* [Gradient boosting multi-class classification from scratch](https://randomrealizations.com/posts/gradient-boosting-multi-class-classification-from-scratch/)
* [XGBoost from scratch](https://randomrealizations.com/posts/xgboost-from-scratch/)
* [Decision tree from scratch](https://randomrealizations.com/posts/decision-tree-from-scratch/)

by [Matt Bowers](https://github.com/mcb00)


## Things that are missing

Many of these reflect the fact that I mostly work with rather small, dense datasets. 

* Column subsampling. I expect this to be implemented soon, as it seems pretty easy to do.
* There are only exact trees, and no sparsity-awareness.
* In general, computational performance is not a priority for this project, at least for now. 
* As mentioned above, the libSVM reading support is very basic, and there is no other file-format supported (such as csv). 
* Only classification is supported. Still, since its  multi-class classification using one-hot-encoding, and the "activation function" (softmax by default) can be changed, I suspect you can trick the function into doing regression by giving one class and an activation function that does nothing.
* There is nothing to deal with missing features in the samples.
* The tests are rather messy and, while complete, more detailed (unit) tests are still missing. This is an area where I'd love contributions,
but will work on anyway, eventually.
* Documentation (though the tests can be used as examples, as stated below). Comments in the code are being improved.
* A better API. chemLearn will remain rather "low-level" but right now the distintion between regular GB and XGB is tricky. I plan to make separate packages for each, that call this one, so the user doesn't deal with the difference on every function. That should be doable without breaking the current API, but no promises there, at least until a "1.0" release (the "basic" way in which functions work will not change, though). 

# Using chemLearn

Hopefully I'll add instructions, for now, take a look at the test file (learn_test.go) to see examples. The code is --mostly--commented, so the regular Go documentation system should work. (I'm working on improving the comments).

 ## On machine learning

If you want to be an informed user of Statistical/Machine learning, these are my big 3:

* [StatQuest with Josh Starmer](https://www.youtube.com/@statquest) Binge-watch worthy.
* [The Random Realizations blog](https://randomrealizations.com) Where most of the knowledge in this library comes from. Do read it.
* [An Introduction to Statistical Learning](https://www.statlearning.com/) They don't call it 'The Bible' for nothing.

(c) 2024 Raul Mera A.

This program, including its documentation, 
is free software; you can redistribute it and/or modify
it under the terms of the GNU Lesser General Public License as 
published by the Free Software Foundation; either version 2.1 of the 
License, or (at your option) any later version.
          
This program and its documentation is distributed in the hope that 
it will be useful, but WITHOUT ANY WARRANTY; without even the 
implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR 
PURPOSE.  See the GNU General Public License for more details.
                    
You should have received a copy of the GNU Lesser General 
Public License along with this program. If not, see 
<http://www.gnu.org/licenses/>. 

