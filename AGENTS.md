# AGENTS.md

This file provides guidance when working with code in this repository.

## Project Overview

This is a **tutoring workspace** for Diana, a BSc Psychology student at the University of Bern. The workspace contains materials for statistics tutoring sessions covering probability theory, distributions, and experimental design.

**Student:** Diana, BSc Psychology
**Course context:** Statistics for Psychology students
**Language:** German (all materials, questions, and explanations)
**Textbook reference:** Eid, M., Gollwitzer, M., & Schmitt, M. (2017). Statistik und Forschungsmethoden (5. Aufl.). Weinheim/Basel: Beltz.

## Directory Structure

```
/home/andrew/Nextcloud/Statistik/Diana/
├── Lektion 1/                          # Lesson 1 materials
│   ├── IMG_*.jpg                       # Photos of Diana's handwritten work
│   ├── Tutoring_Guide_Lektion1.md      # Assessment and explanations (markdown)
│   ├── Tutoring_Guide_Lektion1.qmd     # Assessment with executable R code (Quarto)
│   ├── Tutoring_Guide_Lektion1.html    # Rendered HTML output
│   └── Prüfung.png                     # Exam requirements image
└── probelektion/                       # Initial trial lesson materials
    └── PHOTO-*.jpg                     # Photos from initial session
```

## Tutoring Workflow

### 1. Analyzing Student Work

Student work arrives as **photos** (IMG_*.jpg or PHOTO-*.jpg). The typical workflow:

1. Read photos to understand Diana's solutions
2. Identify correct answers, errors, and misconceptions
3. Create detailed assessment documents

### 2. Creating Tutoring Materials

**Use Quarto documents (.qmd)** for all new tutoring materials. Quarto allows:
- Executable R code chunks for statistical calculations
- Professional HTML/PDF output
- Reproducible examples Diana can run herself

**Document naming convention:**
```
Tutoring_Guide_Lektion{N}.qmd
```

### 3. Annotating Student Work with Xournal++

For direct annotation on student work photos, use Xournal++:

**Convert images to PDF and open in Xournal++:**
```bash
# From within a lesson directory (e.g., Lektion 1/)
magick IMG_*.jpg Diana_Exercises_Lektion{N}.pdf
xournalpp Diana_Exercises_Lektion{N}.pdf &
```

**Benefits:**
- Annotate directly on Diana's handwritten work
- Add corrections, arrows, and explanatory notes visually
- Save annotations as .xopp files (editable) or export to PDF
- Useful for quick feedback before creating full Quarto assessment

**Workflow:**
1. Convert all exercise images to a single PDF
2. Open in Xournal++ for annotation
3. Use pen tool for corrections, text tool for explanations
4. Export annotated PDF or save as .xopp for later editing
5. Use insights to create comprehensive Quarto tutoring guide

### 4. Markdown Formatting Rules

**CRITICAL: Always include a blank line before markdown lists!**

Markdown lists (lines starting with `-`, `*`, or numbers) MUST be preceded by a blank line, otherwise they won't render correctly.

**Bad:**
```markdown
**Teaching Tips:**
- Point 1
- Point 2
```

**Good:**
```markdown
**Teaching Tips:**

- Point 1
- Point 2
```

**Note:** Consecutive list items don't need blank lines between them - only the first list item needs a blank line before it.

### 5. Document Structure for Tutoring Guides

Each tutoring guide should include:

```markdown
---
title: "Tutoring Guide - Lektion N: [Topic]"
author: "BSc Psychology - Diana"
format:
  html:
    toc: true
    toc-depth: 3
    code-fold: true
    code-summary: "Show R code"
    theme: cosmo
    embed-resources: true
execute:
  warning: false
  message: false
---

## Exam Requirements Context
[List what Diana needs to master for exams]

## Aufgabe N: [Problem Title]

**Frage:** [Original question in German]

### Diana's Answer:
[What Diana wrote/calculated]

### Correct Answer:
[Correct solution with R code if applicable]

```{r}
# R calculations here
```

### Assessment:
**Status:** ✓ CORRECT / ✗ INCORRECT / Partially correct

**What went wrong/right:**
[Detailed explanation]

**Misconception:**
[Common error pattern, if applicable]

**Key Learning Points:**
1. [Concept explanation]
2. [Formula or method]
3. [Practical application]

---

## Summary of Diana's Performance

### Strengths:
[What Diana does well]

### Areas for Improvement:
[Specific weaknesses with practice recommendations]
```

## 6. Rendering Quarto Documents

