# Exercise 3

The goal of exercise 3 is to verify a more complex protocol with more sophisticated lemmas, including modeling man-in-the-middle attacks. We focus on the Needham-Schroeder protocol, a method to provide mutual authentication between two parties that was discussed in class. In particular, you will first show that the naive Needham-Schroeder protocol is insecure, and then show that the fix proposed by Lowe patches this insecurity. Open `NSInecure.spthy` and follow the instructions inside.

```mermaid
sequenceDiagram
  Note over Alice: Generate nonce nA
  Alice->>Bob: (Alice, nA)pk(B)
  Note over Bob: Decrypt nA
  Note over Bob: Generate nonce nB
  Bob->>Alice: (nA, nB)pk(A)
  Note over Alice: Decrypt nB
  Alice->>Bob: (nB)pk(B)
```

## Built-ins and Public Key Infrastructure

The begining of the file contains some initial scaffolding, importing the built-in `asymmetric-encryption` functions and defining basic rules to model the public key incfrastructure. Make sure you understand these before moving forward; while the `RegLtk` rule should be familiar by now, it differs slightly for asymmetric encryption, and `GetPk` and `RevLtk` are new. 

## Defining the Protocol

Next, fill in the details of rules `A1`, `B1`, `A2` and `B2`. 

## Defining the Lemmas

## Making Needham-Schroeder Secure

Finally, let us verify that the fix proposed by Lowe makes the protocol secure against man-in-the-middle attacks! Open `NSSecure.spthy`, and start by copying the code from `NSInecure.spthy`. Next, make the necessary changes to the rules. 

```mermaid
sequenceDiagram
  Note over Alice: Generate nonce nA
  Alice->>Bob: (Alice, nA)pk(B)
  Note over Bob: Decrypt nA
  Note over Bob: Generate nonce nB
  Bob->>Alice: (Bob, nA, nB)pk(A)
  Note over Alice: Decrypt nB
  Alice->>Bob: (nB)pk(B)
```

Although the change is simple, you'll have to modify more than one rule! If done correctly, all the lemmas should now pass.