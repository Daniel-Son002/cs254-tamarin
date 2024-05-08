# Tamarin Cheat Sheet

# Rules

## Rule Structure
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

Note that if a rule does not have any action facts then the middle brackets can be omitted.

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
    - This fact must be used when generating fresh (random) values, and can only occur on the left-hand side of a rewrite rule, where its argument is the fresh term. Tamarin’s underlying execution model has a built-in rule for generating instances of Fr(x) facts, and also ensures that each instance produces a term (instantiating x) that is different from all others.
- `pk(x)` - The public key corresponding to the private key `x`.

These facts are <ins>linear</ins> which means they can be produced by rules and also consumed by rules. Linear facts may appear in one state but not the next. Alternatively, <ins>persistent</ins> facts are never removed from the state and are denoted by prefixing the fact with a bang `!`.

## Rule Example

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

*Note*: Variable notation is also used in writing lemmas.

# Lemmas

Lemmas are used to specify a property about a protocol to be verified. Equivalent lemmas can often be written in multiple different ways. 

The following is an example of a lemma that specifies that the fresh value `~n` is distinct in all applications in the function `F`:
```tamarin
lemma distinct_nonce:
  "All n #i #j. F(n)@i & F(n)&j ==> #i=#j"
```

The following are keywords/symbols in lemmas:
- `All` for universal quantifiers
- `Ex` for existential quantifiers
- `==>` for implication
- `&` for conjunction
- `|` for disjunction
- `not` for negation
- `f @ i` for action constraint
- `i < j` for temporal ordering
- `#i = #j` for equality between temporal variables `#i` and `#j`
- `x = y` for equality between message variables `x` and `y`
- `Pred(t_1, ..., t_n)` for instantiating a predicate for the terms `t_1` to `t_n`

Tamarin's built-in deduction rule:
```tamarin
rule isend:
   [ !KU(x) ]
 --[  K(x)  ]-->
   [ In(x)  ]
```
allows us to notate the Dolev-Yao adversary knowledge `K(x)`. This specifies an adversary's knowledge of some information `x`. For example, consider the following lemma:

```tamarin
lemma secrecy:
  "All x #i.
    Secret(x) @ #i ==> not (Ex #j. K(x) @ #j)"
```

In this lemma, we have a `Secrect(x)` action fact where information `x` is a secret. Then the lemma states, for all `x` information and time `#i`, `Secret(x) @ #i` implies that there does not exist a time `#j` where the adversary knows information `x` at time `#j`.


# Builtins
Tamarin has some built-in cryptographic functionality to help model protocols. Their behavior is defined below.

## Symmetric Encryption
`sdec(senc(m, k), k) = m`

## Diffie-Hellman:
```tamarin
(x^y)^z = x^(y*z)
x^1 = 1
x*y = y*x
(x*y)*z = x*(y*z)
x*1 = x
x*inv(x) = 1
```

## Asymmetric Encryption
`adec(aenc(m, pk(sk)), sk) = m`
