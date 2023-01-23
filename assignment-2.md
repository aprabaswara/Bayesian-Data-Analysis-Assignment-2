
**University of Edinburgh**

**School of Mathematics**

**Bayesian Data Analysis, 2021/2022, Semester 2**

**Author: Aditya Prabaswara Mardjikoen (S2264710)**

**Lecturer: Daniel Paulin**

**Assignment 2**

**IMPORTANT INFORMATION ABOUT THE ASSIGNMENT**

**In this paragraph, we summarize the essential information about this
assignment. The format and rules for this assignment are different from
your other courses, so please pay attention.**

**1) Deadline: The deadline for submitting your solutions to this
assignment is the 11 April 12:00 noon Edinburgh time.**

**2) Format: You will need to submit your work as 2 components: a PDF
report, and your R Markdown (.Rmd) notebook. There will be two separate
submission systems on Learn: Gradescope for the report in PDF format,
and a Learn assignment for the code in Rmd format. You are encouraged to
write your solutions into this R Markdown notebook (code in R chunks and
explanations in Markdown chunks), and then select Knit/Knit to PDF in
RStudio to create a PDF report.**

<img src="knit_to_PDF.jpg" width="191" />

**It suffices to upload this PDF in Gradescope submission system, and
your Rmd file in the Learn assignment submission system. You will be
required to tag every sub question on Gradescope. A video describing the
submission process will be posted on Learn.**

**Some key points that are different from other courses:**

**a) Your report needs to contain written explanation for each question
that you solve, and some numbers or plots showing your results.
Solutions without written explanation that clearly demonstrates that you
understand what you are doing will be marked as 0 irrespectively whether
the numerics are correct or not.**

**b) Your code has to be possible to run for all questions by the Run
All in RStudio, and reproduce all of the numerics and plots in your
report (up to some small randomness due to stochasticity of Monte Carlo
simulations). The parts of the report that contain material that is not
reproduced by the code will not be marked (i.e. the score will be 0),
and the only feedback in this case will be that the results are not
reproducible from the code.**

<img src="run_all.jpg" width="376" />

**c) Multiple Submissions are allowed BEFORE THE DEADLINE are allowed
for both the report, and the code. However, multiple submissions are NOT
ALLOWED AFTER THE DEADLINE. YOU WILL NOT BE ABLE TO MAKE ANY CHANGES TO
YOUR SUBMISSION AFTER THE DEADLINE. Nevertheless, if you did not submit
anything before the deadline, then you can still submit your work after
the deadline. Late penalties will apply unless you have a valid
extension. The timing of the late penalties will be determined by the
time you have submitted BOTH the report, and the code (i.e. whichever
was submitted later counts).**

**We illustrate these rules by some examples:**

**Alice has spent a lot of time and effort on her assignment for BDA.
Unfortunately she has accidentally introduced a typo in her code in the
first question, and it did not run using Run All in RStudio. - Alice
will get 0 for the whole assignment, with the only feedback “Results are
not reproducible from the code”.**

**Bob has spent a lot of time and effort on his assignment for BDA.
Unfortunately he forgot to submit his code. - Bob will get no personal
reminder to submit his code. Bob will get 0 for the whole assignment,
with the only feedback “Results are not reproducible from the code, as
the code was not submitted.”**

**Charles has spent a lot of time and effort on his assignment for BDA.
He has submitted both his code and report in the correct formats.
However, he did not include any explanations in the report. Charles will
get 0 for the whole assignment, with the only feedback “Explanation is
missing.”**

**Denise has spent a lot of time and effort on her assignment for BDA.
She has submitted her report in the correct format, but thought that she
can include her code as a link in the report, and upload it online (such
as Github, or Dropbox). - Denise will get 0 for the whole assignment,
with the only feedback “Code was not uploaded on Learn.”**

**3) Group work: This is an INDIVIDUAL ASSIGNMENT, like a 2 week exam
for the course. Communication between students about the assignment
questions is not permitted. Students who submit work that has not been
done individually will be reported for Academic Misconduct which can
lead to serious consequences. Each problem will be marked by a single
instructor, so we will be able to spot students who copy.**

**4) Piazza: You are NOT ALLOWED to post questions about Assignment
Problems visible to Everyone on Piazza. You need to specify the
visibility of such questions as Instructors only, by selecting Post to /
Individual students/Instructors and type in Instructors and click on the
blue Instructors banner that appears below**

![](piazza_instructors.jpg)

**Students who post any information related to the solution of
assignment problems visible to their classmates will**

**a) have their access to Piazza revoked for the rest of the course
without prior warning, and**

**b) reported for Academic Misconduct.**

**Only questions regarding clarification of the statement of the
problems will be answered by the instructors. The instructors will not
give you any information related to the solution of the problems, such
questions will be simply answered as “This is not about the statement of
the problem so we cannot answer your question.”**

**THE INSTRUCTORS ARE NOT GOING TO DEBUG YOUR CODE, AND YOU ARE ASSESSED
ON YOUR ABILITY TO RESOLVE ANY CODING OR TECHNICAL DIFFICULTIES THAT YOU
ENCOUNTER ON YOUR OWN.**

**5) Office hours: There will be two office hours per week (Monday
16:00-17:00, and Wednesdays 16:00-17:00) during the 2 weeks for this
assignment. The links are available on Learn / Course Information. We
will be happy to discuss the course/workshop materials. However, we will
only answer questions about the assignment that require clarifying the
statement of the problems, and will not give you any information about
the solutions. Students who ask for feedback on their assignment
solutions during office hours will be removed from the meeting.**

**6) Late submissions and extensions: Students who have existing
Learning Adjustments in Euclid will be allowed to have the same
adjustments applied to this course as well, but they need to apply for
this BEFORE THE DEADLINE on the website**

<https://www.ed.ac.uk/student-administration/extensions-special-circumstances>

**by clicking on “Access your learning adjustment”. This will be
approved automatically.**

**For students without Learning Adjustments, if there is a justifiable
reason (external circumstances) for not being able to submit your
assignment in time, then you can apply for an extension BEFORE THE
DEADLINE on the website**

<https://www.ed.ac.uk/student-administration/extensions-special-circumstances>

**by clicking on “Apply for an extension”. Such extensions are processed
entirely by the central ESC team. The course instructors have no role in
this decision so you should not write to us about such applications. You
can contact our Student Learning Advisor, Maria Tovar Gallardo
(<maria.tovar@ed.ac.uk>) in case you need some advice regarding this.**

**Students who submit their work late will have late submission
penalties applied by the ESC team automatically (this means that even if
you are 1 second late because of your internet connection was slow, the
penalties will still apply). The penalties are 5% of the total mark
deduced for every day of delay started (i.e. one minute of delay counts
for 1 day). The course intructors do not have any role in setting these
penalties, we will not be able to change them.**

<img src="fishing.jpg" style="width:100.0%" />

**Problem 1 - Fishing in a park**

**Our dataset from UCLA OARC has data on 250 groups that went to a
park.They were questioned about how many fish they caught (count), how
many people were in the group (persons), how many children were in the
group (child), whether or not they brought a camper van to the park
(camper), and whether or not they used live bait (livebait).**

**We are going to apply several regression models on this dataset. The
first step is to load the dataset and JAGS.**

``` r
library(rjags)
#We load JAGS

#You may need to set the working directory first before loading the dataset
#setwd("/Users/dpaulin/Dropbox/BDA_2021_22/Assignments/Assignment2")
fish=read.csv("fish.csv")
#The first 6 rows of the dataframe
print.data.frame(fish[1:6,])
```

    ##   livebait camper persons child count
    ## 1        0      0       1     0     0
    ## 2        1      1       1     0     0
    ## 3        1      0       1     0     0
    ## 4        1      1       2     1     0
    ## 5        1      0       1     0     1
    ## 6        1      1       4     2     0

**a)\[10 marks\]**

**Create a new column in the dataset for proportion of children in the
group (prop.child). Fit a Poisson GLM with log link function on the
number of fish caught (count) as response, and the covariates camper,
livebait, and prop.child as covariates. Use the offset feature of the
Poisson GLM to take the number of persons into account. Interpret the
results and discuss the meaning of the regression coefficients for the 3
covariates.**

Explanation:

Observe that in the dataset we does not have the data regarding the
proportion of children in the group (prop.child). We only have the data
of the number of children and people in each groups. By using this two
data, we can calculate the proportion of children in the group, which is
the number of children in the group per the number of people in a group.
After we compute the proportion of children in each group then we will
fit a Poisson GLM model with log link function on the number of fish
caught (count) as the response variable. In this Poisson GLM, the
variables that we are going to use as the explanatory variables is
prop.child, camper, and livebait. Since we use the $\verb|offset|$
function in $\verb|R|$ to take the number of persons into account into
the model, then we can formulate our Poisson GLM as
$$\log{(\mu)} = \beta_0+\beta_1\text{camper}+\beta_2\text{livebait}+\beta_3\text{prop.child}+\log{(\text{persons})},$$where
$\mu$ is the average number of fish that was caught, $\beta_0$ is the
Poisson GLM intercept, $\beta_1$ is the coefficient of the binary
variable that indicates whether or not a group brought a camper van to
the park ( 0 = no and 1 = yes), $\beta_2$ is the coefficient of the
binary variable that indicates whether or not a group use live baits to
capture the fish ( 0 = no and 1 = yes), and $\beta_3$ is the coefficient
of the proportion of children variable. The Poisson GLM that we
formulated for this problem can be written also as
$$\log{\left(\dfrac{\mu}{\text{persons}}\right)} = \beta_0+\beta_1\text{camper}+\beta_2\text{livebait}+\beta_3\text{prop.child}$$By
using the $\verb|R|$ code below, we will fit this Poisson GLM.

``` r
# Calculate proprotion of children in the group
fish$prop.child = fish$child/fish$persons

#Fit and display model summary of Poisson GLM
m1.log <- glm(count ~ camper+livebait+prop.child+offset(log(persons)),data=fish,
              family=poisson)
summary(m1.log)
```

    ## 
    ## Call:
    ## glm(formula = count ~ camper + livebait + prop.child + offset(log(persons)), 
    ##     family = poisson, data = fish)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -4.7987  -1.7770  -1.0204  -0.4346  20.2478  
    ## 
    ## Coefficients:
    ##             Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept) -1.36776    0.23646  -5.784 7.28e-09 ***
    ## camper       0.93438    0.08901  10.498  < 2e-16 ***
    ## livebait     1.77831    0.23273   7.641 2.16e-14 ***
    ## prop.child  -4.89927    0.25407 -19.283  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for poisson family taken to be 1)
    ## 
    ##     Null deviance: 2557.5  on 249  degrees of freedom
    ## Residual deviance: 1580.9  on 246  degrees of freedom
    ## AIC: 1926
    ## 
    ## Number of Fisher Scoring iterations: 6

From the output above, we obtain $\hat{\beta_0} = -1.36776$,
$\hat{\beta_1} = 0.93438$, $\hat{\beta_2} = 1.77831$, and
$\hat{\beta_3} = -4.89927$. Therefore, we can write our Poisson GLM as
$$\log{\left(\dfrac{\hat{\mu}}{\text{persons}}\right)} = -1.36776+0.93438*\text{camper}+1.77831*\text{livebait}-4.89927*\text{prop.child},$$where
$\hat{\mu}$ is the estimated average number of fish that was caught.
After we obtained our Poisson GLM model, we will interpret the model
estimated parameters. First, lets interpret the Poisson GLM intercept.
We can interpret the regression intercept as the log of the average
number of fish that was caught per the total number of people in a
groups when all covariates in the model equals to zero. In other words,
the average number of fish that was caught per the total number of
people in a groups when there are no children in the groups, the groups
does not bring any camper van to the park, and the groups does not use
any live baits to catch the fish is $e^{\hat{\beta_0}}= 0.2546768$ .

Next, lets interpret the coefficient of the camper variable. The
interpretation for this parameter is that a one unit change in the
camper variable adds log of average number of fish that was caught per
the total number of people in a groups by 0.93438 assuming other
independent variables in the model remains constant. Since the group who
does not bring a camper van in the park is keyed as 0 while the group
that bring it is keyed as 1, this means that the average number of fish
that was caught per the total number of people in a groups increased by
$e^{\hat{\beta_1}} = 2.545635$ times when the group bring a camper van
in the park assuming that other independent variables in the model
remains constant.

Now lets interpret the coefficient of the livebait variable. The
interpretation for this parameter is that a one unit change in the
livebait variable adds log of average number of fish that was caught per
the total number of people in a groups by 1.77931 assuming other
independent variables in the model remains constant. Since the group who
does not use live baits to catch the fish is keyed as 0 while used it is
keyed as 1, this means that the average number of fish that was caught
per the total number of people in a groups increased by
$e^{\hat{\beta_2}} = 5.925766$ times when the group use live baits to
catch the fish assuming that other independent variables in the model
remains constant.

Finally, lets interpret the coefficient of the proportion of children
variable. The interpretation for this parameter is that a one unit
change in the proportion of children variable adds log of average number
of fish that was caught per the total number of people in a groups by
-4.89927 assuming other independent variables in the model remains
constant. This implies that the average number of fish that was caught
per the total number of people in a groups increased by
$e^{\hat{\beta_3}} = 0.007452021$ times for every one unit change in the
proportion of children variable assuming that other independent
variables in the model remains constant. The value of
$e^{\hat{\beta}_i}$, for $i = 0,1,\dots,3$ that we used here can be
obtained using the $\verb|R|$ code below.

``` r
# Exponential values of estimated regression parameter
exp(coef(m1.log))
```

    ## (Intercept)      camper    livebait  prop.child 
    ## 0.254676756 2.545638939 5.919842282 0.007452012

Poisson GLMs assume that the mean and variance of the response variable
increase at the same rate (see the model summary output above and the
statement $\verb|Dispersion|$ $\verb|parameter|$ $\verb|for|$
$\verb|poisson|$ $\verb|family|$ $\verb|taken|$ $\verb|to|$ $\verb|be|$
$\verb|1|$). This assumption must be confirmed. If the residual deviance
of the fitted model is bigger than the residual degrees of freedom, then
we have over-dispersion. Over-dispersion means that a Poisson
distribution does not adequately model the variance and is not
appropriate for the analysis. The over-dispersion statistics (residual
deviance divided by residual degrees of freedom) can be calculated using
the $\verb|R|$ code below:

``` r
# Calculate over-dispersion statistics
cat('Over-dispersion statistics:',m1.log$deviance/m1.log$df.residual)
```

    ## Over-dispersion statistics: 6.426572

From the output above, we can see that the over-dispersion statistics is
greater than 1. This implies that the residual deviance greater than the
residual deviance of the fitted model is bigger than the residual
degrees of freedom. Therefore, our Poisson GLM is not appropriate for
estimating the number of fish that was caught since this model violated
the assumption of the equality of mean and variance of Poisson
distribution. The explanation that I give in this part was based on the
GLMs in R for Ecology written by Carl Smith and Mark Warren. This is the
following link to access the pdf file:
<http://irep.ntu.ac.uk/id/eprint/37478/1/14596_Smith.pdf>

**b)\[10 marks\] Using JAGS, implement a Bayesian version of the model
in part a), i.e. a Bayesian Poisson GLM with log link function and the
number of persons acting as the offset variable. Explain how did you
construct your model. Use a Gaussian prior with mean 0 and variance 100
for the intercept, and independent Gaussian priors with mean 0 and
variance 1 for the other 3 regression coefficients. Do 5000 burn-in
iterations, and obtain 10000 samples from all regression coefficients
from this model using coda.samples.**

Explanation:

Previously in part a) we have formulated our Poisson GLM model. This
model can be formulated as
$$\log{(\mu)} = \beta_0+\beta_1\text{camper}+\beta_2\text{livebait}+\beta_3\text{prop.child}+\log{(\text{persons})},$$where
$\mu$ is the average number of fish that was caught. However, we have
not give further detail how to construct this model. In this part, we
will have a further detail about the derivation of Poisson GLM in part
a). Assume that the distribution of the response variable (the number of
fish that was caught) is a Poisson distribution with rate $\mu$. This
implies that $E[\text{count}] = \mu$, where in this case we can
interpret $\mu$ as the average number of fish that was caught.
Therefore, we can interpret $\frac{\mu}{\text{persons}}$ as the average
number of fish that was caught per the total number of persons in a
group (which represented by the persons variable in the fish.csv
dataset). Recall that in the Poisson GLM the link function is the log
link function, which is $g(\mu) = \log{(\mu)}$ where $\mu$ is the
average number of fish that was caught. Since the Poisson distribution
is a member of the exponential families, then we can treat the
regression problem with the response variable having a Poisson
distribution as a GLM problem. We are going to formulate our Poisson GLM
that shows the relationship between the average number of fish that was
caught per the total number of persons in a group with some explanatory
variable in the fish.csv dataset. We choose prop.child, camper, and
livebait as our explanatory variable in our Poisson GLM. By using the
link function $g(\mu) = \log{(\mu)}$ on the average number of fish that
was caught per the total number of persons in a group, we can formulate
our Poisson GLM as
$$\log{\left(\dfrac{\mu}{\text{persons}}\right)} = \beta_0+\beta_1\text{camper}+\beta_2\text{livebait}+\beta_3\text{prop.child},$$
which is equivalent with
$$\log{(\mu)} = \beta_0+\beta_1\text{camper}+\beta_2\text{livebait}+\beta_3\text{prop.child}+\log{(\text{persons})}.$$

Next, we will construct the Poisson GLM based on the Bayesian approach.
Since we use Poisson GLM here, then the response variable (number of
fish that was caught) is having a Poisson distribution with mean $\mu$.
In the Bayesian approach, we have to decide the prior distribution for
$\beta_i$ that we are going to use in the model, where
$i = 0,1,\dots,3$. We will use the Gaussian prior with mean 0 and
variance 100 for the intercept. As for the 3 regression coefficient in
the model, we will use Gaussian prior with mean 0 and variance 1. Let
$\mu_i$ and $\sigma^2_i$ respectively be the mean and variance parameter
for the Gaussian prior distribution for $\beta_i$, where
$i = 0,1,\dots,3$. In addition, let
$$\mathbf{x}_i = \left(\text{camper}_i, \text{livebait}_i, \text{prop.child}_i, \text{persons}_i\right),$$where
$\text{camper}_i$, $\text{livebait}_i$, $\text{prop.child}_i$, and
$\text{persons}_i$ each represent the i-th values of the observations
for the camper, livebait, prop.child, and persons variable respectively
for $i = 1,2,\dots,250$. Recall that there are 250 groups in the
$\verb|fish.csv|$ dataset. We can formulate our Bayesian Poisson GLM as
follows: $$\begin{aligned}
\text{count}_i|\mu_i, \mathbf{x}_i&\sim
\text{Poisson}(\mu_i), \quad i = 1,2,\dots, 250\\
\log{(\mu_i)} &= \beta_0+\beta_1\text{camper}_i+\beta_2\text{livebait}_i+\beta_3\text{prop.child}_i+\log{(\text{persons}_i)}\\
\beta_0 &\sim \text{N}(\mu_0 = 0, \sigma^2_0 = 100)\\
\beta_1 &\sim \text{N}(\mu_1 = 0, \sigma^2_1 = 1)\\
\beta_2 &\sim \text{N}(\mu_2 = 0, \sigma^2_2 = 1)\\
\beta_3 &\sim \text{N}(\mu_3 = 0, \sigma^2_3 = 1)
\end{aligned}$$

