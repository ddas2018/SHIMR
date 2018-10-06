### SHIMR (Sparse High-order Interaction Model with Rejection option)
SHIMR is basically a forward feature selection with simultaneous sample reduction method to iteratively search for higher order feature interactions from the power set of complex features by maximizing the classification gain.

Sample reduction is achieved by incorporating the notion of <b>"Classification with rejection option"</b> which essentially minimizes the classification uncertainty, specifically in case of noisy data. One potential application of this method could be in clinical diagnosis (or prognosis). Below one can see that SHIMR has the ability to identify the ambiguous low confidence zones (close to the decision boundary) and refrain from taking any decision (R: reject) for those data points (encircled). High rejection rate (rr) conforms to high prediction probability of the classified samples and hence more reliability in prediction. In a sense SHIMR makes decision only for those data points for which it is highly confident (high positive predictive probability) and thus can serve as a highly reliable CAD model to a medical practitioner (e.g. Doctor). 

<img src="Images/moon1.png" width="400">  <img src="Images/moon2.png" width="400">

Our visualization module complements SHIMR by generating a simple and easily comprehensible visual representation of the model generated by SHIMR. Below is a visualization of SHIMR when applied on "Breast Cancer Wisconsin (Diagnostic) Data Set" from UCI Machine Learning Repository (https://archive.ics.uci.edu/ml/datasets/Breast+Cancer+Wisconsin+(Diagnostic)). Our visualization module can clearly represent the weighted combination of simple rules based classification model generated by SHIMR.



<img src="Images/figure_RID_91550.png" width="700"> <img src="Images/legend.png" width="150">




## Getting Started
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.
## Prerequisites
<b> "SHIMR" </b> has the following two dependencies <br/>
1) CPLEX Optimizer  <br/>
2) Linear Time Closed Itemset Miner (LCM v5.3)  <br/>
&emsp; &ensp; Coded by Takeaki Uno,   e-mail:uno@nii.jp, 
homepage:   http://research.nii.ac.jp/~uno/code/lcm.html

Apart from that the current implementation is in python which is tested with the following python setup <br/>

1) Python 3.4.5 <br/>
2) scikit-learn==0.19.1 <br/>
3) scipy==1.0.0 <br/>
4) numpy==1.14.1 <br/>
5) pandas==0.22.0 <br/>
5) matplotlib==2.0.0 <br/>

### Download <br/>
<b> "IBM ILOG CPLEX Optimization Studio" </b>  from  https://www-01.ibm.com/software/websphere/products/optimization/cplex-studio-community-edition/ <br/>
<b> "LCM ver. 5.3" </b>  from  http://research.nii.ac.jp/~uno/codes.htm


## Installing
A step by step instructions that will guide you to get a working copy of "SHIMR" in your own development environment.

<b> A.  Create a virtual environment </b>

Download "anaconda" from https://www.continuum.io/downloads <br/>

1) Install Anaconda <br/>
```
$ bash Anaconda-latest-Linux-x86_64.sh       (Linux)  or
$ bash Anaconda-latest-MacOSX-x86_64.sh      (Mac)
```

2) Activate anaconda environment  <br/>
```
source anaconda/bin/activate anaconda/
```

3) Create a new environment and activate it <br/>
```
$ conda create -n r_boost python=3.4.5
$ source activate r_boost
$ pip install -r requirements.txt
```


<b> B.  Install "IBM ILOG CPLEX Optimization Studio" </b>

1) Download "cplex_studioXXX.linux-x86.bin" (Linux) or "cplex_studioXXX.osx.bin" (Mac) file <br/>

Make sure the .bin file is executable. If necessary, change its permission using the chmod command from the directory where the .bin is located: <br/>

```
$ chmod +x cplex_studioXXX.linux-x86.bin
```

2) Enter the following command to start the installation process: <br/>
```
$ ./cplex_studioXXX.linux-x86.bin
```

3) Provide the follwing installation path: <br/>
```
$ /home/user/ibm/ILOG/CPLEX_StudioXXX 
```
4) Change directory to CPLEX installation path <br/>
```
$ cd /home/username/ibm2/ILOG/CPLEX_StudioXXX/cplex/python/3.4/x86-64_linux                (Linux)  or
$ cd /Users/username/Applications/IBM/ILOG/CPLEX_StudioXXX/cplex/python/3.4/x86-64_osx/     (Mac)
```

5) Install python version of CPLEX
```
$ python setup.py install
```

<b> C.  Install "LCM ver. 5.3" </b>
```
1) Unzip the 'lcm53.zip' directory
2) cd lcm53
3) make
```

## Running the tests
To test SHIMR we included "Breast Cancer Wisconsin (Diagnostic) Data Set" 
from UCI Machine Learning Repository under the Data folder.
Please run 'code/main_WDBC.ipynp' in an interactive mode to see the sparse high order interactions of features generated by
our visualization module. SHIMR can also be tested from command line by running 'main.py'. Please run it with the help flag [- h] to check the argument requirements of SHIMR to run from command line.

```
python main.py -h
```

```
usage: main.py [-h] [-d D] [-n_bins N_BINS] [-c_pos C_POS] [-c_neg C_NEG]
               [-size_u SIZE_U] [-r] [-v] [-pd] [-pa]
               f_data

Usage of SHIMR

positional arguments:
  f_data          File path of input data to SHIMR. File format should be
                  ".npy". The file should contain data in the format of
                  "[data_train, data_test, Feature_dict, class_labels_dict]".
                  Feature_dict is an ordered dictionary (collections.OrderedDict()) 
                  to provide a short name of feature (Key) if it has long name (Value).
                  A typical example can be wdbc_dict["Rad_M"]= "Radius Mean".
                  class_labels_dict is a class labels dictionary. A typical example can
                  be "class_labels_dict={-1:"Benign", +1:"Malignant", 0:"Rejected"}".

optional arguments:
  -h, --help      show this help message and exit
  -d D            Set rejection cost
  -n_bins N_BINS  Set number of bins
  -c_pos C_POS    Set regularization parameter value for positive class
  -c_neg C_NEG    Set regularization parameter value for negative class
  -size_u SIZE_U  Set the order of feature interaction
  -r              To apply rejection option
  -v              To generate visualization
  -pd             To display the plot (default: File saved)
  -pa             To generate visualization for all subjects
  
  ```

## Visualization module
Motivation of our visualization module came from "UpSet: Visualizing Intersecting Sets" (http://caleydo.org/tools/upset/) and its python implementation (https://github.com/ImSoErgodic/py-upset).





