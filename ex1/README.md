# Example 1

The goal of example 1 is to get you familiar with Tamarin syntax and how to perform specific actions. In this exercise, we will model a participant communicating by generating a secret key and sending a symmetrically encrypted message. Open `exSenc.spthy` and follow the instructions inside.

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

## KeyGen

`KeyGen` allows a participant `A` to generate a fresh secret key and store it using the fact `!LongTermKey`.

### Premise

In the premise, we want to generate a unguessable/fresh value `k`. How might we do this? Hint: Check the cheatsheet for any relevant predefined rules that may be useful!
<details>
  <summary>Expected premise</summary>
  [ Fr(~k) ]
</details>


### Conclusion
In the conclustion, we want to save the unguessable/fresh value `k` that we generated in the premise and denote that it is participant `A`'s key. Again, check the cheatsheet for any relevant predefined rules that may be useful!
<details>
  <summary>Expected conclusion</summary>
  [ !LongTermKey($A, ~k) ]
</details>

## SendMsg

`SendMsg` allows a participant `A` to send a message `~msg`, symmetrically encrypted under the key generated using KeyGen. 

### Premise
In the premise, we want to use the previously generated key from `KeyGen`.
<details>
  <summary>Expected premise</summary>
  [ !LongTermKey($A, ~k) ]
</details>

### Action Fact
This part is already given in the stub code. The action fact shows that participant `A` sends the message `~msg`.

### Conclustion
In the conclusion, we want to output the key `~k`. 
<details>
  <summary>Expected conclustion</summary>
  [ Out(~k) ]
</details>



