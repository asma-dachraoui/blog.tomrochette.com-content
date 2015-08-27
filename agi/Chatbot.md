# Chatbot

* Starts and maintains multiple conversation threads
* Knows many facts about the world

* Does not attempt to deceive its interlocutor

-----

# Corpus construction

* Set of letters -> allow to discover anagrams

-----

# Construction of sentences

* Learn about as many words as possible (learn in the sense of knowing how they are formed, not their significance)
* Learn about the valid relations that the word can been seen in (before or after certain words)
* Attempt to generalize a valid grammar

Construction of sentences at this level means that the chatbot has no intent. Sentences may make grammatical/syntactic sense, but semantically they don't mean anything.

By constructing a relation graph between words, the chatbot may *begin* to be able to make semantic sense. For instance, if it has seen **red car** often, it may be able to infer that **red** can be replaced by any other color. To do so, it will have to be able to know that red, blue, green, yellow, orange, etc. are **colors**, and that color maybe changed for one another in some contexts. This construct is known as **[^is-a]**. The question then becomes, how can I tell what is the type of relation between two words? Is it a **is-a/type-of** (hyponym-hypernym), **has-a** (holonym-meronym), **part-of** (meronym-holonym) or **member-of** (meronym-holonym).

Is it possible, simply by looking at enough examples, without supervision, to determine classes of words?
* Noun
* Verb
* Participle
* Article
* Pronoun
* Preposition
* Adverb
* Conjunction

[^is-a]: https://en.wikipedia.org/wiki/Is-a

# Topics of interest
* https://en.wikipedia.org/wiki/Is-a
* https://en.wikipedia.org/wiki/Part_of_speech