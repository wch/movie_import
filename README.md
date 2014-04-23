Movie import scripts
====================

The purpose of these scripts is to make it easier to import movie files from camera memory cards. This is presently a four-step process:

1. Run `copy_movie_files`, which copies movie files from an memory card or attached camera to a directory on disk.
1. Convert the movie files to .mp4 files using Handbrake.
1. Run `movie_time_fix`, which uses copies the EXIF information from the original movie files to the new .mp4 files, using `exiftool`.
1. Finally, import the files into Lightroom or other photo management program.

A lot of this functionality has yet to be implemented,


## Why?

It would be simpler to directly import files from a memory card into Lightroom. So why would you want to take all these extra steps? Here are some reasons:

* The .mp4 files from Handbrake are much smaller than the files from the camera, even at the same resolution.
* The movie files can be converted to a lower resolution, saving more space.
* The movie files can be de-interlaced in the conversion process.
* If you have a Sony camera, when Lightroom imports the .mts files, it fails to recognize EXIF metadata, including the time that a movie was recorded. All the other programs I've used to view .mts files also ignore the EXIF data.


## Handbrake presets

The handbrake_presets/ subdirectory contains some presets for Handbrake conversions. They are based on the the Normal and High Profile presets that come built-in with Handbrake, but with some slight modifications. All of the presets in handbrake_presets/ set the output resolution (the built-in presets do not). Also, the Normal presets add *decombing*, which will de-interlace movies that are interlaced (e.g., 1080i), but won't affect movies that are not interlaced (e.g., 1080p). The High Profile built-in presets already have decombing enabled.


### Conversion file sizes

Below are the file size results of some tests of movie file coversions.

#### Sony a7 .mts file, 1920x1080p 60fps

An .mts movie from a Sony a7 shot at 1920x1080p 60fps takes about 192 MB/minute. After conversion, the resulting data rates are:

fps | Quality | Resolution | Data rate   | Compression ratio
--- | ------- | ---------- | ----------- | -----------------
60  | High    | 1080p      | 55 MB/min   | 3.5x
60  | High    | 720p       | 24 MB/min   | 8x
60  | High    | 480p       | 12.5 MB/min | 15x
60  | Normal  | 1080p      | 43 MB/min   | 4.5x
60  | Normal  | 720p       | 19 MB/min   | 10x
60  | Normal  | 480p       | 10.5 MB/min | 18.5x
30  | High    | 1080p      | 53 MB/min   | 3.5x
30  | High    | 720p       | 22 MB/min   | 8.5x
30  | High    | 480p       | 11.5 MB/min | 16.5x
30  | Normal  | 1080p      | 44.5 MB/min | 4.5x
30  | Normal  | 720p       | 19 MB/min   | 10x
30  | Normal  | 480p       | 10.5 MB/min | 18x

Surprisingly, the 30fps output files are almost exactly the same size as the 60fps files. They also look a lot choppier, so there's no reason to use them. For these reasons, all the presets in handbrake_presets/ leave the framerate at the original setting.



#### Canon EOS M .mov file, 1920x1080p, 30fps

TODO: Fill this in
