We provide an overview of the important files and their relationships.

* *Training*: `train.py` is the main file during training. It will run every epoch, save network parameters. It will call other files one by one that are used for training.
    - **Before training**:
        - **Load optimizer network congifuration**: `config.py`.  The `train.py` will call `config.py` in order to red optimizer net configuration.
        - **Load optimizee problem**: `config.py` -> `problems.py`.   The `train.py` will call `config.py`, which will call `problems.py` in order to load the optimizee problems used for training.
        - **Load optimizer network**: `meta.py`.  The `train.py` will use the optimizer net configuration information to build an optimizer in `meta.py`.
        - **optimizer-optimizee graph**: `meta.py`. The `meta.py` will also build a complete computational graph with both optimizer and optimizee.
    
    - **During training**: 
        - **run every epoch**: `config.py`. This file will run every epoch during training.
    - **After training**:
        - **save meta net parameters**: `train.py`. This file will save the meta net parameters.


* *Evaluation*: `evaluate.py` is the main file during evaluation. It will run a whole evaluation trajectory and save the trajectory. It will call other files one by one that are used for evaluation.
    - **Before evaluation**:
        - **Load optimizer network congifuration**: `config.py`.  The `evaluate.py` will call `config.py` in order to red optimizer net configuration.
        - **Load optimizee problem**: `config.py` -> `problems.py`.   The `evaluate.py` will call `config.py`, which will call `problems.py` in order to load the optimizee problems used for evaluation.
        - **Load optimizer network**: `meta.py`.  The `evaluate.py` will use the optimizer net configuration information to build an optimizer in `meta.py`.
        - **optimizer-optimizee graph**: `meta.py`. The `meta.py` will also build a complete computational graph with both optimizer and optimizee.
    
    - **During evaluation**: 
        - **run the trajectory**: `config.py`. This file will run the trajectory during evaluation.
    - **After evaluation**:
        - **save the trajectory**: `evaluate.py`. This file will save the trajectory.