# [network.py](https://github.com/Shen-Lab/LOIS/blob/master/src/network.py)

The main function for defining the optimizer network.

* `class StandardDeepLSTM(Network)`

	- Standard LSTM layers with a Linear layer on top.
	- **Arguments**:
		- `output_size`: Output sizes of the final linear layer.
		- `layers`: Output sizes of LSTM layers.
		- `preprocess_name`: Gradient preprocessing class name (in `l2l.preprocess` or
		tf modules). Default is `tf.identity`.
		- `preprocess_options`: Gradient preprocessing options.
		- `scale`: Gradient scaling (default is 1.0).
		- `initializer`: Variable initializer for linear layer. See `snt.Linear` and
		- `snt.LSTM` docs for more info. This parameter can be a string (e.g.
		"zeros" will be converted to tf.zeros_initializer).
		name: Module name.

	- **Arributes**:
	- `_build(self, inputs, prev_state):`

		- Connects the `StandardDeepLSTM` module into the graph.

		- Arguments:
			- `inputs`: 2D `Tensor` ([batch_size, input_size]).
			- `prev_state`: `DeepRNN` state.

		- Return:
			- `Tensor` shaped as `inputs`.

* `class CoordinateWiseDeepLSTM(StandardDeepLSTM)`
	- Coordinate-wise LSTM that is used in this study.

	- **Arguments**:
		- `output_size`: Output sizes of the final linear layer.
		- `layers`: Output sizes of LSTM layers.
		- `preprocess_name`: Gradient preprocessing class name (in `l2l.preprocess` or
		tf modules). Default is `tf.identity`.
		- `preprocess_options`: Gradient preprocessing options.
		- `scale`: Gradient scaling (default is 1.0).
		- `initializer`: Variable initializer for linear layer. See `snt.Linear` and
		- `snt.LSTM` docs for more info. This parameter can be a string (e.g.
		"zeros" will be converted to tf.zeros_initializer).
		name: Module name.

	- **Arributes**:
	- `_build(self, inputs, prev_state):`

		- Connects the CoordinateWiseDeepLSTM module into the graph.

		- Arguments:
			- `inputs`: Arbitrarily shaped `Tensor`.
			- `prev_state`: `DeepRNN` state.

		- Return :
			- `Tensor` shaped as `inputs`.