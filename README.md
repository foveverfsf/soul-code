--------------------

## Prerequisites:
1. Python 3.6
2. PyTorch >= 0.4.0
3. numpy
4. skimage
5. imageio
6. matplotlib
7. tqdm

For more informaiton, please refer to <a href="https://github.com/thstkdgus35/EDSR-PyTorch">EDSR</a> and <a href="https://github.com/yulunzhang/RCAN">RCAN</a>.




## Document
Train/             : all train files

Test/              : all test files

demo.sh        : all running instructions


## Dataset
We used DIV2K dataset to train our model. Please download it from <a href="https://data.vision.ee.ethz.ch/cvl/DIV2K/">here</a>  or  <a href="https://cv.snu.ac.kr/research/EDSR/DIV2K.tar">SNU_CVLab</a>.

Extract the file and put it into the Train/dataset.


## Training

Using --ext sep_reset argument on your first running.

You can skip the decoding part and use saved binaries with --ext sep argument in second time.


If you have enough memory, using --ext bin.
 
```
  cd Train/
  # MSRN x2  LR: 48 * 48  HR: 96 * 96
  python main.py --template MSRN --save MSRN_X2 --scale 2 --reset --save_results --patch_size 96 --ext sep_reset
  
  # MSRN x3  LR: 48 * 48  HR: 144 * 144
  python main.py --template MSRN --save MSRN_X3 --scale 3 --reset --save_results --patch_size 144 --ext sep_reset
  
  # MSRN x4  LR: 48 * 48  HR: 192 * 192
  python main.py --template MSRN --save MSRN_X4 --scale 4 --reset --save_results --patch_size 192 --ext sep_reset

```

## Testing
Using pre-trained model for training, all test datasets must be pretreatment by  ''Test/Prepare_TestData_HR_LR.m" and all pre-trained model should be put into "Test/model/".

```
#MSRN x2
python main.py --data_test MyImage --scale 2 --model MSRN --pre_train ../model/MSRN_x2.pt --test_only --save_results --chop --save "MSRN" --testpath ../LR/LRBI --testset Set5

#MSRN+ x2
python main.py --data_test MyImage --scale 2 --model MSRN --pre_train ../model/MSRN_x2.pt --test_only --save_results --chop --self_ensemble --save "MSRN_plus" --testpath ../LR/LRBI --testset Set5


#MSRN x3
python main.py --data_test MyImage --scale 3 --model MSRN --pre_train ../model/MSRN_x3.pt --test_only --save_results --chop --save "MSRN" --testpath ../LR/LRBI --testset Set5

#MSRN+ x3
python main.py --data_test MyImage --scale 3 --model MSRN --pre_train ../model/MSRN_x3.pt --test_only --save_results --chop --self_ensemble --save "MSRN_plus" --testpath ../LR/LRBI --testset Set5

/Users/juncheng/Documents/MSRN-PyTorch
#MSRN x4
python main.py --data_test MyImage --scale 4 --model MSRN --pre_train ../model/MSRN_x4.pt --test_only --save_results --chop --save "MSRN" --testpath ../LR/LRBI --testset Set5

#MSRN+ x4
python main.py --data_test MyImage --scale 4 --model MSRN --pre_train ../model/MSRN_x4.pt --test_only --save_results --chop --self_ensemble --save "MSRN_plus" --testpath ../LR/LRBI --testset Set5
```

We also introduce self-ensemble strategy to improve our MSRN and denote the self-ensembled version as MSRN+.

More running instructions can be found in demo.sh.
