# Applied Multivariate Statistical Analysis

## Ch 1 Aspects of Multivariate Analysis

Goals of Analysis

1. **Data reduction or structural simplification**
   Try to represent data as simply as possible without sacrificing valuable information. It hopes that this will make interpretation easier.

2. **Sorting and grouping**
   Groups similar objects or variables based upon measured characteristics.

3. **Investigation of the dependence among variables**
   The nature of the relationships among variables is of interest. 

4. **Prediction**
   Relationships between variables must be determined for the purpose of predicting the values of one or more variables on the basis of observations on the other variables.

5. **Hypothesis construction and testing**
   Specific statistical hypotheses, formulated in terms of the parameters of multivariate populations, are tested. This may be done to validate assumptions or to reinforce prior convictions. 

### Ch 1.3 The Organization of Data

#### Array

Multivariate data has a number $p\geq1$ of variables or characters to record. The values of these variables are all recorded for each distinct item, individual, or experimental unit. 

We will use the notation $x\_{jx}$ to indicate the particular value of the $k$th variable that is observed on the $j$th item, or trial. That is,

$$ x\_{jk} =  \text{measurement of the } k \text{th variable on the } j \text{th item }$$

Consequently, $n$ measurements on $p$ variables can be displayed as follows:

$$\begin{array}{cccccc} & \text { Variable 1 } & \text { Variable 2 } & \cdots & \text { Variable } k & \cdots & \text { Variable } p \\\ \text { Item 1: } & x\_{11} & x\_{12} & \cdots & x\_{1 k} & \cdots & x\_{1 p} \\\ \text { Item 2: } & x\_{21} & x\_{22} & \cdots & x\_{2 k} & \cdots & x\_{2 p} \\\ \vdots & \vdots & \vdots & & \vdots & & \vdots \\\ \text { Item } j: & x\_{j 1} & x\_{j 2} & \cdots & x\_{j k} & \cdots & x\_{j p} \\\ \vdots & \vdots & \vdots & & \vdots & & \vdots \\\ \text { Item } n: & x\_{n 1} & x\_{n 2} & \cdots & x\_{n k} & \cdots & x\_{n p}\end{array} $$ 

Or we can display these data as a rectangular array, called $X$, of n rows and p columns:

$$\mathbf{X}=\begin{bmatrix}
x\_{11} & x\_{12} & \cdots & x\_{1 k} & \cdots & x\_{1 p} \\\ x\_{21} & x\_{22} & \cdots & x\_{2 k} & \cdots & x\_{2 p} \\\ \vdots & \vdots & & \vdots & & \vdots \\\ x\_{j 1} & x\_{j 2} & \cdots & x\_{j k} & \cdots & x\_{j p} \\\ \vdots & \vdots & & \vdots & & \vdots \\\ x\_{n 1} & x\_{n 2} & \cdots & x\_{n k} & \cdots & x\_{n p}
\end{bmatrix}$$

The array $X$, then contains the data consisting of all of the observations on all of the variables. 

#### Descriptive Statistics

A large data set contains mass information, which can be assessed by calculating certain summary numbers, known as *descriptive statistics*. 

<div>
Let $x\_{11}, x\_{21}, \ldots, x\_{n 1}$ be $n$ measurements on the first variable. Then the arithmetic average of these measurements is
</div>

$$ \bar{x}\_{1}=\frac{1}{n} \sum\_{j=1}^{n} x_{j 1}  $$

If the $n$ measurements a subset of the full set of measurements that might have been observed, then $\bar{x}_1$ is also called the sample mean for the first variable. The sample mean can be computed from the $n$ measurements on each of the $p$ variables, so that, in general, there will be $p$ sample means:

$$ \bar{x}\_{k}=\frac{1}{n} \sum\_{j=1}^{n} x_{j k} \quad \text{ for } k = 1, 2, \ldots, p $$

A measure of spread is provided by the sample variance, defined for $n$ measurements on the first variable as 

