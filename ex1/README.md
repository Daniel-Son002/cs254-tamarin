# Exercise 1

The goal of exercise 1 is to get you familiar with Tamarin syntax and how to perform specific actions. In this exercise, we will model a participant communicating by generating a secret key and sending a symmetrically encrypted message. Open `exSenc.spthy` and follow the instructions inside.

To launch Tamarin and verify the lemmas, run `tamarin-prover interactive ex1/`


## Tamarin Syntax

The following may be useful information to understand when reading Tamarin code.

```tamarin
rule RuleName:
  let t3 = t2 in  // optional
  [ F1(t1, t2) ]  // premise (multiset/list of facts)
  --[ L(t1) ]->
  [ F2(t3) ]      // conclusion (multiset/list of facts)
```

- `F1`, `F2` are *facts*
- `L` is an *action fact*
- `t1`, `t2`, `t3` are *terms*

You can find a more detailed overview in the cheatsheet. 

## KeyGen

`KeyGen` allows a participant `A` to generate a fresh secret key and store it using the fact `!LongTermKey`.

### Premise

In the premise, we want to generate a unguessable/fresh value `k`. How might we do this? Hint: Check the cheatsheet for any relevant predefined rules that may be useful!
<details>
  <summary>Expected premise</summary>
  `[ Fr(~k) ]`
</details>


### Conclusion
In the conclustion, we want to save the unguessable/fresh value `k` that we generated in the premise and denote that it is participant `A`'s key. Again, check the cheatsheet for any relevant predefined rules that may be useful!
<details>
  <summary>Expected conclusion</summary>
  `[ !LongTermKey($A, ~k) ]`
</details>

## SendMsg

`SendMsg` allows a participant `A` to send a message `~msg`, symmetrically encrypted under the key generated using KeyGen. 

### Premise
In the premise, we want to use the previously generated key from `KeyGen`.
<details>
  <summary>Expected premise</summary>
  `[ !LongTermKey($A, ~k) ]`
</details>

### Action Fact
This part is already given in the stub code. The action fact shows that participant `A` sends the message `~msg`.

### Conclustion
In the conclusion, we want to output the key `~k`. 
<details>
  <summary>Expected conclustion</summary>
  `[ Out(~k) ]`
</details>


## Lemma Explanation

At the end of Tamarin protocols we need a lemmas to specify properties about a protocol to be verified. Lemma names are prefixed by the keyword `lemma`.

```tamarin
lemma Secrecy:
  "All p m #t. MessageWasSentBy(p, m) @ #t ==> not Ex #x. K(m) @ #x"
```

The above is the Secrecy lemma that is defined for you in this exercise. `lemma Secrecy` check that for all participants `p`, participant `p` sends a message `m` at time `#t` defined by `All p m #t. MessageWasSentBy(p, m) @ #t`. The `==>` is a logical operand that is equivalent to `p | not q` where the left hand side of the `==>` is `p` and the right hand side is `q`. Thus the right hand side is showing that for some time points `#x`, `K(m)` does not hold.


