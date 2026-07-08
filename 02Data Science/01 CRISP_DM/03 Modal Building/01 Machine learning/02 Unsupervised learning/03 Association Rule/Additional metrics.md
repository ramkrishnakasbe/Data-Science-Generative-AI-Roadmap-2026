# Leverage

## Definition

**Leverage** measures how much more frequently two items occur together than would be expected if they were statistically independent.

Unlike **Lift**, Leverage measures the **difference** between the observed co-occurrence and the expected co-occurrence.

---

# Formula

\[
\text{Leverage}(A \rightarrow B)
=
Support(A \cap B)
-
Support(A)\times Support(B)
\]

or

```text
Leverage(A → B)

=

Support(A ∩ B)

−

Support(A) × Support(B)
```

---

# Intuition

Suppose

- Bread appears in **60%** of transactions.
- Butter appears in **50%** of transactions.

If they were completely independent, we would expect them to occur together

```text
0.60 × 0.50

=

0.30

=

30%
```

Now suppose they actually occur together in

```text
45%
```

Then

```text
Leverage

=

0.45

−

0.30

=

0.15
```

This means the pair appears **15% more often** than expected by chance.

---

# Example

Suppose

| Item | Value |
|------|------|
| Total Transactions | 100 |
| Bread | 60 |
| Butter | 50 |
| Bread & Butter | 45 |

### Step 1

Support(Bread)

```text
60/100

=

0.60
```

---

### Step 2

Support(Butter)

```text
50/100

=

0.50
```

---

### Step 3

Support(Bread ∩ Butter)

```text
45/100

=

0.45
```

---

### Step 4

Compute Leverage

```text
0.45

−

(0.60 × 0.50)

=

0.45

−

0.30

=

0.15
```

---

# Interpretation

### Leverage = 0

Items are independent.

---

### Leverage > 0

Positive association.

Items occur together more often than expected.

---

### Leverage < 0

Negative association.

Items occur together less often than expected.

---

# Range

```text
-1

to

+1
```

---

# Advantages

- Easy to interpret.
- Shows actual improvement over random chance.
- Useful for comparing association rules.

---

# Disadvantages

- Depends on dataset size.
- Small values may still represent useful rules.
- Less commonly used than Lift.

---

# Conviction

## Definition

Conviction measures **how strongly the occurrence of A implies the occurrence of B**.

Unlike Confidence, Conviction also considers **how often the rule makes incorrect predictions**.

Conviction is especially useful for identifying strong implication rules.

---

# Formula

\[
Conviction(A \rightarrow B)
=
\frac{1-Support(B)}
{1-Confidence(A \rightarrow B)}
\]

or

```text
Conviction(A → B)

=

(1 − Support(B))

----------------------

(1 − Confidence(A→B))
```

---

# Intuition

Suppose

Whenever customers buy

```text
Laptop
```

they almost always buy

```text
Laptop Bag
```

Confidence may be high.

Conviction checks

**"How often is this rule wrong?"**

If the rule is rarely wrong,

Conviction becomes very large.

---

# Example

Suppose

Support(Butter)

```text
0.50
```

Confidence(Bread → Butter)

```text
0.80
```

Compute

Numerator

```text
1 − 0.50

=

0.50
```

Denominator

```text
1 − 0.80

=

0.20
```

Conviction

```text
0.50

/

0.20

=

2.5
```

---

# Interpretation

### Conviction = 1

No implication.

A and B are independent.

---

### Conviction > 1

Positive implication.

Higher values indicate a stronger rule.

---

### Conviction → ∞

Perfect rule.

Whenever A occurs,

B always occurs.

Example

```
Confidence = 1
```

Denominator

```text
1 − 1

=

0
```

Therefore

```text
Conviction

=

∞
```

---

### Conviction < 1

Negative association.

The rule is worse than random prediction.

---

# Example Comparison

Suppose

| Metric | Value |
|---------|------|
| Support | 0.45 |
| Confidence | 0.75 |
| Lift | 1.50 |
| Leverage | 0.15 |
| Conviction | 2.00 |

Interpretation

- **Support (0.45):** The itemset appears in **45%** of all transactions.
- **Confidence (0.75):** If A is purchased, there is a **75%** chance B is also purchased.
- **Lift (1.50):** Customers are **1.5 times** more likely to buy B when they buy A compared to random chance.
- **Leverage (0.15):** The pair occurs **15% more often** than expected if A and B were independent.
- **Conviction (2.00):** The rule **A → B** is about **2 times more reliable** than random prediction.

---

# Difference Between Lift, Leverage and Conviction

| Metric | Measures | Best Interpretation |
|---------|----------|--------------------|
| **Lift** | Relative increase over random chance | Strength of association |
| **Leverage** | Absolute increase over random chance | Additional co-occurrence due to association |
| **Conviction** | Reliability of implication | How strongly A implies B |

---

# Python Example

```python
from mlxtend.frequent_patterns import association_rules

rules = association_rules(
    frequent_itemsets,
    metric="confidence",
    min_threshold=0.6
)

print(rules[[
    'support',
    'confidence',
    'lift',
    'leverage',
    'conviction'
]])
```

---

# Interview Questions

### 1. What is Leverage?

Leverage measures the **difference between the observed support of A and B occurring together and the support expected if they were independent**.

---

### 2. What does a Leverage value of 0 indicate?

A leverage of **0** means there is **no association** between A and B; they occur together exactly as expected by chance.

---

### 3. What is Conviction?

Conviction measures the **strength of implication** of the rule **A → B** by considering how often the rule makes incorrect predictions.

---

### 4. What does Conviction = 1 mean?

A conviction of **1** indicates **no implication**; A and B are independent.

---

### 5. When is Conviction infinite?

Conviction approaches **∞** when the confidence is **1**, meaning **every time A occurs, B also occurs** (a perfect implication).
