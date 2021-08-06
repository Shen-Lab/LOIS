# Evaluate your optimizer 

In order to evaluate your optimizer, you can run:

`python evaluate.py --problem=$problem_name --optimizer=L2L --path=$path_to_the_saved_model`

where `$problem_name` is the name of your problem; `--optimizer` gives the name of the optimizer and `--path` is the path to your trained model. For instance,  in order to evalute a 2D Rastrigin function, you can set `--problem=square_cos_2d` and `--path=../trained_models/square_cos_2/`.