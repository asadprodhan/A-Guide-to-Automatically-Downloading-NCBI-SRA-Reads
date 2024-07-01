# **How to automatically download reads from the NCBI SRA?** <br />


<br />


### **AUTHOR: Dr Asad Prodhan** https://asadprodhan.github.io/

[![License GPL 3.0](https://img.shields.io/badge/License-GPL%203.0-yellow.svg)](https://github.com/asadprodhan/How-to-automatically-download-reads-from-the-NCBI-SRA#GPL-3.0-1-ov-file)


<br />


<br />


## **Step 1: Download and setup the SRA Tool Kit**


<br />


- Create a directory on your Linux Desktop


```
mkdir sratoolkits
```


- cd to sratoolkits and download the sra tool kit using the following link:


```
sudo wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/current/sratoolkit.current-ubuntu64.tar.gz
```


> Visit: https://github.com/ncbi/sra-tools/wiki/02.-Installing-SRA-Toolkit


- Move the sratoolkits directory in your /usr/bin directory


- cd to the sratoolkits/sratoolkit.3.1.1-ubuntu64/bin directory


- Find out the path by running the following command


```
pwd
```


- Now, add this path to your PATH variable as follows:


```
export PATH=$PATH:path/to/sratoolkits/sratoolkit.3.1.1-ubuntu64/bin
```


> Note that there should not be any space on either sides of the "=" sign in the above command


<br />


### **However, you log out, the path will drop from the PATH variable. If you want to add the above (or any path) to the PATH variable permanently, then follow the following steps:**


<br />


```
nano ./bashrc
```

The above command will open the bashrc profile.


Now, copy and paste the following command in the bashrc profile, save and close.

 
```
export PATH=$PATH:path/to/sratoolkits/sratoolkit.3.1.1-ubuntu64/bin
```


<br />


### **Has the sratoolkit been added to your PATH variable?**


<br />


To test, get out of your current directory and run the following command:


```
fasterq-dump
```


<br />


> fasterq-dump is one of the executibles located in the sra tool kit bin directory. If the sra tool kit has been added to your PATH variable, the above command should be run from any directory in your Linux computer without needing to specifying the path of its executible in the command. And the above command will produce the usage options on the screen. Then, it's all good!


<br />


Now, you are ready to download the reads from the NCBI SRA


<br />


## **Collect SRA Accession Numbers**


<br />


We will use the Bioproject from the following publication as an example:

https://www.sciencedirect.com/science/article/pii/S094450131930970X#sec0010


- Open the NCBI SRA


https://www.ncbi.nlm.nih.gov/sra/docs/


- Search the Bioproject number as follows



<br />


<p align="center">
  <img 
    src="https://github.com/asadprodhan/How-to-automatically-download-reads-from-the-NCBI-SRA/blob/main/1.PNG"
 align="center" width=50% height=50% >   
</p>
<p align = center>
Figure 1: NCBI SRA Search Box.
</p>

<br />


- Scroll down to the bottom of the page and select "Run Selector" and press Go. See the screenshot below


<br />


<p align="center">
  <img 
    src="https://github.com/asadprodhan/How-to-automatically-download-reads-from-the-NCBI-SRA/blob/main/2.PNG"
 align="center" width=50% height=50% >   
</p>
<p align = center>
Figure 2: NCBI SRA Run Selector.
</p>

<br />


- Click on the Accession List and Metadata as marked on the following screenshot


<br />


<p align="center">
  <img 
    src="https://github.com/asadprodhan/How-to-automatically-download-reads-from-the-NCBI-SRA/blob/main/3.1.png"
 align="center" width=50% height=50% >   
</p>
<p align = center>
Figure 3: NCBI SRA Accesssion List and Metadata.
</p>

<br />



- The Accession List will look like this



<br />


<p align="center">
  <img 
    src="https://github.com/asadprodhan/How-to-automatically-download-reads-from-the-NCBI-SRA/blob/main/4.PNG"
 align="center" width=50% height=50% >   
</p>
<p align = center>
Figure 4: NCBI SRA Accesssion List.
</p>

<br />



- The Metadata will look like this



<br />


<p align="center">
  <img 
    src="https://github.com/asadprodhan/How-to-automatically-download-reads-from-the-NCBI-SRA/blob/main/5.PNG"
 align="center" width=100% height=100% >   
</p>
<p align = center>
Figure 5: NCBI SRA Metadata.
</p>

<br />


<br />

 

## **Download Reads**


<br />


- There are two steps to download the reads


    - The first step will download the reads in SRA format using a command called prefetch


    - The second step will convert the SRA format into fastq using a command called fasterq-dump
 

 <br />

 
### **The following script has combined both commands in a single script to automate downloading reads from a list of accessions**


 <br />
 

```
#!/bin/bash

# Description: This script automatically downloads NCBI SRA reads
# Author: Asad Prodhan PhD
# Email: prodhan82@gmail.com
# Date: 2024-07-01
# Version: 1.0


# File containing the list of SRA accession numbers
SRA_LIST="SRR_Acc_List.txt"

# Loop through each accession number in the list
while IFS= read -r accession; do
    echo "Processing $accession"
    prefetch.3.1.1 $accession && fasterq-dump.3.1.1 $accession --outdir reads
done < "$SRA_LIST"

# The end
```


<br />


> Note that the older versions of prefetch cannot locate the reads in the NCBI SRA. You need to use the latest version.


<br />



[1] Download the script [here](https://github.com/asadprodhan/How-to-automatically-download-reads-from-the-NCBI-SRA/blob/main/prefetch_fasterq-dump.sh) and save as prefetch_fasterq-dump.sh 


<br />


[2] Put the above script and your Accession List in the same directory and run 


<br />


[3] Run the following command to confirm that both documents are in unix format


<br />


```
dos2unix *
```


<br />


[4] Run the following command to confirm that you have execution permission


<br />


```
chmod +x *
```


<br />


[5] Now, run the script as follows


<br />


```
./prefetch_fasterq-dump.sh
```


<br />


### **The reads will be automatically downloaded and saved in the reads directory**


<br />


<p align="center">
  <img 
    src="https://github.com/asadprodhan/How-to-automatically-download-reads-from-the-NCBI-SRA/blob/main/6.PNG"
 align="center" width=100% height=100% >   
</p>
<p align = center>
Figure 6: Automatic NCBI SRA Read Download.
</p>

<br />


<br />


## **POTENTIAL ERRORS**


<br />


- If you get an error that the SRR_Acc_List.txt is a non-kart file, then change the file extension from txt to kart 


<br />


```
mv SRR_Acc_List.txt SRR_Acc_List.kart 
```


And run the script again


```
./prefetch_fasterq-dump.sh
```


<br />


- If you get the following error, then it suggests that you might need to use the latest version of prefetch and fasterq-dump. You specify the versions as prefetch3.1.1 or so on. See the above script.


<br />


<p align="center">
  <img 
    src="https://github.com/asadprodhan/How-to-automatically-download-reads-from-the-NCBI-SRA/blob/main/7.PNG"
 align="center" width=100% height=100% >   
</p>
<p align = center>
Figure 7: Version Conflict.
</p>

<br />

<br />


### **The end**
