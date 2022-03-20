# Webifi

## An "interactive-fictionesque" interface to the web.

### Version: Webifi v0.00 March 20, 2022

Webifi is a text and audio interface that enables command-line interactions with
web pages.

Webifi should be useful for people whose visual abilities are limited. It should
also be useful for scenarios when one wants to interact with a web site
while driving, walking, running, etc.

At this point, Webifi is *not* a general-purpose interface: it only works
for crosswords. However, I plan to expand its capabilities to other kinds
of web pages. Other word game and puzzle pages are likely to be my next targets.

In a Webifi-enabled crossword, there is a link under the crossword that
says "Webifi", which allows toggling the interface.

If a web-page for a Webifi-enabled crossword is accessed with the URL paramater
"webifi" present in the URL, then the Webifi interface will open directly and
will stay open (with the crossword's graphic interface hidden by default).
Such URLs should be useful for sight-challenged users.

## User manual

Here are all the commands that you can use, grouped by "avatars" that handle them.
All input is handled case-insensitively.

### Avatar: Webifi
This is the basic avatar. It provides commands that control settings, display, audiom etc.
The available commands are as follows:

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

- help|list|commands|?
- help|commands on|with|for
- detailed help

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

### Avatar: Crossword
An interactive crossword player.
The available commands are as follows:

#### intro
Describe the crossword, providing info such as grid size, number of clues, title, preamble, etc.

- intro|introduction|describe|puzzle|crossword

#### status
Get current status and lists some unsolved clues in fraction-most-filled order.

- status
- how am I doing
- unsolved clues

#### navigate
Navigate to a clue by naming or characterizing it.

- [number]
- [number]A|[number]D
- [number] across|down|A|D
- best|easiest|solvable
- next|most best|easiest|solvable
- next
- prev|previous|back
- first|last
- first|last across|down|clue

The "best" command and its variants will take you to the next best unsolved
clue that in terms of having the most solved cells. The "back" command
will take you the clue that you were looking at before the current clue.
The "prev" and "next" commands go through the clues in their normal
order.

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

#### enter
Enter the solution for the current clue, optionally starting at a cell.

- enter|fill {letters}
- enter|fill at|in|from cell [number] {letters}

The prefix should be followed by the letters that you want to enter. Note that
if the entered letters have a conflict with some existing letter that was
entered previously, or if you enter more letters than needed, then Webifi
will ask you to confirm. You can enter "yes" or "ok" at that prompt, or
you can enter anything else (to cancel).

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
Get words or phrases matching the current light.

- matches
- matching words
- matching phrases
- what fits

## Serving guide

To enable Webifi on crosswords published on a web site (that uses
[Exolve](https://github.com/viresh-ratnakar/exolve)), you just need to
add the following files in your serving directory:

- [`webifi-version.txt`](https://raw.githubusercontent.com/viresh-ratnakar/webifi/master/webifi-version.txt),
- [`webifi.js`](https://raw.githubusercontent.com/viresh-ratnakar/webifi/master/webifi.js),
- [`words-webifi.js`](https://raw.githubusercontent.com/viresh-ratnakar/webifi/master/words-webifi.js),
- [`crossword-webifi.js`](https://raw.githubusercontent.com/viresh-ratnakar/webifi/master/crossword-webifi.js),
- [`webifi-icon.png`](https://raw.githubusercontent.com/viresh-ratnakar/webifi/master/webifi-icon.png),

You also need these two files from the
[Exet](https://github.com/viresh-ratnakar/exet) project:

- [`exet-lexicon.js`](https://raw.githubusercontent.com/viresh-ratnakar/exet/master/exet-lexicon.js),
- [`lufz-en-lexicon.js`](https://raw.githubusercontent.com/viresh-ratnakar/exet/master/lufz-en-lexicon.js),

Your crossword page that uses Exolve should use Exolve v1.34 or later, in
order for it to automatically offer Webifi. This means that it's either a
derivative of
[`exolve.html`](https://raw.githubusercontent.com/viresh-ratnakar/exolve/master/exolve.html),
or it loads the files
[`exolve-m.js`](https://raw.githubusercontent.com/viresh-ratnakar/exolve/master/exolve-m.js)
and
[`exolve-m.css`](https://raw.githubusercontent.com/viresh-ratnakar/exolve/master/exolve-m.css).

Exolve will automatically create a Webifi link under the crossword, if it
detects that the necessary Webifi script files are available from the
serving directory. It first checks for the presence of the small
`webifi-version.txt` file, and if that can be loaded, only then does it
attempt to load the script files.

## Design and architecture

TODO.

## Acknowledgements

I would like to thank [T. V. Raman](https://en.wikipedia.org/wiki/T._V._Raman),
who is an excellent cryptic crossword solver, for spending several hours
with me discussing ideas about this project, working through crosswords to
figure out important elements for the interface, trying out my demos and
offering excellent insights and suggestions.
