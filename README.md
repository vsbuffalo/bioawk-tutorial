# A Quick bioawk tutorial

There was some interest in bioawk, a useful awk fork for handling
bioinformatics formats at the UC Davis Software Carpentry course, so
here is a quick tutorial.

## Concepts

Don't write your own FASTA/FASTQ parsers! FASTA is much easier, but
*code reuse* is important here. FASTQ is a very hard format to parse
*safely* and *quickly*. See
[this post](http://www.biostars.org/p/10353/#11256) for more info on
how trick it can be to parse FASTQ.


Heng Li (author of samtools, bwa) has written a nice set of parsers
for different languages called
[readfq](https://github.com/lh3/readfq). bioawk is also a tool of Heng
Li's too. 

## Installing 

For this quick tutorial, let's just clone bioawk and install it to
your `/usr/local/bin/`:

    git clone git://github.com/lh3/bioawk.git && cd bioawk && make && mv awk bioawk && sudo cp bioawk /usr/local/bin/


## What's awk?

awk is an old programming language that is useful for processing
*streams* of data. Very quickly, there are three parts of each quick
awk program: BEGIN, middle, and END. BEGIN is loaded before the data,
the middle is run on each line, and the END is run after the lines are
done processing. For example, we could do:

    $ cat animals.txt
    2011-04-22 21:06 Grizzly 36
    2011-04-23 14:12 Elk 25
    2011-04-23 10:24 Elk 26
    2011-04-23 20:08 Wolverine 31
    2011-04-23 18:46 Muskox 20

    $ awk '{ if ($4 > 26) print $3 }' animals.txt
    Grizzly
    Wolverine

So awk maps these columns to column numbers, like `$1` and `$3`. `$0`
is the whole line. Delimiters (field separators) can be set with `-F`.

## Bioawk

Bioawk is just like awk, but instead of working with mapping columns
to variables for you, it maps bioinformatics field formats (like
FASTA/FASTQ name and sequence).


