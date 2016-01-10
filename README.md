# The Bitshift Variations

## Based on [original code](http://txti.es/bitshiftvariationsincminor) by Rob Miles

See [this video](https://www.youtube.com/watch?v=MqZgoNRERY8) for an explanation
by Rob himself.

This Python (2.7+) script takes the algorithm developed by Rob Miles to generate a
four-voice "chiptune" and produces output for [LilyPond](http://www.lilypond.org)
the open-source music engraver. From here you can create sheet music and MIDI
output.

There are a few hard-coded parts, mostly to do with the duration of each voice. If
you change any of the parameters you will probably have to figure out the duration
again. By default, each voice except the first has 4 "parts", with part 1 being
whole-bar rests for a quarter of the overall duration of the voice. So a bit of
trial and error will get you the right number. After that, you need to find the
smallest common multiple to get a complete cycle. By default this is 480 bars:

|  Voice  | Duration   |   Repeats |
|:-------:|:----------:|:---------:|
|     1   |   16 bars  |   30      |
|     2   |   32 bars  |   15      |
|     3   |   96 bars  |   5       |
|     4   |  160 bars  |   3       |

At 120 BPM, this produces 16 minutes of music.

In the original piece, Part 1
remains as silence for voices 2, 3, and 4, and melody for voice 1. Part 2 is
the melody. Part 3 is the same melody an octave lower. I have taken a little
artistic license with how the part 4 is treated. As far as I can tell, it
combines parts 2 and 3 as an octave chord, but the interaction of multiple
sawtooth waves produces all sorts of beats and rhythms that I haven't tried to
reproduce; I have merely stuck with the simple chord.

## MIDI output
LilyPond can produce MIDI output of its score. I have chosen instruments that are
reminiscent of Yann Tiersen, but feel free to change them for something else.
LilyPond does expect the instruments to be in the [standard list](http://lilypond.org/doc/v2.12/Documentation/user/lilypond/MIDI-instruments#MIDI-instruments), so if you want
something funky, you will have to set up patches in your MIDI software.
For something approaching the original chiptune, try using "lead 2 (sawtooth)"
as the MIDI instrument in the LilyPond template.

## Rob's code

`echo "g(i,x,t,o){return((3&x&(i*((3&i>>16?\"BY}6YB6%\":\"Qj}6jQ6%\")[t%8]+51)>>o))<<4);};
main(i,n,s){for(i=0;;i++)putchar(g(i,1,n=i>>14,12)+g(i,s=i>>17,n^i>>13,10)+g(i,s/3,n+((i>>
11)%3),10)+g(i,s/5,8+n-((i>>10)%3),9));}"|gcc -xc -&&./a.out|aplay`
