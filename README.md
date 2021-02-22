# RL

## tensorflow2.x 在实现RL算法时遇到的问题

1. @tf.function 中的model问题
   * model.predict(X)不能用
   * model(X)可以用
2. with tf.GradientTape() as tape 中遇到的问题
   * model.predict(X)不能用
   * model(X)可以用

   ***原因分析***
   > Keras with tensorflow backend was using underlying tensorflow objects, but mostly was providing high level outputs which could be understood outside the tensorflow environment (as an example it could output numpy arrays or python lists).
Today given a model in tensorflow 2.0 (built using the keras library),

   `out_np = model.predict(x)`

   > provides a numpy array which can, as an example, be printed with print(out_np).
On the other hand,

   `out_tf = model(x)`

   > results into a tensorflow object, wich can be converted to a numpy array with .numpy()
The two results are equivalent, as an example, we have that the following is True,

   `out_np.max() == out_tf.numpy().max()`

   
   