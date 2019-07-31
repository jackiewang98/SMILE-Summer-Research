# Preprocess

## Format of data

All files are saved as .mat
1. **OCT image:** 

   - control: 115 normal subjects: [.mat]
     - 100 OCT images ('images'): **(W, H, D)**
       - W: width is 512 pixels
       - H: height is 1000 pixels
       - D: dimension is 100
     - 1 set with 3 thickness maps('layermaps')
       - NSR
       - RPEDC
       - TRT

   - AMD: 269 patient subjects[.mat]

     the same as 'control'

2. **Thickness map:**

   - the layer-maps after interpolation

## Pre-requisition of data-generator

processing for 'images' , 'Ages' and 'layerMaps'

1. **Transpose**

   - former shape: (W, H, D)

     - OCT images: (512, 1000, 100)
     - layermaps: (100, 1000, 3)

   - latter shape: (D, W, H)

     - OCT: images(100,512,1000)
     - layermaps: (3,100, 1000)

2. **Concatenate**

   - read all subject-files in order
   - ignore the file 'control_subject_1088.mat' (the file is not put in the train-test set)
   - output after concatenating all images of subjects: [.npy]
     - 'Control': 
       - images: (11400, 512, 1000)
       - layermaps: 3 * (114, 100, 1000)
     - 'AMD' :
       - images: (26900, 512, 1000)
       - layermaps: 3 * (269, 100, 1000)
   
3. **Split train-valid-test sets**

   - Control subjects: 
   
   - train:  [1001-1087]
     - valid: splited from train set, by set the parameter
     
       ```python
       # keras Model class API
       model.fit(validation_split=0.0)
       ```
     
     - test: [1089-1115]
     
   - AMD subjects

