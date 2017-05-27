---
title: Matej Balog - DeepCoder: Learning to Write Programs (2016)
created: 2017-05-25
taxonomy:
  category: [Machine Learning]
  status: finished
---

## Context

## Learned in this study

## Things to explore

# Overview
* An autoencoder is used to predict whether a given set of program attributes (function calls, mathematical operations) are used to generate the given set of input-output examples
	* Train the network on a lot of functions where you generate input-output pairs which serve as input, and record what functions/operations were used

# Notes
## Abstract
* Empirically, we show that our approach leads to an order of magnitude speedup over the strong non-augmented baselines and a recurrent neural network approach, and that we are able to solve problems of difficulty comparable to the simplest problems on programming competition websites

## 1 Introduction
* We propose two main ideas:
	* Learn to induce programs; that is, use a corpus of program induction problems to learn strategies that generalize across problems
	* Integrate neural network architectures with search-based techniques rather than replace them
* We argue that machine learning can provide significant value towards solving inductive programming synthesis (IPS) by re-casting the problem as a big data problem
* We show that training a neural network on a large number of generated IPS problems to predict cues from the problem description can help a search-based technique
* Three desirable properties
	* We transform a difficult search problem into a supervised learning problem
	* We soften the effect of failures of the neural network by searching over program space rather than relying on a single prediction
	* The neural network's predictions are used to guide existing program synthesis systems, allowing us to use and improve on the best solvers for the programming languages community

## 2 Background on Inductive Program Synthesis
* Given input-output examples, produce a program that has behavior consistent with the examples
* Requires solving two problems:
	* The search problem: to find consistent programs we need to search over a suitable set of possible programs. We need to define the set (i.e., the program space) and search procedure
	* The ranking problem: if there are multiple programs consistent with the input-output examples, which one do we return?
* There are many techniques for searching for programs consistent with input-output examples
	* Perhaps the simplest approach is to define a grammar and then enumerate all derivations of the grammar, checking each one for consistency with the examples
		* This approach can be combined with pruning based on types and other logical reasoning
* A popular choice for ranking is to choose the shortest program consistent with input-output examples

## 3 Learning Inductive Program Synthesis (LIPS)
* The components of LIPS are
	* A DSL specification
	* A data-generation procedure
	* A machine-learning model that maps from input-output examples to program attributes
	* A search procedure that searches program space in an order guided by the model

## 4 DeepCoder
### 4.1 Domain Specific Language and Attributes
* We consider binary attributes indicating the presence or absence of high-level functions in the target program
* The DSL is loosely inspired by query languages such as SQL or LINQ
* A program in the DSL is a sequence of function calls, where the result of each call initializes a fresh variable that is either a singleton integer or an integer array
* Note that the language only allows linear control flow (its functions do perform branching and looping internally)

## 4.2 Data Generation
* To generate a dataset, we enumerate programs in the DSL, heuristically pruning away those with easily detectable issues such as a redundant variable whose value does not affect the program output, or, more generally, existence of a shorter equivalent program

## 4.3 Machine Learning Model
* Our aim is to learn to recognize patterns in the input-output examples, and to leverage them to predict the presence or absence of individual functions
* Use of an autoencoder
	* Encoder: a differentiable mapping from a set of M input-output examples generated by a single program to a latent real-valued vector
	* Decoder: a differentiable mapping from the latent vector representing a set of M input-output examples to predictions of the ground truth program's attribute
* The input/output types are representing by a one-hot-encoding
* The inputs/outputs are padded to a maximum length L with a special NULL value
* Each integer in the inputs and outputs is mapped to a learned embedding vector of size E = 20
* For each input-output example separately, the input types embeddings, the inputs, the output type, and the output are concatenated into a single (fixed-length) vector

## 4.4 Search
* One of the central ideas of this work is to use a neural network to guide the search for a program consistent with a set of input-output examples instead of directly predicting the entire source code

# See also

# References
* Balog, Matej, et al. "DeepCoder: Learning to Write Programs." arXiv preprint arXiv:1611.01989 (2016).