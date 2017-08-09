# Rayark v2 modified

Currently, Cytoid only supports chart files in this format. You should be very familiar with it if you have ever modded the game or used a chart editor like [Cytunity](http://cytus-fanon.wikia.com/wiki/User_blog:JCEXE/List_of_Cytus_simulation_programs:_2017_edition#Cytunity). Nevertheless, here's some unofficial documentation. Below is a sample chart file:

```
VERSION 2
BPM 402.000000
PAGE_SHIFT 0.800000
PAGE_SIZE 0.597015
NOTE	0	1.588880	0.800000	0.000000
NOTE	1	2.782910	0.600000	0.000000
NOTE	2	3.976940	0.400000	0.000000
NOTE	3	5.170969	0.600000	0.298508
NOTE	4	5.767984	0.400000	0.298508
......
LINK 26 27 28 29 
LINK 30 31 32 33 
LINK 34 35 
LINK 36 37 38 
LINK 39 40
......
```

## `VERSION`

Format: `VERSION {0}`

The version of the chart format, used internally in Cytus. Cytoid does not attempt to read this parameter.

## `BPM`

Format: `BPM {0}`

Beats-per-minute of the music, used for timing of visual effects in Cytus. As of `Beta 2`, this parameter has no effect in Cytoid.

## `PAGE_SHIFT`

Format: `PAGE_SHIFT {0}`

A page is literally, a page of the chart. When the scanner inverts direction, it marks the start of a new page. This parameter defines how much the first page "shifts", in seconds. Hard to explain, you will have to try adjusting it to understand the concept.

## `PAGE_SIZE`

Format: `PAGE_SIZE {0}`

This parameter defines how long is a page, in seconds. Less the value, faster the scanner movement.

## `NOTE`

Format: `NOTE {id} {timing} {x} {duration}`

This parameter defines a note. Cytus only accepts `id` in chronological order, while Cytoid works with arbitrary  order. `timing` is when the note should be touched. `x` is a value between `0` and `1`, `0` to the leftmost and `1` to the rightmost. `duration` is... duration. For any value larger than zero, it makes the note a hold note.

## `LINK`

Format: `LINK {id 1} {id 2} {id 3} {id 4} ..."

This parameter defines a note chain. If you want two notes with ids `535` and `537` chained together, just write `LINK 535 537`. It's that simple.

## `OFFSET` (Custom parameter)

Format: `OFFSET {0}`

This chart format is called "Rayark v2 modified" because it introduces custom parameters like this one. This parameter adjusts all the note timings at once. For example, if you want all the notes to be delayed by 0.5s, write `OFFSET 0.5`. To make them appear earlier, write `OFFSET -0.5` instead. This parameter is especially useful when your chart editor is inherently not sync with the audio.