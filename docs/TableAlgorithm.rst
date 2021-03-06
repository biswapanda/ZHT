===========================
Overview of Table operation
=========================== 

Underlying Assumptions / Correctness Caveats
============================================

While trying to devise a simple way to keep values consistent, it became clear that total consistency would come at an excessive cost
to simplicity and performance. If performance is suficiently good, inconsistencies should be fairly uncommon and most applications
that need consistency should be able to build some consistency protocol on top of the primitives provided.

We will have writes carry with them a timestamp, generated at the origin of the write (whichever bucket-holder happens to originate
the write). Whichever timestamp is later wins in the case of a dispute, and if two writes carry the same timestamp, whichever arrived
first wins. This, of course means that concurrent writes may lead to an inconsistent state, and that ordering may depend on the
accuracy of each nodes internal clocks, and that the table is not tolerant of malicious actors (correctness does not exist if there
are attackers from within the table or significant clock drift).

To offset this weakness, there will also be additional classes of buckets that will hold different primitive data sets. A set with
add/delete operations may be useful for overcoming the known correctness issues, or to sidestep possible inconsistencies.



