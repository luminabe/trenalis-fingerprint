# Trenalis daily fingerprint

Each file in `anchors/<year>/<day>.json` holds one day's fingerprint of the Trenalis record: the Merkle root over every
file the record stored that day (each history table's rows of the day, exported, and every raw source file kept that day),
how many files it covers, the root of the day before, and when the root was made. Trenalis makes the root on the night
after the day (UTC) and commits it here the same night, so a root cannot be changed afterwards without the change showing:
in this repository's history, and in the next day's file, which names it.

Anyone holding a file from Trenalis, with its inclusion proof, can check that it was in the record on its day, unchanged:
the proof gives the file's SHA-256 and the path from its leaf to the root published here.

Method (RFC 6962, as Certificate Transparency): leaf = SHA-256(0x00 || the file's SHA-256 (32 bytes) || its path in the
store (UTF-8)), leaves in path order; node = SHA-256(0x01 || left || right); a tree of n leaves splits at the largest power
of two below n; an empty day's root is SHA-256 of nothing. A file's commit date is when it was published: a root published
later than the night after its day (the first ones, from 19 October 2026, were made each night and published together when
this repository was set up) proves only that it has not changed since it was published.
