# Example 1

The goal of example 1 is to get you familiar with Tamarin syntax and how to perform specific actions. Open `exSenc.spthy` and follow the instructions inside.


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

KeyGen allows a participant `A` to generate a fresh secret key and store it using the fact `!LongTermKey`.

### Premise

In the premise, we want to generate a unguessable/fresh value `k`. How might we do this? Hint: Check the cheatsheet for any relevant predefined rules that may be useful!
<details>
  <summary>Expected premise</summary>
  [ Fr(~k) ]
</details>


### Conclusion


