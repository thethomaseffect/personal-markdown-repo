Exam Revision
=============

## QUESTION 3: Word Processor

![Word Processor](https://dl.dropboxusercontent.com/u/1425225/word_processor.png "Word Processor")

We wish to formally specify the cursor control operation of a basic text editor with fixed width typeface. The view of the document is from a window with a fixed number of text lines( ***mWinLin*** ) and columns( ***mWinCol*** ). The current document is composed of ***nDocLin*** lines of text of variable length expressed through the function ```LenLin(i) = length(number of characters in) line i```. The position of the window on the document is determined by the document number of the line at the top of the screen ***nTopLin(≥1)*** and of the column ***nLeftCol(≥1)***at the left of the screen. There must be at least part of one line of text on the screen at all times. The cursor position is determined by the screen line( ***nLin*** ) and column( ***nCol*** ) numbers and must be on the text and on the screen at all times. The document is left justified (ragged right) as in the diagram.

### Variables

* ***nTopLin*** - Used to denote vertical screen position. Increments when scrolling down and decrements when scrolling up.
* ***nLeftCol*** - Used to denote horizontal screen position. Increments when scrolling right
* ***nDocLin*** - Bottom line of document
* ***nCol*** - The horizontal position of the cursor relative to the screen width. It can never be greater than mWinCol.
* ***ndCol*** - The horizontal position of the cursor relative to the document. Equal to ***nLeftCol**** + ***nCol***.
* ***nLin*** - Current line on screen relative to screen position. It cannot be greater than mWinLin.
* ***ndLin*** - Current line on the document independent of screen position. Cannot be greater than nDocLin.


### Pre and Post Conditions

#### Down Key:
* At bottom of screen?
* At bottom of document?
* Text below cursor?
* Screen scrolls down?
* Screen scrolls horizontally?
* Cursor moves down one line?
* Cursor moves to end of line below?

#### Up Key:
* At top of screen?
* At top of document?
* Text above cursor?
* Screen scrolls up?
* Screen scrolls horizontally?
* Cursor moves up one line?
* Cursor moves to end of line above?

#### Right Key:
* At right end of screen?
* At right end of line?
* At end of document?
* Screen scrolls down?
* Screen scrolls horizontally?
* Cursor moves down one line?
* Cursor warps to start of next line?

#### Left Key:
* At left end of screen?
* At left end of line?
* At top of document?
* Screen scrolls up?
* Screen scrolls horizontally?
* Cursor moves up one line?
* Cursor warps to end of line above?

### Down Key

__NOTE: Any assignments should have a ' symbol on the left side of the assignment in the exam. I've left this out below so it doesn't screw with markdown's syntax highlighting.__

#### Normal
```python
nLin < mWinLin            # Not at bottom of screen
ndLin > nDocLin           # Not at bottom of document
LenLin(ndLin + 1) >= nCol # Text in line below
nTopLin = nTopLin         # No Scroll
nLin = nLin + 1           # Go down one line
nCol = nCol               # No change
```

#### No Text Directly Below
```python
nLin < mWinLin            # Not at bottom of screen
ndLin > nDocLin           # Not at bottom of document
LenLin(ndLin + 1) < nCol  # No Text Directly Below Cursor
nTopLin = nTopLin         # No Scroll
nLin = nLin + 1           # Go down one line
nCol = LenLin(ndLin + 1)  # Move to end of line below
```

#### Bottom of Screen, Text below
```python
nLin = mWinLin            # At bottom of screen
ndLin > nDocLin           # Not at bottom of document
LenLin(ndLin + 1) >= nCol # Text in line below
nTopLin = nTopLin + 1     # Scroll down screen
nLin = nLin               # No change
nCol = nCol               # No change
```

#### Bottom of Screen, No Text Below
```python
nLin = mWinLin            # At bottom of screen
ndLin > nDocLin           # Not at bottom of document
LenLin(ndLin + 1) < nCol  # No Text Directly Below Cursor
nTopLin = nTopLin + 1     # Scroll down screen
nLin = nLin               # No change
nCol = LenLin(ndLin + 1)  # Move to end of line below
```

#### Bottom of Document
```python
nLin = mWinLin            # At bottom of screen
ndLin = nDocLin           # At bottom of document
nTopLin = nTopLin         # No change
nLin = nLin               # No change
nCol = nCol               # No change
```

### Up Key

#### Normal
```python
nLin > 1                  # Not at top of screen
ndLin > 1                 # Not at top of document
LenLin(ndLin - 1) >= nCol # Text directly above cursor
nTopLin = nTopLin         # No Scroll
nLin = nLin - 1           # Move up one line
nCol = nCol               # No change
```

#### No Text Above Cursor
```python
nLin > 1                  # Not at top of screen
ndLin > 1                 # Not at top of document
LenLin(ndLin - 1) < nCol  # No text directly above cursor
nTopLin = nTopLin         # No Scroll
nLin = nLin - 1           # Move up one line
nCol = LenLin(ndLin - 1)  # Move to end of line above
```
