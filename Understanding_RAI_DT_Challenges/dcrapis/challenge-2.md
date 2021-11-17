- Can you plot the data used for historical backtesting / future extrapolation on a separate Jupyter notebook?
- What happens if you modify the `data/controller_params.csv` file? For instance, what happens if the simulation is ran with non-zero values on `ki` and `leaky_factor`? Or make kp go up or down?
	- I focused on this part. Initially I changed the params a lot to see were the model would break, and it did indeed break (see below). However, after changing back the params to the original values in the csv file and re-running, the model does not converge anymore whenever I try to extrapolate for more then 5 periods. Even for 5 periods the controller seems to go out of whack (compare output vs output_challenge_1).

	The error below
	```
0. Retrieving Data
---
Retrieving hourly stats: 3it [00:01,  2.49it/s]
Retrieving System States: 100%|████████████████████████████████████████████████████████| 68/68 [00:10<00:00,  6.24it/s]
Retrieving SAFEs History: 100%|████████████████████████████████████████████████████████| 68/68 [00:10<00:00,  6.45it/s]
Data written at /Users/davide/Documents/projects/blockscience/reflexer-digital-twin/data/runs/2021-11-17 01:34:20.678894_retrieval.csv.gz
1. Preparing Data
---
2. Backtesting Model
---

                  ___________    ____
  ________ __ ___/ / ____/   |  / __ \
 / ___/ __` / __  / /   / /| | / / / /
/ /__/ /_/ / /_/ / /___/ ___ |/ /_/ /
\___/\__,_/\__,_/\____/_/  |_/_____/
by cadCAD

cadCAD Version: 0.4.28
Execution Mode: local_proc
Simulation Dimensions:
Entire Simulation: (Models, Unique Timesteps, Params, Total Runs, Sub-States) = (1, 67, 14, 1, 8)
     Simulation 0: (Timesteps, Params, Runs, Sub-States) = (67, 14, 1, 8)
