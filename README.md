# grokking playground

let's say you show a neural network half the answers to a addition table. it memorizes them perfectly. train accuracy goes to 100%, test stays at zero. looks like it just memorized, right?

then you keep training. nothing happens for a long time. and then, thousands of steps later, something clicks. test accuracy jumps from near-zero to near-perfect. the network figured out the *rule*, not just the answers.

that's grokking.

**[try it live](https://saikatkumardey.com/grokking-playground/)**

## what's here

a single html file that trains a small neural network on modular addition (a + b mod p) and visualizes the whole thing in real time.

you get:
- a heatmap showing every (a, b) pair. green = correct, red = wrong. watch it go from mostly red to fully green.
- accuracy and loss charts. the classic grokking curve: train shoots up, test stays flat, then suddenly jumps.
- neuron weight polar plots (MLP) or token embedding PCA (Transformer). you can literally see the network discover circular structure.
- before/after comparisons so you can see what changed.

you can choose between an MLP (single hidden layer, fast) or a Transformer (matches the original paper, slower). both grok.

## the one knob that matters

weight decay. too little and it memorizes forever. too much and it can't even memorize. there's a sweet spot where it memorizes first, then generalizes. that transition is grokking.

## how it works

- one hidden layer MLP with ReLU, or a 1-layer Transformer with 4-head causal attention
- AdamW optimizer (beta1=0.9, beta2=0.98, matching the paper)
- one-hot input encoding, cross-entropy loss, softmax output
- training runs in a Web Worker so the UI stays smooth
- pure javascript, zero dependencies beyond Chart.js

## paper

based on [grokking: generalization beyond overfitting on small algorithmic datasets](https://arxiv.org/abs/2201.02177) (Power et al., 2022). the original paper used a Transformer. this demo shows it works with a simple MLP too.