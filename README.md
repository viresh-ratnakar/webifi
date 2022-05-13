# Webifi

## An "interactive-fictionesque" interface to the web.

### Version: Webifi v0.02 May 9, 2022

#### Author: Viresh Ratnakar

## Introduction

Webifi is a text and audio interface that enables chat interactions with
web pages.

Webifi might be useful for people with limited sight. It might also be useful
when one wants to interact with a web site while walking, running, etc. It
might also be an interesting and fun addendum even outside of these use-cases.

At this point, Webifi is *not* a general-purpose interface: it only works
for crosswords. However, I plan to expand its capabilities to other kinds
of web pages. Other word game and puzzle pages are likely to be my next targets.

In a Webifi-enabled crossword, there is a link under the crossword that
says "Webifi", which allows toggling the interface.

If a web-page for a Webifi-enabled crossword is accessed with the URL parameter
"webifi" present in the URL, then the Webifi interface will open directly and
will stay open (with the crossword's graphic interface hidden by default).
Such URLs should be useful for sight-challenged users.

The webifi interface is a simple chat interface, similar to the command-line
interfaces used in interactive text adventure games. The command prompt is at
the bottom, and above it is scrollable log of recent commands as well as their
responses.

To enter a command, type it at the chat prompt (you may want to use voice-input
if available). You do not have to press the "Enter" key after typing the
command. Webifi will grab the command after a two-second lull (this is to help
with voice-typing, where activating the "Enter" key verbally is difficult on
many mobile platforms). If you need to pause for longer than two seconds while
typing, just type a space at the end and Webifi will then not grab the text
(you can always erase the extra space if it's not needed, when you continue
typing).

## Note on voice-typing
Voice-typing into a web app is quite quirky, as of May 2022 (sadly). I have
mostly tried it on Chrome on Android. The ideal interface that I would like
is one where the microphone stays on while a sight-challenged user interacts
with the web app (or a sighted user interacts with it while on a walk or a
run). Unfortunately, I have not yet found a way to get this functionality. The
closest that I can get is by double-tapping on the microphone icon in the
on-screen keyboard that shows up in Chrome on Android. This keeps the microphone
on for long periods. However, at some point the microphone *will* shut off,
requiring a fresh double-tap on its icon for reactivation.

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

- status
- how am I doing
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

#### clue
Read the current clue and its current entry.

- clue
- read

#### entry
Read just the current entry in the current clue.

- entry|cells|letters|word|phrase
- read|current entry|cells|letters|word|phrase

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

- synonyms|syns {phrase}
- synonyms|syns of {phrase}

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

