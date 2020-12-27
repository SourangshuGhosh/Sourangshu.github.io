## Welcome to My Page

## List of Softwares Developed by Me
Below is a list of softwares that I have developed in **Machine Learning**. They are either used in my project works under various professors or was solely done by me due to my own interest on that topic. Please feel free to contact me if you found any bug or problem existing in the repositories listed below. Each of the repositories are explained in more **details** in a seperate page whose Link are given below each of them respectively.

1. **Stein Variational Gradient Descent(SVGD)**

![](https://raw.githubusercontent.com/SourangshuGhosh/SourangshuGhosh.github.io/master/Pictures/SVGD.png)
<br />We propose a general purpose variational inference algorithm that forms a natural counterpart of gradient descent for optimization. Our method iteratively transports a set of particles to match the target distribution, by applying a form of functional gradient descent that minimizes the KL divergence. Empirical studies are performed on various real world models and datasets, on which our method is competitive with existing state-of-the-art methods. The derivation of our method is based on a new theoretical result that connects the derivative of KL divergence under smooth transforms with Stein&#39;s identity and a recently proposed kernelized Stein discrepancy, which is of independent interest. The repository was build based upon the paper &quot;Stein Variational Gradient Descent: A General Purpose Bayesian Inference Algorithm&quot; by [Qiang Liu](https://arxiv.org/search/stat?searchtype=author&amp;query=Liu%2C+Q), [Dilin Wang](https://arxiv.org/search/stat?searchtype=author&amp;query=Wang%2C+D)

2. **N-gram Model**

![](https://raw.githubusercontent.com/SourangshuGhosh/SourangshuGhosh.github.io/master/Pictures/NGRAM.png)
<br />Given a sequence of N-1 words, an N-gram model predicts the most probable word that might follow this sequence. It&#39;s a probabilistic model that&#39;s trained on a corpus of text. Such a model is useful in many NLP applications including speech recognition, machine translation and predictive text input.An N-gram model is built by counting how often word sequences occur in corpus text and then estimating the probabilities. Since a simple N-gram model has limitations, improvements are often made via smoothing, interpolation and backoff.

An N-gram model is one type of a **Language Model (LM)**, which is about finding the probability distribution over word sequences.

The links to the Github Repository is [https://github.com/SourangshuGhosh/N-gram](https://github.com/SourangshuGhosh/N-gram)

3. **Bag of Words Model**

![](https://raw.githubusercontent.com/SourangshuGhosh/SourangshuGhosh.github.io/master/Pictures/BAGWORDS.png)
<br />The  **bag-of-words model**  is a simplifying representation used in natural language processing an information retreival (IR). In this model, a text (such as a sentence or a document) is represented as the  bag(multiset) of its words, disregarding grammar and even word order but keeping multiplicity. The bag-of-words model has also been used for computer vision. The bag-of-words model is commonly used in methods of document classification where the (frequency of) occurrence of each word is used as a feature for training a classifier. In practice, the Bag-of-words model is mainly used as a tool of feature generation. After transforming the text into a &quot;bag of words&quot;, we can calculate various measures to characterize the text. The most common type of characteristics, or features calculated from the Bag-of-words model is term frequency, namely, the number of times a term appears in the text. For the example above, we can construct the following two lists to record the term frequencies of all the distinct words (BoW1 and BoW2 ordered as in BoW3):

(1) [1, 2, 1, 1, 2, 1, 1, 0, 0, 0]

(2) [0, 1, 1, 1, 0, 1, 0, 1, 1, 1]

Each entry of the lists refers to the count of the corresponding entry in the list (this is also the histogram representation). For example, in the first list (which represents document 1), the first two entries are &quot;1,2&quot;:

- The first entry corresponds to the word &quot;John&quot; which is the first word in the list, and its value is &quot;1&quot; because &quot;John&quot; appears in the first document once.
- The second entry corresponds to the word &quot;likes&quot;, which is the second word in the list, and its value is &quot;2&quot; because &quot;likes&quot; appears in the first document twice.

This list (or vector) representation does not preserve the order of the words in the original sentences. This is just the main feature of the Bag-of-words model.
 The links to the Github Repository is [https://github.com/SourangshuGhosh/Bag-of-words-Model](https://github.com/SourangshuGhosh/Bag-of-words-Model)

4. **Quantum Computing**

Quantum computing is the use of quantum phenomena such as superposition and entanglement to perform computation. Computers that perform quantum computations are known as quantum computers.I-5 Quantum computers are believed to be able to solve certain computational problems, such as integer factorization (which underlies RSA encryption), substantially faster than classical computers. The study of quantum computing is a subfield of quantum information science.There are several models of quantum computers (or rather, quantum computing systems), including the quantum circuit model, quantum Turing machine, adiabatic quantum computer, one-way quantum computer, and various quantum cellular automata. The most widely used model is the quantum circuit. Quantum circuits are based on the quantum bit, or "qubit", which is somewhat analogous to the bit in classical computation. Qubits can be in a 1 or 0 quantum state, or they can be in a superposition of the 1 and 0 states. However, when qubits are measured the result of the measurement is always either a 0 or a 1; the probabilities of these two outcomes depend on the quantum state that the qubits were in immediately prior to the measurement.

This is an implementation of IBM's Quantum Experience in simulation; a 5-qubit quantum computer with a limited set of gates "the world’s first quantum computing platform delivered via the IBM Cloud". Their implementation is available at http://www.research.ibm.com/quantum/.

 The links to the Github Repository is [https://github.com/SourangshuGhosh/Bag-of-words-Model](https://github.com/SourangshuGhosh/QuantumComputing)
