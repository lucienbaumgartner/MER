# MER (Minimal Named-Entity Recognizer)

MER is a Named-Entity Recognition tool which given any lexicon and any input text returns the list of 
terms recognized in the text, including their exact location (annotations).
MER is better described in [link to proceedings paper]. 

## Dependencies

### awk

MER was developed and tested using the GNU awk (gawk). If you have another awk interpreter in your machine, there's no assurance that the program will work.

To install GNU awk on Ubuntu:

```
sudo apt-get install gawk
```

## Preparation of Lexicons 

Let's walk trough an example of adding a sample lexicon to MER. 

First, we have to create the lexicon file. 

```txt
α-maltose
nicotinic acid
nicotinic acid D-ribonucleotide
nicotinic acid-adenine dinucleotide phosphate
```

We save this in a file called "lexicon.txt" and save it in the data/ folder of MER. Next, we do 

```shell
bash produce_data_files.sh lexicon.txt
```

This will create all the necessary files to use MER with this lexicon. 

## Usage

```shell
bash get_entities.sh [text] [lexicon]
```

Ok, let's try to find mentions of chemical compounds in a snippet of text:

```shell
bash get_entities.sh 'α-maltose and nicotinic acid D-ribonucleotide was found, but not nicotinic acid' lexicon
```

The output will be a TSV looking like this:

```tsv
0       9       α-maltose
14      28      nicotinic acid
65      79      nicotinic acid
14      45      nicotinic acid D-ribonucleotide
```

The first column corresponds to the start-index, the second to the end-index and the third to the annotated term.

