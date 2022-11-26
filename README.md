# The One Grammar to Rule Them All

## Syntax

I like making [conlangs](https://conlang.org/), but I hate creating syntaxes for them. `OGTRTA.md` describes what is hopefully the last conlang syntax I will ever have to invent.

## Words

The `words.csv` file contains the wordlist from [Mark Rosenfelder's _Conlanger's Lexipedia_](https://www.zompist.com/lexipedia.html),
expanded to be a suitable basis for building a `lexicon.csv` file as input to [Audition](https://github.com/benchristel/audition). Here is [Mark's original list of the 1500 most frequent words in a corpus of fantasy and SF books](http://www.zompist.com/resources/freqlist.txt). The book tags the words with over two dozen category labels, and I've preserved those in my wordlist. Each label has its own column; you can sort by a column in Excel to see all the words with that label.

Predicates in the list are annotated with their valence: e.g. `give2` means "a predicate that takes 2 complements and means 'give'".

A default translation is provided for each word, so you can cp `words.csv lexicon.csv` and get going with [Audition](https://github.com/benchristel/audition) right away. However, you will probably notice pretty quickly that every word translates to `pø`. If you want other words in your conlang, you'll have to make them yourself.