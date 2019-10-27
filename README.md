# Learn to Optimize in Swarms, guided by posterior estimation (with application to protein docking)


## Dependencies

* TensorFlow >=1.13
* [cNMA](https://github.com/Shen-Lab/cNMA) (For protein docking application)
* [CHARMM27](https://www.charmm.org/charmm/) (For protein docking application)


## Main File Explanation

*  meta.py:   The architecture of the model.
*  train.py:  The training program.
*  problems.py:  Store the optimization problems.
*  util.py:   Store the utility subroutines.
*  evaluate.py: The evaluation programs.

## Training

* Example: quadratic functions (see more problem options in the code)
python train.py --problem=quadratic --save_path=./quadratic


## Evaluation

* Example: quadratic functions (see more problem options in the code)
python evaluate.py --problem=quadratic --optimizer=L2L --path=./quadratic


## Protein Docking

### File Explanation
* get_12basis.py: Get the 12 basis vectors through [cNMA](https://github.com/Shen-Lab/cNMA) 
* force_field.py: The python implementation of CHARMM19 force field (including atom charge and rdii). 
* prepocess_prot.py: Generate input data.
* dataloader.py: Load input data into the model.
* charmm_setup.prl Set up prerequsites before runing CHARMM.

### Datasets:
* You can download data from https://drive.google.com/file/d/1x-Jye87YTWk_8WiooPJ23QJ_0zxiDT9V/view?usp=sharing.
* You can also generate your own data using above programs.
* ZDOCK data are from (https://zlab.umassmed.edu/zdock/) without CHARMM minimization.

### Data Generation Steps:
* 1.Prepare your own pdbs in a folder.
* 2.Modify the path in prepocess_prot.py and get_12basis.py to be the folder of your own pdbs.
* 3.Download CHARMM27 and minimize the pdb complex through CHARMM.
* 3.Download cNMA, and change the path of cNMA in get_12basis.py
* 4.run get_12basis.py, force_filed.py and then prepocess_prot.py.




## Citation