We have already formulated our Bayesian Poisson GLM model. Now, we will
explain how we can create this model in JAGS. Recall that in JAGS the
normal distribution function $\verb|dnorm|$ is parameterize in terms of
mean and precision. Therefore, we need to calculate the precision
parameter of the Gaussian prior distribution for each $\beta_i$,
$i = 0,1,\dots,3$. Let $\tau_i$ be the precision parameter of the
Gaussian prior distribution of $\beta_i$. By using the relationship
between precision and variance, we can formulated the precision
parameter as $\tau_i = \frac{1}{\sigma^2_i}$ for each $i = 0,1,\dots,3$.
Since $\sigma^2_0 = 100$ and $\sigma^2_i = 1$, for $i = 1,2,3$, then
$\tau_0 = 0.01$ and $\tau_i = 1$, for $i = 1,2,3$. The $\verb|R|$ code
below implements the JAGS model of the Bayesian Poisson GLM that we have
already formulated in this part. We ran 13 chains with 10000 samples
after 5000 burn-in iterations.

``` r
# ---- Bayesian model
# Model is now Poisson(mu[i] = exp(b1*camper[i]+b2*livebait[i]+b3*prop.child[i])persons[i])

# Input data and prior hyperparameter for each beta
model1.data <- list(n=nrow(fish),camper=fish$camper,livebait=fish$livebait,
                    prop.child=fish$prop.child,persons=fish$persons, count=fish$count,
                    mu.beta0=0,mu.beta1=0, mu.beta2=0, mu.beta3=0, prec.beta0=1/100, prec.beta1=1,
                        prec.beta2=1, prec.beta3=1)

# Create model block for JAGS
model1_string <- "model {
# Data that will be read in are n, count, camper, livebait, prop.child and persons

# Prior for each parameter beta
beta0 ~ dnorm(mu.beta0,prec.beta0)
beta1 ~ dnorm(mu.beta1,prec.beta1)
beta2 ~ dnorm(mu.beta2,prec.beta2)
beta3 ~ dnorm(mu.beta3,prec.beta3)

#Likelihood
for(i in 1:n) {

# Poisson GLM
log(mu[i]) <- beta0+beta1*camper[i]+beta2*livebait[i] +beta3*prop.child[i]+log(persons[i])

# Observations
count[i] ~ dpois(mu[i])

# Replicates
count.rep[i] ~ dpois(mu[i])}
}"


# Compile the model
model1<- jags.model(file=textConnection(model1_string),data=model1.data,n.chains=13,quiet=T)

# Burnin 5000 iterations
update(model1, n.iter=5000)

# Generate posterior sample
model_param <- c("beta0","beta1","beta2", "beta3")
model1.samps <- coda.samples(model1,n.iter=10000, variable.names=model_param)
```

**c)\[10 marks\] Based on your MCMC samples, compute the Gelman-Rubin
convergence diagnostics (Hint: you need to run multiple chains in
parallel for this by setting the n.chains parameter). Discuss how well
has the chain converged to the stationary distribution based on the
results.**

**Compute and print out the effective sample sizes (ESS) for the
intercept and 3 regression coefficients.**

**If the ESS is below 1000 for any of these 4 parameters, increase the
sample size/number of chains until the ESS is above 1000 for all of
them.**

**Print out the summary of the fitted JAGS model. Compare this with the
results from the GLM model of a).**

**Check the sensitivity of the summary statistics with respect to the
priors.**

Explanation:

As we can see from either the $\verb|gelman.diag|$ or
$\verb|gelman.plot|$ results, the Gelman-Rubin diagnostics values are
below 1.05 for each of the Poisson GLM regression parameters in part b),
indicating that we have approximated the stationary distribution quite
well.

``` r
# Gelman rubin plot
gelman.plot(model1.samps[,c('beta0','beta1')])
```

![](assignment-2_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
gelman.plot(model1.samps[,c('beta2','beta3')])
```

![](assignment-2_files/figure-gfm/unnamed-chunk-6-2.png)<!-- -->

``` r
# Gelman rubin statistics
gelman.diag(model1.samps)
```

    ## Potential scale reduction factors:
    ## 
    ##       Point est. Upper C.I.
    ## beta0       1.01       1.01
    ## beta1       1.00       1.00
    ## beta2       1.01       1.01
    ## beta3       1.00       1.00
    ## 
    ## Multivariate psrf
    ## 
    ## 1.01

In our code in part b), we ran 13 chains with 10000 samples after 5000
burn-in iterations. We have computed the ESS (Effective Sample Size) for
the model parameters $\beta_0$, $\beta_1$, $\beta_2$, and $\beta_3$
using the $\verb|effectiveSize|$ function. The ESS is above 1000 for
each of them, so no further samples are needed.

``` r
# Effective sample size
effectiveSize(model1.samps)
```

    ##     beta0     beta1     beta2     beta3 
    ##  1295.826  9766.462  1297.166 62951.348

Lets have a look at the trace plot of the Poisson GLM parameter
$\beta_0$, $\beta_1$, $\beta_2$, and $\beta_3$ using the $\verb|R|$ code
below. From the trace plot below, we can see that the chain for the
parameter $\beta_0$, $\beta_1$, $\beta_2$, and $\beta_3$ were mixing
well and have converged.

``` r
# Plot trace plot and density plot
plot(model1.samps[,c('beta0','beta1')])
```

![](assignment-2_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

``` r
plot(model1.samps[,c('beta2','beta3')])
```

![](assignment-2_files/figure-gfm/unnamed-chunk-8-2.png)<!-- -->

Next, we printed out the posterior summaries for the Poisson GLM
parameters $\beta_0$, $\beta_1$, $\beta_2$, and $\beta_3$ using the
$\verb|summary(model1.samps)|$ command. We can see that the posterior
standard deviations for these four parameters are typically much smaller
that the posterior means in absolute value, indicating that the amount
of data is sufficient to fit the model parameters with some degree of
confidence. The time series SE of all these four parameters are less
than the posterior means (in absolute value), showing our estimates for
all of these four parameters are rather accurate and the chains was
mixing reasonably well as the trace plot or Gelman-Rubin diagnostic plot
suggested. Thus, our Bayesian Poisson GLM in part b) is accurate to
estimate the number of fish that was caught. In summary, the Bayesian
Poisson GLM in part b) is more accurate to predict the number of fish
that was caught compared to the Poisson GLM in part a).

``` r
# Posterior sample summary
summary(model1.samps)
```

    ## 
    ## Iterations = 6001:16000
    ## Thinning interval = 1 
    ## Number of chains = 13 
    ## Sample size per chain = 10000 
    ## 
    ## 1. Empirical mean and standard deviation for each variable,
    ##    plus standard error of the mean:
    ## 
    ##          Mean      SD  Naive SE Time-series SE
    ## beta0 -1.3100 0.21553 0.0005978      0.0060472
    ## beta1  0.9361 0.08888 0.0002465      0.0008998
    ## beta2  1.6993 0.21172 0.0005872      0.0060123
    ## beta3 -4.6239 0.23447 0.0006503      0.0009349
    ## 
    ## 2. Quantiles for each variable:
    ## 
    ##          2.5%     25%    50%     75%   97.5%
    ## beta0 -1.7535 -1.4508 -1.303 -1.1628 -0.9048
    ## beta1  0.7648  0.8757  0.935  0.9954  1.1131
    ## beta2  1.3034  1.5542  1.690  1.8382  2.1318
    ## beta3 -5.0898 -4.7805 -4.622 -4.4646 -4.1716

Lastly, we will check the sensitivity of our prior by specifying a new
prior for $\beta_0$, $\beta_1$, $\beta_2$, and $\beta_3$. Lets try to
use the Gaussian prior with mean 0 and variance 0.15 for the intercept,
while for the other 3 regression coefficient we will use Gaussian prior
with mean 0 and variance 1000. We ran again 13 chains with 10000 samples
after 5000 burn-in iterations and printed out the posterior summaries
for the parameter $\beta_0$, $\beta_1$, $\beta_2$, and $\beta_3$ using
$\verb|summary(model1.coda)|$ command.

``` r
# Input data and prior hyperparameter for each beta
fish.data <- list(n=nrow(fish),camper=fish$camper,livebait=fish$livebait,
                  prop.child=fish$prop.child,persons=fish$persons, count=fish$count,
                  mu.beta0=0,mu.beta1=0, mu.beta2=0, mu.beta3=0, prec.beta0=1, prec.beta1=1/1000,
                  prec.beta2=1/1000, prec.beta3=1/1000)

# Compile the model
model1.jags <- jags.model(file=textConnection(model1_string),data=fish.data,n.chains=13,quiet=T)

# Burnin 5000 iterations
update(model1.jags, n.iter=5000)

# Generate posterior sample
model1.coda <- coda.samples(model1.jags,n.iter=10000,variable.names=model_param)

# Posterior sample summary after change the prior
summary(model1.coda)
```

    ## 
    ## Iterations = 6001:16000
    ## Thinning interval = 1 
    ## Number of chains = 13 
    ## Sample size per chain = 10000 
    ## 
    ## 1. Empirical mean and standard deviation for each variable,
    ##    plus standard error of the mean:
    ## 
    ##         Mean      SD  Naive SE Time-series SE
    ## beta0 -1.305 0.21798 0.0006046      0.0062421
    ## beta1  0.929 0.08801 0.0002441      0.0008767
    ## beta2  1.719 0.21532 0.0005972      0.0060652
    ## beta3 -4.915 0.25333 0.0007026      0.0009969
    ## 
    ## 2. Quantiles for each variable:
    ## 
    ##          2.5%     25%     50%     75%   97.5%
    ## beta0 -1.7459 -1.4506 -1.3010 -1.1592 -0.8848
    ## beta1  0.7596  0.8691  0.9282  0.9872  1.1048
    ## beta2  1.3021  1.5743  1.7149  1.8609  2.1614
    ## beta3 -5.4199 -5.0841 -4.9106 -4.7413 -4.4291

From the output above, we can see that the posterior standard deviations
are typically much smaller than the posterior means in absolute value,
indicating that the the amount of data is sufficient to fit the model
parameters with some degree of confidence. Furthermore, we can see that
all regression parameters have time series SE that is much smaller than
the posterior means (in absolute value), showing that all of our
estimates are rather accurate. It appears that as we increased the
variance parameter for the Gaussian prior of the regression coefficient
parameters, the posterior standard deviations and time series SE is
still much more smaller than the posterior means (in absolute values).

As we can see from either the $\verb|gelman.diag|$ or
$\verb|gelman.plot|$ results after we use a new prior for our parameter
of interest, the Gelman-Rubin diagnostics values are below 1.05 for each
of the regression parameters, indicating that we have approximated the
stationary distribution quite well.

``` r
# Gelman rubin plot after change the prior
gelman.plot(model1.coda[,c('beta0','beta1')])
```

![](assignment-2_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

``` r
gelman.plot(model1.coda[,c('beta2','beta3')])
```

![](assignment-2_files/figure-gfm/unnamed-chunk-11-2.png)<!-- -->

``` r
# Gelman rubin statistics after change the prior
gelman.diag(model1.coda)
```

    ## Potential scale reduction factors:
    ## 
    ##       Point est. Upper C.I.
    ## beta0       1.01       1.01
    ## beta1       1.00       1.00
    ## beta2       1.01       1.01
    ## beta3       1.00       1.00
    ## 
    ## Multivariate psrf
    ## 
    ## 1.01

In our code in part b), we ran 13 chains with 10000 samples after 5000
burn-in iterations but this time we use a new prior for our parameter of
interest. We have computed the ESS for the model parameters $\beta_0$,
$\beta_1$, $\beta_2$, and $\beta_3$ using the $\verb|effectiveSize|$
function. The ESS is above 1000 for each of them. It seems that the new
prior that we specified for the model parameters $\beta_0$, $\beta_1$,
$\beta_1$, $\beta_2$, and $\beta_3$ does not make the ESS below 1000.

``` r
# Effective sample size after change the prior
effectiveSize(model1.coda)
```

    ##     beta0     beta1     beta2     beta3 
    ##  1227.486 10076.010  1266.659 64720.269

Lets have a look at the trace plot of the parameter $\beta_0$,
$\beta_1$, $\beta_2$, and $\beta_3$ using the $\verb|R|$ code below
after we specified a new prior for these four parameter. From the trace
plot below, we can see that the chain for the parameter $\beta_0$,
$\beta_1$, $\beta_2$, and $\beta_3$ were mixing well and have converged.

``` r
# Plot trace plot and density plot after change the prior
plot(model1.coda[,c('beta0','beta1')])
```

![](assignment-2_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

``` r
plot(model1.coda[,c('beta2','beta3')])
```

![](assignment-2_files/figure-gfm/unnamed-chunk-13-2.png)<!-- -->

In summary, the new prior that we specified by increasing the value of
the variance parameter that we used in our Gaussian prior for the
coefficient parameters does not make the posterior standard deviation
and time series SE for the regression parameters $\beta_0$, $\beta_1$,
$\beta_2$, and $\beta_3$ greater than the posterior means (in absolute
values). Therefore, we can said that the amount of data is sufficient to
fit the model parameters with some degree of confidence and our
estimates for all of these four parameters are rather accurate and the
chains was mixing reasonably well even thought the values of the
variance parameter for the Gaussian prior for the coefficient parameter
is increased.

**d)\[10 marks\] A closer observation of the number of zeros in the
dataset reveals that they are higher than expected. A plausible
explanation for this is that some groups went to the park, but did not
go fishing at all. To better model this, we consider the zero-inflated
Poisson distribution. This is a mixture of a distribution taking 0 with
probability 1 with weight** $w$, and a Poisson distribution with weight
$1-w$ (see <https://en.wikipedia.org/wiki/Zero-inflated_model> for more
information).

**Implement the zero-inflated version of the model from part c) in JAGS.
Use a uniform prior for the weight, and the same priors for the
regression coefficients as in part c). \[Hint: you can use the dbern or
dcat distributions in JAGS as part of this. In order to avoid the
incompatible error in JAGS, you may need to approximate Poisson
distribution with parameter 0 by a Poisson distribution with a small
parameter such as 0.00001.\]**

**Run 5000 burn-in steps, and obtain samples from the weight parameter**
$w$ **and the regression coefficients, including the intercept). Compute
and print out the effective sample sizes (ESS) for these 5 parameters.**

**If the ESS is below 1000 for any of these 5 parameters, increase the
sample size/number of chains until the ESS is above 1000 for all of
them.**

**Print out the summary of the model. Interpret the posterior summaries
of the model parameters.**

Explanation:

In this part, we will formulate our Bayesian zero-inflated Poisson GLM
to estimates the number of fish that was caught. Assume that the number
of fish that was caught have zero-inflated Poisson distribution. Thus,
we will have
$$\text{Pr}(\text{count}=y_i)=\begin{cases}w+(1-w)e^{-\lambda}, \quad y_i = 0\\(1-w)\dfrac{\lambda^{y_i}e^{-\lambda}}{y_i!}, \quad y_i = 1,2,\dots\end{cases}$$where
$y_i$ is a non-negative integer that represents the observations for the
number of fish that was caught, $\lambda$ is the average number of fish
that was caught, and $w$ is the probability of extra zeros. The mean and
variance of the zero-inflated Poisson distribution is $w(1-\lambda)$ and
$w(1-\lambda)(1+w\lambda)$ respectively.

Now lets formulate our Bayesian zero-inflated poisson GLM. First we need
to decide what are the prior that we are going to use for the parameters
$\beta_0$, $\beta_1$, $\beta_2$, $\beta_3$, and $w$. Recall that the
parameters $\beta_0$, $\beta_1$, $\beta_2$, and $\beta_3$ is the
regression parameters. We choose to used the same prior in part b) for
these four parameters. As for the parameters $w$, we will use the
uniform distribution prior $U(0,1)$ since the parameters $w$ is a
probability and the observed values that we can obtained from the
uniform distribution $U(0,1)$ will lies in the interval $[0,1]$ which is
make sense for the values of a probability. In order to avoid
incompatibility error in JAGS, we need to approximate the Poisson
distribution with parameter 0 by a Poisson distribution with smaller
parameter $\lambda$. Let $z\sim\text{Bernoulli}(w)$ and $\mu$ be the
parameter of a Poisson distribution such as $\mu\approx\lambda$ or
$\mu\approx0$. In this report, we let $\mu = \lambda z+0.00001$ to
ensure that the Poisson distribution with parameter $\mu$ have a very
close approximation to a Poisson distribution with parameter $\lambda$
or 0. Since $z\sim\text{Bernoulli}(w)$, then the possible values of $z$
is either 0 or 1. Therefore, we can have either $\mu\approx0$ or
$\mu\approx\lambda$. Let
$$\mathbf{x}_i = \left(\text{camper}_i, \text{livebait}_i, \text{prop.child}_i, \text{persons}_i\right),$$where
$\text{camper}_i$, $\text{livebait}_i$, $\text{prop.child}_i$, and
$\text{persons}_i$ each represent the i-th values of the observations
for the camper, livebait, prop.child, and persons variable respectively
for $i = 1,2,\dots,250$. Recall that there are 250 groups in the
$\verb|fish.csv|$ dataset.The Bayesian zero-inflated Poisson GLM can be
formulated as follows:$$\begin{aligned}
\text{count}_i|\mu_i, \mathbf{x}_i&\sim
\text{Poisson}(\mu_i), \quad i = 1,2,\dots, 250\\
\mu_i &= \lambda_iz_i+0.00001\\
z_i &\sim \text{Bernoulli}(w)\\
\log{(\lambda_i)} &= \beta_0+\beta_1\text{camper}_i+\beta_2\text{livebait}_i+\beta_3\text{prop.child}_i+\log{(\text{persons}_i)}\\
w &\sim U(0,1)\\
\beta_0 &\sim \text{N}(\mu_0 = 0, \sigma^2_0 = 100)\\
\beta_1 &\sim \text{N}(\mu_1 = 0, \sigma^2_1 = 1)\\
\beta_2 &\sim \text{N}(\mu_2 = 0, \sigma^2_2 = 1)\\
\beta_3 &\sim \text{N}(\mu_3 = 0, \sigma^2_3 = 1)
\end{aligned}$$

The $\verb|R|$ code below implement our Bayesian zero-inflated Poisson
GLM that we have already formulated in this part. We ran 13 chains with
10000 samples after 5000 burn-in iterations.

``` r
# Input data and prior hyperparameter for each beta
fish.data <- list(n=nrow(fish),camper=fish$camper,livebait=fish$livebait,
                  prop.child=fish$prop.child,persons=fish$persons, count=fish$count,
                  mu.beta0=0,mu.beta1=0, mu.beta2=0, mu.beta3=0, prec.beta0=1/100, prec.beta1=1,
                  prec.beta2=1, prec.beta3=1)

# Create model block for JAGS
model2_string <- "model {
# Data that will be read in are n, count, camper, livebait, prop.child and persons

# Prior for each parameter beta and the weight (w)
beta0 ~ dnorm(mu.beta0,prec.beta0)
beta1 ~ dnorm(mu.beta1,prec.beta1)
beta2 ~ dnorm(mu.beta2,prec.beta2)
beta3 ~ dnorm(mu.beta3,prec.beta3)
w ~ dunif(0,1)

#Likelihood
for(i in 1:n) {

# Poisson GLM
log(lambda[i]) <- beta0+beta1*camper[i]+beta2*livebait[i] +beta3*prop.child[i]+log(persons[i])

#Zero-inflated Poisson model
z[i] ~ dbern(w)
mu[i] <- lambda[i]*z[i] + 0.00001

# Observations
count[i] ~ dpois(mu[i])

# Replicates
count.rep[i] ~ dpois(mu[i])}
}"

