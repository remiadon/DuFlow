# DuFlow

main source : openbb
main dependencies:
 - polars : fast sourcing and massaging
 - infomeasure : high quality measures like 

We can use tigramite as a baseline, although more modern frameworks have been published

## shortcoming of existing methods: 
regular causal inference makes too many assumptions
 - causal structure meant to be fixed
 - time lag is fixed
CDS-NOTS accounts for time by considering the "arrow of time (Ut)" as a confounding variable, amongth other variables, when running CI tests
available tooling designed for tabular data, not really accounting for the dynamic aspect of time
