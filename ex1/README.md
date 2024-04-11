# Example 1

The goal of example 1 is to get you familiar with Tamarin syntax and how to perform specific actions. Open `exSenc.spthy` and follow the instructions inside.

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