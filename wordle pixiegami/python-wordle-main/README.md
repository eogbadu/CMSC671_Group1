#
This project is for the CMSC671 fall class at UMBC.
This is comprised of code from the pixegami author found on youtube and github (citations below).

The code has been modified and scripts added to provide an interface for an agent to play the game.
This is done by writing guesses to the agent_guesses file.  The main loop is run from the "pixigame_modified_play_wordle_with_agent_loop.ipynb" script.  

## This code is the one you will use to run the program.
## It imports from the other python programs.

there is a data directory where the data files are stored.  
These files are code written by this team which includes code from the play_wordle.py file that was written by the original author.

## Agent_guess_writer.ipynb
    This script provides an interface for the agent to write guesses into a file.  That file is embedded in the game loop and the master agent pulls these guesses into the game.
    
## create_5_letter_word_text.ipynb
    This file creates a 5 letter word list from the nltk words data file, extracting the 5 letter words and writingthese to a file in the data directory.
    
## pixigame_modified_play_wordle_with_agent_loop.ipynb 
    This script includes code from the original author that has been included, augmented, and modified to support the game interface as well as providing a game loop where the agent software can connect.  

# These files are original from the pixegami author

## convert_words.py

## letter_state.py

## play_wordle.py
    This file has been modified to provide some specific alterations required in our agent implementation

## README.md

## word_source.txt

## wordle.py


# Data directory

## convert_words.py  
This is an  script from the original author that creates the word list
## word_source.txt  
This is the author's word list

# These files are written as part of this project
## agent_guesses.txt  
This is a file that provides the agent input to the game.   
## wordle_words.txt
This is a file of the words used in this script


# Citations
This work was significanly informed by code from this youtube site and corresponding github repository.  

Created on Sat Nov  5 13:25:36 2022
@author: johnny
This code was heavily influenced by a design published in youtube under 
this url: https://www.youtube.com/watch?v=SyWeex-S6d0

Youtube citation:
pixegami. (2022b, February 6). Build Wordle in Python • Word Game Python Project for Beginners. 
YouTube. https://www.youtube.com/watch?v=SyWeex-S6d0

github citation:
PIXEGAMI. (n.d.). GitHub - pixegami/python-wordle: 
An implementation of Wordle in Python than can be played via the terminal. 
GitHub. https://github.com/pixegami/python-wordle




# Below is the original readme from the pixegami author
----------------------------------------------------------------------------------------------------------
# python-wordle
An implementation of Wordle in Python than can be played via the terminal.

## Bug Fix Update

It was pointed out to me that the game didn't behave like Wordle does when two identical letters
are in a 'guess', but only one copy of that letter is in the word.

### Problem

For example, if the guess is HELLO and the secret is APPLE, then the previous behavior causes
the first occurrence of the L to be yellow (because it does appear in the word), but then the second
L will be green (because it is in the right position).

On a letter-by-letter basis, this behavior appears fine. But when the entire word is considered, that
first L shouldn't appear yellow. Instead, it should appear grey. That's because there is already another
L in the guess that 'claims' the occurrence of the L in the secret.

### Solution

* Instead of resolving all the letter results in one-pass, we now first initialize it as an array and
default all guess letters to grey (not in the word).
* We create an list, which is a copy of the secret. Each element corresponds to the letter in the string. 
For example `["A", "P", "P", "L", "E"]`.
* We then do a first pass through the guess, and identify any letters in the correct position. If we find one,
then that letter becomes 'green', and the secret list is updated to void out that letter so it can't be used
in a subsequent comparison. So if we guess "HELLO", the remaining secret becomes something like this:
`["A", "P", "P", "*", "E"]`.
* We then do another loop this time identify the guessed letters which are in the word (by using a nested loop),
but not in position.