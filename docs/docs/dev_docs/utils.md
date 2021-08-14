# [util.py](https://github.com/Shen-Lab/LOIS/blob/master/src/util.py)

This file has two main usages:
* To run every eporch for training or evaluation
* To get problem config.

## Run epoch

* `run_epoch(sess, cost_op, ops, reset, num_unrolls, var1, var2)`

	- The training function for training the optimizer for one epoch.

	- Arguments:
		- `sess`: The tensorflow session variable.
		- `cost_op`: The variable for training the optimzier.
		- `ops`:   A list = [variable for training the optimizer, the variable for optimization step].
		- `reset`:  The initialization variable for initializing the optimizee before every epoch.
		- `num_unrolls`: The number of unrolled RNNs.
		- `var1`: The tensor for the constants in the optimizee.
		- `var2`: The variable for optimizer parameters.
	- Return:
		- The running time
		- The objective function values in this epoch.



* `eval_run_epoch(sess, cost_op, ops, reset, num_unrolls, var1, var2)`

	- The evaluation function for optimizing the objective function using the optimizer for one epoch.

	- Arguments:
		- `sess`: The tensorflow session variable.
		- `cost_op`: The variable for training the optimzier.
		- `ops`:   A list = [the variable for optimization step].
		- `reset`:  The initialization variable for initializing the optimizee before every epoch.
		- `num_unrolls`: The number of unrolled RNNs.
		- `var1`: The tensor for the constants in the optimizee.
		- `var2`: The variable for optimizer parameters.
	- Return:
		- The running time
		- The objective function values in this epoch.



## Get problem config

* ` get_config(problem_name, path=None, mode='train')`
	- The function for obtaining the config of the problem and the optimizer

	- Arguments:
		- `problem_name`: The name of the problem.
		- `path`:  The path to the saved optimizer. During training it is None, during evaluation it is set to be the saved optimizer.
		- `mode`:  A string variable which should be set to 'train' during training and 'test' during evaluation.

	- Return:
		- `problem`: The call for the problem (a.k.a objective function/optimizee)
		- `net_config`: A directory stores the configuration of the optmizer network.
		- `net_assignment`: The assignment for the optimizer network.