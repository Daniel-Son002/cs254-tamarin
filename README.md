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

# Tamarin Introduction

Tamarin models use three main ingredients:

- Rules
- Facts
- Terms

A rule in Tamarin needs a unique name and three parts: premise (left-hand side), transition (action facts), and conclusion (right-hand side). Rules will follow the general form:

```tamarin
rule Name:
  [ consumed facts ]
  --[ action facts ]->
  [ output facts ]
```

Note that if the rule does not have any action facts, then the middl brackets can be omitted.

Facts are of the form `F(t_1, ..., t_n)` for a fact `F` and n terms. Some built in facts are:
- `In`
- `Out`
- `Fr`

These facts are <ins>linear</ins> which means they can be produced by rules and also consumed by rules. Linear facts may appear in one state but not the next. Alternatively, <ins>persistent</ins> facts are never removed from the state and are denoted by prefixing the fact with a bang `!`.

More information on Tamarin syntax can be found in the cheat sheet.