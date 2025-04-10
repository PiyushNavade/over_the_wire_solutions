# [Bandit Level 2 → Level 3](https://overthewire.org/wargames/bandit/bandit3.html)

## Goal
The password for the next level is stored in a file called spaces in this filename located in the home directory.

## Theory
Just like the last level, this level tests how to handle odd file names. In this case, the file name has spaces in it.
1. To use a filename with spaces in it, you can wrap it in quotes: `cat "file name with spaces"`
2. You may also escape every space with backslash: `cat file\ name\ with\ spaces`

> Tab completion often works with spaces as well. Your terminal may show the file name with space escaped with backslash if you press tab key for the filename.

## Solution
1. Login to bandit2.
2. Use `cat "spaces in this filename"`
