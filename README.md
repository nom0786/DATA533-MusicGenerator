﻿# DATA533 - Project Doc
Noman Mohammad & Nyx Zhang
# Introduce
- ### Music Player - Noman
  - Users can randomly choose three notes of their choice 
  - The notes will be sent to the music generator to be parsed into playable music 
  - The user can then select play in order to play the music generated from their note selection 
- ### Jam - Nyx
  - Analyze the input three notes. 
  - Generate chord regression based on the analysis results.
  - Generate rhythm and beats. 
  - Generate a melody based on the three notes and chords.
  - Mix the results into an audio file with the metadata.

# Sub-Packages1 - Music Player
Module 1 - Interface generation

The class name is **MusicInterface**. Its main purpose is to create the underlying GUI for our program. It inherits the Frame class from the tkinter library.
- ### Functions
  - Function 1: Init function
    - Calls the initialize\_interface function which is designed to create the widgets within our interface
  - Function 2:  initialize\_interface
    - This function will create all the widgets for our interface
  - Function 3 - 7 : value\_C - value\_B
    - These functions act upon a piano key click. They call a function from out notes.py module and set values for our notes class

  - Function 8: generate
    - Will act upon the generate button. Calls our MusicJam.py module to generate music based on user input from selected keys. Also calls our notes.py module to clear       notes object upon music generation and set status on the main label

  - Function 9: play
    - Will act upon the play button and play the generated ‘mid’ file from our MusicJam.py module.  Also calls our notes.py module to clear notes object upon music          generation and set status on the main label

Module 2 - Note generation

The class name is **Notes**. Its main purpose is to parse the data coming from the user. This includes duration, speed and error checking for expected note count. 

- ### Functions
  - Function 1: Init function
    - Sets empty lists for notes and time

  - Function 2:  getDuration
    - This function will return a ratio of the elapsed time between note selection approximated to the nearest set value 

  - Function 3: addNote

    - This function appends selected note to our initialized list along with time note was clicked so that calculation of speed and duration is possible

- Function 4: getSpeed

    - This function calculates and returns the total elapsed time from first to last note click 


- Function 5: getNote

    - Returns list of notes for label update in Music player interface

- Function 6: clearNotes

  - Clears the current attributes set for class from user input. Called when music is generated/played

- Function 7: getData

  - Packages data in form accepted by MusicJam.py module to be parsed and turned into music. This returns a list of notes, speed and duration.

Module2 - Note generation

- SetNote will assign note values to the object
- GetNote will retrieve the note values from the object 
- Duration will return a ratio of the elapsed time between note selection approximated to the nearest set value 
# Sub-Packages2 - musicJam
## Module1 - music\_analyzor
- ### Class Introduction

|<p>class MusicAnalyzor:<br>`    `def \_\_init\_\_(self, note\_objects, num\_bars):<br>`        `return \_<br>`    `def key\_analyze(self):<br>`        `return count\_note\_ipt<br>`    `def rhythm\_analyze(self):<br>`        `return rhythm\_start<br>`    `def rhythm\_setting(self):<br>`        `return rtm\_beats</p><p>`    `def chord\_setting(self):<br>`        `return chords\_lst</p><p></p>|
| :- |

The class name is **MusicAnalyzor**. It analyzes the input notes Object and sets the key and rhythm of the music.

- Store the input notes from the music player as initial.
- Analyze and Extract the features.
- Using based information to set key and rhythm.
- ### Functions
  - Function 1: key\_analyze
    - Analyze possible music keys and determine the main key of the music by using empirical probability and music theory.
  - Function 2: rhythm\_analyze
    - Determine the start rhythm of the music based on the input rhythm analyzing result
  - Function 3: rhythm\_setting
    - Based on the analyzed-first-rhythm result to generate the whole rhythm by using empirical probability and music theory.
  - Function 4: chord\_setting
    - Based on the analyzed-first-rhythm result to generate the whole chord progression by using empirical probability and music theory.

## Module2 - music\_generator
- ### Class Introduction

