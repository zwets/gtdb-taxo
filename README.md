# gtdb-taxo

_Command line GTDB taxonomy browser_

## Introduction

`gtdb-taxo` is a command line utility to query the GTDB Genome Taxonomy.
It can look up taxons by name, regex, representative genome, and so on.

The program is the GTDB equivalent of [taxo](https://github.com/zwets/taxo)
which does the same for the NCBI/ENA taxonomy.

`gtdb-taxo` can also operate interactively (`gtdb-taxo-browser`), allowing
you to navigate up and down the taxonomy tree from the command line.

`gtdb-taxo` and `gtdb-taxo-browser` use `gtdb-taxo-db` as their back-end.
`gtdb-taxo-db` imports the GTDB taxonomy into a SQLite3 database and offers
a SQL interface to query it.

`gtdb-taxo` is lightweight and requires no special installation, apart from
the initial import of the GTDB database.

Home: <https://github.com/zwets/gtdb-taxo>


## Installation

* Prerequisites

  `gtdb-taxo` requires the `sqlite3` and `GNU awk` programs.  These are often
  already present on your system, or else easily installable.  On Debian/Ubuntu:

      sudo apt-get install sqlite3 gawk

  If you want to search using regular expressions, then install the PCRE
  extension for `sqlite3`:

      sudo apt-get install sqlite3-pcre gawk

  Your distro will have comparable instructions.

* Clone the repository

      git clone https://github.com/zwets/gtdb-taxo.git
      cd gtdb-taxo
      ./gtdb-taxo --help

* Import the taxonomy database

  If you are working with the GTDB, then it is likely you have installed
  [GTDBTk](https://github.com/Ecogenomics/GTDBTk) and have set
  `GTDBTK_DATA_PATH` to point to its data directory.  The file to import
  is then `$GTDBTK_DATA_PATH/taxonomy/gtdb_taxonomy.tsv`:

      gtdb-taxo-db --import "$GTDBTK_DATA_PATH/taxonomy/gtdb_taxonomy.tsv"

  If you do not have GTDBTk installed, see its installation instructions
  for the download location of its database, and extract `gtdb_taxonomy.tsv`
  from it.

* [Optional] Add `gtdb-taxo` to your path

  No further installation is needed.  For convenience you could add `gtdb-taxo`'s
  directory to your `PATH`, or symlink the `gtdb-taxo` script in your `~/bin` or
  `~/.local/bin` directory, depending on your shell.


## Usage

The `gtdb-taxo`, `gtdb-taxo-browser`, and `gtdb-taxo-db` commands are self-contained.
Invoke with `--help` to see usage instructions.  Below are some examples to get you going.

### Examples: Command-line Use

The default is to search on any part of the taxon name:

```bash
$ ./gtdb-taxo Staph
...
family   Staphylococcaceae         f__Staphylococcaceae
order    Staphylococcales          o__Staphylococcales
genus    Staphylococcus            g__Staphylococcus
species  Staphylococcus agnetis    s__Staphylococcus agnetis    RS_GCF_002901865.1
species  Staphylococcus argensis   s__Staphylococcus argensis   RS_GCF_002902305.1
species  Staphylococcus argenteus  s__Staphylococcus argenteus  RS_GCF_000236925.1
...
```

The output are four tab-separated columns.  These list rank, name, unique name (as
used by GTDB), and, for species, accession of the representative genome (see the 
[GTDBTk](doi:10.1101/771964) paper).


*Exact search (`-e` `--exact`):*

```bash
$ gtdb-taxo -e 'Tranquillimonas'
genus   Tranquillimonas g__Tranquillimonas
```

*Regular expression search (`-r`, `--regex`):*

```bash
$ gtdb-taxo -r '.*monas$'
genus    Acidomonas      g__Acidomonas
genus    Aeromonas       g__Aeromonas
genus    Aidingimonas    g__Aidingimonas
genus    Albimonas       g__Albimonas
genus    Alkalimonas     g__Alkalimonas
...
```


### Examples: Interactive Use

If you run `gtdb-taxo` without arguments, it starts an interactive browser.
Use this to navigate a pointer up and down the tree, and examine ancestors,
siblings, or descendants in each context.

```
$ ./gtdb-taxo
Welcome to gtdb-taxo-browser.  Press h for help or q to quit.

(root) ? help
gtdb-taxo - Navigate the GTDB taxonomy

Commands:
-                ENTER key displays current pointer
- NUMBER         jump to taxon marked with NUMBER
- %TEXT          search for taxa whose name contains TEXT
- /REGEX         search for taxo whose name matches REGEX
- u(p)           move current taxon pointer to parent taxon
- p(arent)       show parent but do not move current pointer there
- a(ncestors)    show lineage of current taxon all the way up to root
- s(iblings)     show all siblings of the current taxon
- c(hildren)     show all children of the current taxon
- D(escendants)  show all descendants of the current taxon
- q(uit) or ^D   leave

(root) ? children
     2 domain   Archaea
     3 domain   Bacteria

(root) ? 3
     3 domain   Bacteria

(Bacteria) ? children
       ... omitted ...
     7 phylum   Acidobacteriota
     8 phylum   Actinobacteriota
    10 phylum   Aerophobota
       ... omitted ...
   152 phylum   WOR-3_A
   153 phylum   WOR-3_B
   154 phylum   Zixibacteria

(Bacteria) ? /Acinetobacter baumannii$
 12376 species  Acinetobacter baumannii

(Bacteria) ? 12376
 12376 species  Acinetobacter baumannii

(Acinetobacter baumannii) ? ancestors
     3 domain   Bacteria
   110 phylum   Proteobacteria
   272 class    Gammaproteobacteria
   998 order    Pseudomonadales
  2496 family   Moraxellaceae
  4162 genus    Acinetobacter
 12376 species  Acinetobacter baumannii

(Acinetobacter baumannii) ? 4162
  4162 genus    Acinetobacter

(Acinetobacter) ? siblings
  4260 genus    Agitococcus
  4319 genus    Alkanindiges
  7582 genus    Moraxella
  7583 genus    Moraxella_A
  7584 genus    Moraxella_C
  8168 genus    Perlucidibaca
  8434 genus    Psychrobacter
 10133 genus    UBA2031

(Acinetobacter) ? quit
Bye.
```

### Licence

gtdb-taxo - Command line GTDB genome taxonomy browser  
Copyright (C) 2019  Marco van Zwetselaar

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