# Compile the model
model2 <- jags.model(file=textConnection(model2_string),data=fish.data,n.chains=13,quiet = T)

# Burnin 5000 iterations
update(model2, n.iter=5000)

# Generate posterior sample
model_param <- c("beta0","beta1","beta2", "beta3", "w")
model2.samps <- coda.samples(model2,variable.names=model_param,n.iter=10000)
```

As we can see from either the $\verb|gelman.diag|$ or
$\verb|gelman.plot|$ results, the Gelman-Rubin diagnostics values are
below 1.05 for each of the parameters of interest in our posterior
sample, indicating that we have approximated the stationary distribution
quite well.

``` r
# Gelman rubin plot
gelman.plot(model2.samps[,c('beta0','beta1')])
```

![](assignment-2_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

``` r
gelman.plot(model2.samps[,c('beta2','beta3')])
```

![](assignment-2_files/figure-gfm/unnamed-chunk-15-2.png)<!-- -->

``` r
gelman.plot(model2.samps[,c('w')], main = 'w')
```

![](assignment-2_files/figure-gfm/unnamed-chunk-15-3.png)<!-- -->

``` r
# Gelman rubin statistics
gelman.diag(model2.samps)
```

    ## Potential scale reduction factors:
    ## 
    ##       Point est. Upper C.I.
    ## beta0          1       1.01
    ## beta1          1       1.00
    ## beta2          1       1.01
    ## beta3          1       1.00
    ## w              1       1.00
    ## 
    ## Multivariate psrf
    ## 
    ## 1.01

In our zero-inflated Poisson JAGS code attached in this part, we ran 13
chains with 10000 samples after 5000 burn-in iterations. We have
computed the ESS (Effective Sample Size) for the model parameters $w$,
$\beta_0$, $\beta_1$, $\beta_2$, and $\beta_3$ using the
$\verb|effectiveSize|$ function. The ESS is above 1000 for each of them,
so no further samples are needed.

``` r
# get effective sample size
effectiveSize(model2.samps)
```

    ##     beta0     beta1     beta2     beta3         w 
    ##  1077.912  8645.859  1113.213 34595.152 48467.355

Lets have a look at the trace plot of the regression parameter $w$,
$\beta_0$, $\beta_1$, $\beta_2$, and $\beta_3$ using the $\verb|R|$ code
below. From the trace plot below, we can see that the chain for the
parameter $w$, $\beta_0$, $\beta_1$, $\beta_2$, and $\beta_3$ were
mixing well and have converged.

``` r
# Plot trace plot and density plot
par(mar=c(3,3,3,3))
plot(model2.samps[,c('w','beta0','beta1')])
```

![](assignment-2_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

``` r
plot(model2.samps[,c('beta2','beta3')])
```

![](assignment-2_files/figure-gfm/unnamed-chunk-17-2.png)<!-- -->

Next, we printed out the posterior summaries for the parameters $w$,
$\beta_0$, $\beta_1$, $\beta_2$, and $\beta_3$ using the
$\verb|summary(model2.samps)|$ command. We can see that the posterior
standard deviations for these five parameters are typically much smaller
that the posterior means in absolute value, indicating that the amount
of data is sufficient to fit the model parameters with some degree of
confidence. The time series SE of all these five parameters are less
than the posterior means (in absolute value), showing our estimates for
all of these five parameters are rather accurate and the chains was
mixing reasonably well as the trace plot or Gelman-Rubin diagnostic plot
suggested.

``` r
# Posterior sample summary
summary(model2.samps)
```

    ## 
    ## Iterations = 6001:16000
    ## Thinning interval = 1 
    ## Number of chains = 13 
    ## Sample size per chain = 10000 
    ## 
    ## 1. Empirical mean and standard deviation for each variable,
    ##    plus standard error of the mean:
    ## 
    ##          Mean      SD  Naive SE Time-series SE
    ## beta0 -0.7986 0.23475 0.0006511      0.0072202
    ## beta1  0.6829 0.09472 0.0002627      0.0010204
    ## beta2  1.6667 0.23269 0.0006454      0.0070768
    ## beta3 -3.6264 0.29846 0.0008278      0.0016076
    ## w      0.5316 0.03918 0.0001087      0.0001783
    ## 
    ## 2. Quantiles for each variable:
    ## 
    ##          2.5%     25%     50%     75%   97.5%
    ## beta0 -1.2693 -0.9540 -0.7955 -0.6383 -0.3513
    ## beta1  0.5004  0.6189  0.6819  0.7458  0.8715
    ## beta2  1.2262  1.5070  1.6616  1.8202  2.1396
    ## beta3 -4.2124 -3.8279 -3.6272 -3.4240 -3.0416
    ## w      0.4555  0.5051  0.5312  0.5578  0.6094

**e)\[10 marks\]**

**Compare the quality of the model fit for the two models via DIC
scores.**

**Perform posterior predictive checks for both models for 3 functions:**

**1. number of groups catching no fish,**

**2. number of groups catching more than 5 fish,**

**3. average number of fish caught among groups who brought a camper
van.**

**Discuss your results.**

Explanation:

First, we will perform posterior predictive checks on the Bayesian
Poisson GLM model in part b). The histograms below show posterior
predictive distribution for the average number of fish caught among
groups who brought a camper van (right plot on first row), number of
groups catching no fish (left plot on first row), and number of groups
catching more than 5 fish (right plot on second row) for the Bayesian
fit to the number of fish that was caught. The descriptive statistic
values (the average number of fish caught among groups who brought a
camper van, number of groups catching no fish, and number of groups
catching more than 5 fish) in the observed dataset are shown by vertical
red lines. The lines seem to be within the typical range of the
replicates for the posterior predictive distribution of the average
number of fish that was caught among groups who brought a camper van,
while in the case of the posterior predictive distributions of the
number of groups catching no fish and the number of groups catching more
than 5 fish are lies outside the typical ranges of the replicates. This
indicates that there is an issues with the priors that was used Poisson
GLM in part b) that have been detected by this posterior predictive
checks when predicting the posterior predictive distributions for the
number of groups catching no fish and the number of groups catching more
than 5 fish .

``` r
library(fBasics)

# Generate replicate observations
res1.replicates <- coda.samples(model1,variable.names=c("count.rep"),n.iter=10000,progress.bar="none")

countrep <- as.matrix(res1.replicates)

# Compute the required data for posterior predictive checks
ind.camper <- which(fish$camper==1)
ind.count0 <- which(fish$count==0)
ind.count5.more <- which(fish$count > 5)

count.camper <- fish[ind.camper,'count']
countrep.camper <- countrep[,ind.camper]

countrep.camper.mean <- apply(countrep.camper,1,mean)

count0 <- fish[ind.count0,'count']
countrep0 <- countrep[,ind.count0]

countrep0.count <- rowSums(countrep==0)

countrep5.great.count <- rowSums(countrep>5)

m1 <- max(countrep.camper.mean,mean(fish$count[ind.camper]))
m2 <- max(countrep0.count,length(ind.count0))
m3 <- max(countrep5.great.count,length(ind.count5.more))

# Plot the posterior predictive distribution histogram
par(mfrow=c(2,2))
hist(countrep.camper.mean,col="gray40",xlim=c(0,m1),cex.main = 0.75,
     main='Predictive Distribution Capture Fish (Camper)')
abline(v = mean(fish$count[ind.camper]),col='red',lwd=2)

hist(countrep0.count,col="gray40",xlim=c(0,m2),cex.main = 0.75,
     main='Predictive Distribution Groups Capture No Fish')
abline(v = length(ind.count0),col='red',lwd=2)

hist(countrep5.great.count,col="gray40",xlim=c(0,m3),cex.main = 0.75,
     main='Predictive Distribution Groups Capture >5 Fish')
abline(v = length(ind.count5.more),col='red',lwd=2)
```

![](assignment-2_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

Next, we will perform posterior predictive checks on the Bayesian
zero-inflated Poisson GLM model in part d). The histograms below show
posterior predictive distribution for the average number of fish caught
among groups who brought a camper van (right plot on first row), number
of groups catching no fish (left plot on first row), and number of
groups catching more than 5 fish (right plot on second row) for the
Bayesian fit to the number of fish that was caught. The descriptive
statistic values (the average number of fish caught among groups who
brought a camper van, number of groups catching no fish, and number of
groups catching more than 5 fish) in the observed dataset are shown by
vertical red lines. The lines seem to be within the typical range of the
replicates for the posterior predictive distribution of the average
number of fish that was caught among groups who brought a camper van and
the posterior predictive distributions of the number of groups catching
no fish, while in the case of the posterior predictive distributions of
the number of groups catching more than 5 fish are lies outside the
typical ranges of the replicates. This indicates that there is an issues
with the priors that was used in the zero-inflated Poisson GLM in part
d) that have been detected by this posterior predictive checks when
predicting the posterior predictive distributions for the number of
groups catching more than 5 fish.

``` r
# Generate replicate samples
res2.replicates <- coda.samples(model2,variable.names=c("count.rep"), n.iter=10000,progress.bar="none")
countrep <- as.matrix(res2.replicates)

# Compute required data for posterior predictive checks
ind.camper <- which(fish$camper==1)
ind.count0 <- which(fish$count==0)
ind.count5.more <- which(fish$count > 5)

count.camper <- fish[ind.camper,'count']
countrep.camper <- countrep[,ind.camper]

countrep.camper.mean <- apply(countrep.camper,1,mean)

count0 <- fish[ind.count0,'count']
countrep0 <- countrep[,ind.count0]

countrep0.count <- rowSums(countrep==0)

countrep5.great.count <- rowSums(countrep>5)

m1 <- max(countrep.camper.mean,mean(fish$count[ind.camper]))
m2 <- max(countrep0.count,length(ind.count0))
m3 <- max(countrep5.great.count,length(ind.count5.more))

# Plot the posterior predictive probability histogram
par(mfrow=c(2,2))
hist(countrep.camper.mean,col="gray40",xlim=c(0,m1),cex.main = 0.75,
     main='Predictive Distribution Capture Fish (Camper)')
abline(v = mean(fish$count[ind.camper]),col='red',lwd=2)

hist(countrep0.count,col="gray40",xlim=c(0,m2),cex.main = 0.75,
     main='Predictive Distribution Groups Capture No Fish')
abline(v = length(ind.count0),col='red',lwd=2)

hist(countrep5.great.count,col="gray40",xlim=c(0,m3),cex.main = 0.75,
     main='Predictive Distribution Groups Capture >5 Fish')
abline(v = length(ind.count5.more),col='red',lwd=2)
```

![](assignment-2_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

Lastly, we will compute the DIC score for the Bayesian Poisson GLM in
part b) and the Bayesian zero-inflated Poisson GLM in part d) using the
function $\verb|dic.samples()|$ in the $\verb|R|$ code below.

``` r
# DIC score for original Poisson GLM
dic.samples(model1, n.iter=10000)
```

    ## Mean deviance:  1923 
    ## penalty 3.935 
    ## Penalized deviance: 1927

``` r
# DIC score for Zero-Inflated Poisson GLM
dic.samples(model2, n.iter=10000)
```

    ## Mean deviance:  1382 
    ## penalty 261.1 
    ## Penalized deviance: 1643

From the output above, we can see that the DIC score for the Bayesian
zero-inflated Poisson GLM in part d) is lower than the DIC score for the
Poisson GLM in part b), which indicates that the Bayesian zero-inflated
Poisson GLM in part d) is fits better on the data compared to the
Bayesian Poisson GLM in part b).

<img src="money.jpg" style="width:100.0%" />

**Problem 2 - Personal loans data**

**In this problem, we are going to analyze some personal loans data from
a US bank named LendingClub.**

**The dataset contains information about 188181 personal loans in the US
whose term has already completed.**

**The column that we aim to model is loan.status, which is either
’’Fully Paid”, or “Charged Off”. In our response variable** $y$**, value
1 will to “Charged Off”, while value 0 corresponds to “Fully paid”.
Hence we are modelling whether or not the client defaulted on their
loan.**

**The other columns in the dataset are**

**loan.amnt: The amount of principle given in the loan in USD**

**interest.rate: The interest rate assigned to the loan by LendingClub**

**sub.grade: A grade assigned to the loan internally by LendingClub**

**annual.income: The lendee’s annual income in USD**

**debt.to.income: The lendee’s debt-to-income ratio. This explains what
percent of the client’s income is spent on loans each month before
taking out this new personal loan (such as mortgage, rent, car loan,
etc., see
<https://www.lendingclub.com/loans/resource-center/calculating-debt-to-income>)**

**state, the US state in which the borrower lives (in a 2 letter
abbreviated format)**

**term, the term of the loan, i.e. the number of months in which it has
to be paid off**

**loan.status: The final status, either “Paid” or “Charged Off”, of the
loan**

**We are going to use INLA to fit several different logistic regression
models to this dataset. First, we load ILNA and the dataset and display
the first few rows.**

``` r
rm(list=ls()) # Empty memory used in question 1
library(INLA)

#If it loaded correctly, you should see this in the output:
#Loading required package: Matrix
#Loading required package: foreach
#Loading required package: parallel
#Loading required package: sp
#This is INLA_21.11.22 built 2021-11-21 16:13:28 UTC.
# - See www.r-inla.org/contact-us for how to get help.
# - To enable PARDISO sparse library; see inla.pardiso()

#The following code does the full installation. You can try it if INLA has not been installed.
#First installing some of the dependencies
#install.packages("BiocManager")
#BiocManager::install("Rgraphviz")
#if (!requireNamespace("BiocManager", quietly = TRUE))
#    install.packages("BiocManager")
#BiocManager::install("graph")
#Installing INLA
#install.packages("INLA",repos=c(getOption("repos"),INLA="https://inla.r-inla-download.org/R/stable"), dep=TRUE)
#library(INLA)
```

``` r
lending <- read.csv(file = 'lending.csv')
head(lending)
```

    ##   loan.amount interest.rate sub.grade annual.income debt.to.income loan.status
    ## 1       12000        11.99%        B3        130000         13.03%  Fully Paid
    ## 2       15000         8.90%        A5         63000         16.51%  Fully Paid
    ## 3       24000        13.53%        B5        100000         22.18%  Fully Paid
    ## 4       12000        13.53%        B5         40000         16.94%  Fully Paid
    ## 5       10000         9.67%        B1        102000         15.55%  Fully Paid
    ## 6       11100        14.98%        C3         90000          3.73%  Fully Paid
    ##   state       term
    ## 1    CO  36 months
    ## 2    FL  36 months
    ## 3    MI  36 months
    ## 4    NM  36 months
    ## 5    MA  36 months
    ## 6    NY  36 months

**a)\[10 marks\]**

**In this question, we are going to fit a logistic GLM on the dataset.
First, we need to do some data manipulation.**

**Create a response column y such that** $y=1$ **corresponds to
loan.status being “Charged Off”, and** $y=0$ **corresponds to
loan.status being “Paid”.**

**Convert the interest.rate and debt.to.income columns from strings into
numbers \[Hint: you can use the str_replace_all function from the
stringr library to get rid of the % signs\].**

**Create new columns for the logarithm of the loan amount, the logarithm
of the interest rate, the logarithm of the annual income.**

**Scale these 3 columns (i.e. center them and divide them by their
standard deviation). Also scale the debt-to-income column (but do not
apply log transformation).**

**Fit a logistic GLM on the response y as a function of the scaled log
interest rate, scaled log annual income, scaled log loan amount, scaled
debt-to-income, sub.grade, and term (sub.grade and term can be kept
categorical). Interpret the results.**

Explanation:

Before we begin analyze our data, we will start by introducing the
terminology of a defaulted loans and charge-off that we are going to use
in this report. Default is the failure to repay a debt, including
interest or principal, on a loan or security. A default can occur when a
borrower is unable to make timely payments, misses payments, or avoids
or stops making payments. Individuals, businesses, and even countries
can default if they cannot keep up their debt obligations. The reference
that I use to explain the terminology defaulted loan is cited from this
following link: <https://www.investopedia.com/terms/d/default2.asp>.

Meanwhile, charge-off refers to debt that a company believes it will no
longer collect as the borrower has become delinquent on payments.
Charged-off debt does not mean that the consumer does not have to repay
the debt anymore. After a lender has charged off a debt, it could sell
the debt to a third-party collections agency that would attempt to
collect on the delinquent account. A consumer owes the debt until it is
paid off, settled, discharged in a bankruptcy proceeding, or in case of
legal proceedings, becomes too old due to the statute of limitations.
The reference that I used to explained the charge-off terminology is
cited from this following link:
[https://www.investopedia.com/terms/c/chargeoff.asp.](https://www.investopedia.com/terms/c/chargeoff.asp#:~:text=A%20charge%2Doff%20refers%20to,to%20repay%20the%20debt%20anymore.)

In this part, we will fit a logistic GLM with the binary response
variable is the loan status and the explanatory variables are the
logarithm of interest rate, logarithm of annual income, logarithm of
loan amount, debt-to-income ratio, grade assigned to the loan, and the
term of the loan. Before we fit the data of the response and explanatory
variables, we will do some data manipulation. First, we will convert the
loan status variable into a binary variable by converting the loan
status “Charged Off” into 1 and the loan status “Fully Paid” into 0.
Next, we will convert the interest rate and debt-to-income ratio by
removing the “%” pattern from the data using $\verb|str_replace_all()|$
function in $\verb|R|$ and then convert the variable into a numeric
variable by using the $\verb|as.numeric()|$ function in $\verb|R|$.
After that, we calculate the logarithm of the loan amount, the logarithm
of the interest rate, and the logarithm of the annual income using the
$\verb|log()|$ function in $\verb|R|$. We add this three variable to the
data and scale the data (centering the data by the means then divide by
the standard deviations) using the $\verb|scale()|$ function in
$\verb|R|$. In addition, we will also used the $\verb|scale()|$ function
on the debt-to-income data but we would not use log transformations on
these data. Lastly, we will fit our logistic GLM model using the
$\verb|R|$ code below.

``` r
library(stringr)

# Create response column y
lending$y <- ifelse(lending$loan.status=="Charged Off",1,0)

# Extract numbers from interest rate and debt-to-income
lending$interest.rate <- as.numeric(str_replace_all(lending$interest.rate,"%", ""))
lending$debt.to.income <- as.numeric(str_replace_all(lending$debt.to.income,"%", ""))

# Create logarithm on loan amount, interest rate, and annual income
lending$log.loan.amount <- log(lending$loan.amount)
lending$log.interest.rate <- log(lending$interest.rate)
lending$log.annual.income <- log(lending$annual.income)

# Scale the converted log column and debt-to-income
lending$log.loan.amount <- scale(lending$log.loan.amount)
lending$log.interest.rate <- scale(lending$log.interest.rate)
lending$log.annual.income <- scale(lending$log.annual.income)
lending$debt.to.income <- scale(lending$debt.to.income)

# Logistic GLM model
m1.logit <- glm(y~log.interest.rate+log.annual.income+log.loan.amount+debt.to.income+sub.grade+term,
                data = lending, family = binomial)
