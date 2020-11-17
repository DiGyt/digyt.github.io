---
title: "Neuropynamics"
excerpt: "A simple and interactive collection of introductory notebooks into Neurodynamics."
header:
  teaser: "assets/images/posts/neuropynamics.png"
  overlay_image: "assets/images/posts/neuropynamics.png"
  overlay_text: ""
tags:
  - Neuroscience
  - Dynamical Systems
  - Neural Networks
---


If you ever wanted to get in touch with the field of Neurodynamics, understand the complex behavior of different neuron 
simulations or just wanted to play around with the parameters of a Hodgkin-Huxley model, this might be the place for you:

Checkout this collection of introductory notebooks into the field of neurodynamics at 
<https://github.com/DiGyt/neuropynamics>

Neuropynamics is a course project I created with Lucas Feldmann and Hunaid Hameed for the 2020 Neurodynamics lecture at 
the University of Osnabrück. Our aim was to provide some nice tutorials and visualization tools which allow students of 
Neurodynamics to practically learn about the field by directly simulating the processes.

We use Google Colaboratory in combinations with Jupyter Ipywidgets. This allows you to run these notebooks simply and 
interactively in your internet browser, without requiring deeper understanding of the Python language and without needing 
to install anything. You just can run the entire script on Google's hosted runtime, and then click through the examples 
while adjusting model parameters via ipywidgets.

Just try it out by yourself by opening one of the below notebooks.


### Single neurons

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DiGyt/neuropynamics/blob/master/notebooks/Single_neurons.ipynb)

We suggest you start your journey with this notebook as it introduces you to the brian2 toolbox that will be used throughout our examples. 
In this notebook you can interactively examine the spiking and reset behavior of different types of single neurons. We will show the equations for the underlying dynamical systems for the neuron models and implement them using brian2. 

---

### Stability analysis for different neuron models
[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DiGyt/neuropynamics/blob/master/notebooks/Stability_analysis.ipynb)

Expanding on the notebook above, this one provides an introduction to stability analysis of 1D and 2D dynamical systems.

---

### Multi-neuron networks

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DiGyt/neuropynamics/blob/master/notebooks/multineuron_networks.ipynb)

In this notebook, you will learn how to build multineuron networks with brian2 and visualize them using our neuropynamics plotting functions.

---

### Dendritic computation

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DiGyt/neuropynamics/blob/master/notebooks/dendritic_computation.ipynb)

Learn what difference dendritic computation can make in the localization of a sound stimulus and see how it changes depending on the timing of sound reaching the left ear and right ear.

---

### Bifurcation and chaotic behavior

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DiGyt/neuropynamics/blob/master/notebooks/bifurcation.ipynb)

Investigate complex and chaotic behavior resulting from the interaction of different parameters in different neuron models.

---

### How to do Stability Analysis - Examining Dynamical Systems
[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/DiGyt/neuropynamics/blob/master/notebooks/pplane.ipynb)

Stability analysis is widely done in a [Java based software](https://www.cs.unm.edu/~joel/dfield/). We have implemented it as a Python notebook. The notebook provides a clean interface to plug in all the parameters for Non-Linear Ordinary Differential Equations. The code is clean and reusable. It can be extended to include more types of differential equations and controls over the plotting.


---