$$ s^2\_1 = \frac{1}{n} \sum^n\_{j=1} (x_{jk} - \bar{x}\_1)^2 $$

where $\bar{x}\_1$ is the sample mean of the $x\_{j1}$'s. In general, for p variables, we have 

$$ s^2\_k = \frac{1}{n} \sum^n\_{j=1} (x_{jk} - \bar{x}\_k)^2 \quad \text{ for }  k = 1, 2, \ldots, p $$

Two comments are in order. First, many authors define the sample variance with a divisor of $ n - 1 $ rather than $n$, and it is particularly appropriate if the number of measurements, n, is small. The two versions of the sample variance will always be differentiated by displaying the appropriate expression. 

Second, although the $s^2$ notation is traditionally used to indicate the sample variance, we shall eventually consider an array of quantities in which the sample variance lie along the main diagonal. In this situation, it is convenient to use double subscripts on the variances in order to indicate their positions in the array. Therefore. we introduce the notation $s_{kk}$ to denote the same variance computed from measurements on the $k$th variable, and we have the notional identities. 

$$ s^2\_k = s\_{kk} = \frac{1}{n} \sum^n\_{j=1} (x_{jk} - \bar{x}\_k)^2 \quad \text{ for }  k = 1, 2, \ldots, p $$

The square root of the sample variance, $\sqrt{s_{k k}},$ is known as the sample standard deviation. This measure of variation uses the same units as the observations Consider $n$ pairs of measurements on each of variables 1 and 2

$$ 
 \left[\begin{array}{l} x\_{11} \\\ x\_{12} \end{array}\right],
 \left[\begin{array}{l} x\_{21} \\\ x\_{22} \end{array}\right],
 \dots,\left[\begin{array}{l} x\_{n 1} \\\ x\_{n 2} \end{array}\right] 
$$

That is, $x\_{j 1}$ and $x\_{j 2}$ are observed on the jth experimental item $(j=1,2, \ldots, n) .$ A measure of linear association between the measurements of variables 1 and 2 is provided by the sample covariance

$$
s\_{12}=\frac{1}{n} \sum\_{j=1}^{n}\left(x\_{j 1}-\bar{x}\_{1}\right)\left(x\_{j 2}-\bar{x}\_{2}\right)
$$

The sample variance measure the association between the *i*th and *k*th variables. 

$$
s\_{i k}=\frac{1}{n} \sum\_{j=1}^{n}\left(x\_{j i}-\bar{x}\_{i}\right)\left(x\_{j k}-\bar{x}\_{k}\right) \quad i=1,2, \ldots, p, \quad k=1,2, \ldots, p
$$

The *sample correlation coefficient (or Pearson	s product-moment correlation coefficient)*. This measure the linear association between two variables does not depend on the units of measurement. The sample sample correlation cofficient for the *i*th and *k*th variables is defined as 

$$
r\_{i k} = \frac{S\_{i k}}{\sqrt{S\_{ii}} \sqrt{S\_kk} } 
= \frac{ \sum\_{j=1}^{n}\left(x\_{j i}-\bar{x}\_{i}\right)\left(x\_{j k}-\bar{x}\_{k}\right)  }
{ 
\sqrt{\sum\_{j=1}^{n}\left(x\_{j i}-\bar{x}\_{i}\right)^2} 
\sqrt{\sum\_{j=1}^{n}\left(x\_{j k}-\bar{x}\_{k}\right)^2} 
}
\quad i=1,2, \ldots, p, \quad k=1,2, \ldots, p, \quad and \quad r\_{ik} = r\_{ki}
$$

The sample correlation coefficient $r\_{i k}$ is a standardized version of sample covariance, where the product of the square roots of the sample variances provides the standardization. 

