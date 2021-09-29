# purge-and-merge
A collection of puzzles and binaries used in the publication _Strengthening probabilistic graphical models: the purge-and-merge algorithm_

# Puzzle databases
- `sudoku-champagne-collection` is [sourced from Champagne's google drive](http://drive.google.com/drive/u/0/folders/0B5lH6mGXxWzXTDFRMnVTbGNlZU0) with a running discussion over at [enjoysudoku.com](http://forum.enjoysudoku.com/the-hardest-sudokus-new-thread-t6539.html). It contains 1000 Sudokus samples from the ph_1910 dataset. The full dataset uses the SER rating system and contains the most difficult Sudoku puzzles known to literature.
- `sudoku-sterten-collection` is [sources from magictour.free.fr](http://magictour.free.fr/top95). It contains 95 Sudokus of moderate difficulty.
- `sudoku-gordon-royle-sudoku-17-entries-collection` were originally available on [Royle's website](https://web.archive.org/web/20120722180233/http://mapleta.maths.uwa.edu.au/~gordon/sudokumin.php) and can be found in the [Tdoku dataset](https://github.com/t-dillon/tdoku/blob/master/data.zip). It contains 49151 Sudokus with 17-entries from Royle's 2010 dataset.
- `sumsudoku-krazydad-collection` is [sourced from krazydad.com](https://krazydad.com/play/killer). It contains 40000 Killer Sudoku puzzles, labelled according to five difficulty levels. Note that the purge-and-merge paper sampled the first 2000 from each difficulty level, totaling up to a 10000 puzzles.
- `sumsudoku-dailykillersudoku-collection` is [sourced from dailykillersudoku.com](www.dailykillersudoku.com). It contains 16615 Sumsudoku puzzles.
- `calcudoku-collection` is [sourced from menneske.no](https://menneske.no/calcudoku/9/eng/index.html). It contains 4597 Calcudoku puzzles.
- `kakuro-collection` is [sourced from en.grandgames.net](https://grandgames.net/kakuro/). It contains 6360 Kakuro puzzles.
- `fillapix-collection` is [sourced from en.grandgames.net](https://en.grandgames.net/mosaic). It contains 2340 Fill-a-pix puzzles.
- `gizmodo-10-hardest-puzzles` is [sourced from gizmodo.com](https://gizmodo.com/can-you-solve-the-10-hardest-logic-puzzles-ever-created-1064112665). It contains ten puzzles, one of each of the above-mentioned types .

# How to run purge-and-merge
The the purge-and-merge algorithm uses Stellenbosch University's emdw library, which is currently closed source. We are working on bringing the code into the open domain, but for now it is still tied to a licensing  agreement. All algorithms used in this paper is therefore shared in binary form and is made available as `bin.tar.gz` in [releases](https://github.com/heetbeet/purge-and-merge/releases/latest), tested on Ubuntu 20.04.3 LTS.

In order to run the binaries, first install the following dependencies:

    sudo apt-get install build-essential liblapack-dev libblas-dev libexpat1-dev zlib1g-dev

## run_purge_and_merge
`Usage run_purge_and_merge <puzzle-type> <input-puzzle> [<input-puzzle>...]`

⚠️Warning `run_purge_and_merge` works only with the `-(legacy-format)` filetype versions of Sumsudoku and Calcudoku⚠️ 

- `puzzle-type` can be one of: `sudoku`, `sumsudoku`, `calcudoku`, `kakuro` or `fillapix`. 
- `input-puzzle...`: a list of puzzle filepaths to solve.

For example: `./run_purge_and_merge calcudoku "calcudoku-collection/calcudoku-menneske.no-10.txt"`

## run_puzzle_to_uai
`Usage run_puzzle_to_uai <puzzle-type> <input-puzzle> <output-file>`

⚠️Warning `run_puzzle_to_uai` works only with the default filetype versions of Sumsudoku and Calcudoku⚠️ 

- `puzzle-type` can be one of: `sudoku`, `sumsudoku`, `calcudoku`, `kakuro` or `fillapix`. 
- `input-puzzle...`: Filepath to a puzzle.
- `output-file`: Filepath to output file

For example `./run_puzzle_to_uai calcudoku "calcudoku-collection-(legacy-format)/calcudoku-menneske.no-10.txt output.uai"`

This will convert any puzzle in this database to a `.uai` file that can be consumed by [ACE](http://reasoning.cs.ucla.edu/ace/).

## run_ace_on_uai
`Usage run_ace_on_uai <input.uai>`

For example `./run_ace_on_uai output.uai`

This is a small wrapper over [ACE](http://reasoning.cs.ucla.edu/ace/) to load a `.uai` file created from one of the puzzles, compile the puzzle into a circuit, and query all the unknown variables in that circuit. 
