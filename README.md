## Scalable Hidden Markov Model ##
> Shane Neph

This is written in the hopes of scaling to big data.  The library is roughly based upon Rabiner's pseudo code for
a discrete HMM, though it is modified to give various tradeoffs between memory and time.

Just type 'make' in the main directory and run with bin/rHMM.

<p><br />
#######################################<br />
<h3>Usage</h3>

<ul>
<li><code>rHMM --help</code> or <code>--version</code></li>
<li><code>rHMM train [--seed &lt;+integer&gt;] &lt;number-states&gt; &lt;number-iterations&gt; &lt;observed-sequence-file&gt;</code></li>
<li><code>rHMM probability &lt;hmm-parameters-file&gt; &lt;observed-sequence-file&gt;</code></li>
<li><code>rHMM decode &lt;hmm-parameters-file&gt; &lt;observed-sequence-file&gt;</code></li>
<li><code>rHMM train-and-decode [--seed &lt;+integer&gt;] &lt;number-states&gt; &lt;number-iterations&gt; &lt;observed-sequence-file&gt;</code></li>
</ul>
</p>

All output is sent to stdout.
You can train an hmm, save its output, and then use it as an &lt;hmm-parameters-file&gt; to
determine the probability of another observed sequence, or to decode the hidden states
of another observed sequence.
You can also train an hmm on an observed sequence and decode the hidden states of that
same sequence using train-and-decode.<br />


-------------------------------
I'm utilizing the train() function in include/impl/train.hpp.  There are 2 other versions in that
same file (slightly different names), that take the same arguments.  One version focuses on speed
with a max memory footprint (most closely resemble's Rabiner's pseudo-code), while the other is
the most efficient in memory, where it improves upon how things scale in the number of symbols
and states.  Typically, it's the number of observations that can lead to problems when it comes
to big data.  However, just swap out train() in src/hmm.cpp with train_mem() or train_full() as
you see fit.  There are comments in include/impl/train.hpp to help you to decide best.
