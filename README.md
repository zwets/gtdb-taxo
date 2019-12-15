# gtdb-taxo

_Command line GTDB taxonomy browser_


## Introduction

`gtdb-taxo` is a command line utility to query the GTDB Genome Taxonomy.
It can look up taxons by name, regex, representative genome, and so on.

The program is based on, and operates identically to, [taxo](https://github.com/zwets/taxo)
which does the same for the NCBI/ENA taxonomy.

`gtdb-taxo` can also operate interactively (`gtdb-taxo-browser`), allowing
you to navigate up and down the taxonomy tree from the command line.

`gtdb-taxo` and `gtdb-taxo-browser` use `gtdb-taxo-db` as their back-end.
`gtdb-taxo-db` imports the GTDB taxonomy and offers a SQL interface to
query it.

`gtdb-taxo` is lightweight and requires no special installation.

Home: <https://github.com/zwets/gtdb-taxo>


## Installation

* Prerequisites

  `gtdb-taxo` requires the `sqlite3` and `GNU awk` programs.  These are often
  already present on your system, or else easily installable.  On Debian/Ubuntu:

      sudo apt-get install sqlite3 gawk

  If you want to search using regular expressions, then install the PCRE
  extension for `sqlite3`:

      sudo apt-get install sqlite3-pcre gawk

* Clone the repository

      git clone https://github.com/zwets/gtdb-taxo.git
      cd gtdb-taxo
      ./gtdb-taxo --help

* Import the taxonomy database

  If you have installed [GTDBTk](https://github.com/Ecogenomics/GTDBTk), then
  `GTDBTK_DATA_PATH` should point to its data directory, and the file to import
  is `$GTDBTK_DATA_PATH/taxonomy/gtdb_taxonomy.tsv`:

      gtdb-taxo-db --import "$GTDBTK_DATA_PATH/taxonomy/gtdb_taxonomy.tsv"

* [Optional] Add `gtdb-taxo` to your path

  No further installation is needed.  For convenience you could add `gtdb-taxo`'s
  directory to your `PATH`, or symlink the `gtdb-taxo` script in your `~/bin` or
  `~/.local/bin` directory, depending on your shell.


## Usage

The `gtdb-taxo`, `gtdb-taxo-browser`, and `gtdb-taxo-db` commands are self-contained.
Invoke with `--help` to see usage instructions.  Below are some examples to get you going.

### Examples: Command-line Use

Searching on taxonomic name

@@@TODO@@@


### Examples: Interactive Use

@@@TODO@@@


#### Licence

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

