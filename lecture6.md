# Lecture 6 (02/02/2017) - Visualization and Communication

*by Prof. Nolan*

Why is visualization important?

- Visualization belongs in every stage of the data life cycle
- Plots uncover structure that numerical summaries can't detect
  - http://debrouwere.org/2017/02/01/unlearning-descriptive-statistics/
- Visualization is an important communication skill

**Today:**

- Techniques for making good visualizations
- Guidelines for making good visualizations

Starting point: understand what kind of data you have (numerical, ordinal,
categorical)

## Four examples of what not to do

### 2015 Congressional Hearing: Planned Parenthood

The chair of the congressional committee presented a plot:

    <plot of abortion and cancer screenings vs. time>

Plot shows 2006 - 2013

How many data points? What's suspicious about the plot?

Problems

- The lines are on different y-scales and the axis isn't even labeled
- The slope is uninterpretable
- Deb: "Actually this makes no sense."
- Only 4 data points plotted (2 per line)

    <show better version>

What strikes you now?

- Cancer screenings went down by a lot! And abortions had almost no change in
  comparison.
- Since the scales are so different, it's hard to make comparisons since the
  abortion line is squashed visually.

    <show point plot using percentages>

- This is much clearer since the scales are normalized.
- Shows that the number of abortion procedures have doubled.
- Example of bad Scale

### Voter Registration Trends in California

State publishes registration summaries and historical counts in previous years.

    <plot of majority party by County in California>

Problems

- x and y axis labels are terrible (not every election year is labeled)
- y-axis is really hard to understand
- Color of bars should indicate which party it is
- Confusing title
- Think about the message in the plot. Is this plot conveying the message well?
- Also, it's missing data! Think about decline to state vs. other parties.

### Earnings

Federal gov. does a lot of surveys/studies. Bureau of Labor Statistics released
data on labor statistics.

    <plot of median weekly earnings, split by gender and edu level>

What's the interesting / important comparison? Have I made it with this plot?

- Think about the data. We're comparing education (ordinal) and gender
  (nominal).
- We'd like to compare bars at the same education level side-by-side but
  they're split in the graph.
- We want to facilitate the important comparisons. This plot emphasizes
  education comparison but not gender comparisons.
- Deb: "Also, colors are horrible."

    <show line plot>

- This plot lets us make a simple vertical comparison
- We can see now that the gap between gender earnings grows as education level
  increases.
- Example of bad Conditioning

### Cherry Blossom Run

10 mile in DC during April, results available on Web. In 2012 nearly 17,000
runners ran.

    <scatterplot of time to finish vs. age>

Problems

- Too many points on the plot, maybe we can make points more transparent.
- Could use 3D histogram but those are hard to come by.
- Example of bad Smoothing

We could use heat map, hexbin, or transparency (bin regions together).

    <scatterplot using transparency>

Note that our data isn't longitundinal. We didn't follow anyone in time so we
have to be careful making judgements on race time vs. age. It's a different set
of people in each year.

Note: these plots don't start at 0. If we did, we would lose information rather
than gain since all the points would be squashed.

Be careful: there is a balance of using visualization and hypothesis testing.
Doing only one without the other is dangerous and can be misleading.

## Making good visualizations

### Scale

Choose a consistent scale.

<see slides for more notes>

### Conditioning

- Superpose density curves, fitted curves and lines from different subgroups.
- But need to juxtapose scatterplots, histograms (since bars hide each other).

### Perception

Color schemes

- Choosing color is difficult, so use something researchers have vetted.
- Very bright colors are hard to look at for a while.
- Lighter colors tend to make areas look larger than dark colors
- The color scheme you use depends on the type of data!
  - Qualitative schemes: Just trying to distinguish different categories
  - Quantitative schemes: Emphasize ends of a spectrum

Length

- Angle and area judgements are difficult for the human eye
- We're much better at distinguishing lengths
- Also, dot charts make differences easier to see than bar charts

Why does Deb like the line charts for salary rather than bar charts?

- It's easier to perceive the difference vs a bar chart (your eyes move less).
- The spacing between categories doesn't matter, but connecting with lines lets
  us see growth.

Deb shows two visualizations for GDP by African country. One is cool with
colorful squares but it's hard to compare areas. The other is boring but
actually emphasizes the important differences. Don't alphabetize the countries;
show in order.

Stacked bar plots (one bar on top of another) makes it really hard to make
comparisons across the graph since the visual baseline changes. Same for line
plots where the area between lines means something.

    <CO2 emissions examples>

Avoiding stacking in this example shows us countries increasing emissions
exponentially fast and those that are not.

But the first visualizations has two goals: show global emission levels and
make comparisons. The second doesn't try to show global emission levels.

There are no hard rules. Even for pie charts!

### Transformations

Why transform? It lets us see relationships that otherwise would be hard to
see.

Power Transformation:

    x^p = (x^p - 1) / p

This stretches/shrinks the data while preserving order of values.

One reason to transform is to make data straight (eg. log-log plot). Once data
is straight, you can say with more clarity what kind of relationship the
variables have.

Example: life expectancy vs. healthcare expenditure

    <scatterplot showing curve through the top left corner>

Healthcare costs distribution have a very long right tail, logging data shows
symmetry.

Life expectancy has left tail, suggests upper bound of life expectancy.

(What do you think distributions of exam scores are like? Skew right? Left?
100% is a hard stop, so usually skew left.)

We can make the spread of life expectancy even by doing `(life expectency - 37)
^ 3`. But is that interpretable? You probably wouldn't say so unless your model
is complex enough.

But there's like a "sweet spot" where once you get up to 100 on the healthcare
expenditure on the x-axis you get sharply increasing life expectancy. How can
we show this? We can color by income / continent.

### Context

Labeling axes, units, reference lines/markers, etc.

### Smoothing

When you have many data points the are densely packed, smoothing is used to
group similar points together so overall patterns are more clear.

### Philosophy

- Reveal the data
- Avoid overplotting
- Facilitate comparisons
- Favor length over area
- Making plot info rich
