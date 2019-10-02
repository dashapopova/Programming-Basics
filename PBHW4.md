## Homework 4 Assignment -- due 9.10 by noon

#### Task 1: Initial Consonant Clusters \[9 points\]

Your task is to show me how to use pattern matching to investigate the distribution of
word-initial consonant clusters in *Alice* (alice.txt). The basic question is how frequent different
kinds of initial consonant clusters are. 

An initial consonant cluster is a sequence of consonants (not interrupted by vowels) at the beginning of a word.
E.g., *crouton* has an initial consonant cluster *cr*, *flamingo* has an initial consonant cluster *fl*, 
*mimosa* does not have an initial consonant cluster, it starts with a single consonant. 

A challenge here is that English orthography only indirectly reflects the phonology.
First, you must deal with silent letters. These include cases like *know* or *gnostic* where *k* and
*g* are silent. Another issue to wrestle with is that sometimes a single consonant
is written with several letters, e.g. [θ] as in *thimble* or [ʃ] as in *show*, etc. Finally,
there are cases where the same letter (sequence) has multiple pronunciations. For
example, *c* is pronounced [s] in *city*, but [k] in *coat*. Similarly, *ch* is pronounced [tʃ]
in *church*, but [k] in *chord*. Note that sometimes the difference is predictable, as in
the case of *c*, but sometimes it is not, as in the case of *ch*. You should set aside
the mapping of orthography to precise phonological forms, except insofar as you
need to decide what a cluster is.

You will need to do the following (or something which is analogous to the following):

1. tokenize alice.txt, please apply the tokenization function you wrote for hw3 -- 1 point;
2. apply the `gutenberg_file_wc` function (also from hw3) to alice.txt to get the word counts -- 1 point;
3. try to search for (word) initial consonant clusters using regular expression(s) (Don't forget to `import re` at the beginning of your program) -- 3 points;
4. print the counts for all the clusters that you have identified, you should end up with a dictionary like `{'pr': 26, 'sp': 15,...}` -- 2 points; 
5. print the total number of different clusters you've identified, e.g., 10 clusters or 40 clusters -- 1 point;
6. print the list of all the clusters in the alphabetical order, ['bl', 'br',...] -- 1 point;

#### Task 2: Final Project Idea -- 1 point

Write a couple of sentences about what you want to do for your final project. Keep in mind that your final project should be an original piece of code that is roughly equivalent to one homework. Come ready to discuss your idea in class on Oct 9th.