The sample correlation coefficient $r\_{i k}$ can also be viewed as a sample covariance. Suppose the original values $x\_{j i}$ and $x\_{j k}$ are replaced by standardized values $(x\_{j i} - \bar{x\_{i}})/ \sqrt{s\_{ii}}$ and $(x\_{j k} - \bar{x\_{k}})/ \sqrt{s\_{kk}}$. The standardized values are commensurable because both sets are centered at zero and expressed in standard deviation units. The sample correlation coefficient is just the sample covariance of the standardized observations. 

The correlation is ordinarily easier to interpret because its magnitude is bounded. To summarize, the sample correlation r has the following properties:

1. The value of r must be between -1 and +1 inclusive.
2. Here r measures the strength of the linear association. If r = 0, this implies a lack of linear association between the components. Otherwise, the sign of r indicates the direction of the association: r < 0 implies a tendency for one value in the pair to be larger than its average when the other is smaller than its average; and r > 0 implies a tendency for one value of the pair to be large when the other value is large and also for both values to be small together. 
3. The value of $r\_{i k}$ remains unchanged if the measurements of the *i*th variable are changed to $y\_{j i} = a x\_{j k} + b, j = 1, 2, \ldots, n$, and the values of the *k*th variable are changed to $y\_{j k} = c x\_{j k} + d, j = 1, 2, \ldots, n$, provided that the constants a and c have the same sign. 

The quantities $s\_{i k}$ and $r\_{i k}$ do not, in general, convey all there is to know about the association between two variables, Nonlinear associations can exist that are not revealed by these descriptive statistics. Covariance and correlation provide measures of linear association, or association along a line. Their values are less informative for other kinds of association. On the other hand, these quantities can be very sensitive to "wild" observations ("outliers") and may indicate association when, in fact, little exists. In spite of these shortcomings, covariance and correlation coefficients are routinely calculated and analyzed. They provide cogent numerical summaries of association when the data do not exhibit obvious nonlinear patterns of association and when wild observations are not present. 

Suspect observations must be accounted for by correcting obvious recording mistakes and by taking actions consistent with the identified causes. The values of $s\_{i k}$ and $r_{i k}$ should be quoted both with and without these observations. 

The sum of squares of the deviations from the mean and the sum of cross-product deviations are often of interest themselves. These quantities are 

$$ w\_{k k} = \sum{j=1}^n (x\_{j k} - \bar{x\_k})^2 \quad k = 1, 2, \ldots, p$$

and $$ w\_{k k} = \sum{j=1}^n (x\_{j i} - \bar{x\_i})(x\_{j k} - \bar{x\_k}) \quad i = 1, 2, \ldots, p \quad k = 1, 2, \ldots, p$$

The descriptive statistics computed from n measurements on p variables can also be organized into arrays. 

<p align="center">
  <b>Arrays of Basic Descriptive Statistics</b>
</p>

$$
\begin{align}
\text { Sample mean }  \quad
\overline{\mathbf{x}}= & \left[\begin{array}{c}
\bar{x}\_{1} \\\\
\bar{x}\_{2} \\\\
\vdots \\\\
\bar{x}\_{p}
\end{array}\right]
\\\\
\text { Sample variances and covariances }  \quad \mathbf{S}\_{n}= & \left[\begin{array}{cccc}
s\_{11} & s\_{12} & \cdots & s\_{1 p} \\\\
s\_{21} & s\_{22} & \cdots & s\_{2 p} \\\\
\vdots & \vdots & \ddots & \vdots \\\\
s\_{p 1} & s\_{p 2} & \cdots & s\_{p p}
\end{array}\right]
\\\\
\text { Sample correlations }  \quad \mathbf{R}= & \left[\begin{array}{cccc}
1 & r\_{12} & \cdots & r\_{1 p} \\\\
r\_{21} & 1 & \cdots & r\_{2 p} \\\\
\vdots & \vdots & \ddots & \vdots \\\\
r\_{p 1} & r\_{p 2} & \cdots & 1
\end{array}\right]
\end{align}
$$



