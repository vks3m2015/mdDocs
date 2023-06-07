
## Difference between Collection and Stream



Collections are mainly used to store and group the data.	
Streams are mainly used to perform operations on data.

Collections have to be iterated externally.	
Streams are internally iterated.

Collections can be traversed multiple times.	
Streams are traversable only once.

Collections are eagerly constructed i.e all the elements are computed at the beginning itself. Ex : List, Set, Map…
Streams are lazily constructed i.e intermediate operations are not evaluated until terminal operation is invoked. Ex : filtering, mapping, matching…