# One Grammar To Rule Them All

## Technical Description (for the linguistically inclined)

OGTRTA recognizes two main parts of speech: the noun and the predicate. The relationships formed by these two parts of speech create most of the syntactic structure of the language.

OGTRTA embodies a key insight into the nature of language: that syntactic relationships among words can be viewed as purely structural and devoid of inherent meaning. Meaning is "layered onto" the syntax by the lexicon. The lexical structure of a language depends on the syntactic structure—not the other way around.

As an example of how this works, consider a couple of English sentences:

- _He did it for their sake_
- _She headed in the direction of the tower_

Here, the words "sake" and "direction" don't refer to physical entities. Their role in the sentence is to impart a specific meaning to the syntactical relationships among verb, preposition, and now.

### Nouns

Nouns are more or less like nouns in English: they refer to people, places, and things, but also to abstractions and nominalized actions (like "chewing") that are being discussed as if they were things.

### Predicates

Predicates play the roles that verbs, adjectives, adverbs, and prepositions do in English. A predicate describes a noun or another predicate (its _subject_) and has zero or more slots for _complement_ nouns. The roles that the complements play in relation to the predicate are lexically determined by the predicate.

The number of complement slots that a predicate has is called its _valence_. The valence of a predicate can be altered via derivation. Valence is quite important for minimizing syntactic ambiguity. Because of this, valence is indicated by a number in `words.csv`, and in the syntax below. E.g. in this file, `P0` means a nilvalent predicate, and `P1` is a monovalent predicate.

You can think of P0s as adjectives or intransitive verbs, P1s as prepositions or transitive verbs, and P2s as ditransitive verbs.

Every predicate is the head of a _predicate phrase_ (denoted PP in the syntax) and its complements are also part of the predicate phrase. The subject of a predicate is not part of the predicate phrase.

### Other Parts of Speech

- noun conjunctions
- predicate conjunctions
- sentence conjunctions
- determiners
- sentence-level particles (e.g. the TAM and SUB particles below)
- pronouns (which generally behave like nouns, but may have different inflectional patterns).

### Post-serialization transformations

Languages may define rules that act on combinations of morphemes after the syntax arranges them into a series. For example, languages might have contractions, or phonologically conditioned consonant mutations.

### Syntax

The syntax of OGTRTA is really two syntaxes in one, since it is completely reversible. The word order presented below is head-initial, VOS, but if you reverse each of the expansions in the syntax rules listed below, you get the head-final, SOV version of the grammar.

Notation for syntax rules:

```
A -> B = phrase type A expands to B
X?     = 0 or 1 X
X*     = 0 or more Xs
X{n}   = exactly n Xs
A | B  = A or B
A B    = A followed by B
(...)  = grouping
```

#### Noun Phrases

A noun phrase may consist of a head noun optionally preceded by a determiner, and followed by any number of modifiers, which are predicate phrases.

Semantically, the head noun is the subject of the PPs modifying it.

```
NP -> DET? N PP*
```

A noun phrase can also be assembled from two other noun phrases via conjunction:

```
NP -> NP NCONJ NP
```

Optional extension: nilvalent modifiers (i.e. adjectives) may be allowed between the determiner and the noun.

Semantically, the head noun is the subject of those P0s.

```
NP -> (DET P0*)? N PP*
```

#### Predicate Phrases

A predicate phrase may consist of a predicate with valence N, followed by any number of modifying predicate phrases and then N complements.

```
PP -> Pn PP* NP{n}
```

Predicate phrases can also be formed by conjunction. Semantically, the conjoined predicate phrases both have the same subject.

```
PP -> PP PCONJ PP
```

Optional extension: predicate modifiers may be allowed after the complements:

```
PP -> Pn PP* NP{n} PP*
```

#### Sentences

A sentence consists of a tense/aspect/mood particle, a predicate phrase, and a subject. (This section of the grammar is still being researched, and is likely to change.)

```
S -> TAM? PP NP
```

Some languages may not require a subject:

```
S -> TAM? PP NP?
```

The subject may move to the beginning of the sentence.

```
S -> NP? TAM? PP
```

Sentences can be conjoined:

```
S -> S SCONJ S
```

Finally, sentences can become subordinate clauses that behave like noun phrases:

```
NP -> SUB S
```

### Morphology

OGTRTA languages show some diversity of morphology, but there are a few common patterns:

- The main verb of a sentence is often marked, sometimes with a person/number subject agreement marker that only appears on the main verb.
- The head of the first PP in a sequence of modifier PPs is sometimes marked. In VOS languages, the marking is usually a prefix or initial consonant mutation. In SOV languages, it is usually a suffix.
- There are always affixes for changing the valence of verbs, and for passivization.
- There may be noun classes/genders, with which predicates agree.

### Idioms

The syntax says that a predicate's modifiers have to immediately follow it. However, they can be moved to the end of the sentence if we conjoin an anaphoric predicate that the modifiers can attach to.

> __Gob yim Poik hi xi nuan wikto__
> `shovel snow NAME and_p do_so use haste`

"Poik shoveled the snow and did so in a hurry"

Post-serialization transformations can turn the `and_p do_so` morphemes into just about anything... including nil. So really, you _can_ put predicate modifiers at the end of the sentence.