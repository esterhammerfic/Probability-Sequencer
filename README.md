# Probability-Sequencer

<b>"Probability Sequencer"</b> is a Pure Data patch inspired by my interest in musical intelligence. 
While I want to eventually incorporate Markov-chain programming, this is a simple sequencer with a degree of chance built in. 

Here's how it functions: 

I use <a title="Loop Midi" href="http://www.tobias-erichsen.de/software/loopmidi.html">Loop Midi</a>: Set up a port from Pure Data to your DAW of choice. Within Pure Data, make sure (in the midi preferences) that you're sending to that port. Likewise, make sure your DAW is accepting incoming midi data from that same port.

Like any sequencer, you designate the <b>speed in BPMs</b> with which it cycles through the 16 beats. You can also choose a shorter <b>"Cycle Length"</b> than the default 16.
You can edit the <b>duration</b> and <b>velocity</b> of each midi note sent, as well as the master duration and master velocity of all notes simultaneously, on the left side. (Note that this over-rides the individual settings.)

<b>"Piano Roll Start Location"</b> changes where on the keyboard you're sending your midi notes. It would be a pain if you wanted to send out midi notes between 60 and 70 and had to set that manually each time: instead, set the Piano Roll Start Location to 60, and now sending 0 refers to 60, 1 refers to 61, etc. (-5 would refer to 55).

<b>Probability Functions</b><br><br>
Here's where the patch differs from a standard sequencer in some cool ways.

Suppose you want the program to randomly use one of two different snare sounds each measure. You could go to that beat, set "note 1" for the first snare sample, set "note 2" for the second. <b>Probability Split 1</b> basically determines how frequently it will favor one over the other: if it's 50, the program will choose each sample 50% of the time. If you choose 70, then it will favor the first note 70% of the time. 

If you add another two notes, and you set the splits at 50, 75, and 85 it would do this: <br>
On the beat, a number between 1 and 100 is generated. <br>
If the number is 50 or lower, note 1 will be sent to your DAW, playing whatever note you have it set to.<br>
If the number is between 50 and 75, note 2 will be sent.<br>
If the number is between 75 and 85, note 3 will be sent.<br>
And if the number is above 85, note 4 will be sent. <br>

<b>Master Probability Split</b> changes all Probability Splits at the same time. This is helpful if you intend to set all of them near 50%, for example. All outgoing notes can be assigned <b>random</b> values, or values of <b>zero</b> on the right side.<br><br><br><br>

<b>Philosophy</b><br><br>
The idea behind this is that at any given point in a musical composition/improvisation, there is a certain probability that a certain "next note" will be selected from all possible notes. Going up seven notes in a scale heavily implies the eighth scale note; you can thwart that expectation, but thwarting it is only a significant decision because of how unexpected it would be. <br>
<b>Given all of that, it's easy to see that if you set up the right "probabilities" for each successive note, you can get a sequencer to "pseudo-randomly" make very musically appropriate decisions.</b>