```bash
# Render to HTML (default, embedded resources)
quarto render Tutoring_Guide_Lektion1.qmd

# Render to PDF
quarto render Tutoring_Guide_Lektion1.qmd --to pdf

# Preview with live reload
quarto preview Tutoring_Guide_Lektion1.qmd
```

## Topics Covered

### Lektion 1: Wahrscheinlichkeitstheorie und Verteilungen

Core topics from Lektion 1:

1. **Binomial Distribution** (Binomialverteilung)
   - Expected value: E(X) = n · π
   - Variance: Var(X) = n · π · (1 - π)

2. **Discrete Probability Distributions**
   - E(X) = Σ [X · P(X)]
   - Var(X) = Σ [(X - μ)² · P(X)] or E(X²) - [E(X)]²

3. **Normal Distribution** (Normalverteilung)
   - Parameters: μ (mean) and σ (standard deviation)
   - Empirical rule: 68-95-99.7 rule
   - Z-scores: z = (X - μ) / σ

4. **Compound Probability**
   - Multiplication rule: P(A AND B) = P(A) × P(B|A)
   - Sequential events and conditional probability

5. **Experimental Design**
   - Counting principles
   - Factorial designs (main effects and interactions)

6. **Expected Value Applications**
   - Decision-making based on E(X)
   - Games and risk assessment

## Key R Patterns for Statistics Tutoring

### R Coding Style

**Always use modern tidyverse R code:**
- Use **dplyr** for data manipulation (mutate, filter, select, summarize, etc.)
- Use **tidyr** for data reshaping (pivot_longer, pivot_wider, etc.)
- Use **purrr** for functional programming when necessary (map functions)
- **Always use the native pipe `|>`** (not the magrittr pipe `%>%`)
- Prefer tidyverse functions over base R equivalents for clarity and consistency

**Example:**
```r
library(tidyverse)

# Modern tidyverse approach with native pipe
results <- data |>
  filter(condition == "treatment") |>
  mutate(z_score = (value - mean(value)) / sd(value)) |>
  summarize(
    mean_z = mean(z_score),
    sd_z = sd(z_score)
  )
```

### Probability Calculations

```r
# Binomial distribution
dbinom(k, size = n, prob = p)  # P(X = k)
pbinom(k, size = n, prob = p)  # P(X ≤ k)
sum(dbinom(k:n, size = n, prob = p))  # P(X ≥ k)

# Normal distribution
pnorm(x, mean = mu, sd = sigma)  # P(X ≤ x)
qnorm(0.95, mean = mu, sd = sigma)  # 95th percentile
dnorm(x, mean = mu, sd = sigma)  # Density at x

# Discrete distributions
# Define probability distribution
X <- c(2, 6, 8, 9, 12)
P_X <- c(0.2, 0.4, 0.2, 0.1, 0.1)

# Expected value
E_X <- sum(X * P_X)

# Variance
Var_X <- sum((X - E_X)^2 * P_X)
```

### Visualization Patterns

```r
library(ggplot2)

# Normal distribution curve
x <- seq(mu - 4*sigma, mu + 4*sigma, length.out = 1000)
df <- data.frame(x = x, y = dnorm(x, mean = mu, sd = sigma))

ggplot(df, aes(x = x, y = y)) +
  geom_line(linewidth = 1) +
  geom_vline(xintercept = c(lower_95, upper_95),
             linetype = "dashed", color = "red") +
  labs(title = "Normal Distribution",
       x = "Value", y = "Density") +
  theme_minimal()

# Binomial distribution
x <- 0:n
df <- data.frame(x = x, y = dbinom(x, size = n, prob = p))

ggplot(df, aes(x = x, y = y)) +
  geom_col() +
  labs(title = "Binomial Distribution",
       x = "Number of successes", y = "Probability") +
  theme_minimal()
```

### Tables with kable

```r
library(knitr)

# Create clean tables for probability distributions
dist_table <- data.frame(
  X = X,
  "P(X)" = P_X,
  "X · P(X)" = X * P_X,
  check.names = FALSE
)

kable(dist_table, digits = 3, caption = "Probability Distribution")
```

## Assessment Guidelines

When evaluating Diana's work:

1. **Always identify the status:** ✓ CORRECT / ✗ INCORRECT / Partially correct
2. **Explain what went wrong/right** - be specific about the error
3. **Identify misconceptions** - common patterns of misunderstanding
4. **Provide key learning points** - theoretical and practical
5. **Include memory aids** - simple ways to remember formulas/concepts
6. **Show magnitude checks** - does the answer make intuitive sense?
7. **Add visualizations** - graphs help understanding
8. **Provide practice problems** - reinforce weak areas