summary(m1.logit)
```

    ## 
    ## Call:
    ## glm(formula = y ~ log.interest.rate + log.annual.income + log.loan.amount + 
    ##     debt.to.income + sub.grade + term, family = binomial, data = lending)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.2531  -0.6324  -0.4904  -0.3457   2.8634  
    ## 
    ## Coefficients:
    ##                    Estimate Std. Error z value Pr(>|z|)    
    ## (Intercept)       -3.291996   0.216234 -15.224  < 2e-16 ***
    ## log.interest.rate  0.011836   0.080788   0.147  0.88352    
    ## log.annual.income -0.283867   0.008275 -34.302  < 2e-16 ***
    ## log.loan.amount    0.145856   0.008652  16.858  < 2e-16 ***
    ## debt.to.income     0.078952   0.006800  11.611  < 2e-16 ***
    ## sub.gradeA2        0.180632   0.121990   1.481  0.13868    
    ## sub.gradeA3        0.437717   0.124095   3.527  0.00042 ***
    ## sub.gradeA4        0.694329   0.121156   5.731 9.99e-09 ***
    ## sub.gradeA5        0.810250   0.136982   5.915 3.32e-09 ***
    ## sub.gradeB1        0.914577   0.154554   5.918 3.27e-09 ***
    ## sub.gradeB2        1.005759   0.173317   5.803 6.51e-09 ***
    ## sub.gradeB3        1.096628   0.191249   5.734 9.81e-09 ***
    ## sub.gradeB4        1.277451   0.207295   6.162 7.16e-10 ***
    ## sub.gradeB5        1.392832   0.221342   6.293 3.12e-10 ***
    ## sub.gradeC1        1.419330   0.227347   6.243 4.29e-10 ***
    ## sub.gradeC2        1.464603   0.240091   6.100 1.06e-09 ***
    ## sub.gradeC3        1.615127   0.248818   6.491 8.52e-11 ***
    ## sub.gradeC4        1.689473   0.256823   6.578 4.76e-11 ***
    ## sub.gradeC5        1.731184   0.269296   6.429 1.29e-10 ***
    ## sub.gradeD1        1.814751   0.277534   6.539 6.20e-11 ***
    ## sub.gradeD2        1.877746   0.286405   6.556 5.52e-11 ***
    ## sub.gradeD3        1.901931   0.292001   6.513 7.34e-11 ***
    ## sub.gradeD4        1.986315   0.297275   6.682 2.36e-11 ***
    ## sub.gradeD5        1.922989   0.306068   6.283 3.32e-10 ***
    ## sub.gradeE1        1.969282   0.315074   6.250 4.10e-10 ***
    ## sub.gradeE2        2.117495   0.320845   6.600 4.12e-11 ***
    ## sub.gradeE3        2.096305   0.327251   6.406 1.50e-10 ***
    ## sub.gradeE4        2.147414   0.333104   6.447 1.14e-10 ***
    ## sub.gradeE5        2.195430   0.338579   6.484 8.92e-11 ***
    ## sub.gradeF1        2.149179   0.344549   6.238 4.44e-10 ***
    ## sub.gradeF2        2.320966   0.349015   6.650 2.93e-11 ***
    ## sub.gradeF3        2.334287   0.353903   6.596 4.23e-11 ***
    ## sub.gradeF4        2.420862   0.358415   6.754 1.43e-11 ***
    ## sub.gradeF5        2.406711   0.361484   6.658 2.78e-11 ***
    ## sub.gradeG1        2.562936   0.371996   6.890 5.59e-12 ***
    ## sub.gradeG2        2.247266   0.381928   5.884 4.00e-09 ***
    ## sub.gradeG3        2.615114   0.390856   6.691 2.22e-11 ***
    ## sub.gradeG4        2.103986   0.419345   5.017 5.24e-07 ***
    ## sub.gradeG5        2.227437   0.430541   5.174 2.30e-07 ***
    ## term 60 months     0.339471   0.017890  18.975  < 2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 164015  on 188180  degrees of freedom
    ## Residual deviance: 153242  on 188141  degrees of freedom
    ## AIC: 153322
    ## 
    ## Number of Fisher Scoring iterations: 5

We display our fitted logistic GLM summary statistics using the
$\verb|summary(m1.logit)|$ command. We obtained our estimates for the
intercept parameter is -3.291996. Thus, we can said that the probability
of the loan status is defaulted by the clients is exp(-3.291996)
(approximately 3.72%) times the probability of the loan status is not
defaulted by the clients when the values of all the numerical variable
observations is zero and the observations of all categorical variable
are at the reference category. Therefore, we can said that the
probability of the loan status is defaulted by the clients is lower than
the the probability of the loan status is not defaulted by the clients
under the assumptions when the values of all the numerical variable
observations is zero and the observations of all categorical variable
are at the reference category. Now lets interpret the other estimated
parameter for the coefficient of the numerical variable in our logistic
GLM model.

We can see that the estimated coefficient parameters for the logarithm
of the interest rate is 0.011836. This implies that the probability of
the loan status is defaulted by the clients is exp(0.011836)
(approximately 1.01) times the probability of the loan status is not
defaulted by the clients for every increase the value of the logarithm
of interest rate by 1 unit assuming all other explanatory variables
remain constant.

Now lets interpret the estimated coefficient parameters on the logarithm
of annual income variables. We can see that the estimated coefficient
parameters for the logarithm of the annual income is -0.283867. This
implies that the probability of the loan status is defaulted by the
clients is exp(-0.283867) (approximately 0.75) times the probability of
the loan status is not defaulted by the clients for every increase the
value of the logarithm of annual income by 1 unit assuming all other
explanatory variables remain constant.

Next, lets interpret the estimated coefficient parameters on the
logarithm of loan amount variables. We can see that the estimated
coefficient parameters for the logarithm of the loan amount is 0.145856.
This implies that the probability of the loan status is defaulted by the
clients is exp(0.145856) (approximately 1.16) times the probability of
the loan status is not defaulted by the clients for every increase the
value of the logarithm of loan amount by 1 unit assuming all other
explanatory variables remain constant.

Lastly lets interpret the estimated coefficient parameters on the
debt-to-income variables. We can see that the estimated coefficient
parameters for the debt-to-income is 0.078952. This implies that the
probability of the loan status is defaulted by the clients is
exp(0.078952) (approximately 1.08) times the probability of the status
is not defaulted by the clients for every increase the value of the
debt-to-income by 1 unit assuming all other explanatory variables remain
constant.

Recall that the loans are classified by grade (A through G) and
sub-grade (1 through 5). As for the estimated coefficient for the dummy
variable of the sub-grade categorical variable, we can see that as the
grade increased from A (lowest risk) to G (highest risk), the estimated
coefficient of each sub-grade in each grade increased. As the estimated
coefficient increased, then the risk of a loan will be defaulted becomes
higher than the loan will be un-defaulted. Therefore, we can said that
loan in the grade G will have higher probability of being defaulted,
while loan from grade A will have lower probability of being defaulted.
The description about the loan grade can be find in this following link:
<https://www.marlo.online/loan-grades>.

As for the terms variable, we can see that when the loan terms is 60
months, then the probability of the loan being defaulted will be
exp(0.339471) (approximately 1.404) times the probability of a loan
being un-defaulted when other explanatory variables remained constant.

The exponential values of the regression parameters that we are using
here is provided by the $\verb|R|$ code below.

``` r
#exp(beta)where beta is regression parameter
exp(coef(m1.logit))
```

    ##       (Intercept) log.interest.rate log.annual.income   log.loan.amount 
    ##        0.03717958        1.01190615        0.75286658        1.15702922 
    ##    debt.to.income       sub.gradeA2       sub.gradeA3       sub.gradeA4 
    ##        1.08215207        1.19797451        1.54916578        2.00236543 
    ##       sub.gradeA5       sub.gradeB1       sub.gradeB2       sub.gradeB3 
    ##        2.24847080        2.49571971        2.73398206        2.99405431 
    ##       sub.gradeB4       sub.gradeB5       sub.gradeC1       sub.gradeC2 
    ##        3.58748494        4.02623781        4.13434971        4.32582704 
    ##       sub.gradeC3       sub.gradeC4       sub.gradeC5       sub.gradeD1 
    ##        5.02852840        5.41662752        5.64733495        6.13954597 
    ##       sub.gradeD2       sub.gradeD3       sub.gradeD4       sub.gradeD5 
    ##        6.53875194        6.69881834        7.28862765        6.84137538 
    ##       sub.gradeE1       sub.gradeE2       sub.gradeE3       sub.gradeE4 
    ##        7.16553103        8.31029813        8.13604776        8.56268569 
    ##       sub.gradeE5       sub.gradeF1       sub.gradeF2       sub.gradeF3 
    ##        8.98386212        8.57781560       10.18550837       10.32210257 
    ##       sub.gradeF4       sub.gradeF5       sub.gradeG1       sub.gradeG2 
    ##       11.25555325       11.09740184       12.97385394        9.46183107 
    ##       sub.gradeG3       sub.gradeG4       sub.gradeG5    term 60 months 
    ##       13.66877539        8.19878298        9.27605960        1.40420499

We can evaluate our logistic GLM curve performance using the AUC score.
AUC represents the degree or measure of separability. It tells us how
much the model is capable of distinguishing categorical values between
classes (category in the response categorical variable). If the AUC
become higher, our model become much more better at predicting the
categorical variable values. By analogy, the higher the AUC, the better
the logistic GLM is at distinguishing between clients with the loan
status charged off and fully paid.

The area under the ROC curve (AUC) results were considered excellent for
AUC values between 0.9-1, good for AUC values between 0.8-0.9, fair for
AUC values between 0.7-0.8, poor for AUC values between 0.6-0.7 and
failed (very poor) for AUC values between 0.5-0.6.

In the ROC curves, we can see that the AUC score for the logistic GLM is
between 0.6 and 0.8, which suggest that our model is performs poor at
distinguishing between clients with the loan status charged off and
fully paid. Further references about an interpretation of AUC score can
be found in this following link:
[https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2935260/](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2935260/#:~:text=The%20area%20under%20the%20ROC,AUC%20values%20between%200.5%2D0.6.).

There are two metrics observed in the ROC curves: sensitivity and
specificity. Sensitivity (true positive rate) is the metric that
evaluates a prediction model’s ability to predict true positives (in our
case is charged off loan status) of each available category in our
binary response variable (loan status). On the other hands, specificity
(true negative rate) is the metric that evaluates a prediction model’s
ability to predict true negatives (in our case is fully paid loan
status) of each available category in our binary response variable (loan
status). Further reference about specificity and sensitivity can be
found in this following link:
<https://en.wikipedia.org/wiki/Sensitivity_and_specificity>

The $\verb|R|$ code below computes the AUC score and plot the ROC
curves.

``` r
library(pROC)
#plot ROC curve for the logistic GLM model
prob <- predict(m1.logit, newdata = lending, type = "response")
roc(loan.status ~ prob, data = lending, plot = T, print.auc = T, quiet = T, 
    main= 'Model 1 ROC Curve')
```

![](assignment-2_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->

    ## 
    ## Call:
    ## roc.formula(formula = loan.status ~ prob, data = lending, plot = T,     print.auc = T, quiet = T, main = "Model 1 ROC Curve")
    ## 
    ## Data: prob in 29671 controls (loan.status Charged Off) > 158510 cases (loan.status Fully Paid).
    ## Area under the curve: 0.6835

From to the ROC curve above we can see that as the performance of our
logistic GLM decreased in terms of identifying a client who have fully
paid loan status is decreased, the performance of our model in terms of
identifying the client who have charged off loan status is increased. In
the opposite, if the performance of our logistic GLM decreased in terms
of identifying a client who have charged off loan status is decreased,
the performance of our model in terms of identifying the client who have
fully paid loan status is increased.

**b)\[10 marks\] (Identical Model)**

**Implement a Bayesian logistic GLM of the same structure as in a) in
INLA \[Hint: use need to use the “binomial” family with Ntrials=1 to
indicate logistic regression in INLA, see
<https://rpubs.com/corey_sparks/431920> for an example).**

**Propose your own priors for the model parameters (you can take into
account slides 45-46 of Lecture 4).**

**Print out the model summary. Check the sensitivity of the results with
respect to the prior choices.**

**Compute DIC and negative log-CPO (NLSCPO).**

**Do posterior predictive checks with the functions being evaluated
chosen as the proportion of defaults among clients in each of the 49
states contained in the dataset \[Hint: plot these in a 7 x 7 format
using par(mfrow=c(7,7)). Make sure to write par(mfrow=c(1,1)) after your
plots to change back to the default setting\]. Discuss the model fit.**

Explanation:

In this part, we are going to implement the identical model, which in
this case is a Bayesian logistic GLM requiring only fixed effects. The
model used the same intercept for all the 49 states. First, we are going
to choose the prior for our regression parameters. Observe that in USA
there are six types of debt: personal loan, student loan, auto loan,
credit card, HELOC (Home Equity Lines of Credit), and mortgage. Overall,
mortgages by far represent the largest outstanding debt in the USA. The
average mortgage balance stands at \$208,185, and 44% of USA adults have
this type of debt.

As for the personal loans, nearly 25% of USA adults have this type of
debt, and personal loan average American debt stands at \$16,458. The
percentage of accounts that were 30 or more days past due decreased by
27% between 2019 and 2020.

The average debt of personal loans in 2020 is \$16,458, which is
significantly smaller than the average debt of mortgages in 2020 (which
is \$208,185). Compare to other consumer debts, personal loans continue
to make up the smallest sliver of consumer debt held by Americans
(around 0.9% of the total debt consumer in America), despite their
growth over the past decade.

The reference about debt in USA is provided in this following links:
[https://www.bankrate.com/personal-finance/debt/average-american-debt/](https://www.bankrate.com/personal-finance/debt/average-american-debt/#:~:text=Personal%20loan%20debt&text=Nearly%20a%20quarter%20of%20U.S.,percent%20between%202019%20and%202020.).
Furthermore, further reference about personal loans can be seen in this
following links:
<https://www.lendingtree.com/personal/personal-loans-statistics/>.

Since most American mostly have smaller debt of personal loans despite
the increased of the outstanding balance of personal loans, then it
appears that the probability of un-defaulted personal loans is higher
than the probability of defaulted personal loans. Therefore, we choose
to use the Gaussian prior $\text{N}\left(0,100\right)$ for all the
regression parameter in the logistic GLM to ensure that the logarithm of
defaulted probability per un-defaulted probability less than zero (which
equivalently to ensure that the probability of a loan status being
charge-off is less than the probability of a loan status being
fully-paid). As we can see from the density plot below, the normal
distribution $\text{N}\left(0,100\right)$ is more centered around the
mean ($\mu = 0$) and the log-normal distribution
$\log\text{N}\left(0,100\right)$ tends to decreased in order to
approached zero. Thus, choosing the Gaussian prior for the regression
parameter to ensure that the probability of a loan status being
charge-off is less than the probability of a loan status being
fully-paid seems quite make sense.

``` r
# Plot N(0,100) and logN(0,100) density curve
xx <- -100:100
plot(xx,dnorm(xx,0,10),col='red',type='l',xlab="",ylab="")
lines(xx,dlnorm(exp(xx),0,10),col='blue')
legend("topright", c(expression(N(0,10^2)),expression(logN(0,10^2))),
       col = c("red","blue"),lwd = 1,bty='n',cex=0.7)
```

![](assignment-2_files/figure-gfm/unnamed-chunk-28-1.png)<!-- -->

Since the variance parameter of our Gaussian prior is $\sigma^2 = 100$,
then the precision parameter for our Gaussian prior is
$\tau = \frac{1}{\sigma^2} = 0.01$. The $\verb|R|$ code below implement
our identical model with these Gaussian prior for all of the regression
parameters and printed out the model summary using the
$\verb|summary(m2.I)|$ command. We set $\verb|Ntrials|=1$,
$\verb|family| = \verb|binomial|$, and $\verb|control.family|$ equals to
$\verb|list(link="logit")|$ in order to use logistic GLM in in INLA. In
this part, we will only use the first 90000 observations to build our
identical model since INLA will crash and produce error if we use all
the observations in our dataset.

``` r
# Prior for regression parameters
prior.beta <- list(mean.intercept = 0,prec.intercept = 0.01,mean = 0,prec = 0.01)

# Fit the logistc GLM identical model into INLA
m2.I<-inla(y~log.interest.rate+log.annual.income+log.loan.amount+debt.to.income+sub.grade+term,
           data=lending[1:90000,],family="binomial",Ntrials = 1,
           control.family=list(link="logit"),control.fixed=prior.beta,
           control.compute=list(waic=T,config=T,cpo=T,dic=T))

