---
type: assignment
date: 2020-03-07
title: 'Project 1: Variant detection using the FM-index'
due: 2020-03-30
published: true
---

**Due: Mon March 30, 2020**  
**Posted: March 9, 2020**  
**Last updated: March 9, 2020**  

**Note**: This assignment is based on a project developed by Héctor Corrada Bravo for a previous 
iteration of the course.  However, it has been modified (in parts, substantially) for the current iteration of the course.

You will implement approximate string matching using a seed-and-check / seed-and-extend strategy based on exact matching using the FM-index, as well as a "fitting alignment" to build a basic read aligner. 

As you develop your proejct, I **highly, highly** recommend that you use [`git`](https://git-scm.com/book/en/v1/Getting-Started) for developing your code.

To get started, you can clone [this](https://github.com/rob-p/CMSC423_bwt_variant) repository, which contains a `data` sub-directory with the data that is described below that you will use for this project.

## Assignment ##

The goal of this project is to build a _very, very basic_ read aligner with the purpose of using it to discover variants 
in a genome.  

### The problem of variant finding ###

The problem of using a sequenced sample to determine genomic variants with respect to some reference genome is common.  In reality, there are [entire _pipelines_](https://gatk.broadinstitute.org/hc/en-us) focused around the challenges posed by variant detection from experimental data.  One of the big challenges includes potentially low sequencing coverage of the variant regions, which makes it difficult to distinguish a true variant from sequencing errors.

However, for the purposes of this assignment, our focus is on implementing the concepts we've built up in class, and so we've made the actual variant detection problem easy by (1) providing _very high_ coverage of the target genome so that the detection of variants is easier (2) limiting the size of variants to be very small, which makes them easier to detect and (3) giving you extra information (the number of variants).

The basic variant detection procedure is as follows.  You will build a tool to align your reads to the reference genome.  Then, by looking at "pile ups" of the reads on the reference genome, you will determine places where the sequenced sample (represented in the simulated reads) differs from the reference data, as evidenced by the repeated variation in the reads that cover a certain position in the genome.

### Your data ###

You are provided with a _reference genome_ for a particular strain of the coronavirus (2019-nCoV/USA-IL1/2020).
This genome is a single "contig" (a single fasta file entry) and is provided in `data/2019-nCoV.fa`.  *NOTE*: This is the _real_ sequence for this strain of the coronavirus (cool, huh?).

Additionally, you are provided with a set of _single-end_ sequencing reads in the file `data/reads.fa.gz`.  These reads are gzipped to save space; you can either unzip them or use a library for reading the data that reads directly from a gzipped file.  There are 1,000,000 reads, each of length 100 nucleotides / base pairs (100bp).  They have been simulated from a _variant strain_ of the coronavirus that has a small number of variations (both point mutations and small insertions and deletions) with respect to the reference strain provided in `data/2019-nCoV.fa`.

### Your goal ###

**Your task is to write a basic read alignment tool, based on the seed-and-extend or seed-and-vote paradigm (whichever you prefer) using the FM-index for efficient seed finding**.

Simplifications for the data provided in this project:

  * Often, reads will be drawn (approximately equally) from both the forward and reverse complement strands of
  the underlying (c)DNA.  However, to simplify the read alignment problem for this project, the reads are 
  _all drawn from the forward strand_.  That means that instead of having to consider aligning both the provided 
  sequence of each read as well as that read's reverse complement (or, instead of having to index both the index
  and the reverse complement of the index), you can simply index the reference in the provided orientation and 
  you can assume that each read will align in its provided orientation.


### Your tool ###

You should implement a tool named `fmmap` (for FM-index mapper).  The `fmmap` tool should have two commands:

The first command is called `index`, and it takes 2 arguments.  The first argument is the path to a FASTA
format file and the second is the location of an output file where the index will be written.  When invoked
in this mode, `fmmap` will read the input file and will compute the FM-index of the corresponding string.
In this case, the index should consist of:

  1. The name and length of the input sequence (which is referred to below as S)
  2. An efficient representation of the first column of BWM(S)
  3. The last column of BWM(S)
  4. The occ table (can be sampled if you want, but it need not be) for the characters 'A', 'C', 'G', and 'T'
  5. The suffix array (can be sampled if you want, but it need not be) of S
  
together, these components will allow you to perform efficient backward search in over S for seed finding.
It is highly recommened you write your index down in a _binary_ format. This will make writing and reading 
it more efficient.  Importantly, it will also let you think about how actual tools might pack multiple different
components for their indices into a file.

The index command should be executed as follows:

~~~bash
$ fmmap index reference.fa ref_index
~~~

This will index `reference.fa` and write the output index, with the components described above, to `output_index`.  **While you are free to implement the indexing procedure however you want**, I would recommend building the suffix array first, then using that to read off the BWT(S), from which you can derive the first column of BWM(S), and the occ table for all characters in linear time.

The second command that `fmmap` should implement is a command called `align`.  This command should be executed as such:

~~~bash
$ fmmap align ref_index reads.fq alignments.sam
~~~

This command takes 3 arguments, the first is the index built by `fmmap index`, the second is a FASTA format file 
containing the read sequences, and the third is the output file where the alignments for the reads are to be written.
The reads are to be written in SAM format, for which the specification is [here](https://samtools.github.io/hts-specs/SAMtags.pdf).  **NOTE**: You should immediately take some time to familiarize yourself with the SAM format.  It is the _lingua franca_ of read alignments in genomics, but it is not the most intuitive thing in the world.  For this project, we are trying to keep things as simple as possible by dealing only with single-end reads, most of which should map in only one location.  Nonetheless, your program should needs to write a _valid_ SAM file; otherwise, the steps described below for converting your output to BAM format, sorting and indexing it, and loading it into IGV will not work.  Specifically, when you perform alignment using your "fitting alignment" function, you will have to convert the alignment string into the CIGAR format that is used by SAM to encode alignments.  The format is not difficult, but you should write and thorougly test the functions for converting the backtrace from your alignment to a CIGAR string.

**How should my mapping algorithm work?** We are providing you with some freedom to explore the space of algorithms / heuristics if you wish.  However, here is a somewhat naive (but acceptable) basic algorithm for determining the alignments for each read in pseudocode:

~~~python

ninf = float("-inf")
seed_skip = lambda l: math.floor(l / 5.0)
gap = 5

for name, seq, qual in readfq(readfile):
    alignments = []
    read_len = len(seq)
    best_score = ninf
    seed_pos = 0
    skip = seed_skip(read_len)
    for seed_start in range(0, read_len, skip):
    	seed_end = min(read_len, seed_start + skip) 
    	##
	# get_interval takes a string and performs backward search until 
	# either (1) the entire string is matched or (2) the search interval
	# becomes empty.  The second return value, match_len, is the length of
	# the query matched in backward search.  If the interval is non-empty
	# then this is just equal to `skip` above.
	##
    	interval, match_len = bwt_index.get_interval(seq[seed_start:seed_end])
	
	# given all the places where the seed matches, look for an alignment around it
	# the ref_positions member of `bwt_index` will return positions on the reference 
	# string corresponding to the *beginning of the read*, assuming there are no gaps
	# in the alignment before the start of the seed (handling that is why we do fitting 
	# alignment below).
	for ref_pos in bwt_index.ref_positions(interval, seed_end, match_len):
	    # Perform a "fitting" alignment of the query (seq) into the reference (ref)
	    # the returned alignment object contains the score, the alignment and the 
	    # implied position where the query (seq) begins under the alignment.
	    # To perform the fitting alignment, you should "slice out" a region of the 
	    # reference around the implied start position (ref_pos) with a bit of padding
	    # (e.g. gap bases) before the first base where the read would start and after
	    # the last base where the read would end.  This will ensure that the fitting_alignment
	    # procedure can find the optimal position for the query within the reference
	    # window that contains it, even if there are insertions or deletions in the read.
	    alignment = fitting_alignment(seq, ref, ref_pos, gap)
	    if alignment.score > best_score:
	    	best_score = alignment.score
		alignments = [alignment]
	    elif alignment.score == best_score:
	        alignments.append(alignment)
    for a in alignments:
        write_to_sam(output_file, a)
~~~

Of course, there are all kinds of heuristics you can use to speed things up.  For example, if you have already determined that a read should align to a specific reference position, then there is no use aligning the read to that position again (due to another seed), so you could keep the list of aligned positions in a hash table for each read to avoid redundant work.  Likewise, if a read maps end-to-end with no edits, then there can be no better alignment, and you must have found all equally-best alignments, so you can skip lookup for the rest of the seeds of that read etc.  You are not required to implement such heuristics, but you are encouraged to try them out (and write about them in the report).

**Question**. The provided reads are drawn from a strain of the coronavirus; your goal is to determine _what variants_ this strain has with respect to the reference genome with which you are provided (in `data/2019-nCoV.fa`)?

**How to look for variants:** To look for variants, I _highly_ suggest you use the Integrative Genomics Viewer (IGV), which you can get for all platforms [here](https://software.broadinstitute.org/software/igv/download).  This is a tool to let you visualize the pileup of alignments on the genome and determine what the relevant variants are.  To load the SAM file generated by your program into IGV, you first need to sort and index the file.  The easiest way to do this is with [samtools](http://www.htslib.org/download/).

The easiest way to do this is to install [samtools](http://www.htslib.org).  If you don't want to compile these from source, you can install it using the [bioconda package manager](https://bioconda.github.io), which will acquire a pre-compiled binary for you.  Once you have samtools installed, you can convert your SAM file to a BAM file (a compressed, binary version of the SAM file that is commonly used in bioinformatics tools) using the following command:

~~~bash
$ samtools view -b -o mapping.bam mapping.sam
~~~

Now, you have a BAM file of your alignments.  The next task is to sort the alignments by coordinate, which can be completed
with the following command:

~~~bash
$ samtools sort -o mapping_sorted.bam mapping.bam
~~~

Finally, you can generate the index used by IGV with:

~~~bash
$ samtools index mapping_sorted.bam
~~~

As an alternative to samtools, the above can also be done with the Picard tools (written in Java), which is available [here](https://broadinstitute.github.io/picard/), though the exact syntax and command names are slightly different.

Now, you have both the original genome `2019-nCoV.fa` and the sorted BAM file with your alignments `mapping_sorted.bam`. 
Open up IGV, and load the genome.  You can do this through the main menu by *Genomes* -> *Load Genome From File*, and pointing it at `2019-nCoV.fa`.  Then, you can load your alignments using *File* -> *Load from File*, and pointing it at `mapping_sorted.bam`.  IGV will load the file and you can now explore the visualization.  Detailed instructions on how to navigate your alignments using IGV can be found [here](https://software.broadinstitute.org/software/igv/AlignmentData).  **You can use IGV to interactively navigate the pileup and locate the variants**.

### Hints ###

The reads encode *8* variants with respect to the reference strain.  So, you should be looking to find *8* total differences between the reference strain and your reads.  Moreover, exactly *4* of these variants are single nucleotide variants (SNVs) (i.e. point mutations where a base in the reference is replaced by a different base in the sample).  The other *4* are small insertions or deletions from the reference strain (to keep things simple, all of the indels are <= 5 base pairs in length).

## Deliverables ##

Your deliverable consists of a tarball containing:

 1. Your source code, along with a README.md file containing instructions for building your tool.  If your tool is written in a compiled language (C/C++, Java, Rust, Go, etc.), then it should build using a single command using the canonical build system for the language (e.g. `make` for C/C++, `cargo` for Rust, etc.).
 
 2. A report, in PDF format, that is a writeup discussing your findings.  Specifically, your report
    should contain _at least_ the following sections:
    
      * Discovered variants : what variants did you discover?  What is the evidence you found for these 
      variants?  You are encouraged to include e.g. screenshots from IGV showing your pileups in the variant regions.
      Specifically, **for each variant, what is the position (with respect to the original reference) at which it occurs, and what is the nature of the variant / edit?**. Is it a substitution, an insertion, or a deletion.  If it is a substitution, what reference base is substituted for what variant base?  If it is a deletion, which bases are deleted?  If it is an insertion, what bases are inserted?
      
      * Design : what specific design decisions did you make in your tool, and why?  If you were going to start the 
        project again from scratch, what, if anything, would you do differently?
      
      * Roadblocks : what part of the project did you find the most difficult?  Where did you get stuck and how did you 	(hopefully) overcome this difficulty?

### Notes:

* You may use an existing library to help with the parsing of the input.  Very simple functions to read FASTA and FASTQ files in a few different languages can be found [here](https://github.com/lh3/readfq).  If you have a question about whether or not you can use a specific library, just ask.  The requirements for this project are _much less strict_ than for Project      Rosalind.  Unless the library performs one of the core functions we want you to implement, we are likely to say "yes" to it.