Execution Method: local_simulations
Execution Mode: single_threaded
Total execution time: 0.04s
Backtesting loss: 0.17%
3. Fitting Stochastic Processes
---
Auto-assigning NUTS sampler...
Initializing NUTS using jitter+adapt_diag...
Sequential sampling (2 chains in 1 job)
NUTS: [beta, alpha]
Sampling 2 chains for 1_000 tune and 5_000 draw iterations (2_000 + 10_000 draws total) took 13 seconds. 1 divergences]
There were 5 divergences after tuning. Increase `target_accept` or reparameterize.
The acceptance probability does not match the target. It is 0.6854416215716941, but should be close to 0.8. Try to increase the number of tuning steps.
There were 6 divergences after tuning. Increase `target_accept` or reparameterize.
The number of effective samples is smaller than 25% for some parameters.
4. Extrapolating Exogenous Signals
---
5. Extrapolating Future Data
---

                  ___________    ____
  ________ __ ___/ / ____/   |  / __ \
 / ___/ __` / __  / /   / /| | / / / /
/ /__/ /_/ / /_/ / /___/ ___ |/ /_/ /
\___/\__,_/\__,_/\____/_/  |_/_____/
by cadCAD

cadCAD Version: 0.4.28
Execution Mode: local_proc
Simulation Dimensions:
Entire Simulation: (Models, Unique Timesteps, Params, Total Runs, Sub-States) = (1, 24, 14, 40, 8)
     Simulation 0: (Timesteps, Params, Runs, Sub-States) = (24, 14, 40, 8)
Execution Method: local_simulations
Execution Mode: parallelized
 ** On entry to DLASCLS parameter number  4 had an illegal value
 ** On entry to DLASCLS parameter number  4 had an illegal value
multiprocess.pool.RemoteTraceback: 
"""
Traceback (most recent call last):
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/multiprocess/pool.py", line 125, in worker
    result = (True, func(*args, **kwds))
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/multiprocess/pool.py", line 48, in mapstar
    return list(map(*args))
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/pathos/helpers/mp_helper.py", line 15, in <lambda>
    func = lambda args: f(*args)
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD/engine/execution.py", line 91, in <lambda>
    lambda t: t[0](t[1], t[2], t[3], t[4], t[5], t[6], t[7], t[8], t[9], configured_n), params
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD/engine/simulation.py", line 245, in simulation
    [execute_run(sweep_dict, states_list, configs, env_processes, time_seq, run)]
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD/engine/simulation.py", line 237, in execute_run
    first_timestep_per_run: List[Dict[str, Any]] = self.run_pipeline(
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD/engine/simulation.py", line 199, in run_pipeline
    pipe_run: List[Dict[str, Any]] = self.state_update_pipeline(
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD/engine/simulation.py", line 174, in state_update_pipeline
    states_list: List[Dict[str, Any]] = self.partial_state_update(
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD/engine/simulation.py", line 120, in partial_state_update
    self.get_policy_input(sweep_dict, sub_step, sH, last_in_obj, policy_funcs, additional_objs)
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD/engine/simulation.py", line 55, in get_policy_input
    col_results = get_col_results(sweep_dict, sub_step, sL, s, funcs)
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD/engine/simulation.py", line 42, in get_col_results
    return list(map(lambda f: policy_scope_tuner(additional_objs, f), funcs))
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD/engine/simulation.py", line 42, in <lambda>
    return list(map(lambda f: policy_scope_tuner(additional_objs, f), funcs))
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD/engine/simulation.py", line 39, in policy_scope_tuner
    return f(sweep_dict, sub_step, sL, s)
  File "/Users/davide/Documents/projects/blockscience/reflexer-digital-twin/rai_digital_twin/models/digital_twin_v1/model/parts/token_state.py", line 46, in p_user_action
    ewm_action = fit_predict_action(states,
  File "/Users/davide/Documents/projects/blockscience/reflexer-digital-twin/rai_digital_twin/system_identification.py", line 192, in fit_predict_action
    transformed_prediction = VAR_prediction(transformed_errors,
  File "/Users/davide/Documents/projects/blockscience/reflexer-digital-twin/rai_digital_twin/system_identification.py", line 107, in VAR_prediction
    results = model.fit(lag)
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/statsmodels/tsa/vector_ar/var_model.py", line 696, in fit
    return self._estimate_var(lags, trend=trend)
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/statsmodels/tsa/vector_ar/var_model.py", line 744, in _estimate_var
    params = np.linalg.lstsq(z, y_sample, rcond=1e-15)[0]
  File "<__array_function__ internals>", line 5, in lstsq
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/numpy/linalg/linalg.py", line 2306, in lstsq
    x, resids, rank, s = gufunc(a, b, rcond, signature=signature, extobj=extobj)
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/numpy/linalg/linalg.py", line 100, in _raise_linalgerror_lstsq
    raise LinAlgError("SVD did not converge in Linear Least Squares")
numpy.linalg.LinAlgError: SVD did not converge in Linear Least Squares
"""

The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "/usr/local/Cellar/python@3.9/3.9.7_1/Frameworks/Python.framework/Versions/3.9/lib/python3.9/runpy.py", line 197, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/local/Cellar/python@3.9/3.9.7_1/Frameworks/Python.framework/Versions/3.9/lib/python3.9/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/Users/davide/Documents/projects/blockscience/reflexer-digital-twin/rai_digital_twin/__main__.py", line 25, in <module>
    main()
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/click/core.py", line 1128, in __call__
    return self.main(*args, **kwargs)
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/click/core.py", line 1053, in main
    rv = self.invoke(ctx)
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/click/core.py", line 1395, in invoke
    return ctx.invoke(self.callback, **ctx.params)
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/click/core.py", line 754, in invoke
    return __callback(*args, **kwargs)
  File "/Users/davide/Documents/projects/blockscience/reflexer-digital-twin/rai_digital_twin/__main__.py", line 17, in main
    extrapolation_cycle(use_last_data=use_last_data,
  File "/Users/davide/Documents/projects/blockscience/reflexer-digital-twin/rai_digital_twin/execution_logic.py", line 284, in extrapolation_cycle
    extrapolation_df = extrapolate_data(extrapolated_signals,
  File "/Users/davide/Documents/projects/blockscience/reflexer-digital-twin/rai_digital_twin/execution_logic.py", line 189, in extrapolate_data
    sim_df = easy_run(initial_state,
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD_tools/execution/easy_run.py", line 50, in easy_run
    (records, tensor_field, _) = executor.execute()
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD/engine/__init__.py", line 152, in execute
    simulations_results = self.exec_method(
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD/engine/execution.py", line 131, in local_simulations
    return parallelize_simulations(
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD/engine/execution.py", line 101, in parallelize_simulations
    results = flatten(list(map(lambda params: process_executor(params), new_params)))
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD/engine/execution.py", line 101, in <lambda>
    results = flatten(list(map(lambda params: process_executor(params), new_params)))
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/cadCAD/engine/execution.py", line 90, in process_executor
    results = pp.map(
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/pathos/multiprocessing.py", line 139, in map
    return _pool.map(star(f), zip(*args)) # chunksize
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/multiprocess/pool.py", line 364, in map
    return self._map_async(func, iterable, mapstar, chunksize).get()
  File "/Users/davide/Documents/projects/blockscience/venv_rai/lib/python3.9/site-packages/multiprocess/pool.py", line 771, in get
    raise self._value
numpy.linalg.LinAlgError: SVD did not converge in Linear Least Squares
	```
- Are you able to modify the existing notebook template? What if we print summary statistics like the average Redemption Price over all the trajectory?
- Are you able to create a new notebook template that gets generated on each run? 

I'd like to try stress tests similar to [this](https://medium.com/reflexer-labs/summoning-the-money-god-2a3f3564a5f2):
- construct a scenario with 10x variance in price of ETH, etc
- add speculator behavioral model
- does it break controller outcome?
