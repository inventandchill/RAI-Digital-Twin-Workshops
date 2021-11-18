1. Can you tweak the error being used by the RAI controller? What happens if the integral error is simply the immediate error? Or if other integration rules are used? like Simpson's rule?
2. Right now, the RAI is being modelled as a PI controller. What is required in order to turn it to a PID one? Are you able to implement a demonstration?
3. How would you introduce events into the past and future? How should someone proceed to include shocks into the extrapolation phase?
4. What behavioural model would you introduce on the model? How it would modify the TokenState object? Are you able to implement it?
    - One simple example would be to simulate the effect of an arbitrary liquidity incentive mechanism. This should modify the TokenState on the `rai_reserve` and `eth_reserve` simultaneously.
 