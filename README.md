Keep Track of Training and Testing Loss When Using Caffe
When using Caffe to train a deep neural network, how to record the training/testing loss or accuracy, throughout iterations?

I know the following works, though without understanding the details.

Run in terminal:

 $ caffe_root/build/tools/caffe train --solver=solver.prototxt 2>&1 | tee mylog.log  


Notice the appended part in red, which will log the information shown in the terminal to "mylog.log"

Then run in terminal,

 $ python caffe_root/tools/extra/parse_log.py mylog.log ./  
Now you will see under ./, there are two files, mylog.log.train, and mylog.log.test. They are two csv files that record training and testing loss.

Then you could run gnuplot to quickly visualize the loss/accuracy during iterations. But first you need to comment the 1st line of the two files by #

The .train (or .test) file is of the following form:

#NumIters,Seconds,LearningRate,accuracy,loss
0,****,****,****,****
100,****,****,****,****
.
.
.

Then in terminal run,

 $ gnuplot  
 gnuplot> set datafile separator ','  
 gnuplot> plot 'mylog.log.train' using 1:4 with line # accuracy throughout the iterations  
 gnuplot> plot 'mylog.log.train' using 1:5 with line # loss throughout the iterations  