# Display model summary
summary(m2.I)
```

    ## 
    ## Call:
    ##    c("inla.core(formula = formula, family = family, contrasts = contrasts, 
    ##    ", " data = data, quantiles = quantiles, E = E, offset = offset, ", " 
    ##    scale = scale, weights = weights, Ntrials = Ntrials, strata = strata, 
    ##    ", " lp.scale = lp.scale, link.covariates = link.covariates, verbose = 
    ##    verbose, ", " lincomb = lincomb, selection = selection, control.compute 
    ##    = control.compute, ", " control.predictor = control.predictor, 
    ##    control.family = control.family, ", " control.inla = control.inla, 
    ##    control.fixed = control.fixed, ", " control.mode = control.mode, 
    ##    control.expert = control.expert, ", " control.hazard = control.hazard, 
    ##    control.lincomb = control.lincomb, ", " control.update = 
    ##    control.update, control.lp.scale = control.lp.scale, ", " 
    ##    control.pardiso = control.pardiso, only.hyperparam = only.hyperparam, 
    ##    ", " inla.call = inla.call, inla.arg = inla.arg, num.threads = 
    ##    num.threads, ", " blas.num.threads = blas.num.threads, keep = keep, 
    ##    working.directory = working.directory, ", " silent = silent, inla.mode 
    ##    = inla.mode, safe = FALSE, debug = debug, ", " .parent.frame = 
    ##    .parent.frame)") 
    ## Time used:
    ##     Pre = 1.15, Running = 17, Post = 20.7, Total = 38.9 
    ## Fixed effects:
    ##                     mean    sd 0.025quant 0.5quant 0.975quant mode kld
    ## (Intercept)       -3.160 0.364     -3.862   -3.164     -2.432   NA   0
    ## log.interest.rate  0.229 0.133     -0.023    0.226      0.499   NA   0
    ## log.annual.income -0.306 0.012     -0.330   -0.306     -0.282   NA   0
    ## log.loan.amount    0.185 0.013      0.160    0.185      0.211   NA   0
    ## debt.to.income     0.085 0.010      0.065    0.085      0.104   NA   0
    ## sub.gradeA2        0.330 0.222     -0.099    0.328      0.771   NA   0
    ## sub.gradeA3        0.394 0.226     -0.042    0.391      0.843   NA   0
    ## sub.gradeA4        0.704 0.222      0.275    0.701      1.147   NA   0
    ## sub.gradeA5        0.813 0.242      0.341    0.812      1.291   NA   0
    ## sub.gradeB1        0.818 0.263      0.302    0.818      1.335   NA   0
    ## sub.gradeB2        0.970 0.293      0.390    0.971      1.541   NA   0
    ## sub.gradeB3        0.973 0.320      0.336    0.975      1.594   NA   0
    ## sub.gradeB4        1.108 0.345      0.421    1.112      1.775   NA   0
    ## sub.gradeB5        1.166 0.366      0.435    1.170      1.872   NA   0
    ## sub.gradeC1        1.192 0.379      0.434    1.197      1.922   NA   0
    ## sub.gradeC2        1.193 0.397      0.399    1.199      1.957   NA   0
    ## sub.gradeC3        1.355 0.412      0.530    1.361      2.147   NA   0
    ## sub.gradeC4        1.414 0.426      0.560    1.421      2.232   NA   0
    ## sub.gradeC5        1.434 0.446      0.539    1.441      2.288   NA   0
    ## sub.gradeD1        1.452 0.461      0.526    1.459      2.335   NA   0
    ## sub.gradeD2        1.549 0.475      0.593    1.556      2.459   NA   0
    ## sub.gradeD3        1.528 0.488      0.547    1.535      2.461   NA   0
    ## sub.gradeD4        1.568 0.498      0.566    1.576      2.521   NA   0
    ## sub.gradeD5        1.522 0.512      0.492    1.531      2.502   NA   0
    ## sub.gradeE1        1.534 0.526      0.476    1.543      2.539   NA   0
    ## sub.gradeE2        1.674 0.535      0.596    1.683      2.697   NA   0
    ## sub.gradeE3        1.681 0.546      0.581    1.690      2.725   NA   0
    ## sub.gradeE4        1.706 0.557      0.585    1.716      2.770   NA   0
    ## sub.gradeE5        1.632 0.564      0.495    1.642      2.711   NA   0
    ## sub.gradeF1        1.543 0.574      0.387    1.553      2.640   NA   0
    ## sub.gradeF2        1.845 0.582      0.673    1.855      2.956   NA   0
    ## sub.gradeF3        1.699 0.589      0.514    1.710      2.824   NA   0
    ## sub.gradeF4        1.816 0.596      0.615    1.826      2.955   NA   0
    ## sub.gradeF5        1.875 0.603      0.661    1.886      3.027   NA   0
    ## sub.gradeG1        1.771 0.619      0.525    1.781      2.955   NA   0
    ## sub.gradeG2        1.589 0.626      0.331    1.599      2.785   NA   0
    ## sub.gradeG3        2.069 0.630      0.803    2.079      3.274   NA   0
    ## sub.gradeG4        1.469 0.662      0.140    1.479      2.738   NA   0
    ## sub.gradeG5        1.608 0.666      0.271    1.618      2.885   NA   0
    ## term 60 months     0.315 0.025      0.266    0.315      0.365   NA   0
    ## 
    ## Deviance Information Criterion (DIC) ...............: 72308.57
    ## Deviance Information Criterion (DIC, saturated) ....: -1340091.67
    ## Effective number of parameters .....................: 39.93
    ## 
    ## Watanabe-Akaike information criterion (WAIC) ...: 72308.71
    ## Effective number of parameters .................: 39.99
    ## 
    ## Marginal log-Likelihood:  -36318.69 
    ## CPO, PIT is computed 
    ## Posterior summaries for the linear predictor and the fitted values are computed
    ## (Posterior marginals needs also 'control.compute=list(return.marginals.predictor=TRUE)')

As we can see from the model summary output above, the column
$\verb|0.025quant|$ and $\verb|0.975quant|$ represents the lower and
upper bound of a 95% credible interval for our regression parameter. In
Bayesian statistics, we can interpret the 95% credible interval for the
regression parameter as a fix interval where the value of interest of
our regression parameter will lies on that interval with probability
95%.

If we observe the output of the identical model that we obtained from
INLA using the $\verb|summary(m2.I)|$ command, we can see that the
posterior mean for our identical model parameter are not significantly
different from the estimated values of our logistic GLM parameter in a).
This implies that the our estimated regression parameter of the
identical model that we obtained using INLA by specifying our proposed
Gaussian prior $\text{N}(0,100)$ does not significantly change the
estimated regression parameter even though we use different method than
in part a) to obtain the estimated values of our parameter of interest.
Furthermore, we can see that the values of the posterior mean and
standard deviation for the posterior distribution of the regression
parameter coefficient for the explanatory variable that we obtained
using the $\verb|summary(m2.I)|$ command is significantly different from
zero, which implies that all the explanatory variable that we used in
the identical model is most likely important in the model.

Lets try to see the model summary output from INLA using different
Gaussian prior. We test different Gaussian prior to check the
sensitivity of the estimated logistic GLM parameter posterior mean in
order to investigate does different Gaussian prior affect the estimated
values of our regression parameters.

``` r
prior.check <- function(mu.beta0,prec.beta0,mu.beta,prec.beta,dat){
  # Function to display summary statistics for different prior
  #Input:
  #mu.beta0 = mean parameter in Gaussian prior for beta_0 
  #mu.beta = mean parameter in Gaussian prior for beta_1,..,beta_n
  #prec.beta0 = precision parameter in Gaussian prior for beta_0 
  #prec.beta0 = precision parameter in Gaussian prior for beta_1,..,beta_n
  #dat = inputed data
  #Output: model summary from INLA
  
  # Prior for regression parameter
  prior.beta <- list(mean.intercept = mu.beta0,prec.intercept = prec.beta0,
                     mean = mu.beta,prec = prec.beta)
  
  # Fit the logistc GLM identical model into INLA
  m.I<-inla(y~log.interest.rate+log.annual.income+log.loan.amount+debt.to.income+sub.grade+term,
            data=dat,family="binomial",Ntrials = 1,
            control.family=list(link="logit"),control.fixed=prior.beta,
            control.compute=list(waic=T,config=T,cpo=T,dic=T))
  
  # Display model summary
  summary(m.I)
}

#Perform first prior sensitivity check
prior.check(mu.beta0=0,prec.beta0=1e-6,mu.beta=0,prec.beta=1e-6,dat=lending[1:90000,])
```

    ## 
    ## Call:
    ##    c("inla.core(formula = formula, family = family, contrasts = contrasts, 
    ##    ", " data = data, quantiles = quantiles, E = E, offset = offset, ", " 
    ##    scale = scale, weights = weights, Ntrials = Ntrials, strata = strata, 
    ##    ", " lp.scale = lp.scale, link.covariates = link.covariates, verbose = 
    ##    verbose, ", " lincomb = lincomb, selection = selection, control.compute 
    ##    = control.compute, ", " control.predictor = control.predictor, 
    ##    control.family = control.family, ", " control.inla = control.inla, 
    ##    control.fixed = control.fixed, ", " control.mode = control.mode, 
    ##    control.expert = control.expert, ", " control.hazard = control.hazard, 
    ##    control.lincomb = control.lincomb, ", " control.update = 
    ##    control.update, control.lp.scale = control.lp.scale, ", " 
    ##    control.pardiso = control.pardiso, only.hyperparam = only.hyperparam, 
    ##    ", " inla.call = inla.call, inla.arg = inla.arg, num.threads = 
    ##    num.threads, ", " blas.num.threads = blas.num.threads, keep = keep, 
    ##    working.directory = working.directory, ", " silent = silent, inla.mode 
    ##    = inla.mode, safe = FALSE, debug = debug, ", " .parent.frame = 
    ##    .parent.frame)") 
    ## Time used:
    ##     Pre = 0.775, Running = 15.5, Post = 15.6, Total = 31.9 
    ## Fixed effects:
    ##                     mean    sd 0.025quant 0.5quant 0.975quant mode kld
    ## (Intercept)       -3.253 0.375     -3.974   -3.258     -2.502   NA   0
    ## log.interest.rate  0.197 0.136     -0.060    0.194      0.473   NA   0
    ## log.annual.income -0.306 0.012     -0.330   -0.306     -0.282   NA   0
    ## log.loan.amount    0.185 0.013      0.160    0.185      0.211   NA   0
    ## debt.to.income     0.085 0.010      0.065    0.085      0.104   NA   0
    ## sub.gradeA2        0.355 0.224     -0.078    0.353      0.802   NA   0
    ## sub.gradeA3        0.431 0.230     -0.013    0.428      0.889   NA   0
    ## sub.gradeA4        0.746 0.227      0.307    0.743      1.199   NA   0
    ## sub.gradeA5        0.866 0.249      0.381    0.865      1.357   NA   0
    ## sub.gradeB1        0.880 0.271      0.348    0.880      1.411   NA   0
    ## sub.gradeB2        1.041 0.302      0.444    1.043      1.629   NA   0
    ## sub.gradeB3        1.053 0.330      0.396    1.056      1.691   NA   0
    ## sub.gradeB4        1.195 0.355      0.487    1.200      1.880   NA   0
    ## sub.gradeB5        1.259 0.377      0.505    1.264      1.984   NA   0
    ## sub.gradeC1        1.289 0.390      0.507    1.294      2.038   NA   0
    ## sub.gradeC2        1.295 0.408      0.476    1.301      2.079   NA   0
    ## sub.gradeC3        1.461 0.424      0.609    1.467      2.274   NA   0
    ## sub.gradeC4        1.524 0.439      0.642    1.531      2.364   NA   0
    ## sub.gradeC5        1.548 0.459      0.626    1.556      2.425   NA   0
    ## sub.gradeD1        1.570 0.474      0.616    1.578      2.476   NA   0
    ## sub.gradeD2        1.671 0.489      0.686    1.679      2.605   NA   0
    ## sub.gradeD3        1.653 0.501      0.642    1.662      2.610   NA   0
    ## sub.gradeD4        1.696 0.512      0.663    1.705      2.674   NA   0
    ## sub.gradeD5        1.654 0.527      0.592    1.663      2.658   NA   0
    ## sub.gradeE1        1.669 0.540      0.578    1.678      2.699   NA   0
    ## sub.gradeE2        1.811 0.550      0.701    1.821      2.860   NA   0
    ## sub.gradeE3        1.821 0.562      0.688    1.832      2.891   NA   0
    ## sub.gradeE4        1.849 0.572      0.694    1.860      2.939   NA   0
    ## sub.gradeE5        1.777 0.580      0.606    1.788      2.882   NA   0
    ## sub.gradeF1        1.690 0.590      0.499    1.701      2.813   NA   0
    ## sub.gradeF2        1.993 0.597      0.787    2.005      3.131   NA   0
    ## sub.gradeF3        1.850 0.605      0.629    1.861      3.001   NA   0
    ## sub.gradeF4        1.968 0.612      0.732    1.980      3.134   NA   0
    ## sub.gradeF5        2.029 0.619      0.778    2.040      3.208   NA   0
    ## sub.gradeG1        1.926 0.635      0.644    1.938      3.138   NA   0
    ## sub.gradeG2        1.745 0.642      0.451    1.756      2.969   NA   0
    ## sub.gradeG3        2.225 0.646      0.923    2.236      3.458   NA   0
    ## sub.gradeG4        1.626 0.678      0.262    1.637      2.922   NA   0
    ## sub.gradeG5        1.764 0.682      0.393    1.776      3.068   NA   0
    ## term 60 months     0.315 0.025      0.265    0.315      0.365   NA   0
    ## 
    ## Deviance Information Criterion (DIC) ...............: 72308.67
    ## Deviance Information Criterion (DIC, saturated) ....: -1340091.57
    ## Effective number of parameters .....................: 40.01
    ## 
    ## Watanabe-Akaike information criterion (WAIC) ...: 72308.80
    ## Effective number of parameters .................: 40.05
    ## 
    ## Marginal log-Likelihood:  -36502.43 
    ## CPO, PIT is computed 
    ## Posterior summaries for the linear predictor and the fitted values are computed
    ## (Posterior marginals needs also 'control.compute=list(return.marginals.predictor=TRUE)')

``` r
# Perform second prior sensitivity check
prior.check(mu.beta0=0,prec.beta0=100,mu.beta=0,prec.beta=100,dat=lending[1:90000,])
```

    ## 
    ## Call:
    ##    c("inla.core(formula = formula, family = family, contrasts = contrasts, 
    ##    ", " data = data, quantiles = quantiles, E = E, offset = offset, ", " 
    ##    scale = scale, weights = weights, Ntrials = Ntrials, strata = strata, 
    ##    ", " lp.scale = lp.scale, link.covariates = link.covariates, verbose = 
    ##    verbose, ", " lincomb = lincomb, selection = selection, control.compute 
    ##    = control.compute, ", " control.predictor = control.predictor, 
    ##    control.family = control.family, ", " control.inla = control.inla, 
    ##    control.fixed = control.fixed, ", " control.mode = control.mode, 
    ##    control.expert = control.expert, ", " control.hazard = control.hazard, 
    ##    control.lincomb = control.lincomb, ", " control.update = 
    ##    control.update, control.lp.scale = control.lp.scale, ", " 
    ##    control.pardiso = control.pardiso, only.hyperparam = only.hyperparam, 
    ##    ", " inla.call = inla.call, inla.arg = inla.arg, num.threads = 
    ##    num.threads, ", " blas.num.threads = blas.num.threads, keep = keep, 
    ##    working.directory = working.directory, ", " silent = silent, inla.mode 
    ##    = inla.mode, safe = FALSE, debug = debug, ", " .parent.frame = 
    ##    .parent.frame)") 
    ## Time used:
    ##     Pre = 0.663, Running = 15.8, Post = 13.1, Total = 29.6 
    ## Fixed effects:
    ##                     mean    sd 0.025quant 0.5quant 0.975quant mode   kld
    ## (Intercept)       -1.883 0.023     -1.928   -1.882     -1.837   NA 0.001
    ## log.interest.rate  0.533 0.019      0.497    0.533      0.570   NA 0.000
    ## log.annual.income -0.299 0.012     -0.322   -0.298     -0.275   NA 0.000
    ## log.loan.amount    0.187 0.013      0.163    0.187      0.212   NA 0.000
    ## debt.to.income     0.085 0.010      0.066    0.085      0.104   NA 0.000
    ## sub.gradeA2       -0.113 0.080     -0.270   -0.112      0.044   NA 0.000
    ## sub.gradeA3       -0.160 0.075     -0.308   -0.160     -0.014   NA 0.000
    ## sub.gradeA4       -0.049 0.069     -0.185   -0.049      0.085   NA 0.000
    ## sub.gradeA5       -0.050 0.061     -0.171   -0.050      0.069   NA 0.000
    ## sub.gradeB1       -0.122 0.052     -0.225   -0.122     -0.021   NA 0.000
    ## sub.gradeB2       -0.081 0.047     -0.174   -0.081      0.010   NA 0.000
    ## sub.gradeB3       -0.147 0.044     -0.234   -0.147     -0.061   NA 0.000
    ## sub.gradeB4       -0.090 0.041     -0.171   -0.090     -0.010   NA 0.000
    ## sub.gradeB5       -0.082 0.047     -0.174   -0.082      0.009   NA 0.000
    ## sub.gradeC1       -0.091 0.042     -0.174   -0.091     -0.009   NA 0.000
    ## sub.gradeC2       -0.124 0.041     -0.204   -0.123     -0.043   NA 0.000
    ## sub.gradeC3       -0.018 0.039     -0.094   -0.018      0.057   NA 0.000
    ## sub.gradeC4        0.005 0.038     -0.070    0.005      0.079   NA 0.000
    ## sub.gradeC5       -0.021 0.039     -0.097   -0.021      0.055   NA 0.000
    ## sub.gradeD1       -0.040 0.042     -0.122   -0.040      0.042   NA 0.000
    ## sub.gradeD2        0.009 0.045     -0.080    0.009      0.097   NA 0.000
    ## sub.gradeD3       -0.033 0.047     -0.126   -0.033      0.060   NA 0.000
    ## sub.gradeD4       -0.019 0.047     -0.111   -0.019      0.073   NA 0.000
    ## sub.gradeD5       -0.078 0.049     -0.175   -0.078      0.018   NA 0.000
    ## sub.gradeE1       -0.079 0.057     -0.190   -0.078      0.032   NA 0.000
    ## sub.gradeE2        0.002 0.053     -0.102    0.002      0.106   NA 0.000
    ## sub.gradeE3       -0.008 0.057     -0.120   -0.008      0.104   NA 0.000
    ## sub.gradeE4       -0.007 0.058     -0.120   -0.006      0.106   NA 0.000
    ## sub.gradeE5       -0.068 0.060     -0.186   -0.067      0.050   NA 0.000
    ## sub.gradeF1       -0.129 0.064     -0.255   -0.129     -0.005   NA 0.000
    ## sub.gradeF2        0.048 0.065     -0.080    0.048      0.176   NA 0.000
    ## sub.gradeF3       -0.048 0.067     -0.180   -0.048      0.084   NA 0.000
    ## sub.gradeF4        0.011 0.070     -0.127    0.011      0.148   NA 0.000
    ## sub.gradeF5        0.033 0.074     -0.112    0.033      0.178   NA 0.000
    ## sub.gradeG1       -0.017 0.083     -0.180   -0.017      0.145   NA 0.000
    ## sub.gradeG2       -0.063 0.086     -0.231   -0.063      0.105   NA 0.000
    ## sub.gradeG3        0.057 0.088     -0.116    0.057      0.229   NA 0.000
    ## sub.gradeG4       -0.045 0.093     -0.228   -0.045      0.138   NA 0.000
    ## sub.gradeG5       -0.025 0.094     -0.209   -0.025      0.159   NA 0.000
    ## term 60 months     0.272 0.024      0.225    0.272      0.320   NA 0.000
    ## 
    ## Deviance Information Criterion (DIC) ...............: 72315.94
    ## Deviance Information Criterion (DIC, saturated) ....: -1340084.30
    ## Effective number of parameters .....................: 26.97
    ## 
    ## Watanabe-Akaike information criterion (WAIC) ...: 72315.53
    ## Effective number of parameters .................: 26.54
    ## 
    ## Marginal log-Likelihood:  -36374.67 
    ## CPO, PIT is computed 
    ## Posterior summaries for the linear predictor and the fitted values are computed
    ## (Posterior marginals needs also 'control.compute=list(return.marginals.predictor=TRUE)')

We can see that the regression parameter of estimates (in this case the
posterior mean in the $\verb|mean|$ column) is not significantly
different from the regression parameter of estimates using our Gaussian
original prior under the case we reduces the values of the precision
parameter. However, as we increased the values of the precision
parameter in our Gaussian prior, it turns out that the result showed a
great difference in terms of the estimated parameters. Thus, we can said
that the Gaussian prior we used have a tendency to produces estimated
values of regression parameter which is closer to the estimated values
like in the logistic GLM part a) if we used smaller precision.

Now lets compute the DIC and negative log-CPO (NSLCPO). According to the
output below, we can see that the NSLCPO and DIC are 36154.35 and
72308.57 respectively.

``` r
# Compute NSLCPO
cat("NSLCPO model 2:",-sum(log(m2.I$cpo$cpo)),"\n")
```

    ## NSLCPO model 2: 36154.36

``` r
# Compute DIC
cat("DIC model 2:",m2.I$dic$dic,"\n")
```

    ## DIC model 2: 72308.57

Lastly, we will perform posterior predictive checks on the posterior
predictive distribution of the proportion of defaults among clients in
each of the 49 states contained in the dataset. As the Predictor
variables in the posterior samples of INLA contain the linear predictors
$\eta_i = \text{logit}(p_i)$ where
$\eta_i=\beta_0+\sum\limits_{j=1}^{n}\beta_{j}x_{ji}$, in order to get
the posterior predictive samples of the proportion of defaults among
clients in each of the 49 states, we need to apply the inverse logit
function on these linear predictors. The logit link function is of the
form $$\text{logit}(p)=\log{\left(\dfrac{p}{1-p}\right)},$$and so the
inverse logit function is
$$\text{inv.logit}(x) = \dfrac{1}{1+e^{-x}}.$$The $\verb|R|$ code below
perform a posterior predictive check on the posterior predictive
distribution of the proportion of defaults among clients in each of the
49 states.

``` r
library(fBasics)

