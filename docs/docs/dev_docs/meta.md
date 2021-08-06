# [meta.py](https://github.com/Shen-Lab/LOIS/blob/master/src/meta.py)

The main function for defining the meta-optimizer computational graph and set up meta-training pipeline.

## Functions:

* `_nested_assign(ref, value)`

	- Returns a nested collection of TensorFlow assign operations.
	- Arguments:
		- `ref`: Nested collection of TensorFlow variables.
		- `value`: Values to be assigned to the variables. Must have the same structure
        as `ref`.

* `_nested_variable(init, name=None, trainable=False)`

	- Returns a nested collection of TensorFlow variables.
	- Arguments:
		- `init`: Nested collection of TensorFlow initializers.
		- `name`: Variable name.
		- `trainable`: Make variables trainable (`False` by default).

* `_wrap_variable_creation(func, custom_getter)`

	- Provides a custom getter for all variable creations.

* `_get_variables(func)`:
	- Calls func, returning any variables created, but ignoring its return value.

	- Arguments:
		- `func`: Function to be called.

	- Return:
		- A tuple (variables, constants) where the first element is a list of
    	trainable variables and the second is the non-trainable variables.

* `_make_with_custom_variables(func, variables)`:
	- Calls func and replaces any trainable variables.


* `_make_nets(variables, config, net_assignments):`:
	- Creates the optimizer networks.
	- Arguments:
		- `variables`: A list of variables to be optimized.
		- `config`: A dictionary of network configurations, each of which will be
		passed to networks.Factory to construct a single optimizer net.
		- `net_assignments`: A list of tuples where each tuple is of the form (netid,
		variable_names) and is used to assign variables to networks. netid must
		be a key in config.

	- Return:
		- A tuple (nets, keys, subsets) where nets is a dictionary of created
    optimizer nets such that the net with key keys[i] should be applied to the
    subset of variables listed in subsets[i].

## Classes:

* `class MetaOptimizer(object):`
	- Learning to learn (meta) optimizer.   Optimizer which has an internal RNN which takes as input, at each iteration,
  the gradient of the function being minimized and returns a step direction.
  This optimizer can then itself be optimized to learn optimization on a set of
  tasks.

  	- Attributes:
  		- `meta_loss(self,make_loss,len_unroll,net_assignments=None,model_path = None,second_derivatives=False)`

        - Arguments:	

			- `make_loss`: Callable which returns the optimizee loss; note that this
			should create its ops in the default graph.
			- `len_unroll`: Number of steps to unroll.
			- `net_assignments`: variable to optimizer mapping. If not None, it should be
			a list of (k, names) tuples, where k is a valid key in the kwargs
			passed at at construction time and names is a list of variable names.
			second_derivatives: Use second derivatives (default is false).

		- Return:
			- `loss`:  The tensor for the meta loss.
			- `update`: The variable for updating optimization trajectory.
			- `reset`:  The variable for reset optimizee.
			- `fx_final`:  The variable for final objective function value.
			- `x_final`:  The variable for final decision variable value.
			- `sub_constants`:  The variabler for optimizee constants.


		- `meta_minimize(self, make_loss, len_unroll, learning_rate=0.01, **kwargs)`
			- Returns an operator minimizing the meta-loss

			- Arguments:

				- `make_loss`: Callable which returns the optimizee loss; note that this
				should create its ops in the default graph.
				- `len_unroll`: Number of steps to unroll.
				- `learning_rate`: Learning rate for the Adam optimizer.
				- `**kwargs:` keyword arguments forwarded to meta_loss.

			- Return:
				- namedtuple containing (`step`, `update`, `reset`, `fx`, `x`)