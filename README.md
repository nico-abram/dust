[![Build Status](https://travis-ci.org/bootandy/dust.svg?branch=master)](https://travis-ci.org/bootandy/dust)


# Dust
du + rust = dust. Like du but more intuitive

## Install

 * Download linux / mac binary from [Releases](https://github.com/bootandy/dust/releases)
 * unzip file: tar -xvf _downloaded_file.tar.gz_
 * move file to executable path: sudo mv dust /usr/local/bin/

## Overview
Dust is meant to give you an instant overview of which directories are using disk space without requiring sort or head. Dust will print a maximum of 1 'Did not have permissions message'.

Dust will list the 15 biggest sub directories or files and will smartly recurse down the tree to find the larger ones. There is no need for a '-d' flag or a '-h' flag. The largest sub directory will have its size shown in *red*

## Why?
du has a number of ways of showing you what it finds, in terms of disk consumption, but really, there are only one or two ways you invoke it: with -h for “human readable” units, like 100G or 89k, or with -b for “bytes”. The former is generally used for a quick survey of a directory with a small number of things in it, and the latter for when you have a bunch and need to sort the output numerically, and you’re obligated to either further pass it into something like awk to turn bytes into the appropriate human-friendly unit like mega or gigabytes, or you just do some rough math in your head and use the ordering to sanity check. Then once you have the top offenders, you recurse down into the largest one and repeat the process until you’ve found your cruft or gems and can move on.

Dust assumes that’s what you wanted to do in the first place, and takes care of tracking the largest offenders in terms of actual size, and showing them to you with human-friendly units and in-context within the filetree. 

## Usage
```
Usage: dust <dir>
Usage: dust <dir> <another_dir> <and_more>
Usage: dust -s <dir> (apparent-size - shows the length of the file as opposed to the amount of disk space it uses)
Usage: dust -n 30  <dir>  (Shows 30 directories not 15)
```


```
djin:git/dust> dust
  65M  .
  65M └─┬ ./target
  49M   ├─┬ ./target/debug
  26M   │ ├─┬ ./target/debug/deps
  21M   │ │ └── ./target/debug/deps/libclap-9e6625ac8ff074ad.rlib
  13M   │ ├── ./target/debug/dust
 8.9M   │ └─┬ ./target/debug/incremental
 6.7M   │   ├─┬ ./target/debug/incremental/dust-2748eiei2tcnp
 6.7M   │   │ └─┬ ./target/debug/incremental/dust-2748eiei2tcnp/s-ezd6jnik5u-163pyem-1aab9ncf5glum
 3.0M   │   │   └── ./target/debug/incremental/dust-2748eiei2tcnp/s-ezd6jnik5u-163pyem-1aab9ncf5glum/dep-graph.bin
 2.2M   │   └─┬ ./target/debug/incremental/dust-1dlon65p8m3vl
 2.2M   │     └── ./target/debug/incremental/dust-1dlon65p8m3vl/s-ezd6jncecv-1xsnfd0-4dw9l1r2th2t
  15M   └─┬ ./target/release
 9.2M     ├─┬ ./target/release/deps
 6.7M     │ └── ./target/release/deps/libclap-87bc2534ea57f044.rlib
 5.9M     └── ./target/release/dust
```
## Performance
dust is currently about 4 times slower than du.

## Alternatives
 * [NCDU](https://dev.yorhel.nl/ncdu)
 * du -d 1 -h | sort -h

Note: Apparent-size is calculated slightly differently in dust to gdu. In dust each hard link is counted as using file_length space. In gdu only the first entry is counted.
