# Webifi

## An "interactive-fictionesque" chat interface to the web.

### Version: Webifi v0.04 May 14, 2022

#### Author: Viresh Ratnakar

## Introduction

Webifi is a text and audio interface that enables chat interactions with
web pages, in a style similar to an interactive-fiction game.

At this point, Webifi is *not* a general-purpose interface: it only works
for crosswords. However, I plan to expand its capabilities to other kinds
of web pages (mainly other word and number games). For now, the rest of
this README guide describes everything in terms of the crossword application.

There are three motivating use cases for Webifi:
1. An interactive-fiction interface can be a lot of fun. One can simply use
   Webifi as an additional interface to a crossword, coexisting with a standard
   interface. Using Webifi, you can navigate and solve the puzzle with some
   powerful extra features, while continuing to be able to also use the standard
   grid-based interactive interface.
2. Using voice input and audio output, the Webifi interface can be used to solve
   a crossword without using the screen much (for example, while out running
   or walking).
3. A sight-challenged user can use Webifi to solve a crossword, using voice
   inputs. They can use the text interface in conjunction with any screen-reading
   mechanism or extension that they may already be using, or they can use
   Webifi's own audio output.

In an interactive-fiction game (aka a text adventure), you move between various
locations, interacting with your surroundings using simple text commands. Each
crossword can be thought of as a text adventure game, where the clues are the
individual locations. When you are "at" a particular clue, you can access the
clue (command: **clue**), you can review what letters have been entered so far
(command: **entry**), you can consult wordplay tools for help (commands:
**matches**, **anagrams**, **synonyms**, etc.), you can enter (command:
**type**) and check solutions (command: **check**), and so on. You can navigate
across clues in various orders, jumping off to crossing lights or to clues that
have the fewest unfilled letters, etc.

Here's a mock interaction with a Webifi-powered crossword, as an illustration:
```
> entry

Current entry in this 11 Across clue is: A_S__

> clue

The way to approach a wedding is through strong beer (5)

> matches

Here are some matches.

Assam, Assad, Aisha, Aisne
Aesop, asset, at sea, aisle
arson, assay, apses, asses
arsis, aesir, assai, apsis
arses, absey, adsum, absit
assot, A'asia

> type aisle

Entered aisle in 11 Across.

> check

All cells are correct

> next best

Inspects the foundations of some Berry Ave houses (4)

Current entry in this 6 Down clue is: ___S

```

Webifi provides some powerful assistive features for solving crosswords (of
course, it's up to you as a solver to decide how much assistance you want to
use—my own philosophy as a solver is to maximize my *fun* in solving, which
sometimes means using some assistance to get past a clue that I might be stuck
on). Webifi can help you find words matching a partial solution; it can offer
possibilities for some cryptic wordplays such as anagrams and homophnes.
When online, it can also look up definitions and synonyms.

## The basic interface
In a Webifi-enabled crossword, there is a link under the crossword that
says "Webifi"; clicking on this link toggles the Webifi interface.

The webifi interface is a simple chat interface, similar to the command-line
interfaces used in interactive text adventure games. The command prompt is at
the bottom, and above it is scrollable log of recent commands as well as their
responses.

If a web-page for a Webifi-enabled crossword is accessed with the URL parameter
`webifi` present in the URL, then the Webifi interface will open directly and
will stay open (the toggle link is not shown). Such a URL should be useful for
sight-challenged users, as it starts off the puzzle with the graphic interface
hidden, so that it does not get in the way.

To enter a command, type it at the chat prompt (you can also use voice-input
if available). You do not have to press the "Enter" key after typing the
command. Webifi will grab the command after a two-second lull in typing (this
is to help with voice-typing, where activating the "Enter" key verbally is
difficult on many mobile platforms). If you need to pause for longer than two
seconds while typing, just type a space at the end and Webifi will then not
grab the text (you can always erase the extra space if it's not needed, when
you continue typing).

You can use commands to toggle audio output on and off, and to toggle the
standard graphic interface on and off.

