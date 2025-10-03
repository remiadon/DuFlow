# DuFlow

main source : openbb
main dependencies:
 - polars : fast sourcing and massaging
 - infomeasure : high quality measures like 


approach : 
regular causal inference makes too many assumptions
 - causal structure meant to be fixed
 - time lag is fixed
available tooling designed for tabular data, not really accounting for the dynamic aspect of time

shortcomings of CD-NOTS
 - accounts for time by considering the "arrow of time (Ut)" as a confounding variable, amongth other variables, when running CI tests
 - fixed lags


We can use tigramite as a baseline, although more modern frameworks have been published


Running CI tests ?
- a baseline is the Kernel Conditional Independance test, but it's not designed for Time Series. We would try building a bespoke kernel based on dtw ... but DTW has many caveats and this is not really theoretically sound
- another caveat of KCI, and CI more generally, is that we don't get a direction + a strength in the relation
- we can used the conditional Transfer Entropy from infomeasure
- knowing that does not solve our "optimal time warping" issue

If a fixed lag approach is not relevant, how can we find an efficient vector of lags from a source to a target ?
Here is the proposed approached
 - a baseline can be drawn using a rolling window XI-corr approach : we pick a window size and roll on with xi-corr, we pick the lag yielding the best corr. This can be achieved in pure polars. Careful with the ranks needed for xi-corr : they need to be built once for all
 - we can use a similar approach but using Transfer Entropy, either in a rolling-window fashion or using Dynamic Programming.
 - Once the vector of "optimal time warping" is found: it can be studied as a standalone output. It is the context in which information from `source` ideally transits to `target`
 - we can reuse this vector to twist the source series, and then study statistical dependence from this derived source to the target 
