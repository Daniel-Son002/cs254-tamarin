# Tamarin Problem Set

This repository includes tutorials and exercises to help you learn Tamarin. The Tamarin prover is a powerful tool for modeling and analyzing security protocols. In the `*spthy` files, we model the actions taken by agents and specify the desired properties of each set of rules. The benefit of the Tamarin prover is that it allows us to automatically construct proofs of correctness where an arbitrary number of protocol instances are interleaved in parallel. The link to find more information on Tamarin is available on the Tamarin website [here](https://tamarin-prover.com/manual/master/book/003_example.html).

## Tamarin Installation

First, begin by following the [installation guide](https://tamarin-prover.com/manual/master/book/002_installation.html). Alternatively, you can run `brew install tamarin-prover/tap/tamarin-prover` to install with [brew](https://brew.sh/).
<!-- Additionally, install graphviz: `sudo apt install graphviz`, install [Maude](https://github.com/SRI-CSL/Maude/releases/tag/Maude3.3.1) -->

## Using Tamarin

In order to launch tamarin, use the command 

```sh
tamarin-prover interactive {folder_name}/
```

If there are no errors, navigate to http://127.0.0.1:3001 to see the GUI. Note that Tamarin does not auto update the files, you must save and restart after changing a `*.spthy` file.

## Using the Tamarin solver GUI

Once you have launched your desired Tamarin folder, you will navigate to http://127.0.0.1:3001 to see the GUI. Once there, navigate to the theory name of the exercise to start verifying your lemmas!

In the GUI you will see your lemmas followed by `by sorry` in the following format:

```tamarin
lemma Secrecy:
  all-traces
  "∀ p m #t.
         (MessageWasSentBy( p, m ) @ #t) ⇒ (¬(∃ #x. K( m ) @ #x))"
by sorry
```

`sorry` is clickable and will be how you autoprove lemmas using the Tamarin solver! Try completing exercise 1 and verify its lemma.

# Problem Set Overview

## Exercise 1
In exercise 1, you will implement symmetrically encrypted messaging where a participant `A` sends a symmetrically encrypted message. This utilizes the *built-in*, `symmetric-encryption`. 

## Exercise 2
In exercise 2, you will implement the Diffie-Hellman protocol that we discussed in class. More specifically, you will implement the following rules:
- `Ltk` where we generate a long term key under the Diffie-Hellman protocol
- `A_Init` where a participant `A` sends a request to participant `B`
- `B_Init` where a participant `B` acknowledges participant `A`'s request
- `A_SendMsg` where a participant `A` uses participant `B`'s acknowledgement to send a message

## Exercise 3
In exercise 3, you will implement the Needham-Schroeder protocol that we discussed in class. This exercise has two parts. In the first part, you will implement the version that is *not* secure in the man-in-the-middle attack, and verify that it is insecure. The next part will be to make the Needham-Schroeder protocol secure using the fix proposed by Lowe. This problem is more open-ended than the previous two exercises and involves implementing both rules and lemmas.