# Create inverse logistic function
inv.logit <- function(x) {
  return(1/(1+exp(-x)))
}

# Generate replicate samples
nbsamp=100
n=nrow(lending[1:90000,])

lending.identical.samples=inla.posterior.sample(n=nbsamp, result=m2.I)

predictor.samples.identical=inla.posterior.sample.eval(function(...) {Predictor},
                                                       lending.identical.samples)


# Calculate replicate probability defaulted loans
probarep1 <- rowMeans(inv.logit(predictor.samples.identical))

# Plot histogram of predictive distribution for each state

par(mfrow=c(7,7),mar=c(1,1,1,1))

for (i in unique(lending$state[1:n])){
  ind.default <- which(lending$state[1:n]==i & lending$y[1:n]==1)
  ind.state <- which(lending$state[1:n]==i)
  proba.default <- length(ind.default)/length(ind.state)
  max.vert <- max(c(proba.default,probarep1[ind.state]))
    min.vert <- min(c(proba.default,probarep1[ind.state]))
    hist(probarep1[ind.state],col="gray40",xlim=c(min.vert,max.vert),cex.main = 0.7,
         cex.axis=0.5,main=i)
  abline(v = proba.default,col='red',lwd=2)
}
```

![](assignment-2_files/figure-gfm/unnamed-chunk-33-1.png)<!-- -->

The histograms above show posterior predictive distribution for the
proportion of defaults among clients in each of the 49 states for the
Bayesian fit to the loan status in the $\verb|lending.csv|$ dataset. The
proportion of defaults among clients in each of the 49 states in the
observed dataset are shown by vertical red lines.

Based on these plots, we can confirm that for several state (NE, IA, and
MS), the observed number of proportion of defaults among clients falls
outside the range of the replicates proportion of defaults in the
predictive distributions plot. This might be due to we only use the
first 90000 observations in the dataset instead using all observations
in the dataset.

**c)\[10 marks\] (Independent model)**

**Using INLA, implement a Bayesian logistic GLM with y as a function of
the scaled log interest rate, scaled log annual income, scaled log loan
amount, scaled debt-to-income, and sub.grade, and an independent
intercept for the state variable (see the Radon levels example on page
38 of Lecture 5).**

**Propose your own priors for the model parameters (you can take into
account slides 57-58 of Lecture 4).**

**Print out the model summary.**

**Compute DIC and negative log-CPO (NLSCPO).**

**Do posterior predictive checks with the functions being evaluated
chosen as the proportion of defaults among clients in each of the 49
states contained in the dataset. Discuss the model fit.**

Explanation:

In this part, we are going to implement the independent model, which in
this case is a Bayesian logistic GLM where each state has an independent
random intercept. This can be achieved using random effects in INLA by
adding $\verb|0|$ and
$$\verb|f(state,model="iid",hyper=prec.prior.random.eff)|$$into the
model formula that we are provide to INLA in our $\verb|R|$ code, with
the appropriate prior distribution set by the $\verb|hyper|$ attribute.
Note that there is no “global” intercept in the independent model, hence
we specified it to be $\verb|0|$ in the formula. The reference that we
used for understanding the logistic GLM independent model was inspired
from this following link:
[https://becarioprecario.bitbucket.io/inla-gitbook/ch-multilevel.html](https://becarioprecario.bitbucket.io/inla-gitbook/ch-multilevel.html#sec:binarydata).

Now, we will specify the prior that we are going to use in INLA. For the
regression parameters, we will use the same Gaussian prior in part b).
Thus the Gaussian prior for the regression parameters in our independent
model is $\text{N}\left(0,100\right)$.

Next, we will specify the prior for the random effect terms $u_j$, where
$j = 1,2,\dots,49$. We will used the Gaussian prior with mean 0 and
variance $\sigma^2_u$ for the random effect terms $u_j$. In addition, we
choose the prior distribution for $\sigma_u$ be a Uniform distribution
$U[0,10]$ to ensure that the standard deviation of $\sigma_u$ becomes
much more larger, which will ensure that the logarithm of defaulted
probability per un-defaulted probability less than zero (which
equivalently to ensure that the probability of a loan status being
charge-off is less than the probability of a loan status being
fully-paid). As in INLA, we need to specify the prior on
$\log{(\tau_u)}$ for $\tau_u = \frac{1}{\sigma^2_u}$ where $\tau_u$ is
the precision parameter of the Gaussian prior for the random effect
terms $u_j$. As explained in Section 5.3.2 of Bayesian Inference in INLA
(<https://becarioprecario.bitbucket.io/inla-gitbook/ch-priors.html>),
the corresponding prior on $\theta=\log{(\tau_u)}$ can be written as
$$\log{(\pi(\theta))} = \log{\left(\pi_{\sigma_u}\left(e^{-\frac{\theta}{2}}\right)\right)}-\frac{\theta}{2}-\log{(2)}.$$In
the specific case of $\sigma_u \sim U[0,b]$, we have
$\pi_{\sigma_u}(x) = \frac{1}{b}$ for $x \in [0,b]$, and 0 elsewhere. So
after rearrangement, it follows that
$$\log{(\pi(\theta))} = \begin{cases}-\log{(b)}-\frac{\theta}{2}-\log{(2)} \quad \text{if} \quad \theta \geq -2\log{(b)},\\ -\infty \quad \text{if} \quad \theta < -2\log{(b)}.\end{cases}$$We
can input this prior in INLA using the “expression:” string, see the
$\verb|R|$ code below that also implement the independent model. In this
part, we choose to use the first 90000 first observations in the
$\verb|lending.csv|$ dataset to ensure that INLA would not crashed and
also not produced error when we fit too much dataset.

``` r
sigma.unif.prior.random.eff = "expression:
  b = 10;
  log_dens = (theta>=(-2*log(b)))*(-log(b)-theta/2-log(2)) + (theta<(-2*log(b)))*(-Inf);
  return(log_dens);"

b=10;

#We select the prior for the regression coefficients
prior.beta <- list(mean.intercept = 0,prec.intercept = 0.01,mean = 0, prec = 0.01)

#The hyperparameter precision of the random effect is stored on the log-scale, 
#and it has to be input in this form when specifying it
#fixed=TRUE ensures that it is fixed at its initial value
prec.prior.random.eff <- list(prec=list(prior=sigma.unif.prior.random.eff,
                                        initial=(-2*log(b)+1),fixed = FALSE))


# Fit the logistic GLM independent model in INLA
m3.I<-inla(y~0+log.interest.rate+log.annual.income+log.loan.amount+debt.to.income+sub.grade
           +term+f(state,model="iid",hyper=prec.prior.random.eff),
           data=lending[1:90000,],family ="binomial",Ntrials=1,
           control.family=list(link="logit"),control.fixed=prior.beta,
           control.compute=list(waic=T,config=T,cpo=T,dic=T))

# Display model summary
summary(m3.I)
```

    ## 
    ## Call:
    ##    c("inla.core(formula = formula, family = family, contrasts = contrasts, 
    ##    ", " data = data, quantiles = quantiles, E = E, offset = offset, ", " 
    ##    scale = scale, weights = weights, Ntrials = Ntrials, strata = strata, 
    ##    ", " lp.scale = lp.scale, link.covariates = link.covariates, verbose = 
    ##    verbose, ", " lincomb = lincomb, selection = selection, control.compute 
    ##    = control.compute, ", " control.predictor = control.predictor, 
    ##    control.family = control.family, ", " control.inla = control.inla, 
    ##    control.fixed = control.fixed, ", " control.mode = control.mode, 
    ##    control.expert = control.expert, ", " control.hazard = control.hazard, 
    ##    control.lincomb = control.lincomb, ", " control.update = 
    ##    control.update, control.lp.scale = control.lp.scale, ", " 
    ##    control.pardiso = control.pardiso, only.hyperparam = only.hyperparam, 
    ##    ", " inla.call = inla.call, inla.arg = inla.arg, num.threads = 
    ##    num.threads, ", " blas.num.threads = blas.num.threads, keep = keep, 
    ##    working.directory = working.directory, ", " silent = silent, inla.mode 
    ##    = inla.mode, safe = FALSE, debug = debug, ", " .parent.frame = 
    ##    .parent.frame)") 
    ## Time used:
    ##     Pre = 1.36, Running = 46, Post = 24.8, Total = 72.1 
    ## Fixed effects:
    ##                     mean    sd 0.025quant 0.5quant 0.975quant mode kld
    ## log.interest.rate  0.197 0.135     -0.058    0.194      0.471   NA   0
    ## log.annual.income -0.306 0.012     -0.330   -0.306     -0.282   NA   0
    ## log.loan.amount    0.186 0.013      0.161    0.186      0.212   NA   0
    ## debt.to.income     0.088 0.010      0.068    0.088      0.108   NA   0
    ## sub.gradeA1       -3.272 0.374     -3.992   -3.277     -2.524   NA   0
    ## sub.gradeA2       -2.913 0.316     -3.519   -2.918     -2.278   NA   0
    ## sub.gradeA3       -2.831 0.261     -3.331   -2.835     -2.308   NA   0
    ## sub.gradeA4       -2.518 0.231     -2.960   -2.522     -2.053   NA   0
    ## sub.gradeA5       -2.398 0.182     -2.746   -2.401     -2.030   NA   0
    ## sub.gradeB1       -2.386 0.142     -2.658   -2.389     -2.100   NA   0
    ## sub.gradeB2       -2.230 0.102     -2.425   -2.231     -2.025   NA   0
    ## sub.gradeB3       -2.220 0.072     -2.359   -2.221     -2.077   NA   0
    ## sub.gradeB4       -2.079 0.050     -2.177   -2.079     -1.980   NA   0
    ## sub.gradeB5       -2.014 0.052     -2.117   -2.014     -1.914   NA   0
    ## sub.gradeC1       -1.988 0.048     -2.083   -1.987     -1.894   NA   0
    ## sub.gradeC2       -1.984 0.058     -2.098   -1.983     -1.872   NA   0
    ## sub.gradeC3       -1.816 0.068     -1.951   -1.815     -1.686   NA   0
    ## sub.gradeC4       -1.757 0.081     -1.919   -1.756     -1.603   NA   0
    ## sub.gradeC5       -1.730 0.100     -1.931   -1.728     -1.539   NA   0
    ## sub.gradeD1       -1.712 0.116     -1.946   -1.710     -1.490   NA   0
    ## sub.gradeD2       -1.609 0.132     -1.875   -1.607     -1.358   NA   0
    ## sub.gradeD3       -1.629 0.145     -1.922   -1.626     -1.353   NA   0
    ## sub.gradeD4       -1.585 0.156     -1.899   -1.582     -1.289   NA   0
    ## sub.gradeD5       -1.629 0.171     -1.975   -1.626     -1.304   NA   0
    ## sub.gradeE1       -1.611 0.188     -1.989   -1.607     -1.253   NA   0
    ## sub.gradeE2       -1.471 0.195     -1.866   -1.467     -1.099   NA   0
    ## sub.gradeE3       -1.464 0.208     -1.885   -1.460     -1.067   NA   0
    ## sub.gradeE4       -1.436 0.219     -1.879   -1.432     -1.019   NA   0
    ## sub.gradeE5       -1.507 0.228     -1.968   -1.502     -1.073   NA   0
    ## sub.gradeF1       -1.590 0.239     -2.074   -1.586     -1.134   NA   0
    ## sub.gradeF2       -1.291 0.247     -1.790   -1.286     -0.820   NA   0
    ## sub.gradeF3       -1.438 0.255     -1.954   -1.433     -0.952   NA   0
    ## sub.gradeF4       -1.320 0.264     -1.853   -1.315     -0.816   NA   0
    ## sub.gradeF5       -1.259 0.274     -1.811   -1.254     -0.737   NA   0
    ## sub.gradeG1       -1.355 0.299     -1.956   -1.350     -0.783   NA   0
    ## sub.gradeG2       -1.538 0.311     -2.163   -1.533     -0.942   NA   0
    ## sub.gradeG3       -1.075 0.318     -1.712   -1.070     -0.464   NA   0
    ## sub.gradeG4       -1.645 0.377     -2.402   -1.639     -0.922   NA   0
    ## sub.gradeG5       -1.501 0.384     -2.272   -1.495     -0.764   NA   0
    ## term 60 months     0.319 0.025      0.269    0.319      0.368   NA   0
    ## 
    ## Random effects:
    ##   Name     Model
    ##     state IID model
    ## 
    ## Model hyperparameters:
    ##                      mean    sd 0.025quant 0.5quant 0.975quant mode
    ## Precision for state 80.22 29.49      38.45    75.04     150.23   NA
    ## 
    ## Deviance Information Criterion (DIC) ...............: 72231.69
    ## Deviance Information Criterion (DIC, saturated) ....: -1340168.55
    ## Effective number of parameters .....................: 68.23
    ## 
    ## Watanabe-Akaike information criterion (WAIC) ...: 72231.66
    ## Effective number of parameters .................: 68.07
    ## 
    ## Marginal log-Likelihood:  -36296.58 
    ## CPO, PIT is computed 
    ## Posterior summaries for the linear predictor and the fitted values are computed
    ## (Posterior marginals needs also 'control.compute=list(return.marginals.predictor=TRUE)')

As we can see from the model summary output above, the column
$\verb|0.025quant|$ and $\verb|0.975quant|$ represents the lower and
upper bound of a 95% credible interval for our regression parameter. In
Bayesian statistics, we can interpret the 95% credible interval for the
regression parameter as a fix interval where the value of interest of
our regression parameter will lies on that interval with probability
95%.

If we observe the output of the independent model that we obtained from
INLA using the $\verb|summary(m3.I)|$ command, we can see that the
values of the posterior mean and standard deviation for the posterior
distribution of the regression parameter coefficient for the explanatory
variable that we obtained using the $\verb|summary(m3.I)|$ command is
significantly different from zero, which implies that all the
explanatory variable that we used in the independent model is most
likely important in the model.

Next, we printed out the summary statistics of $\sigma_u$ and the
posterior density curves of $\sigma_u$. According to the posterior
density curve for the standard deviation $\sigma_u$, we can see that the
posterior distribution for $\sigma_u$ is a right-skewed distribution. In
addition, we also obtain a summary statistics about the posterior mean
and standard deviation for $\sigma_u$, which is 0.116921 and 0.0203579
respectively. Not only that, we also obtain the 2.5% and 97.5% quantile
for $\sigma_u$, which is 0.0812029 and 0.161289 respectively. As we
already know, the 2.5% and 97.5% quantile for $\sigma_u$ represents the
lower and upper bound for the 95% credible interval for the standard
deviation $\sigma_u$. Therefore, we can said that the true values of the
standard deviation $\sigma_u$ will lies between 0.0812029 and 0.161289
with a probability 95%.

``` r
# Summary statistics of sigma
marginal.tau=m3.I$marginals.hyperpar[[1]]
marginal.sigma <- inla.tmarginal(function(tau) tau^(-1/2),marginal.tau)
inla.zmarginal(marginal.sigma)
```

    ## Mean            0.116951 
    ## Stdev           0.0202157 
    ## Quantile  0.025 0.0815501 
    ## Quantile  0.25  0.102566 
    ## Quantile  0.5   0.115402 
    ## Quantile  0.75  0.129607 
    ## Quantile  0.975 0.161109

``` r
# Plot posterior density of sigma
plot(marginal.sigma,type ="l",xlab=expression(sigma),ylab="Density",
     main='Posterior density of'~sigma~'for independent model',cex.main=0.7)
