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

## Sample Answers

__NOTE: Any assignments should have a ' symbol on the left side of the assignment in the exam. I've left this out below so it doesn't screw with markdown's syntax highlighting.__

TOTAL CONDITIONS: 7 for full up, down. 5 for full right, left.

### Down Key

#### Normal
```python
nLin < mWinLin                             # Not at bottom of screen
LenLin(ndLin + 1) >= ndCol                 # Text in line below
nTopLin = nTopLin                          # No Vertical Scroll
nLeftCol = nLeftCol                        # No Horizontal Scroll
nLin = nLin + 1                            # Go down one line
nCol = nCol                                # No change
```

#### No Text Directly Below, No Hori Scroll
```python
nLin < mWinLin                             # Not at bottom of screen
LenLin(ndLin + 1) < ndCol                  # No Text Directly Below Cursor
LenLin(ndLin +1) >= nLeftCol               # End of line below is on the screen
nTopLin = nTopLin                          # No Scroll
nLeftCol = nLeftCol                        # No Horizontal Scroll
nLin = nLin + 1                            # Go down one line
nCol = LenLin(ndLin + 1) - (nLeftCol - 1)  # Move to end of line below
```

### Move to End of Line Below, Hori Scroll
```python
nLin < mWinLin                             # Not at bottom of screen
LenLin(ndLin + 1) < nLeftCol               # End of line below not on screen
nTopLin = nTopLin                          # No Scroll
nLeftCol = LenLin(ndLin + 1)               # Scroll to end of line below in first screen col position.
nLin = nLin + 1                            # Go down one line
nCol = 1                                   # Move to left of screen
```

#### Bottom of Screen, Text below, No Hori Scroll
```python
nLin = mWinLin                             # At bottom of screen
ndLin > nDocLin                            # Not at bottom of document
LenLin(ndLin + 1) >= ndCol                 # Text in line below
nTopLin = nTopLin + 1                      # Scroll down screen
nLeftCol = nLeftCol                        # No change
nLin = nLin                                # No change
nCol = nCol                                # No change
```

#### Bottom of Screen, Move to End of Line Below, No Hori Scroll
```python
nLin = mWinLin                             # At bottom of screen
ndLin > nDocLin                            # Not at bottom of document
LenLin(ndLin + 1) < ndCol                  # No Text Directly Below Cursor
LenLin(ndLin + 1) >= nLeftCol              # End of line below on screen
nTopLin = nTopLin + 1                      # Scroll down screen
nLeftCol = nLeftCol                        # No change
nLin = nLin                                # No change
nCol = LenLin(ndLin + 1)-(nLeftCol - 1)    # Move to end of line below
```

#### Bottom of Screen, Move to End of Line Below, Hori Scroll
```python
nLin = mWinLin                             # At bottom of screen
ndLin > nDocLin                            # Not at bottom of document
LenLin(ndLin + 1) < nLeftCol               # End of line below not on screen
nTopLin = nTopLin + 1                      # Scroll down screen
nLeftCol = LenLin(ndLin + 1)               # Scroll to end of line below in first screen somumn position.
nLin = nLin                                # No change
nCol = 1                                   # Move to left of screen
```

#### Bottom of Document
```python
nLin = mWinLin                             # At bottom of screen
ndLin = nDocLin                            # At bottom of document
nTopLin = nTopLin                          # No change
nLeftCol = nLeftCol                        # No change
nLin = nLin                                # No change
nCol = nCol                                # No change
```

### Up Key

#### Normal
```python
nLin > 1                                   # Not at top of screen
LenLin(ndLin - 1) >= ndCol                 # Text in line above
nTopLin = nTopLin                          # No Vertical Scroll
nLeftCol = nLeftCol                        # No Horizontal Scroll
nLin = nLin - 1                            # Go up one line
nCol = nCol                                # No change
```

#### No Text Directly above, No Hori Scroll
```python
nLin > 1                                   # Not at top of screen
LenLin(ndLin - 1) < ndCol                  # No Text Directly above Cursor
LenLin(ndLin - 1) >= nLeftCol              # End of line above is on the screen
nTopLin = nTopLin                          # No Scroll
nLeftCol = nLeftCol                        # No Horizontal Scroll
nLin = nLin - 1                            # Go up one line
nCol = LenLin(ndLin - 1) - (nLeftCol - 1)  # Move to end of line above
```

