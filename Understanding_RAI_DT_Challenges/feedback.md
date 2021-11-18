- @dcrapis
    1. When dealing with live systems, it's always important to keep in mind
    what's happening with the data. For instance, notice that the ones that are
    breaking are using recent data rather than data in May. 
    Inspecting the backtesting result shows that we're having some 
    TBD issues, possibly with the data sources. 
    (We didn't had any data for Nov 14 for instance).
    That's one of the challenges with simulating live systems with open data,
    sometimes it simply breaks :')
    2. Some tips:
        - Sweeping controller params: 
            - "Easy" way: change `controller_params.csv` and run the DT
                          several times in a row using the same data (`-l`).
            - "Pro" way: refactor the DT so that `controller_params.csv` has
            an additional column for keeping track of the sweeps. This would
            enable simulating counterfactual trajectories in terms of the
            history of controller params.
        - 10x variance in price of ETH: modify `https://github.com/reflexer-labs/reflexer-digital-twin/blob/79e49b78e1c5dbc2fb4297053ec4943e75ef4142/rai_digital_twin/stochastic.py#L133`
        so that `scale=fit_params.scale * 10` rather than just `scale=fit_params.scale`. 
        - Speculator model: logic should go on `p_user_action`: https://github.com/reflexer-labs/reflexer-digital-twin/blob/79e49b78e1c5dbc2fb4297053ec4943e75ef4142/rai_digital_twin/models/digital_twin_v1/model/parts/token_state.py#L35
- @zcstarr
    - Really great job! Super excited that you were able to create a new template
    and getting it working. As for the parameter changes: indeed your conclusions
    is what I would expect. Typical values for the params are on the order of 1E-8
    in order to not overshoot. 
- @henrikaxelsen (HAX)
    1. Great job!
    2. Good lit review! Those conclusions were based on previous design work,
       and one optional challenge is to see if they continue to hold given that 
       we now have real data and a live integrated model
    3. It is really about adding a new cell at `templates/extrapolation.ipynb`
    4. Actually, for creating a new notebook template you would need to create a jupyter notebook
    and then use the `execute_notebook` function of the Papermill library on `execution_logic.py`. Your notebook would need to be aware of the papermill parameters. (https://github.com/reflexer-labs/reflexer-digital-twin/blob/79e49b78e1c5dbc2fb4297053ec4943e75ef4142/rai_digital_twin/execution_logic.py#L294)
- @tree-pi (zhiwei_li)
    -  Good job overall! See the above feedback for a pointer on how to create
    a new template.
- @inventandchill
    - See previous feedbacks