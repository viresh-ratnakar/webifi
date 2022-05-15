# Changelog

### Version: Webifi v0.04, May 14, 2022

- Revision and simplification of audio markup:
  - Just remove annotateText() and &lt;phonetc&gt; and add a few other ones.
  - Here's the list of tags:
    - &lt;pause&gt; inserts a pause in speech.
    - &lt;punctuate&gt;...&lt;/punctuate&gt; spells out any punctuation
      present in the enclosed text.
    - &lt;verbose&gt;...&lt;/verbose&gt; spells out any punctuation
      present in the enclosed text *and* spells out words as well as
      mentions spaces.
    - &lt;spoken:X&gt; is spoken out as X (and not rendered in the written
      output). X should not contain any spaces.
    - &lt;written:X&gt; is written out as X (and not rendered in the audio
      output). X should not contain any spaces.

### Version: Webifi v0.03, May 13, 2022

- Add a few more "markup" to the output text apart from &lt;pause&gt;:
  - &lt;phonetic&gt;X renders as X in written text and as "X (as in X-ray)"
    in spoken text.
  - &lt;spoken-X&gt; renders as nothing in written text and as X in spoken text.
- Simplify annotateText(), reducing the kinds of things it would add
  a note for. Also, make it add &lt;phonetic&gt; tags when spelling out words.
- Add commands to read out parts of a clue. You can do that with
  "words at 3" or "words after|before &lt;some-phrase&gt;" etc.
- When reading the clue, just read the clue, do not read its number (read that
  when reading the current entry in the clue).
- Read blanks in entries as "dash" or "dashes" as somehow TTS is better with
  that phrasing.

### Unnumbered tweak, May 10, 2022

- Allow pausing longer than 2 seconds while typing, if the last char
  entered is space.

### Unnumbered bug-fix, May 9, 2022

- Use the renamed command name (type, not enter).

### Version: Webifi v0.02, May 9, 2022

- Add "type" as the main alias for enter/fill (in voice-typing, "enter"
  is often misinterpreted, and "fill" is often taken to be "Phil").
- Use a scriptUrlBase to prefix script files for loading.

### Unnumbered bug-fix, May 3, 2022

- Bug-fix: HTML tags have to be removed from clues before showing them.

### Unnumbered bug-fix, May 3, 2022

- Bug-fix: in-clue annos have to be removed from clues before showing them.

### Unnumbered tweak, May 3, 2022

- More doc tweaking.
- Add "navigate" as a synonym command for "best"

### Version: Webifi v0.01 May 3, 2022

- Grab the input without waiting for "Enter", after a two-second lull.
  This is especially helpful for voice-typing.
- Add "next clue" and "previous clue" commands as variants of "next"
  and "previous" as they are natural instinctive completions.
- Update the documentation a bit.

### Unnumbered tweak, March 20, 2022

- Minor bug-fixes. Remove webifi-version.txt as that mechanism
  is not used any more by Exolve.

### Version: Webifi v0.00 March 20, 2022

- First check-in. This whole thing is still quite experimental.
  The [README.md](README.md) describes the project.

