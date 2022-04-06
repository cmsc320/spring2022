# Project 3

Posted: April 5, 2022

Due: April 26, 2022


## Part 1: Regression analysis of Gapminder data

In this part of this project you will practice and experiment with linear regression using data from [gapminder.org]("http://gapminder.org"). We recommend spending a little time looking at material there, it is quite an informative site.

We will use a subset of data provided by gapminder provided by [Jennifer Bryan](https://jennybryan.org/) described in its [github page](https://github.com/jennybc/gapminder)

Get the data from: https://github.com/jennybc/gapminder/blob/master/data-raw/08_gap-every-five-years.tsv

(A mirror of that data is available in the project repository, in the `mirror` directory.)

```
import pandas as pd
data = pd.read_csv("gap.tsv", sep='\t')
data.head()
```

```
    country	 continent	year	lifeExp	pop	        gdpPercap
0	Afghanistan	Asia	1952	28.801	8425333	    779.445314
1	Afghanistan	Asia	1957	30.332	9240934	    820.853030
2	Afghanistan	Asia	1962	31.997	10267083	853.100710
3	Afghanistan	Asia	1967	34.020	11537966	836.197138
4	Afghanistan	Asia	1972	36.088	13079460	739.981106
```

For this exercise you will explore how life expectancy has changed over 50 years across the world, and how economic measures like gross domestic product (GDP) are related to it.

**Exercise 1**: *Make a scatter plot of life expectancy across time.*

**Question 1**: *Is there a general trend (e.g., increasing or decreasing) for life expectancy across time? Is this trend linear? (answering this qualitatively from the plot, you will do a statistical analysis of this question shortly)*

A slightly different way of making the same plot is looking at the distribution of life expectancy across countries as it changes over time:

```
    fig, ax = plt.subplots()

    ax.violinplot(life_exp_per_year,years,widths=4,showmeans=True)
    ax.set_xlabel("Year")
    ax.set_ylabel("Life Expectancy")
    ax.set_title("Violin Plot Example")
    fig.savefig("violin.png")
```

<img src="figs/violin.png" height="242">

This type of plot is called a <em>violin plot</em>, and it displays the distribution of the variable in the y-axis for each value of the variable in the x-axis. (It is okay to use other plotting libraries and tools to create this plot, and others throughout the assignment.)
Note that in order for the example code above, you will have to wrangle the data using Pandas. The way I did it was to create an array for each year, storing the Life Expectancy values for that year, then collected those arrays into a list: `life_exp_per_year`. It's not the only way of doing it, but it's how I first thought of it.

**Question 2**: <em>How would you describe the distribution of life expectancy across countries for individual years? Is it skewed, or not? Unimodal or not? Symmetric around it’s center?</em>

Based on the Violin plot you made, consider the following questions.

**Question 3**: <em>Suppose I fit a linear regression model of life expectancy vs. year (treating it as a continuous variable), and test for a relationship between year and life expectancy, will you reject the null hypothesis of no relationship? (do this without fitting the model yet. I am testing your intuition.)</em>

**Question 4**: <em>What would a violin plot of residuals from the linear model in Question 3 vs. year look like? (Again, don’t do the analysis yet, answer this intuitively)</em>

**Question 5**: <em>According to the assumptions of the linear regression model, what <strong>should</strong> that violin plot look like?  That is, consider the assumptions the linear regression model you used assumes (e.g., about noise, about input distributions, etc); do you think everything is okay?</em>

**Exercise 2**: <em>Fit a linear regression model using, e.g., the `LinearRegression` function from Scikit-Learn or the closed-form solution, for life expectancy vs. year (as a continuous variable).  There is no need to plot anything here, but please print the fitted model out in a readable format.</em>

**Question 6**: <em>On average, by how much does life expectancy increase every year around the world?</em>

**Question 7**: <em>Do you reject the null hypothesis of no relationship between year and life expectancy? Why?</em>

**Exercise 3**: <em>Make a violin plot of residuals vs. year for the linear model from Exercise 2.</em>

**Question 8**: <em>Does the plot of Exercise 3 match your expectations (as you answered Question 4)?</em>

**Exercise 4**: <em>Make a boxplot (or violin plot) of model residuals vs. continent.</em>

**Question 9**: <em>Is there a dependence between model residual and continent? If so, what would that suggest when performing a regression analysis of life expectancy across time?</em>

**Exercise 5**: <em>As in the Moneyball project, make a scatter plot of life expectancy vs. year, grouped by continent, and add a regression line.  The result here can be given as either one scatter plot per continent, each with its own regression line, or a single plot with each continent's points plotted in a different color, and one regression line per continent's points.  The former is probably easier to code up.</em>

**Question 10**: <em>Based on this plot, should your regression model include an interaction term for continent <strong>and</strong> year? Why?</em>

**Exercise 6**: <em>Fit a linear regression model for life expectancy including a term for an interaction between continent and year.  Print out the model in a readable format, e.g., print the coefficients of the model (no need to plot).  Hint: adding interaction terms is a form of feature engineering, like we discussed in class (think about, e.g., using (a subset of) polynomial features here).</em>

**Question 11**: <em>Are all parameters in the model significantly (in the p-value sense) different from zero? If not, which are not significantly different from zero? Other libraries (`statsmodels` or `patsy` may help you solve this problem)</em>

**Question 12**: <em>On average, by how much does life expectancy increase each year for each continent? (Provide code to answer this question by extracting relevant estimates from model fit)</em>

**Exercise 7**: <em>Make a residuals vs. year violin plot for the interaction model. Comment on how well it matches assumptions of the linear regression model.</em>


## Part 2: Classification

<div id="try-it-out" class="section level2">


<ol style="list-style-type: lower-alpha">
<li><p>Find a dataset on which to try out different classification (or regression) algorithms.  If you'd like, you can use a dataset provided by SKLearn; more info <a href="https://scikit-learn.org/stable/datasets/toy_dataset.html">here</a>.</p></li>
<li><p>Choose <strong>two</strong> of the following algorithms, or feel free to use other ``standard'' classifiers or regressors from SKLearn:</p></li>
</ol>
<ol style="list-style-type: decimal">
<li>Linear Discriminant Analysis (LDA) (only classification)</li>
<li>decision trees,</li>
<li>random forests,</li>
<li>linear SVM,</li>
<li>non-linear SVM</li>
<li>k-NN classification (or regression)</li>
</ol>
<p>(It will likely make sense to choose two classifiers or two regressors, not one of each, for most datasets and tasks.)</p>

<p>Compare the two chosen algorithms on their prediction performance, using your chosen dataset.  Let us know what your performance metric is (e.g., accuracy, false negative rate (FNR), false positive rate (FPR), precision, recall, etc), and feel free to use more than one.  Use either (i) holdout validation, like we discussed in class (11/9), or (ii) 10-fold cross-validation.  SKLearn offers some one-liners to help with cross-validation; more info can be found <a href="https://scikit-learn.org/stable/modules/cross_validation.html">here</a>.  </p>

<p>Note: for those algorithms that have hyper-parameters, i.e., all of the above except for LDA, you need to specify in your writeup which model selection procedure you used.</p>

<p>As a bonus (+2 points), if you ran 10-fold cross-validation, feel free to run a statistical test such as a paired t-test to further support your performance comparison above.</p>
</div>



<div id="handing-in" class="section level2">

### Handing in:

 * As usual, we expect a Notebook (in PDF, _and_ _static_ HTML form) where each problem and question are addressed as code and/or prose (where appropriate). We expect the code to be commented (the _how_) and the prose to explain _what_ and _why_.
 * For the part that requires you to choose your own dataset, organize your writeup as follows:</p></li>
    - Describe the dataset you are using, including: what is the outcome you are predicting (remember this should be a classification task) and what are the predictors you will be using.</p></li>
    - Include code to obtain and prepare your data as a dataframe to use with your two classification algorithms. In case your dataset includes non-numeric predictors, include the code you are using to transform these predictors into numeric predictors you can use with your logistic regression implementation.</p></li>
    - Specify the two additional algorithms you have chosen in part (b), and for algorithms that have hyper-parameters specify the method you are using for model selection.</p></li>
    - Include all code required to perform the holdout or 10-fold cross-validation procedure on your two algorithms.</p></li>
    - Write up the result of your holdout or 10-fold cross-validation procedure. If the latter, make sure to report the 10-fold CV error estimate (with standard error) of each of the two algorithms.</p></li>