|<p>class MusicGenerator(MysicAnalyzor):<br>`    `def \_\_init\_\_(self, note\_object, num\_bars):<br>`        `return \_<br>`    `def chords\_generate(self):<br>`        `return chords\_lst<br>`    `def melody\_generate(self):<br>`        `return melody\_lst</p><p>`    `def melody\_str2notes(self,melody\_notes):<br>`        `return melody\_lst<br>`    `def chords\_f3notes(self,melody\_lst):<br>`        `return melody\_lst<br>`    `def mix\_melody\_chords(self)<br>`        `return stream</p>|
| :- |

The class name is **MusicGenerator**. It inherits the **MusicAnalyzor** class

- Set all the parent class features as initial.
- The primary model that generates the music.
- Output the music audio, music score picture, and other metadata to the music player.
- ### Functions
  - Function 1: chords\_generate

Transform the generated chords to music21 objects.

- Function 2: melody\_generate
  - generate notes object(pitches and durations) stream based on the beats setting result and generated chords progression by using empirical probability and music theory.
- Function 3: melody\_str2notes
  - a tool for melody\_generate to transform chords objects from roman numerals.
- Function 4: melody\_f3notes
  - a tool for melody\_generate to replace the first several notes to the inputs.
- Function 5: mix\_melody\_chords
  - Mix the stream of notes and stream of chords. 
  - Mix the score of the music.
  - Return the chords, score, and other metadata.

references of music-related metadata

|metadata\_sample = <br>{<br>`   `// beats per minute<br>`   `// default and flexible<br>`   `"bpm":111,<br>`   `//  the major or minor scale around which a piece of music revolves<br>`   `//  default and fixed<br>`   `"Key":"C",<br>`   `// rhythmic pattern constituted by the grouping of basic temporal units, called beats, into regular measures, or bars<br>`   `// default and fixed<br>`   `"meter":"4/4",<br>`   `// music genre: such as Blues, Jazz, Metal.<br>`   `// default and fixed<br>`   `"genre":"pop",<br>`   `// chords of music melody in this key<br>`   `// model generated the whole melody chords divided by the bars.<br>`   `"chords":[<br>`      `{<br>`      	`// chords<br>`         `"chords":[<br>`            `"C",<br>`            `"G",<br>`            `"Am",<br>`            `"B-"<br>`         `],<br>`         `// Offset of the chord in the unit beat<br>`         `"chordRythm":[<br>`            `"1",<br>`            `"2",<br>`            `"3",<br>`            `"4"<br>`         `]<br>`      `},<br>`      `{<br>`         `"chords":[<br>`            `"G",<br>`            `"A",<br>`            `"C",<br>`            `"D"<br>`         `],<br>`         `"chordRythm":[<br>`            `"1",<br>`            `"2",<br>`            `"3",<br>`            `"4"<br>`         `]<br>`      `}<br>`   `],<br>`   `// notes of music melody in this key<br>`   `// user random input several notes, then model generated the whole melody notes divided by the bars.<br>`   `"notes":[<br>`      `{<br>`      	`// notes<br>`         `"notes":[<br>`            `"C",<br>`            `"E",<br>`            `"A",<br>`            `"G",<br>`            `"C",<br>`            `"D",<br>`            `"F",<br>`            `"D"<br>`         `],<br>`         `// Offset of the notes in the unit beat<br>`         `"notesRythm":[<br>`            `"0.25",<br>`            `"0.25",<br>`            `"0.125",<br>`            `"0.75",<br>`            `"1",<br>`            `"0.25",<br>`            `"0.5",<br>`            `"1"<br>`         `]<br>`      `},<br>`      `{<br>`         `"notes":[<br>`            `"G",<br>`            `"A",<br>`            `"F",<br>`            `"G",<br>`            `"C",<br>`            `"D",<br>`            `"G",<br>`            `"D"<br>`         `],<br>`         `"notesRythm":[<br>`            `"0.75",<br>`            `"1",<br>`            `"0.5",<br>`            `"0.25",<br>`            `"0.5",<br>`            `"1",<br>`            `"0.5",<br>`            `"1"<br>`         `]<br>`      `}<br>`   `]<br>}|
| :- |





