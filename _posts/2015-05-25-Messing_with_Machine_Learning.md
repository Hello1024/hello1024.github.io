---
layout: post
title: Messing with Machine Learning
---

I started from <a href="http://karpathy.github.io/2015/05/21/rnn-effectiveness/">Karpathy's really good post about RNN's for text generation</a> and thought I'd extend it.

<h3>Beam search</h3>
So far I have added a beam search on the output to try to find maximum likleyhood phrases rather than maximum likleyhood individual characters.   A naieve beam search simply generates 3-4 characters ahead and then takes the best and continues.   Instead I decided to mimic a* and make a very basic predictor of how good future characters would be to do a more informed search of the problem space.

While I successfully brought sequence entropy down well below 0.8 bits per character for shakespeare, results weren't very pleasing, with frequent loops and going on and on and on and on about the same topic...


<h3>Larger LSTM networks</h3>
Karpathy's LSTM networks are layers with fully-connected layers between them.  That inhibits large layer sizes, since the memory and compute requirements go up with the square of the layer size (together, presumably with the amount of training data to avoid overfitting).

Hence, I decided to produce a "divided" connectivity map wherein each LSTM node has connections only to the outputs of nodes locally close on the layer below and locally close on it's layer.   That should help with "specialization" too, so parts of the network can get good at certain things.   It seems to get lower entropy numbers with all other parameters being the same than without the edit, so promising.

<h3>Future ideas</h3>
<ul>
<li>Exponentially distributed connectivity.  Allow nodes lots of interconnects to other nearby nodes, and less and less dense interconnects to further away parts of the net, hopefully allowing even better specialization.</li>
<li>"slow" nodes.  Make some LSTM nodes, or even entire sections of the network, only "tick" at a much reduced frequency - for example every 10 "ticks" of the rest of the network.  Use filters on the input and output to accumulate gradient and inputs.  The goal is to be able to have lots of these because they don't use much compute oomph and will be better for long term behaviours.</li>
<li>"super" nodes.   Make some nodes have disproportionately large fan-in or fan-out than other network nodes, in the hope they will pick up more interesting features.</li>
<li>Node resetting.   Keep a counter of the "usefulness" of a node, by taking the d(activiation)/d(output) of that node with respect to the networks entire output.  Useless nodes get culled and new ones with entirely new weights put in their place at runtime.</li>
<li>Layer resizing.  At runtime (ie. without retraining) resize different layers of the network and demonstrate gains from the "new" bit without loss of functionality of the "old" bit, while still allowing dense interconnects between new and old.</li>
<li>"Never retrain" networks.  Linked to the above, design an architecture such that all experiments simply continue from the best available previous architecture and add/remove/change nodes as necessary.  As long as the eval function stays the same, a network could run for weeks or months being redesigned every few hours.</li>
</ul>


Code to be published for all the above whenever I get round to tidying it up, and/or when you guys nag me.