```

![](assignment-2_files/figure-gfm/unnamed-chunk-35-1.png)<!-- -->

We printed out the summary statistics of the random effect terms in the
independent model for each 49 state in the dataset. Noted that the
random effect terms is the intercept parameters for each of the 49
state. From the summary statistics of the random effect terms below, we
can see that some of the posterior standard deviation is typically
smaller than the posterior means in absolute values, indicating that the
amount of data is sufficient to fit some of the random effect terms
parameters with some degree of confidence.

``` r
# Summary statistics for random effect
m3.I$summary.random$state
```

    ##    ID          mean         sd   0.025quant     0.5quant  0.975quant mode
    ## 1  AK  0.0357671897 0.09887313 -0.156253440  0.034653793  0.23398083   NA
    ## 2  AL  0.0253799522 0.06826878 -0.107945369  0.025089812  0.16032072   NA
    ## 3  AR  0.0529741002 0.07930305 -0.100842880  0.052206873  0.21104040   NA
    ## 4  AZ  0.0409000169 0.05774945 -0.071739723  0.040633411  0.15502974   NA
    ## 5  CA  0.0106832206 0.03221878 -0.052177794  0.010533754  0.07439248   NA
    ## 6  CO -0.2267242085 0.06520596 -0.357437996 -0.225705269 -0.10168745   NA
    ## 7  CT -0.0470360673 0.06739491 -0.180144994 -0.046784753  0.08468415   NA
    ## 8  DC -0.0377954245 0.10046469 -0.239203243 -0.036697840  0.15751247   NA
    ## 9  DE  0.0240023967 0.09822562 -0.167713340  0.023236634  0.21998157   NA
    ## 10 FL  0.1069983688 0.03992133  0.029368251  0.106740297  0.18608315   NA
    ## 11 GA -0.0890575944 0.05266379 -0.193001177 -0.088857198  0.01377057   NA
    ## 12 HI  0.0103582039 0.08457079 -0.155382244  0.010087963  0.17760298   NA
    ## 13 IA  0.0118946149 0.11870182 -0.221792623  0.011217842  0.24943008   NA
    ## 14 ID -0.0018185890 0.11864687 -0.237620580 -0.001715787  0.23339890   NA
    ## 15 IL -0.0521833405 0.04887876 -0.148265631 -0.052137446  0.04364618   NA
    ## 16 IN -0.0037051414 0.06258676 -0.126431213 -0.003777911  0.11943083   NA
    ## 17 KS -0.1091030314 0.07900467 -0.267753553 -0.107879728  0.04278877   NA
    ## 18 KY  0.0303468499 0.07478627 -0.115517323  0.029929777  0.17852709   NA
    ## 19 LA  0.1256662574 0.07017695 -0.009402106  0.124700558  0.26608975   NA
    ## 20 MA  0.0182035979 0.05978183 -0.098680861  0.018020506  0.13611217   NA
    ## 21 MD  0.0589442980 0.05739824 -0.052810787  0.058611861  0.17255631   NA
    ## 22 MI  0.0626515278 0.05498225 -0.044404893  0.062338876  0.17145652   NA
    ## 23 MN  0.0428434815 0.06344524 -0.080801442  0.042500242  0.16840096   NA
    ## 24 MO  0.0645404125 0.06479469 -0.061355292  0.064056765  0.19312702   NA
    ## 25 MS -0.0004639283 0.11872433 -0.236208233 -0.000437641  0.23513090   NA
    ## 26 MT -0.1086683450 0.10037167 -0.314578036 -0.105734541  0.08098888   NA
    ## 27 NC  0.0570476647 0.05302703 -0.046279491  0.056775046  0.16190140   NA
    ## 28 NE  0.0111838334 0.11865948 -0.222533626  0.010547872  0.24851733   NA
    ## 29 NH -0.1173218274 0.09442424 -0.310071690 -0.114822800  0.06161779   NA
    ## 30 NJ  0.1366525940 0.04880367  0.041986437  0.136261908  0.23351045   NA
    ## 31 NM -0.0247750446 0.08747107 -0.198101571 -0.024397574  0.14647055   NA
    ## 32 NV  0.1247083920 0.06822578 -0.006760430  0.123829394  0.26105623   NA
    ## 33 NY  0.1414126349 0.03761410  0.068386122  0.141127425  0.21604812   NA
    ## 34 OH  0.0195133408 0.05053425 -0.079275187  0.019365546  0.11913236   NA
    ## 35 OK  0.1589475426 0.07720600  0.011547717  0.157469427  0.31452124   NA
    ## 36 OR -0.0911605464 0.06991697 -0.230300546 -0.090514716  0.04440461   NA
    ## 37 PA  0.0091009373 0.04972314 -0.088179776  0.008983226  0.10704420   NA
    ## 38 RI -0.0282338352 0.09283998 -0.212863094 -0.027656223  0.15320192   NA
    ## 39 SC -0.1624566602 0.07661043 -0.316938696 -0.160977922 -0.01615334   NA
    ## 40 SD  0.0739367487 0.10299804 -0.122605506  0.071527596  0.28386058   NA
    ## 41 TN  0.1393525678 0.06310201  0.017586759  0.138615604  0.26522082   NA
    ## 42 TX -0.0462568238 0.03941144 -0.123533897 -0.046291027  0.03121707   NA
    ## 43 UT -0.0411070959 0.07924712 -0.198226129 -0.040660520  0.11354807   NA
    ## 44 VA  0.0382862433 0.05255883 -0.064292664  0.038072662  0.14206236   NA
    ## 45 VT -0.0272843057 0.10887805 -0.245788895 -0.026193663  0.18510986   NA
    ## 46 WA -0.1444510960 0.05953470 -0.262847104 -0.143896513 -0.02914019   NA
    ## 47 WI -0.0858798382 0.07049777 -0.226122790 -0.085251934  0.05088836   NA
    ## 48 WV -0.1343055698 0.09123543 -0.320428620 -0.131871042  0.03837825   NA
    ## 49 WY -0.0615353700 0.10062659 -0.265132109 -0.059732467  0.13204473   NA
    ##             kld
    ## 1  2.066031e-08
    ## 2  3.164731e-09
    ## 3  1.056359e-08
    ## 4  2.434596e-09
    ## 5  3.278557e-09
    ## 6  2.250350e-08
    ## 7  2.805182e-09
    ## 8  2.101444e-08
    ## 9  1.769796e-08
    ## 10 4.090958e-09
    ## 11 1.705534e-09
    ## 12 7.653065e-09
    ## 13 7.179842e-09
    ## 14 7.178199e-09
    ## 15 5.426960e-10
    ## 16 1.272331e-09
    ## 17 2.086318e-08
    ## 18 5.325645e-09
    ## 19 1.660541e-08
    ## 20 1.632261e-09
    ## 21 3.391556e-09
    ## 22 3.222938e-09
    ## 23 3.410264e-09
    ## 24 5.524890e-09
    ## 25 7.030643e-09
    ## 26 5.912158e-08
    ## 27 2.698186e-09
    ## 28 7.244250e-09
    ## 29 5.268771e-08
    ## 30 5.943506e-09
    ## 31 9.751577e-09
    ## 32 1.464847e-08
    ## 33 5.537481e-09
    ## 34 1.196037e-09
    ## 35 3.197701e-08
    ## 36 8.358202e-09
    ## 37 9.446266e-10
    ## 38 1.385683e-08
    ## 39 3.176974e-08
    ## 40 4.032184e-08
    ## 41 1.224676e-08
    ## 42 6.696356e-10
    ## 43 6.857022e-09
    ## 44 1.880738e-09
    ## 45 2.027006e-08
    ## 46 7.845944e-09
    ## 47 7.989454e-09
    ## 48 5.525091e-08
    ## 49 2.933097e-08

Now lets compute the DIC and negative log-CPO (NSLCPO). According to the
output below, we can see that the NSLCPO and DIC are 36115.83 and
72231.68 respectively. Compared to the NSLCPO and DIC of the identical
model, we can see that NSLCPO and DIC of the independent model is much
more smaller than the NSLCPO and DIC of the identical model. This
indicates that the independent model fits well on the data compared to
the identical model.

``` r
# Compute NSLCPO
cat("NSLCPO model 3:",-sum(log(m3.I$cpo$cpo)),"\n")
```

    ## NSLCPO model 3: 36115.83

``` r
# Compute DIC
cat("DIC model 3:",m3.I$dic$dic,"\n")
```

    ## DIC model 3: 72231.69

Lastly, we will perform posterior predictive checks on the posterior
predictive distribution of the proportion of defaults among clients in
each of the 49 states contained in the dataset. As the Predictor
variables in the posterior samples of INLA contain the linear predictors
$\eta_i = \text{logit}(p_i)$ where
$\eta_i=\beta_0+\sum\limits_{j=1}^{n}\beta_{j}x_{ji}$, in order to get
the posterior predictive samples of the proportion of defaults among
clients in each of the 49 states, we need to apply the inverse logit
function on these linear predictors. The logit link function is of the
form $$\text{logit}(p)=\log{\left(\dfrac{p}{1-p}\right)},$$and so the
inverse logit function is
$$\text{inv.logit}(x) = \dfrac{1}{1+e^{-x}}.$$The $\verb|R|$ code below
perform a posterior predictive check on the posterior predictive
distribution of the proportion of defaults among clients in each of the
49 states.

``` r
# Generate replicate samples
nbsamp=100
n=nrow(lending[1:90000,])

lending.independent.samples=inla.posterior.sample(n=nbsamp, result=m3.I)

predictor.samples.independent=inla.posterior.sample.eval(function(...){Predictor},
                                                         lending.independent.samples)


# Calculate replicate probability defaulted loans
probarep2 <- rowMeans(inv.logit(predictor.samples.independent))

# Plot histogram of predictive distribution for each state

par(mfrow=c(7,7),mar=c(1,1,1,1))

for (i in unique(lending$state[1:n])){
  ind.default <- which(lending$state[1:n]==i & lending$y[1:n]==1)
  ind.state <- which(lending$state[1:n]==i)
  proba.default <- length(ind.default)/length(ind.state)
  max.vert <- max(c(proba.default,probarep2[ind.state]))
  min.vert <- min(c(proba.default,probarep2[ind.state]))
  hist(probarep2[ind.state],col="gray40",xlim=c(min.vert,max.vert),cex.main = 0.7,
         cex.axis=0.5,main=i)
  abline(v = proba.default,col='red',lwd=2)
}
```

![](assignment-2_files/figure-gfm/unnamed-chunk-38-1.png)<!-- -->

The histograms above show posterior predictive distribution for the
proportion of defaults among clients in each of the 49 states for the
Bayesian fit to the loan status in the $\verb|lending.csv|$ dataset. The
proportion of defaults among clients in each of the 49 states in the
observed dataset are shown by vertical red lines.

Based on these plots, we can confirm that for several state (NE, IA, and
MS), the observed number of proportion of defaults among clients falls
outside the range of the replicates proportion of defaults in the
predictive distributions plot. This might be due to we only use the
first 90000 observations in the dataset instead using all observations
in the dataset.

**d)\[10 marks\] (Hierarchical model)**

**Using INLA, implement a Bayesian logistic GLM with y as a function of
the scaled log interest rate, scaled log annual income, scaled log loan
amount, scaled debt-to-income, and sub.grade, and an hierarchical model
for the state variable (each state has a different intercept but the
intercepts are random draws from the same distribution, see the Radon
levels example on page 38 of Lecture 5).**

**Propose your own priors for the model parameters.**

**Print out the model summary.**

**Compute DIC and negative log-CPO (NLSCPO).**

**Do posterior predictive checks with the functions being evaluated
chosen as the proportion of defaults among clients in each of the 49
states contained in the dataset. Discuss the model fit.**

Explanation:

In this part, we are going to implement the hierarchical model, which in
this case is a Bayesian logistic GLM where each state has a different
intercept but the intercepts are random draws from the same
distribution. This can be achieved using random effects in INLA by
adding $\verb|1|$ and
$$\verb|f(state,model="iid",hyper=prec.prior.random.eff)|$$into the
model formula that we are provide to INLA in our $\verb|R|$ code, with
the appropriate prior distribution set by the $\verb|hyper|$ attribute.
Note that the common mean of the random intercepts is achieved by having
a “global” intercept in this model, hence we specified it to be 1 in the
formula. The appropriate priors on the hyperparameters are set by
choosing $\verb|prec.prior.random.eff|$, and also set the
$\verb|control.family|$ equals to $\verb|list(hyper=prec.prior)|$ along
with set the $\verb|control.fixed|$ equals to $\verb|prior.beta|$
options. The reference that we used for understanding the logistic GLM
hierarchical model was inspired from this following link:
[https://becarioprecario.bitbucket.io/inla-gitbook/ch-multilevel.html](https://becarioprecario.bitbucket.io/inla-gitbook/ch-multilevel.html#sec:binarydata).

Now, we will specify the prior that we are going to use in INLA. For the
regression parameters, we will use the same Gaussian prior in part b).
Thus the Gaussian prior for the regression parameters in our independent
model is $\text{N}\left(0,100\right)$.

Next, we will specify the prior for the random effect terms $u_j$, where
$j = 1,2,\dots,49$. We will used the Gaussian prior with mean 0 and
variance $\sigma^2_u$ for the random effect terms $u_j$ just like in
part c). This time we let the prior distribution for $\sigma_u$ be a
Uniform distribution $U[0,20]$ to ensure that $\sigma_u$ become much
more larger, which will ensure that the probability of a loan status
being charge-off is smaller than the probability of a loan status being
fully-paid. In this part, we will use the first 90000 first observations
in the $\verb|lending.csv|$ dataset to ensure that INLA would not
crashed and also not produced error when we fit too much dataset. The
$\verb|R|$ code below implement the hierarchical model in INLA.

``` r
sigma.unif.prior.random.eff = "expression:
  b = 20;
  log_dens = (theta>=(-2*log(b)))*(-log(b)-theta/2-log(2)) + (theta<(-2*log(b)))*(-Inf);
  return(log_dens);"

b=20;


#We select the prior for the regression coefficients
prior.beta <- list(mean.intercept = 0, prec.intercept = 0.01,mean = 0, prec = 0.01)

#The hyperparameter precision of the random effect is stored on the log-scale, 
#and it has to be input in this form when specifying it
#fixed=TRUE ensures that it is fixed at its initial value
prec.prior.random.eff <- list(prec=list(prior=sigma.unif.prior.random.eff,
                                        initial=(-2*log(b)+1),fixed = FALSE))

# Fit the logistc GLM hierarchical model into INLA
m4.I<-inla(y~1+log.interest.rate+log.annual.income+log.loan.amount+debt.to.income+sub.grade
           +term+f(state,model="iid",hyper=prec.prior.random.eff),
           data=lending[1:90000,],family ="binomial",Ntrials=1,
           control.family=list(link="logit"),control.fixed=prior.beta,
           control.compute=list(waic=T,config=T,cpo=T,dic=T))

# Display model summary
summary(m4.I)
```

    ## 
    ## Call:
    ##    c("inla.core(formula = formula, family = family, contrasts = contrasts, 
    ##    ", " data = data, quantiles = quantiles, E = E, offset = offset, ", " 
    ##    scale = scale, weights = weights, Ntrials = Ntrials, strata = strata, 
    ##    ", " lp.scale = lp.scale, link.covariates = link.covariates, verbose = 
    ##    verbose, ", " lincomb = lincomb, selection = selection, control.compute 
    ##    = control.compute, ", " control.predictor = control.predictor, 
    ##    control.family = control.family, ", " control.inla = control.inla, 
    ##    control.fixed = control.fixed, ", " control.mode = control.mode, 
    ##    control.expert = control.expert, ", " control.hazard = control.hazard, 
    ##    control.lincomb = control.lincomb, ", " control.update = 
    ##    control.update, control.lp.scale = control.lp.scale, ", " 
    ##    control.pardiso = control.pardiso, only.hyperparam = only.hyperparam, 
    ##    ", " inla.call = inla.call, inla.arg = inla.arg, num.threads = 
    ##    num.threads, ", " blas.num.threads = blas.num.threads, keep = keep, 
    ##    working.directory = working.directory, ", " silent = silent, inla.mode 
    ##    = inla.mode, safe = FALSE, debug = debug, ", " .parent.frame = 
    ##    .parent.frame)") 
    ## Time used:
    ##     Pre = 1.06, Running = 339, Post = 47.8, Total = 388 
    ## Fixed effects:
    ##                     mean    sd 0.025quant 0.5quant 0.975quant mode kld
    ## (Intercept)       -3.173 0.366     -3.877   -3.177     -2.443   NA   0
    ## log.interest.rate  0.232 0.133     -0.021    0.229      0.502   NA   0
    ## log.annual.income -0.306 0.012     -0.330   -0.306     -0.282   NA   0
    ## log.loan.amount    0.186 0.013      0.161    0.186      0.212   NA   0
    ## debt.to.income     0.088 0.010      0.068    0.088      0.108   NA   0
    ## sub.gradeA2        0.328 0.222     -0.101    0.325      0.769   NA   0
    ## sub.gradeA3        0.394 0.226     -0.043    0.391      0.843   NA   0
    ## sub.gradeA4        0.701 0.222      0.272    0.699      1.145   NA   0
    ## sub.gradeA5        0.811 0.242      0.339    0.810      1.290   NA   0
    ## sub.gradeB1        0.815 0.264      0.298    0.815      1.332   NA   0
    ## sub.gradeB2        0.962 0.294      0.382    0.964      1.534   NA   0
    ## sub.gradeB3        0.964 0.321      0.326    0.966      1.586   NA   0
    ## sub.gradeB4        1.098 0.346      0.410    1.102      1.766   NA   0
    ## sub.gradeB5        1.157 0.367      0.426    1.162      1.864   NA   0
    ## sub.gradeC1        1.181 0.380      0.423    1.186      1.913   NA   0
    ## sub.gradeC2        1.181 0.398      0.385    1.186      1.945   NA   0
    ## sub.gradeC3        1.344 0.413      0.517    1.350      2.137   NA   0
    ## sub.gradeC4        1.400 0.427      0.543    1.406      2.219   NA   0
    ## sub.gradeC5        1.421 0.447      0.525    1.428      2.277   NA   0
    ## sub.gradeD1        1.435 0.462      0.508    1.443      2.320   NA   0
    ## sub.gradeD2        1.534 0.476      0.577    1.542      2.446   NA   0
    ## sub.gradeD3        1.511 0.488      0.529    1.519      2.446   NA   0
    ## sub.gradeD4        1.552 0.499      0.549    1.561      2.507   NA   0
    ## sub.gradeD5        1.504 0.513      0.472    1.513      2.486   NA   0
    ## sub.gradeE1        1.520 0.527      0.460    1.529      2.527   NA   0
    ## sub.gradeE2        1.656 0.536      0.577    1.665      2.681   NA   0
    ## sub.gradeE3        1.661 0.547      0.559    1.670      2.707   NA   0
    ## sub.gradeE4        1.686 0.558      0.563    1.696      2.752   NA   0
    ## sub.gradeE5        1.613 0.566      0.474    1.623      2.693   NA   0
    ## sub.gradeF1        1.527 0.575      0.369    1.537      2.626   NA   0
    ## sub.gradeF2        1.825 0.583      0.652    1.835      2.938   NA   0
    ## sub.gradeF3        1.676 0.590      0.488    1.686      2.802   NA   0
    ## sub.gradeF4        1.792 0.597      0.589    1.803      2.933   NA   0
    ## sub.gradeF5        1.852 0.604      0.635    1.863      3.006   NA   0
    ## sub.gradeG1        1.753 0.620      0.505    1.764      2.939   NA   0
    ## sub.gradeG2        1.570 0.627      0.310    1.581      2.769   NA   0
    ## sub.gradeG3        2.033 0.631      0.765    2.044      3.241   NA   0
    ## sub.gradeG4        1.458 0.663      0.127    1.469      2.729   NA   0
    ## sub.gradeG5        1.602 0.667      0.263    1.612      2.881   NA   0
    ## term 60 months     0.319 0.025      0.269    0.319      0.369   NA   0
    ## 
    ## Random effects:
    ##   Name     Model
    ##     state IID model
    ## 
    ## Model hyperparameters:
    ##                      mean    sd 0.025quant 0.5quant 0.975quant mode
    ## Precision for state 80.09 29.51      38.84    75.00     151.16   NA
    ## 
    ## Deviance Information Criterion (DIC) ...............: 72231.47
    ## Deviance Information Criterion (DIC, saturated) ....: -1340168.77
    ## Effective number of parameters .....................: 68.03
    ## 
    ## Watanabe-Akaike information criterion (WAIC) ...: 72231.59
    ## Effective number of parameters .................: 68.02
    ## 
    ## Marginal log-Likelihood:  -36296.96 
    ## CPO, PIT is computed 
    ## Posterior summaries for the linear predictor and the fitted values are computed
    ## (Posterior marginals needs also 'control.compute=list(return.marginals.predictor=TRUE)')

As we can see from the model summary output above, the column
$\verb|0.025quant|$ and $\verb|0.975quant|$ represents the lower and
upper bound of a 95% credible interval for our regression parameter. In
Bayesian statistics, we can interpret the 95% credible interval for the
regression parameter as a fix interval where the value of interest of
our regression parameter will lies on that interval with probability
95%.

If we observe the output of the hierarchical model that we obtained from
INLA using the $\verb|summary(m4.I)|$ command, we can see that the
values of the posterior mean and standard deviation for the posterior
distribution of the regression parameter coefficient for the explanatory
variable that we obtained using the $\verb|summary(m4.I)|$ command is
significantly different from zero, which implies that all the
explanatory variable that we used in the hierarchical model is most
likely important in the model.

Next, we printed out the summary statistics of $\sigma_u$ and the
posterior density curves of $\sigma_u$. According to the posterior
density curve for the standard deviation $\sigma_u$, we can see that the
posterior distribution for $\sigma_u$ is a right-skewed distribution. In
addition, we also obtain a summary statistics about the posterior mean
and standard deviation for $\sigma_u$, which is 0.117008 and 0.0204664
respectively. Not only that, we also obtain the 2.5% and 97.5% quantile
for $\sigma_u$, which is 0.081166 and 0.16151 respectively. As we
already know, the 2.5% and 97.5% quantile for $\sigma_u$ represents the
lower and upper bound for the 95% credible interval for the standard
deviation $\sigma_u$. Therefore, we can said that the true values of the
standard deviation $\sigma_u$ will lies between 0.081166 and 0.16151
with a probability 95%.

``` r
# Summary statistics of sigma
marginal.tau=m4.I$marginals.hyperpar[[1]]
marginal.sigma <- inla.tmarginal(function(tau) tau^(-1/2),marginal.tau)
inla.zmarginal(marginal.sigma)
```

    ## Mean            0.116912 
    ## Stdev           0.0200963 
    ## Quantile  0.025 0.0813968 
    ## Quantile  0.25  0.102656 
    ## Quantile  0.5   0.115455 
    ## Quantile  0.75  0.129593 
    ## Quantile  0.975 0.160583

``` r
# Plot posterior density of sigma
plot(marginal.sigma,type ="l",xlab=expression(sigma),ylab="Density",
     main='Posterior density of'~sigma~'for hierarchical model',cex.main=0.7)
