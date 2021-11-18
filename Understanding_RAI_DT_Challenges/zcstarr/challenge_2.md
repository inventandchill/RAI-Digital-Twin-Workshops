## Challenges Overview 

- Can you plot the data used for historical backtesting / future extrapolation on a separate Jupyter notebook?

- What happens if you modify the `data/controller_params.csv` file? For instance, what happens if the simulation is ran with non-zero values on `ki` and `leaky_factor`? Or make kp go up or down?

- Are you able to modify the existing notebook template? What if we print summary statistics like the average Redemption Price over all the trajectory?

- Are you able to create a new notebook template that gets generated on each run? 

### Can you plot the data used for historical backtesting / future extrapolation on a separate Jupyter notebook?

- yes, I opted for displaying the data as a function of steps, would probably be better to do the timeseries like extrapolation 
[jupyternotebook](challenge_2.ipynb)

### What happens if you modify the `data/controller_params.csv` file? For instance, what happens if the simulation is ran with non-zero values on `ki` and `leaky_factor`? Or make kp go up or down? 

- Essentially the controller state values change in particular. The initial controller values track historical state.  

- For ki post modification increased to 1.0 from 0 does not track in fact flat lines the redemption price from backtesting and the redemption rate value also increases significantly, additionally it introduces huge proportional errors. 

- Oddly I didn't notice too much of a perceptible difference with modifying the leaky factor in proportional errors I did 0.5 for half of the time period to try and see what would happen. 

- Modifying kp caused the redemption prices and rates to swing wildly and overshoot, granted I did put in a number like 5 to push it to the extremes.

### Are you able to modify the existing notebook template? What if we print summary statistics like the average Redemption Price over all the trajectory?


- Yes I did just the average redemption price for the time series. [extrapolation.ipynb](extrapolation.ipynb)

### Are you able to create a new notebook template that gets generated on each run? 

- Yes, I modified the output via [execution_logic.py](execution_logic.py) and [zcstarr_template.ipynb](zcstarr_template.ipynb) here is the net [result](z2021-11-1801:02:02.350062-extrapolation.html)