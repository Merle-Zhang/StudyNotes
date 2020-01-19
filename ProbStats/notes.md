# Probability

1. Probability
   * Sample Space
   
     * A set of points which are the possible **outcomes** of a **trial**.
   
   * Event
   
     * A subset of a sample space.
   
   * Probability
     * A map from events to real numbers
       * $ P(A) \geq 0$ for all events
       
       * $P(X) = 1$
       
       * If $A \cap B = \emptyset$ for two events $A$ and $B$ then
         $$
         P(A \cup B) = P(A) + P(B)
         $$
     
   * Probability mass function
   
     * A map from points in the sample space to real numbers
       * $p(x) \geq 0$ for all $x \in X$
       * $\sum_{x \in A}p(x) = 1$
   
   * $P(A)=\sum_{x\in A}p(x)$
   
   * If all the points in a sample space have the same probability then
     $$
     P(A)=\frac{\mbox{number of points in }A}{\mbox{number of points in }X}=\frac{\#A}{\#X}
     $$
     where $\#(A)$ means the number of points in $A$.
   
   * The **binomial coefficient**(Combination)
     $$
     \left(\begin{array}{c}n\\r\end{array}\right)=\frac{n!}{r!(n-r)!}
     $$








binomial distribution







# Statistics

* **Linear Regression**:

  * **Standard error of the estimate**: $\sqrt{\frac{\sum(estimated\space\hat {y}-actual\space y)^2}{(sample\space size-2)}}$, 

    sample size - 2 also called degree of freedom

  * **R squared**: $\frac{\sum(estimated\space\hat {y}-mean\space y)^2}{\sum(actual\space y-mean\space y)^2}$

* **Chi square**: 

  * **goodness of fit**: $X^2=\sum\frac{(o-e)^2}{e}$

    where o is observed value, e is expected value

* 1sd: 68%, 2sd: 95%, 3sd: 99%

* Type of data
  * continuous independent variable
    * continuous dependent variable: **regressions**
    * discrete dependent variable: **Logistic regressions**
  * discrete independent variable
    * continuous dependent variable
      * normally distributed
        * 2 groups
          * non paired: **T-test**
          * pared: **Paired-t-test**
        * more than 2 groups: **ANOVA**
      * Check normality: 
        * **Kolmogorov-Smirnov test**: $n>50$, not sensitive to problems in the tails
        * **Shapiro-Wilks test**: $n<50$, doesn't work well if several values are same
      * skewed
        * 2 groups
          * non paired: **Mann-Whitney U Test**
          * paired: **Wilcoxon signed rank test**
        * more than 2 groups
          * non paired: **Kruskal-Wallis test**
          * paired: **Friedman test**
    * discrete/categorical dependent variable
      * 2 groups
        * non paired
          * Counts >= 5 in >= 75% cells: **Chi-square test**
          * Counts >= 5 in < 75% cells: **Fisher's exact test**
        * paired: **McNemar's test**
      * more than 2 groups: **Chi-square test**