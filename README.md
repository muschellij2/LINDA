# LINDA
Lesion Identification with Neighborhood Data Analysis  
  
Download all the repository and unzip the folder in your local computer.  
  
Open R and source linda_predict.R.  
  
A file dialog will appear on the screen, select the T1 nifti file of the patient with left hemispheric brain damage.
LINDA will run and the results will be found in a folder named "linda" in the same path where the T1 is located.  
  
Example  
10:42 Loading template...  
10:42 Creating folder: /data/jag/myhome/LINDAtest/linda  
10:42 Loading file: SybjectT1.nii  
10:42 Skull stripping... (long process)  
11:06 Saving skull stripped files  
11:06 Loading LINDA model  
11:06 Computing asymmetry mask...  
11:09 Saving asymmetry mask...   
11:09 Running 1st registration...   
11:16 Feature calculation...   
11:21 Running 1st prediction...   
11:22 Saving 1st prediction...   
11:22 Backprojecting 1st prediction...   
11:22 Running 2nd registration...   
11:29 Feature calculation...   
11:33 Running 2nd prediction...   
11:34 Saving 2nd prediction... 
11:34 Backprojecting 1st prediction... 
11:34 Running 3rd registration... (long process)
13:15 Saving 3rd registration results... 
13:15 Feature calculation... 
13:19 Running 3rd prediction... 
13:20 Saving 3rd final prediction... 
13:20 Saving 3rd final prediction in native space... 
DONE