### Move to End of Line Above, Hori Scroll
```python
nLin > 1                                   # Not at top of screen
LenLin(ndLin - 1) < nLeftCol               # No Text Directly above Cursor
nTopLin = nTopLin                          # No Scroll
nLeftCol = LenLin(ndLin - 1)               # Scroll to end of line above in first screen col position.
nLin = nLin - 1                            # Go up one line
nCol = 1                                   # Move to left of screen
```

#### Top of Screen, Text Above, No Hori Scroll
```python
nLin = 1                                   # At top of screen
nTopLin > 1                                # Not at top of document
LenLin(ndLin - 1) >= ndCol                 # Te                 xt in line above
nTopLin = nTopLin - 1                      # Scroll up screen
nLeftCol = nLeftCol                        # No change
nLin = nLin                                # No change
nCol = nCol                                # No change
```

#### Top of Screen, Move to End of Line above, No Hori Scroll
```python
nLin = 1                                   # At top of screen
nTopLin > 1                                # Not at top of document
LenLin(ndLin - 1) < ndCol                  # No Text Directly above Cursor
LenLin(ndLin - 1) >= nLeftCol              # End of line above on screen
nTopLin = nTopLin - 1                      # Scroll up screen
nLeftCol = nLeftCol                        # No change
nLin = nLin                                # No change
nCol = LenLin(ndLin - 1)-(nLeftCol - 1)    # Move to end of line above
```

#### Top of Screen, Move to End of Line above, Hori Scroll
```python
nLin = 1                                   # At top of screen
nTopLin > 1                                # Not at top of document
LenLin(ndLin - 1) < nLeftCol               # End of line above not on screen
nTopLin = nTopLin - 1                      # Scroll up screen
nLeftCol = LenLin(ndLin - 1)               # Scroll to end of line above in first screen somumn position.
nLin = nLin                                # No change
nCol = 1                                   # Move to left of screen
```

#### Top of Document
```python
nLin = 1                                   # At top of screen
nTopLin = 1                                # At top of document
nTopLin = nTopLin                          # No change
nLeftCol = nLeftCol                        # No change
nLin = nLin                                # No change
nCol = nCol                                # No change
```

### Right Key

#### Normal
```python
ndCol < LenLin(ndLin)                      # Not at end of current line
nCol < mWinCol                             # Not at right of screen
nCol = nCol + 1                            # Cursor moves right
nLin = nLin                                # No change
nTopLin = nTopLin                          # No change
nLeftCol = nLeftCol                        # No Change
```
#### Same Line, Horizontal Scroll Right
```python
ndCol < LenLin(ndLin)                      # Not at end of current line
nCol = mWinCol                             # At right of screen
nCol = mWinCol                             # No change
nLin = nLin                                # No change
nTopLin = nTopLin                          # No change
nLeftCol = 1                               # Scroll screen right
```

#### End of Line and Screen, Move Down and Scroll Left
```python
ndCol = LenLin(ndLin)                      # At end of current line
ndLin < nDocLin                            # Not at bottom of document
nLin < mWinLin                             # Not at bottom of screen
nCol = 1                                   # Cursor moves to the left side
nLin = nLin + 1                            # Moves down one line
nTopLin = nTopLin                          # No vertical scroll
nLeftCol = 1                               # Scroll left
```
#### End of Line at left and bottom of screen, Scroll Left and Down
```python
ndCol = LenLin(ndLin)                      # At end of current line
ndLin < nDocLin                            # Not at end of document
nLin = mWinLin                             # At bottom of screen
nCol = 1                                   # Cursor moves to left side
nLin = nLin                                # No change
nTopLin = nTopLin + 1                      # Scroll down
nLeftCol = 1                               # Scroll left
```

#### End of document
```python
ndCol = LenLin(ndLin)                      # At end of current line
ndLin = nDocLin                            # At bottom of document
nCol = nCol                                # No change
nLin = nLin                                # No change
nTopLin = nTopLin                          # No change
nLeftCol = nLeftCol                        # No change
```