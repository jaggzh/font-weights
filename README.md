## Scan through Linux fonts and examine weights

Usage:

```bash
$ ./font-weights >list.txt
$ sort -n list.txt >sorted.txt
```

## Explanation
This uses imagemagick's `convert -list font` to get a list
of fonts.  It currently then only accepts TTFs.  It then
estimates the font weight -- really it just generates a
400x100 image with the text ABCDEFGabcdefg in it, and
counts the black pixels.  It outputs the % black followed
by the filename on each line (so newlines in filenames will
screw up the output).  (Convert will scale the text to the
largest size that'll fit in the 400x100 image.)

## Improvements

1. I used "convert" to generate the text image, then later
switched to coding this in perl, but still call "convert".
It could probably be made faster doing the text in perl.
1. The method of examing weights is going to have issues,
in particular with weird-shaped letters (glyphs).  If they're
really wide, they might still be bold (high weight), but because
`convert` will scale the whole thing down to, fit in the fixed-size image,
they'll end up with a lower percentage of black pixels.  Nevertheless,
it works good enough to find a bunch of heavy or light fonts on the system.
1. I use English letters to test.  You can change the string by looking for the ABCDEFGabcdefg.
1. Output format ignores newlines in filenames.
