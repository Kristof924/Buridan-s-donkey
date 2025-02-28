# AI Decision Making System

This repository contains an AI decision-making system that addresses the **Buridan's Ass
Problem** , **Deterministic Decision Making** , and introduces strategies for breaking ties
when decisions are not clear-cut. This system demonstrates various ways to implement
decision-making in AI using determinism, randomness, bias, and probabilistic
approaches.

## Table of Contents

- Buridan's Ass Problem
- Deterministic Decision Making
- Impossibility of Choice
- Possible Decision Strategies
    o Randomness
    o Bias
    o Softmax
- Summary

## Buridan's Ass Problem

**Buridan's Ass** is a philosophical paradox that describes a donkey placed exactly halfway
between a pile of hay and a bucket of water. The donkey is equally thirsty and hungry and
has no preference for one over the other. According to the paradox, the donkey is unable to
decide between the two options, and as a result, it starves to death.

This paradox highlights the **Impossibility of Choice** when two alternatives are equally
attractive or when no decision-making criteria are available to break the tie. It forms the
foundation of our decision-making system.

In formal decision-making systems, this paradox is translated into situations where the
system faces two equally desirable options and no external factor or mechanism is
available to decide between them. This results in the system being unable to make a
choice, thus encountering a deadlock.


## Deterministic Decision Making

**Deterministic Decision Making** refers to systems in which decisions are made based on
fixed, predefined rules without randomness or ambiguity. This guarantees that for any
given input, the outcome is always predictable.

In our decision-making system, this is implemented with the following function:

```
Definition AI_decision (x y : nat) : AI_Choice :=
if Nat.ltb x y then First_Choice
else if Nat.ltb y x then Second_Choice
else No_Choice.
```

In this implementation:

- If x < y, the system chooses First_Choice.
- If y < x, it chooses Second_Choice.
- If x = y, the system cannot decide and returns No_Choice.

This approach ensures that the system's decision is deterministic and follows the
comparisons between x and y.

## Impossibility of Choice

In some cases, such as when x = y, the system cannot make a decision. This is the
**Impossibility of Choice** , where the system faces a tie and cannot break it with the existing
criteria. This is exactly what happens in **Buridan's Ass** , where the donkey cannot choose
between equally attractive options, leading to inaction.

In AI systems, this problem occurs when two options are equally valid, and no additional
mechanism exists to break the tie. This is where the **Impossibility of Choice** emerges, and
to resolve this, we must introduce other decision-making mechanisms.


## Possible Decision Strategies

To handle cases where the system cannot decide between two equally valid options,
several decision strategies can be introduced. These strategies add mechanisms to break
ties and ensure that the system always makes a decision.

### Randomness

One way to break the tie is by introducing randomness into the decision-making process. If
both options are equally valid, the system can randomly select one. Here's how it's
implemented:

```
Parameter random_choice : AI_Choice.
Definition AI_decision_with_randomness (x y : nat) : AI_Choice :=
if x <? y then First_Choice
else if y <? x then Second_Choice
else random_choice.
```

In this approach:

- If x < y, the system chooses First_Choice.
- If y < x, it chooses Second_Choice.
- If x = y, it chooses a random option (random_choice).

### Bias

Another approach is to apply a **bias** to the decision-making process. The bias is an external
factor that can be used when both options are equally attractive. Here's the
implementation:

```
Definition AI_decision_with_bias (x y : nat) (bias : AI_Choice) :
AI_Choice :=
if x <? y then First_Choice
else if y <? x then Second_Choice
```

else bias.

With this approach:

- If x < y, the system chooses First_Choice.
- If y < x, it chooses Second_Choice.
- If x = y, it applies the given bias to make the decision.

### Softmax

For a more probabilistic approach, we can use the **softmax** function to make decisions.
This introduces a probabilistic aspect to the decision, which can help avoid deterministic
deadlocks. Here’s how we can implement it:

```
Parameter softmax : nat -> nat -> AI_Choice.
Definition AI_decision_with_softmax (x y : nat) : AI_Choice :=
if x <? y then First_Choice
else if y <? x then Second_Choice
else softmax x y.
```

In this case:

- If x < y, the system chooses First_Choice.
- If y < x, it chooses Second_Choice.
- If x = y, it uses the **softmax** function to probabilistically decide between the two
    options.

### Summary

- **Buridan's Ass Problem** demonstrates the difficulty of decision-making when two
    options are equally attractive, leading to the **Impossibility of Choice**.
- **Deterministic Decision Making** ensures predictable outcomes based on fixed
    criteria, but it can result in deadlocks when two options are equally valid.
- To resolve the **Impossibility of Choice** , we introduce several decision strategies:
    o **Randomness** introduces a random decision when a tie occurs.
    o **Bias** applies external preferences when both options are equal.


```
o Softmax adds probabilistic decision-making to resolve ties.
```
These strategies ensure that the decision-making system can always make a choice, even
in situations where the options are equally valid.

## Usage

To use the AI decision-making system, you can call the relevant function based on your
preference for deterministic or probabilistic decision-making:

1. **Deterministic Decision** : Use AI_decision.
2. **Random Choice** : Use AI_decision_with_randomness.
3. **Bias-Based Decision** : Use AI_decision_with_bias.
4. **Softmax Decision** : Use AI_decision_with_softmax.

For each of these, you provide two natural numbers x and y as inputs, and the system will
return an AI_Choice (either First_Choice, Second_Choice, or No_Choice).

## License

This project is licensed under the MIT License - see the LICENSE.md file for details.
