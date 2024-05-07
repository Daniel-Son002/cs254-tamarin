# Tamarin Cheat Sheet

```tamarin
rule Register_pk:
    [ Fr(~ltk) ]
  -->
    [ !Ltk($A, ~ltk), !Pk($A, pk(~ltk)) ]
```

The rule can be read as follows:
First, generate a fresh name `~ltk` (of sort fresh), which is the new private key, and non-deterministically choose a public name `A`, for the agent for whom we are generating the key-pair. Afterward, generate the fact `!Ltk($A, ~ltk)` (the exclamation mark `!` denotes that the fact is persistent, i.e., it can be consumed arbitrarily often), which denotes the association between agent `A` and its private key `~ltk`, and generate the fact `!Pk($A, pk(~ltk))`, which associates agent `A` and its public key `pk(~ltk)`.

## Variables
- `~x` denotes `x:fresh` (fresh variable)
- `$x` denotes `x:pub` (public variable)
- `%x` denotes `x:nat`
- `#i` denotes `i:temporal`
- `m` denotes `m:msg`

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
    - This fact is used to model a party sending a message to the untrusted network that is controlled by a Dolev-Yao adversary, and can only occur on the right-hand side of a rewrite rule.
- `In(m)` - Receive `m` (this fact will only appear in the premise)
    - This fact is used to model a party receiving a message from the untrusted network that is controlled by a Dolev-Yao adversary, and can only occur on the left-hand side of a rewrite rule.
- `Fr(x)` - Generate unguessable/fresh value `x` (this fact will only appear in the premise)
    -This fact must be used when generating fresh (random) values, and can only occur on the left-hand side of a rewrite rule, where its argument is the fresh term. Tamarin’s underlying execution model has a built-in rule for generating instances of Fr(x) facts, and also ensures that each instance produces a term (instantiating x) that is different from all others.
- `pk(x)` - The public key corresponding to the private key `x`.


We denote persistent facts by prefixing them with a bang (!), otherwise facts are linear.


## Diffie-Hellman:
```tamarin
(x^y)^z = x^(y*z)
x^1 = 1
x*y = y*x
(x*y)*z = x*(y*z)
x*1 = x
x*inv(x) = 1
```


## Lemma Writing and Syntax

Lemmas are used to specify a property about a protocol to be verified. Equivalent lemmas can often be written in multiple different ways. 

The following is an example of a lemma that specifies that the fresh value `~n` is distinct in all applications in the function `F`:
```tamarin
lemma distinct_nonce:
  "All n #i #j. F(n)@i & F(n)&j ==> #i=#j"
```