```

![](assignment-2_files/figure-gfm/unnamed-chunk-40-1.png)<!-- -->

We printed out the summary statistics of the random effect terms in the
hierarchical model for each 49 state in the dataset. Noted that the
random effect terms is the intercept parameters for each of the 49
state. From the summary statistics of the random effect terms below, we
can see that some of the posterior standard deviation is typically
smaller than the posterior means in absolute values, indicating that the
amount of data is sufficient to fit some of the random effect terms
parameters with some degree of confidence.

``` r
# Summary statistics for random effect
m4.I$summary.random$state
```

    ##    ID          mean         sd   0.025quant      0.5quant  0.975quant mode
    ## 1  AK  0.0356154892 0.09857028 -0.155884290  0.0345220685  0.23313942   NA
    ## 2  AL  0.0254564781 0.06816984 -0.107673289  0.0251643683  0.16020412   NA
    ## 3  AR  0.0528896987 0.07915590 -0.100655303  0.0521259509  0.21063815   NA
    ## 4  AZ  0.0410258630 0.05768190 -0.071477274  0.0407575558  0.15502248   NA
    ## 5  CA  0.0109623007 0.03216621 -0.051791860  0.0108124099  0.07456410   NA
    ## 6  CO -0.2260877520 0.06509415 -0.356443994 -0.2251121087 -0.10117361   NA
    ## 7  CT -0.0466938149 0.06729024 -0.179584192 -0.0464456057  0.08483364   NA
    ## 8  DC -0.0373844206 0.10013040 -0.238006077 -0.0363182877  0.15737280   NA
    ## 9  DE  0.0238741651 0.09793265 -0.167317748  0.0231218994  0.21921446   NA
    ## 10 FL  0.1071749971 0.03987974  0.029623654  0.1069192169  0.18616437   NA
    ## 11 GA -0.0887023826 0.05259605 -0.192502411 -0.0885040268  0.01399823   NA
    ## 12 HI  0.0103961489 0.08439177 -0.154999419  0.0101256566  0.17728651   NA
    ## 13 IA  0.0117732622 0.11810106 -0.220804838  0.0111239340  0.24799447   NA
    ## 14 ID -0.0018062282 0.11805066 -0.236392251 -0.0017072601  0.23222460   NA
    ## 15 IL -0.0519443636 0.04881819 -0.147902404 -0.0518997636  0.04376963   NA
    ## 16 IN -0.0034306400 0.06250314 -0.125986724 -0.0035061202  0.11954893   NA
    ## 17 KS -0.1086174296 0.07882350 -0.266816852 -0.1074153964  0.04297333   NA
    ## 18 KY  0.0303085145 0.07466023 -0.115314223  0.0298912332  0.17823442   NA
    ## 19 LA  0.1256264848 0.07008344 -0.009282105  0.1246741003  0.26580320   NA
    ## 20 MA  0.0183344074 0.05970682 -0.098398939  0.0181492773  0.13609884   NA
    ## 21 MD  0.0590313280 0.05733375 -0.052594218  0.0586979974  0.17251186   NA
    ## 22 MI  0.0627645174 0.05492314 -0.044173007  0.0624512169  0.17144813   NA
    ## 23 MN  0.0429302365 0.06336399 -0.080552271  0.0425852246  0.16832642   NA
    ## 24 MO  0.0645713566 0.06471228 -0.061161924  0.0640873573  0.19298593   NA
    ## 25 MS -0.0004589695 0.11812692 -0.234995510 -0.0004337636  0.23393615   NA
    ## 26 MT -0.1079297139 0.09994716 -0.312640600 -0.1050861285  0.08114557   NA
    ## 27 NC  0.0571210744 0.05296973 -0.046090937  0.0568478159  0.16185800   NA
    ## 28 NE  0.0110682491 0.11805993 -0.221536636  0.0104581256  0.24709617   NA
    ## 29 NH -0.1166728361 0.09407929 -0.308465333 -0.1142424832  0.06177169   NA
    ## 30 NJ  0.1367662505 0.04876532  0.042164252  0.1363818230  0.23352122   NA
    ## 31 NM -0.0246209672 0.08726562 -0.197516672 -0.0242501525  0.14624908   NA
    ## 32 NV  0.1246545119 0.06814070 -0.006667758  0.1237872041  0.26077933   NA
    ## 33 NY  0.1415894720 0.03757521  0.068632733  0.1413082318  0.21612909   NA
    ## 34 OH  0.0197018051 0.05047672 -0.078969535  0.0195524934  0.11920922   NA
    ## 35 OK  0.1585958370 0.07706756  0.011390232  0.1571559466  0.31375427   NA
    ## 36 OR -0.0907855660 0.06979519 -0.229650175 -0.0901467506  0.04456051   NA
    ## 37 PA  0.0092699437 0.04966530 -0.087893180  0.0091508128  0.10710132   NA
    ## 38 RI -0.0279714782 0.09259047 -0.212056325 -0.0274071820  0.15302331   NA
    ## 39 SC -0.1618667900 0.07642936 -0.315843906 -0.1604277187 -0.01583283   NA
    ## 40 SD  0.0735013635 0.10261197 -0.122473096  0.0711531536  0.28240181   NA
    ## 41 TN  0.1392592916 0.06303566  0.017600798  0.1385350616  0.26494308   NA
    ## 42 TX -0.0460004674 0.03935804 -0.123167700 -0.0460358314  0.03136977   NA
    ## 43 UT -0.0408319264 0.07908915 -0.197613772 -0.0403915713  0.11353878   NA
    ## 44 VA  0.0384722198 0.05250038 -0.063987705  0.0382571663  0.14213326   NA
    ## 45 VT -0.0271239501 0.10843958 -0.244624359 -0.0260650179  0.18451275   NA
    ## 46 WA -0.1439752468 0.05944911 -0.262163443 -0.1434298597 -0.02881339   NA
    ## 47 WI -0.0856233063 0.07037490 -0.225592572 -0.0850012056  0.05092112   NA
    ## 48 WV -0.1335669882 0.09091395 -0.318784238 -0.1312022493  0.03865955   NA
    ## 49 WY -0.0610995407 0.10026588 -0.263785644 -0.0593437522  0.13192450   NA
    ##             kld
    ## 1  2.104063e-08
    ## 2  3.126898e-09
    ## 3  1.034736e-08
    ## 4  2.406075e-09
    ## 5  3.135759e-09
    ## 6  2.100737e-08
    ## 7  2.720972e-09
    ## 8  2.165993e-08
    ## 9  1.801114e-08
    ## 10 3.955447e-09
    ## 11 1.632897e-09
    ## 12 7.575207e-09
    ## 13 1.625756e-08
    ## 14 1.608627e-08
    ## 15 5.078392e-10
    ## 16 1.254759e-09
    ## 17 2.007409e-08
    ## 18 5.242191e-09
    ## 19 1.612172e-08
    ## 20 1.613025e-09
    ## 21 3.344580e-09
    ## 22 3.176177e-09
    ## 23 3.368460e-09
    ## 24 5.437668e-09
    ## 25 1.597236e-08
    ## 26 5.838032e-08
    ## 27 2.656231e-09
    ## 28 1.628717e-08
    ## 29 5.111548e-08
    ## 30 5.733110e-09
    ## 31 9.628494e-09
    ## 32 1.422850e-08
    ## 33 5.320302e-09
    ## 34 1.175118e-09
    ## 35 3.063898e-08
    ## 36 8.073814e-09
    ## 37 9.232349e-10
    ## 38 1.379472e-08
    ## 39 3.030469e-08
    ## 40 4.108399e-08
    ## 41 1.183932e-08
    ## 42 6.158211e-10
    ## 43 6.687445e-09
    ## 44 1.855953e-09
    ## 45 2.369110e-08
    ## 46 7.537115e-09
    ## 47 7.735699e-09
    ## 48 5.307629e-08
    ## 49 3.000517e-08

Now lets compute the DIC and negative log-CPO (NSLCPO). According to the
output below, we can see that the NSLCPO and DIC are 36115.78 and
72231.59 respectively. Compared to the NSLCPO and DIC of the identical
model and independent model, we can see that NSLCPO and DIC of the
hierarchical model is much more smaller than the NSLCPO and DIC of the
identical model and independent model. This indicates that the
hierarchical model fits well on the data compared to the identical model
and independent model.

``` r
# Compute NSLCPO
cat("NSLCPO model 4:",-sum(log(m4.I$cpo$cpo)),"\n")
```

    ## NSLCPO model 4: 36115.8

``` r
# Compute DIC
cat("DIC model 4:",m4.I$dic$dic,"\n")
```

    ## DIC model 4: 72231.47

Lastly, we will perform posterior predictive checks on the posterior
predictive distribution of the proportion of defaults among clients in
each of the 49 states contained in the dataset. As the Predictor
variables in the posterior samples of INLA contain the linear predictors
$\eta_i = \text{logit}(p_i)$ where
$\eta_i=\beta_0+\sum\limits_{j=1}^{n}\beta_{j}x_{ji}$, in order to get
the posterior predictive samples of the proportion of defaults among
clients in each of the 49 states, we need to apply the inverse logit
function on these linear predictors. The logit link function is of the
form $$\text{logit}(p)=\log{\left(\dfrac{p}{1-p}\right)},$$and so the
inverse logit function is
$$\text{inv.logit}(x) = \dfrac{1}{1+e^{-x}}.$$The $\verb|R|$ code below
perform a posterior predictive check on the posterior predictive
distribution of the proportion of defaults among clients in each of the
49 states.

``` r
# Generate replicate samples
nbsamp=100
n=nrow(lending[1:90000,])

lending.hierarchical.samples=inla.posterior.sample(n=nbsamp, result=m4.I)

predictor.samples.hierarchical=inla.posterior.sample.eval(function(...) {Predictor},
                                                       lending.hierarchical.samples)

# Calculate replicate probability defaulted loan
probarep3 <- rowMeans(inv.logit(predictor.samples.hierarchical))

# Plot histogram of predictive distribution for each state

par(mfrow=c(7,7),mar=c(1,1,1,1))

for (i in unique(lending$state[1:n])){
  ind.default <- which(lending$state[1:n]==i & lending$y[1:n]==1)
  ind.state <- which(lending$state[1:n]==i)
  proba.default <- length(ind.default)/length(ind.state)
  max.vert <- max(c(proba.default,probarep3[ind.state]))
  min.vert <- min(c(proba.default,probarep3[ind.state]))
  hist(probarep3[ind.state],col="gray40",xlim=c(min.vert,max.vert),cex.main = 0.7,
         cex.axis=0.5,main=i)
  abline(v = proba.default,col='red',lwd=2)
}
```

![](assignment-2_files/figure-gfm/unnamed-chunk-43-1.png)<!-- -->

The histograms above show posterior predictive distribution for the
proportion of defaults among clients in each of the 49 states for the
Bayesian fit to the loan status in the $\verb|lending.csv|$ dataset. The
proportion of defaults among clients in each of the 49 states in the
observed dataset are shown by vertical red lines.

Based on these plots, we can confirm that for several state (NE, IA, and
MS), the observed number of proportion of defaults among clients falls
outside the range of the replicates proportion of defaults in the
predictive distributions plot. This might be due to we only use the
first 90000 observations in the dataset instead using all observations
in the dataset.

**e)\[10 marks\] Prediction of probability of default based on salary**

**Consider a set of clients with loan amount of 20000\$, interest rate
of 15%, sub grade of B1, debt to income of 10%, state of “CA”
(California), term of 60 months, and annual incomes of**

**40000, 50000, 60000, … , 300000\$.**

**Plot the posterior means of the probabilities of default on the loans
in function of the annual incomes based on the hierarchical model from
part d).**

Explanation:

In this part we are going to predict the probability of default based on
salary. First we will store the new data containing the loan amount,
interest rate, sub grade, debt to income, state, term, and loan amount
in a data frame called $\verb|lending2|$. Then we add a new column of
loan status to the $\verb|lending2|$ data where this columns contains
all $\verb|NA|$ values. After we create the data that we want to predict
the probability of defaulted loans in each observations, we then load
the $\verb|lending.csv|$ data into $\verb|R|$ as a data frame called
$\verb|lending1|$. Then we combine the $\verb|lending2|$ and
$\verb|lending1|$ data frame into a single data frame called
$\verb|lending3|$. Before we fit our hierarchical model in part d) using
the $\verb|lending3|$ data, we need to do some data manipulation.

First, we will convert the loan status variable into a binary variable
by converting the loan status “Charged Off” into 1 and the loan status
“Fully Paid” into 0. Next, we will convert the interest rate and
debt-to-income ratio by removing the “%” pattern from the data using
$\verb|str_replace_all()|$ function in $\verb|R|$ and then convert the
variable into a numeric variable by using the $\verb|as.numeric()|$
function in $\verb|R|$. After that, we calculate the logarithm of the
loan amount, the logarithm of the interest rate, and the logarithm of
the annual income using the $\verb|log()|$ function in $\verb|R|$. We
add this three variable to the data and scale the data (centering the
data by the means then divide by the standard deviations) using the
$\verb|scale()|$ function in $\verb|R|$. In addition, we will also used
the $\verb|scale()|$ function on the debt-to-income data but we would
not use log transformations on these data.

Next, we will fit our logistic hierarchical model in part d) using the
first 90027 observations in the $\verb|lending3|$ dataset to ensure that
INLA would not crashed and also not produced error when we fit too much
dataset. The reason we used the first 90027 dataset is because we put
all the observations of the $\verb|lending2|$ dataset as our first 27
observations in the $\verb|lending3|$ dataset and the next 90000
observations after the 27th observations is the original dataset that we
used to build our hierarchical model in part d). As for the prior of the
regression parameters and random effect terms that we are going to use
here, we will use the same prior that we proposed in part d).

Lastly, we will perform posterior predictive sampling and then used the
inverse logistic function to on the our posterior predictive sampling to
obtain the posterior probability of a loan being defaulted sample. We
then use the $\verb|rowMeans()|$ function in $\verb|R|$ to compute the
posterior mean of the probability of the loan being defaulted.
Subsequently, we will provide the results in a line chart of annual
incomes against the posterior mean of the probability of the loan being
defaulted along with the 95% credible interval of the probability of the
loan being defaulted. The $\verb|R|$ code below implement the entire
data analysis procedure that we explained in this part.

``` r
# Write data frame to predict
lending2 = data.frame(loan.amount=rep(20000,27),
                      interest.rate=rep('15%',27),
                      sub.grade=rep('B1',27),
                      annual.income=seq(40000,300000,10000),
                      debt.to.income=rep('10%',27),
                      loan.status=rep('NA',27),
                      state=rep('CA',27),
                      term=rep(" 60 months",27))

# Read original data frame
lending1 = read.csv(file='lending.csv')

# Combine two data frame
lending3 = rbind(lending2,lending1)

# Create response column y
lending3$y <- ifelse(lending3$loan.status=="Charged Off",1,0)

# Extract numbers from interest rate and debt-to-income
lending3$interest.rate <- as.numeric(str_replace_all(lending3$interest.rate,"%",""))
lending3$debt.to.income <- as.numeric(str_replace_all(lending3$debt.to.income,"%",""))

# Create logarithm on loan amount, interest rate, and annual income
lending3$log.loan.amount <- log(lending3$loan.amount)
lending3$log.interest.rate <- log(lending3$interest.rate)
lending3$log.annual.income <- log(lending3$annual.income)

# Scale the converted log column and debt-to-income
lending3$log.loan.amount <- scale(lending3$log.loan.amount)
lending3$log.interest.rate <- scale(lending3$log.interest.rate)
lending3$log.annual.income <- scale(lending3$log.annual.income)
lending3$debt.to.income <- scale(lending3$debt.to.income)

# Prior for random effects term
sigma.unif.prior.random.eff = "expression:
  b = 20;
  log_dens = (theta>=(-2*log(b)))*(-log(b)-theta/2-log(2)) + (theta<(-2*log(b)))*(-Inf);
  return(log_dens);"

b=20;


#We select the prior for the regression coefficients
prior.beta <- list(mean.intercept = 0, prec.intercept = 0.01,mean = 0, prec = 0.01)

#The hyperparameter precision of the random effect is stored on the log-scale, 
#and it has to be input in this form when specifying it
#fixed=TRUE ensures that it is fixed at its initial value
prec.prior.random.eff <- list(prec=list(prior=sigma.unif.prior.random.eff,
                                        initial=(-2*log(b)+1),fixed = FALSE))

# Fit the logistc GLM hierarchical model into INLA
m5.I<-inla(y~1+log.interest.rate+log.annual.income+log.loan.amount+debt.to.income+sub.grade
           +term+f(state,model="iid",hyper=prec.prior.random.eff),
           data=lending3[1:90027,],family ="binomial",Ntrials=1,
           control.predictor=list(compute=T),control.family=list(link="logit"),
           control.fixed=prior.beta,
           control.compute=list(waic=T,config=T,cpo=T,dic=T))

# Generate replicate samples
nbsamp=100

hierarchical.samples=inla.posterior.sample(n=nbsamp, result=m5.I,
                                           selection = list(Predictor=1:27))

predictor.samples=inla.posterior.sample.eval(function(...) {Predictor},
                                             hierarchical.samples)

# Calculate posterior means probability defaulted loan
post.mean = rowMeans(inv.logit(predictor.samples))

# Calculate 95% credible interval for probability defaulted loans
post.q025=apply(inv.logit(predictor.samples), MARGIN=1,FUN=function(x) quantile(x,prob=0.025))

post.q975=apply(inv.logit(predictor.samples),MARGIN=1,FUN=function(x) quantile(x,prob=0.975))

# Plot annual income vs posterior means 
lower.vert = min(c(post.q025,post.mean,post.q975))
upper.vert = max(c(post.q025,post.mean,post.q975))
vert.lim = c(lower.vert,upper.vert)
plot(lending2$annual.income,post.mean,type='l',col='red',xlab='Annual Incomes($)',
     ylab='Probability of Defaulted Loans',cex.lab=0.7,cex.main=0.7,
     ylim=vert.lim,
     main='Probability of Defaulted Loans Based on Salary')

# Plot 95% Credible interval for probability of defaulted loans
lines(lending2$annual.income,post.q025,lty=2,col="dark red")
lines(lending2$annual.income,post.q975,lty=3,col="dark red")

# Add legend to plot
legend("topright",legend=c("2.5% quantile","posterior mean","97.5% quantile"),
       col=c("dark red","red","dark red"),lty=c(2,1,3),bty='n',cex=0.7)
```

![](assignment-2_files/figure-gfm/unnamed-chunk-44-1.png)<!-- -->

From the plot above, we can see that the probability of a loan being
defaulted decreased as the annual income increases. Based on this plot,
we can said that the client from California with annual income \$300000
have small chances for having a defaulted loans compared to other 26
clients from California who have annual income between \$50000 and
\$290000.
