# Add your function

In order to add your functions for either training or evaluation, you should first navigate to the file `src/problems.py` and provide your function like the following example:

	def quadratic(batch_size=128, num_dims=10, stddev=0.01, dtype=tf.float32):
	  """Quadratic problem: f(x) = ||Wx - y||."""

	  def build():
	    """Builds loss graph."""
	    
	    # Trainable variable.
	    x = tf.get_variable(
	        "x",
	        shape=[batch_size, num_dims],
	        dtype=dtype,
	        initializer=tf.random_normal_initializer(stddev=stddev))
	    w = tf.get_variable("w",
	                        shape=[batch_size, num_dims, num_dims],
	                        dtype=dtype,
	                        initializer=tf.random_uniform_initializer(),
	                        trainable=False)
	    y = tf.get_variable("y",
	                        shape=[batch_size, num_dims],
	                        dtype=dtype,
	                        initializer=tf.random_uniform_initializer(),
	                        trainable=False)
	    print(y.get_shape())
	    product = tf.squeeze(tf.matmul(w, tf.expand_dims(x, -1)))
	    
	        
	    return (tf.reduce_sum((product - y) ** 2, 1))

	  return build

The above example creates a quadratic function f(x) = ||Wx - y||, where W and y are sampled from normal distributions.