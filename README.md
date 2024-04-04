# Tamarin Problem Set

This repository includes tutorials and exercises to help you learn Tamarin.

## Tamarin Installation

First, begin by following the [installation guide](https://tamarin-prover.com/manual/master/book/002_installation.html)
Alternatively, you can run `brew install tamarin-prover/tap/tamarin-prover` to brew install. Install [brew](https://brew.sh/)
<!-- Additionally, install graphviz: `sudo apt install graphviz`, install [Maude](https://github.com/SRI-CSL/Maude/releases/tag/Maude3.3.1) -->

## Using Tamarin

In order to launch tamarin, use the command 

```sh
tamarin-prover interactive {folder_name}/
```

If there are no errors, navigate to http://127.0.0.1:3001 to see the GUI. Note that Tamarin does not auto update the files, you must save and restart after changing a `*.spthy` file.