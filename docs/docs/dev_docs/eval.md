# [evaluate.py](https://github.com/Shen-Lab/LOIS/blob/master/src/evaluate.py)

The main function for evaluating in LOIS.

`python evaluate.py --problem=$problem_name --optimizer=L2L --path=$path_to_the_saved_model`

* Arugments:
	- `problem`:  The name of the optimization problem for evaluation.
	- `optimizer`:  The optimizer used for optimizing the problem. For LOIS, set it equal = L2L.
	- `path`: The path to the trained model.