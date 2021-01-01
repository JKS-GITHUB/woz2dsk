# woz2dsk #

*woz2dsk* is a utility for converting .woz files to .dsk, .po and .nib
files.  These formats are widely used by Apple II emulators.


## Synopsis ##

    woz2disk [options...] in.woz out.dsk

Options:

* `-f STR`, `--format STR`:
  output format: one of `auto`, `DOS`, `ProDOS`, `nibble`
* `-q`, `--quiet`:
  suppress output messages
* `-d`, `--debug`:
  show debug messages
* `-h`, `--help`:
  print usage message and exit


## Description ##

Convert an Apple II disk image from `.woz` format
to one of `.dsk` (a.k.a. `.do`), `.po` or `.nib` format.
Only images for 5.25" single-sided disks
in the standard 16-sector format
(i.e. 35 tracks * 16 sectors * 512 bytes)
without copy protection
are supported.

Not every Apple II emulator supports the recent `.woz` format.
Most emulators, however, support the well established
`.dsk`, `.po` and `.nib` formats.
This tool thus provides a means for such emulators to
use disk images available only in `.woz` format.


### Input format ###

This program only accepts
[WOZ version 2](https://applesaucefdc.com/woz/reference2/) image files.

### Output format ###
If the output format is `auto` (default), then it is determined from
the extension of the output file.
If the extension begins with `p`, then the output format is `ProDOS`.
If the extension begins with `nib`, then the output format is `nibble`.
Otherwise the output format is `DOS`.

* `DOS`: This format is very common and is usually found in image files
  with the extensions `.dsk` and `.do`.
  The file contains the contents of the formatted disk,
  track after track.
  Within each track, sectors are ordered by logical sector numbers,
  mapped to physical sector numbers in the DOS 3.3 way.[[1]][r1]
  These images have a fixed size of 144360 bytes (= 140KB).

* `ProDOS`: This format is usually found in files with the `.po` extension.
  It is like the `DOS` format in most aspects, except that the
  mapping between logical and physical sector numbers follows
  the ProDOS convention.[[1]][r1]
  
* `nibble`: This is usually associated with filename extension `.nib`.
  These files contain the raw nibbles in each track, one track after another.
  Each track has exactly 6656 (hex 1A00) bytes per track.
  The total file size is 232960 (277.5 KB).

[r1]: http://www.applelogic.org/TheAppleIIEGettingStarted.html


## Examples ##

    woz2dsk 'DOS 3.3 System Master.woz' DOS_3.3_System_Master.dsk
    woz2dsk 'DOS 3.3 System Master.woz' DOS_3.3_System_Master.nib
    woz2dsk 'The Apple at Play.woz' The_Apple_at_Play.po
    woz2dsk 'The Apple at Play.woz' The_Apple_at_Play.nib

These two `.woz` files come from
[WOZ test images](http://evolutioninteractive.com/applesauce/woz_images.zip).


## GitHub ##

<https://github.com/leesaudan2/woz2dsk>