## Voice-typing
Voice-typing into a web app is quite quirky, as of May 2022 (sadly). I have
mostly tried it with Chrome on Android. The ideal interface that I would like
is one where the microphone stays on while a user interacts with the web app.
Unfortunately, I have not yet found a good way to get this functionality. The
closest that I can get to it is by double-tapping on the microphone icon in the
on-screen keyboard that shows up in Chrome on Android. This keeps the microphone
on for long periods. However, at some point the microphone *does* shut off,
requiring a fresh double-tap on its icon for reactivation.

Voice-typing will hopefully only get better over time, making use-cases (2) and
(3) much more seamless than they currently are.

## Commands
Here are all the commands that you can use, grouped by "avatars" that handle them.
All input is handled case-insensitively. When audio is on, you can cut short
any long output from Webifi by entering *any* text ("ok" and "shh" are good,
natural choices).

### Avatar: Webifi
This is the basic avatar. It provides commands that control settings, display,
audio, etc. The available commands are as follows:

#### hello
Get an introduction to Webifi and a listing of available avatars.

- whats your name
- what's your name
- who are you
- hi|hello|greeting|greetings

#### audio
Report or set audio mode.

- audio
- audio off|on|us|gb|au|in|za
  - The US, GB, AU, IN, and ZA options allow you to switch to that
    country's accent, if available.

When you turn audio on, please prefer to use headphones for privacy as well as to avoid interference if using voice-typing.

#### display
Report or set whether the "peer element" is getting displayed.

- display
- display off|on

The peer element is the HTML element that Webifi has assumed the responsibility
for providing interactivity with. Currently, that means the Exolve
crossword's main DIV element. With this command, you can hide or un-hide
that element.

#### echo
Test how a word or phrase or sentence gets spoken.

- echo {sentence}

#### talking-speed
Get Webifi to talk faster or slower or at its normal speed.

- talk fast|faster
- talk slow|slower|slowly
- talk normal|normally
- talk|speed|rate [number]
- talk at [number]
- talking speed|rate [number]

The number, if specified, can be in the range 0.1 to 2.0.

#### help
Get a listing of all commands or get help on a specific command or topic.

- help|list|commands|? [{topic}]
- help|commands on|with|for [{topic}]
- detailed help

### Avatar: Crossword
An interactive crossword player.
The available commands are as follows:

#### intro
Describe the crossword, providing info such as grid size, number of clues, title, preamble, etc.

- intro|introduction|describe|puzzle|crossword

#### status
Get current status and list some unsolved clues in fraction-most-filled order.

- status|look|where
- where am i
- how am i doing
- unsolved clues

#### navigate
Navigate to a clue by naming or characterizing it.

- [number]
- [number]A|[number]D
- [number] across|down|A|D
- navigate|best|easiest|solvable
- next|most best|easiest|solvable
- next
- next clue
- prev|previous|back
- previous clue
- first|last
- first|last across|down|clue

The "best" command and its variants will take you to the next best unsolved
clue (in terms of having the most solved cells). The "back" command will take
you the clue that you were looking at before the current clue. The "prev" and
"next" commands go through the clues in their normal order.

When the result of a navigation clue takes you to a clue different from the
clue that you were at, then after showing the new clue, its current entry
is also shown.

#### clue
Read the current clue again.

- clue

### words
You also access different parts of the clue, which is especially useful
when you are listening to the interface using audio. Each one of these
commands will show three words from the clue (or fewer, if the clue
ends before three words). With audio on, looking at a part of the
clue with one of these commands will also read out any punctuation marks
in the clue part.

- words|word|part|parts [number]
- words|word|part|parts at|from [number]
- clue words|word|part|parts [number]
- clue words|word|part|parts at|from [number]
- clue start|starting|end|ending
- words|word|clue at start|starting|end|ending
- words|word|clue at the start|starting|end|ending
- clue words|word at start|starting|end|ending
- clue words|word at the start|starting|end|ending
- words|word|clue after
- clue words|word after
- words|word|clue before
- clue words|word before