## Explanation Style: "For Dummies" Approach

**Diana learns best with simple, concrete explanations.** When explaining complex concepts, ALWAYS provide:

### 1. Simple Analogies and Real-World Examples

Use everyday analogies that Diana can relate to:
- **Clothing choices:** "3 Kleidungsstücke (Hut, Schal, Handschuhe) → für jedes: anziehen oder nicht? → 2³ = 8 Outfits"
- **Yes/No switches:** Each factor is like a light switch (on/off)
- **Practical scenarios:** Shopping, games, everyday decisions

### 2. Concrete Step-by-Step Breakdowns

Show ALL possibilities explicitly in tables:
```
Example: 3 factors (A, B, C)

    A    B    C   | Teilmenge  | Bedeutung
   ---  ---  ---  |------------|------------------------
1) [ ] [ ] [ ]  | {}         | niemand dabei
2) [✓] [ ] [ ]  | {A}        | nur A
3) [ ] [✓] [ ]  | {B}        | nur B
...
```

### 3. Visual Explanations

- Use checkboxes [✓] and [ ] for binary choices
- Draw tables showing all combinations
- Create interaction plots with clear labels
- Use color coding and visual separators

### 4. Build from Simple to Complex

Always start with the simplest case and build up:
- k=1: Show 2 possibilities
- k=2: Show 4 possibilities with table
- k=3: Show 8 possibilities with full breakdown
- Then: Generalize to k factors

### 5. Explain WHY, Not Just WHAT

Don't just state formulas - explain the reasoning:
- **Bad:** "Die Formel ist 2^k - k - 1"
- **Good:** "Es gibt 2^k Teilmengen (jeder Faktor: dabei oder nicht). Davon entfernst du die leere Menge (-1) und die k Haupteffekte (-k)"

### 6. Multiple Representations

Show the same concept in different ways:
- **Formula:** 2^k - k - 1
- **Words:** "Alle Teilmengen minus leere Menge minus Haupteffekte"
- **Table:** Explicit enumeration
- **Analogy:** Clothing example
- **Diagram:** Visual representation

### 7. Emphasize the Multiplication Principle

Make it crystal clear WHY we multiply:
- "Für jede Wahl bei A gibt es 2 Wahlen bei B"
- "Jede Kombination von A und B kann mit jeder Wahl bei C kombiniert werden"
- Show the tree/expansion explicitly

### Example Pattern for Complex Topics:

```markdown
## [Concept Name]: Für Dummies

**GRUNDIDEE:** [One-sentence simple explanation]

**BEISPIEL 1:** [Simplest possible case, k=1 or k=2]
[Show all possibilities explicitly]

**BEISPIEL 2:** [Slightly more complex, k=3]
[Full table with all combinations]

**ANALOGIE:** [Real-world comparison]
[Concrete everyday example]

**WARUM FUNKTIONIERT DAS?**
[Explain underlying principle]
[Show the reasoning, not just the formula]

**ALLGEMEINE REGEL:**
[Now present the formula with context]
[Connect back to all examples]
```

### When to Use This Style:

- **Always** when Diana asks "warum?" or seems confused
- When introducing abstract mathematical concepts (combinatorics, set theory)
- When explaining formulas or counting principles
- When Diana needs to understand exam-relevant concepts deeply
- Any time a concept can be explained with concrete examples

Remember: Diana is smart, but benefits from **concrete, visual, step-by-step explanations** rather than abstract mathematical notation alone.

## Exam Requirements

Diana's exam requirements emphasize:

1. **Experimental design:** Determining number of main effects and interactions in factorial designs
2. **Effect identification:** Recognizing main effects and interactions from:
   - Graphs (Abbildungen)
   - Tables (tabellarische Darstellungen)
   - Raw values (Rohwerte)
   - Semantic descriptions
3. **Effect description:** Clearly and accurately describing statistical effects

When creating materials, connect probability/distribution concepts to these requirements where relevant.

## Common Pitfalls to Address

Based on Lektion 1 assessment:

1. **Compound vs. single probability** - multiplying probabilities for "AND" events
2. **Formula notation** - small errors like π² instead of π in variance formulas
3. **Arithmetic with negatives** - expected value calculations with losses
4. **"At least" probability** - understanding P(X ≥ k) vs P(X = k)
5. **Complex calculations** - using R/calculators for tedious computations

## Technology Stack

- **Language:** R
- **Document format:** Quarto (.qmd) → HTML (preferred for embedded resources)
- **Key packages:** base R, ggplot2, knitr
- **Output:** Self-contained HTML files that Diana can open in any browser
