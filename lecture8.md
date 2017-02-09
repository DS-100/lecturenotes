# Lecture 8 (2/9/2017) - Advanced Python Data Science Tools (con't), Prediction and Inference

*Prof. Gonzalez and Prof. Yu*

## More `pandas`

### `pandas` indexing

`pandas` dataframes have a index on the rows, which allows you to select rows
using values in the index.

### Baby Names Dataset

This dataset contains the names and state of birth for babies born in the US
with a social security card number for each year since 1910.

Note that the dataset doesn't contain names that are reported less than 5 times
to protect privacy.

`pd.read_csv` reads in file, uses first line of file as header unless
otherwise specified (using the `names` kwarg).

Loading in the entire dataset of names gives us 5.7 million names! This is hard
to work with in Excel.

### Derived columns

Creating an new column in `pandas` is as easy as:

    df['new_col'] = <some series>

Use `df.str.<func>` to call a string function on every value in a Series.

For example:

    df['Name'].str[-1].str.lower()

Gives the last letter of each name, lowercased.

### Advanced slicing

Use a boolean expression on a series to create a mask you can use for indexing.

    mask = df['Name'] == 'Sam'
    df[mask]

Note that you have to use the bitwise and/or (`&` and `|`) instead of the
normal ones:

    # Wrong!
    (df['Name'] == 'Sam') or (df['Name'] == 'Joseph')

    # Right
    (df['Name'] == 'Sam') | (df['Name'] == 'Joseph')

This is just an implementation decision of `pandas`.

### Grouping

We often want to make aggregate computations on subgroups of the original
dataset. For example, how many total babies (computation) were there for each
gender (subgroup)

This generally has the pattern of:

1. Split the data
2. Aggregate each group

    baby_names.groupby('Sex')[['Count']].sum()
                      ^                   ^
                   grouping            aggregation

Example: Breaking down popular names by gender

1. How to split? Group by both sex and name.
2. Find the sum of each group's Count column.

    baby_names.groupby(['Sex', 'Name'])['Count'].sum()

## Prediction, Machine Learning, and Inference

### Prediction

Prediction problems are everywhere: eg. from an image, predict what is
contained in the image.

A prediction problem needs a predictor (eg. the input image) and produces a
label (eg. image contains a hot dog).

Prediction is a basic tool in science:

- Replication: similar conditions result in similar outcomes
- Extrapolation: related but different conditions result in related but
  different outcomes

Must ask question: Are we in a replication or an extrapolation situation? It's
never exactly one or the other; humans needs need to make judgement calls.

#### Example: Gallup Poll

Population: people with phone numbers

Goal: Predict people's votes on election day

Assumptions:

1. People don't change their votes
2. People tell the truth
3. People with phones vote similarly as people without
4. Undecided voters vote similarly as decided voters

These are never all true all the time! But humans have made a judgement call
here.

Use the outcome of a prediction to evaluate whether assumptions are valid or
not.

If we change goal to predict people with phone's votes on election day, this
becomes more like a replication problem.

### Machine Learning

What is machine learning? Traditional statistics has prediction but not at its
center. Machine learning is like modern statistics + computer science.

Supervised learning (regression and classification): given `x`, predict `y`.

- `x = traffic flows in lanes 2 and 3`, `y = traffic flow in lane 1`
- `x = pixel values in an image`, `y = dog or cat label`
- `x = gene expression levels`, `y = cancer status`

Unsupervised learning (clustering): given `x`, find patterns.

- `x = pixels on image`, find important parts of image

Note: AlphaGo uses "deep learning" (new name for neural nets) to determine the
best move to make, but it was ultimately a big human-computer collaboration
since it needed significant computing power and good moves were pre-programmed
in.

Uncertainty: Machine learning is headed in this direction -- to determine how
uncertain a prediction is.

### Inference

Making a prediction to a degree of accuracy sufficient for another person to
confirm it.

So what is "sufficient accuracy"?

Example: gene mutation

- One team discovers a gene means you have 58% chance of getting breast cancer,
  another team tries to replicate. Will they get exactly the same number?
  Probably not.

Statistical inference: assessing uncertainty about a conclusion from data.

- Or more precisely, assessing uncertainty about quantities from from data
  under a probabilistic data generation mechanism (eg. sampling from
  population, randomization).

How do we measure uncertainty?

- Ideally we replicate data collection many times so that we describe natural
  variability. Then we can pull out a uncertainty measure eg. confidence
  interval.

But often we can't replicate data collection too many times...

- So we use the bootstrap to generate pseudo-replicate data.

### Case study: traffic problem

J wants to know: which lane should I take to get to work fastest?

Question: Is lane 1 more crowded than lane 4 in terms of flow during rush hour
7-8am?

Problem: All work day flows over 60 min intervals at Beaument Ave

R: What data are considered respresentative?

What does J mean by the "best"? Less crowded on average? Less surprises with
travel time?

We create a bootstrap confidence interval for the difference in flows and it
includes 0. However, all we can say is that *mean* difference is not
significantly large. Looking at the data actually suggests there is a
difference. So, the confidence interval is probably not the right tool for J.