The [number], if used, should be the 1-based index of words in the clue.
The "words after" and "words before" commands look within the clue for the
phrase specified right after the command prefix.

#### entry
Read the current entry (letters entered as well as blanks) and identify the current clue again.

- entry|current|read|cells|letters
- read|current entry|cells|letters

#### crossers
Describe clues for lights that cross the current lights.

- crossers
- crossing clues
- crossing lights

#### type
Enter the solution for the current clue, optionally starting at a cell.

- type|enter|fill {letters}
- type|enter|fill at|in|from cell [number] {letters}

The command should be followed by the letters that you want to enter. Note that
if the entered letters have a conflict with some existing letter that was
entered previously, or if you enter more letters than needed, then Webifi
will ask you to confirm. You can enter "yes" or "ok" at that prompt, or
you can enter anything else (to cancel).

The command "enter" may pose a problem when voice-typing (it might get
ignored on some platforms). The command "fill" may get misinterpreted as
"Phil". Hence, "type" is perhaps the best verbal command for entering
letters into the grid.

#### clear
Clear entries in the current light or a particular cell.

- clear
- clear cell [number]

#### check
Check entries in the current light or a particular cell or everywhere.

- check
- check cell [number]
- check all

Any incorrect cells in scope will get cleared. This option is only available in
crossword where the solution has been provided.

#### reveal
Reveal entries in the current light or a particular cell or everywhere.

- reveal
- reveal cell [number]
- reveal all

This option is only available in crossword where the solution has been provided.

#### matches
Get words or phrases matching the letters that have been entered so far in the
current light.

- matches
- matching words
- matching phrases
- what fits

### Avatar: Words
Word patterns, anagrams, word sounds, definitions, synonyms.
The available commands are as follows:

#### define
Use dictionarydev.api to look up a word or phrase.

- define|definition|definitions {phrase}
- look up definition|definitions|meaning of {phrase}

#### synonyms
Use dictionarydev.api to look up synonyms of a word or phrase.

- synonym|synonyms|syns {phrase}
- synonym|synonyms|syns of {phrase}

The synonyms obtained from this free API are not that great, unfortunately: very
few words have available synonyms. I am still looking for a good, free synonym
service not encumbered with API tokens etc.

#### pattern
Get words or phrases matching the given letter pattern.

- pattern|word-pattern|letter-pattern {pattern>}

The pattern can be something like *c??ssw?r?* or *s?u? u?*, etc.

#### anagrams
Get anagrams of a word or phrase or any set of letters.

- anagrams|anagram {phrase}
- anagrams|anagram of {phrase}

#### homophones
Get homophones of a word or phrase.

- homophone|homophones {phrase}
- homophone|homophones of {phrase}
- words sounding like

#### spoonerisms
Get Spoonerisms of a word or phrase.

- spoonerism|spoonerisms {phrase}
- spoonerism|spoonerisms of {phrase}

## Serving guide

