# [problems.py](https://github.com/Shen-Lab/LOIS/blob/master/src/problems.py)

This file stores the problems (a.k.a. objective function or optimizee) that you want LOIS to train or evaluate. Every problem should be in a format of function. Typically the function has two arguments:

- `num_dims`:   The dimension of the problem.
- `mode`:       A str indicates whether the problem is used during training or testing.

This file is called by the function `get_config` in [util.py](https://github.com/Shen-Lab/LOIS/blob/master/src/util.py).  You need to add this function in `get_config` as well following the template there.

An example of a problem is Rastrigin (square_cos):

	def square_cos(num_dims=2, mode='train'):

		def build():
			"""Builds loss graph."""

			batch_size=128
			stddev=0.01
			dtype=tf.float32
			if mode=='test':
			x = tf.get_variable(
				"x",
				shape=[batch_size, num_dims],
				dtype=dtype,
				initializer=tf.random_uniform_initializer(-3, 3))
			return ( tf.reduce_sum(x*x - 10*tf.math.cos(2*3.1415926*x), 1)+ 10*num_dims )


			# Trainable variable.
			x = tf.get_variable(
				"x",
				shape=[batch_size, num_dims],
				dtype=dtype,
				initializer=tf.random_uniform_initializer(-3, 3))

			# Non-trainable variables.
			w = tf.get_variable("w",
								dtype=dtype,
								initializer=indentity_init(batch_size, num_dims, stddev/num_dims),
								trainable=False)

			y = tf.get_variable("y",
								shape=[batch_size, num_dims],
								dtype=dtype,
								initializer=tf.random_normal_initializer(stddev=stddev/num_dims),
								trainable=False)

			wcos = tf.get_variable("wcos",
								shape=[batch_size, num_dims],
								dtype=dtype,
								initializer=tf.random_normal_initializer(mean=1.0, stddev=stddev/num_dims),
								trainable=False)

			product = tf.squeeze(tf.matmul(w, tf.expand_dims(x, -1)))
			product2 = tf.reduce_sum(wcos*10*tf.math.cos(2*3.1415926*x), 1)


			return (tf.reduce_sum((product - y) ** 2, 1)) - tf.reduce_mean(product2) + 10*num_dims
		return build


Its caller in `get_config` function is:


	elif  "square_cos" in problem_name:
		num_dims = int(problem_name.split('_')[-1])
		problem = problems.square_cos(batch_size=128, num_dims=num_dims, mode=mode)
		net_config = {"cw": {
			"net": "CoordinateWiseDeepLSTM",
			"net_options": {"layers": (20, 20)},
			"net_path": get_net_path("cw", path)
		}}
		net_assignments = None