# Tamarin Cheat Sheet

## Rules
A basic rule will follow the following format:

```tamarin
rule RuleName:
    let t3 = t2 in // optional
    [ F1(t1, t2) ] // premise
    --[ L(t1) ]->
    [ F2(t3) ] // conclustion
```

- `F1`, `F2` are facts
- `L` is an action term
- `t1`, `t2`, `t3` are terms


There are some facts that are reserved that you will often see in Tamarin syntax:
- `Out(m)` - Send `m` (this fact will only appear in the conclusion)
- `In(m)` - Receive `m` (this fact will only appear in the premise)
- `Fr(x)` - Generate unguessable/fresh value `x` (this fact will only appear in the premise)


## Diffie-Hellman:
```tamarin
(x^y)^z = x^(y*z)
x^1 = 1
x*y = y*x
(x*y)*z = x*(y*z)
x*1 = x
x*inv(x) = 1
```