To enable Webifi on crosswords published on a web site (that uses
[Exolve](https://github.com/viresh-ratnakar/exolve)), you need to
add the following files in your serving directory:

- [`webifi.js`](https://raw.githubusercontent.com/viresh-ratnakar/webifi/master/webifi.js)
- [`words-webifi.js`](https://raw.githubusercontent.com/viresh-ratnakar/webifi/master/words-webifi.js)
- [`crossword-webifi.js`](https://raw.githubusercontent.com/viresh-ratnakar/webifi/master/crossword-webifi.js)
- [`webifi-icon.png`](https://raw.githubusercontent.com/viresh-ratnakar/webifi/master/webifi-icon.png)

You also need these two files from the
[Exet](https://github.com/viresh-ratnakar/exet) project:

- [`exet-lexicon.js`](https://raw.githubusercontent.com/viresh-ratnakar/exet/master/exet-lexicon.js)
- [`lufz-en-lexicon.js`](https://raw.githubusercontent.com/viresh-ratnakar/exet/master/lufz-en-lexicon.js)

Your crossword page that uses Exolve should use Exolve v1.34 or later, in
order for it to offer Webifi. This means that it's either a
derivative of
[`exolve.html`](https://raw.githubusercontent.com/viresh-ratnakar/exolve/master/exolve.html),
or it loads the files
[`exolve-m.js`](https://raw.githubusercontent.com/viresh-ratnakar/exolve/master/exolve-m.js)
and
[`exolve-m.css`](https://raw.githubusercontent.com/viresh-ratnakar/exolve/master/exolve-m.css).

Assuming the necessary Webifi scripts and icon files listed above are made
available by the server, Exolve can be made to offer the Webifi interface in
one of three ways.
- The webifi script files are included through script tags in the crossword
  file.
- `exolve-option: webifi` is used in the crossword specifications.
- `webifi` is passed as a URL parameter.
Note that in the `exolve-option: webifi` case and in the URL
parameter case, it is not necessary to add script tags to load the webifi
scripts, as they will automatically loaded if not already present.

## Design and architecture

TODO.

## Acknowledgements

I would like to thank [T. V. Raman](https://en.wikipedia.org/wiki/T._V._Raman),
who is an excellent cryptic crossword solver, for spending several hours
with me discussing ideas about this project, working through crosswords to
figure out important elements for the interface, trying out my demos and
offering excellent insights and suggestions.

## Copyright notices

### UKACD18

```
UKACD18
Copyright (c) 2009 J Ross Beresford
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions
are met:

1. Redistributions of source code must retain the above copyright
   notice, this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright
   notice, this list of conditions and the following disclaimer in the
   documentation and/or other materials provided with the distribution.

3. The name of the author may not be used to endorse or promote products
   derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE AUTHOR "AS IS" AND ANY EXPRESS OR
IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES
OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED.
IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY DIRECT, INDIRECT,
INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT
NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF
THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```

### CMUdict

```
CMUdict
-------

CMUdict (the Carnegie Mellon Pronouncing Dictionary) is a free
pronouncing dictionary of English, suitable for uses in speech
technology and is maintained by the Speech Group in the School of
Computer Science at Carnegie Mellon University.

The Carnegie Mellon Speech Group does not guarantee the accuracy of
this dictionary, nor its suitability for any specific purpose. In
fact, we expect a number of errors, omissions and inconsistencies to
remain in the dictionary. We intend to continually update the
dictionary by correction existing entries and by adding new ones. From
time to time a new major version will be released.

We welcome input from users: Please send email to Alex Rudnicky
(air+cmudict@cs.cmu.edu).

The Carnegie Mellon Pronouncing Dictionary, in its current and
previous versions is Copyright (C) 1993-2014 by Carnegie Mellon
University.  Use of this dictionary for any research or commercial
purpose is completely unrestricted. If you make use of or
redistribute this material we request that you acknowledge its
origin in your descriptions, as per the license information included
in the dictionary file (a Simplified BSD lincense).

If you add words to or correct entries in your version of this
dictionary, we would appreciate it if you could send these additions
and corrections to us (air+cmudict@cs.cmu.edu) for consideration in a
subsequent version. All submissions will be reviewed and approved by
the current maintainer, Alex Rudnicky at Carnegie Mellon University.

----------------------------------------------------------------------
The current version of cmudict is now cmudict-0.7b 
[First released November 19, 2014]

Note that the first '.' in the file name has changed to a '-' as it
was observed that file systems occasionally get confused about the
scope of the extension.

Please note that the dictionary is modified incrementally, to correct
errors are incorporate new words. If you require a unique version, be
sure to specify a revision when you check it out.

cmudict-0.7b includes various systematic fixes and additional words.
As always please let us know if you see a problem or want to suggest a
word.

----------------------------------------------------------------------
```

### Webifi, Exolve, Exet

```
MIT License

Copyright (c) 2022 Viresh Ratnakar

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

The latest code and documentation for Exet can be found at:
https://github.com/viresh-ratnakar/exet
```

