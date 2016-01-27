
Also useful, R for Octave users: https://cran.r-project.org/doc/contrib/R-and-octave.txt

# Robin Lovelace's demonstration of nls
http://robinlovelace.net/2013/10/23/nls-demonstation.html

## basic curve fitting

```R
> len <- 24

# the function y = x^3 plus some noise
> x = runif(len)
> y = x^3 + runif(len, min = -0.1, max = 0.1)
> plot(x, y)

# this is our raw data
> df <- data.frame(x, y)

# fitting some power function, with unknown exponent
> m <- nls(y ~ I(x^power), data = df, start = list(power = 1), trace = T)

# this is neat, can just use `predict` to plot the line the model makes
> s <- seq(from = 0, to = 1, length = 50)
> lines(s, predict(m, list(x=s)), col="green")
```

![alt text](https://github.com/nadiahpk/playground-for-r/blob/master/ch2-nls/fit.png?raw=true "Fit to x cubed")

Measure fit
```R
> (RSS.p <- sum(residuals(m)^2))  # Residual sum of squares
[1] 0.06333526
> (TSS <- sum((y - mean(y))^2))  # Total sum of squares
[1] 1.831651
> 1 - (RSS.p/TSS)  # R-squared measure
[1] 0.9654218
```

## fitting to a pre-defined function

```R
> exp.eq <- function(x, a, b) {
+     exp(1)^(a + b * sin(x^4))
+ }
> m.sinexp <- nls(y ~ exp.eq(x, a, b), data = df, start = list(a = 1, b = 1))
> plot(x,y)
> lines(s,predict(m.sinexp, list(x=s)), col=2)
```

![alt text](https://github.com/nadiahpk/playground-for-r/blob/master/ch2-nls/fit2.png?raw=true "Fit to more complex equation")
