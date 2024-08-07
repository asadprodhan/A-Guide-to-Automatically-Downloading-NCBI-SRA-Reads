<h1 align="center">A Guide to Automatically Downloading NCBI SRA Reads</h1>


<h3 align="center">M. Asaduzzaman Prodhan<sup>*</sup></h3>


<div align="center"><b> DPIRD Diagnostics and Laboratory Services, Department of Primary Industries and Regional Development </b></div>


<div align="center"><b> 3 Baron-Hay Court, South Perth, WA  6151, Australia. <sup>*</sup>Correspondence: prodhan82@gmail.com </b></div>


<br />


<p align="center">
  <a href="https://github.com/asadprodhan/How-to-automatically-download-reads-from-the-NCBI-SRA/tree/main#GPL-3.0-1-ov-file"><img src="https://img.shields.io/badge/License-GPL%203.0-yellow.svg" alt="License GPL 3.0" style="display: inline-block;"></a>
  <a href="https://doi.org/10.5281/zenodo.12622074"><img src="https://zenodo.org/badge/DOI/10.5281/zenodo.12622074.svg" alt="DOI"></a>
  <a href="https://orcid.org/0000-0002-1320-3486"><img src="https://img.shields.io/badge/ORCID-green?style=flat-square&logo=ORCID&logoColor=white" alt="ORCID" style="display: inline-block;"></a>
</p>


<br />


<br />


The National Center for Biotechnology Information (NCBI) is a global public repository that houses a vast collection of genomic information. Within the NCBI, the Sequence Read Archive (SRA) is a dedicated repository for housing the raw DNA sequencing reads that are submitted to the NCBI. Therefore, SRA serves as a critical resource for researchers providing an open-access to millions of sequences from diverse organisms and environments. As such, SRA reads fuel groundbreaking research ranging from genome assembly and variation analysis to transcriptomics and metagenomics.


<br />


Here, I present a guide on how to automatically download the NCBI SRA reads of your interest.


<br />



### Content


[Step 1: Download and Setup the SRA Tool Kit](https://github.com/asadprodhan/How-to-automatically-download-reads-from-the-NCBI-SRA/blob/main/README.md#step-1-download-and-setup-the-sra-tool-kit)


[Step 2: Collect SRA Accession Numbers](https://github.com/asadprodhan/How-to-automatically-download-reads-from-the-NCBI-SRA/blob/main/README.md#step-2-collect-sra-accession-numbers)


[Step 3: Download Reads](https://github.com/asadprodhan/How-to-automatically-download-reads-from-the-NCBI-SRA/blob/main/README.md#step-3-download-reads)


[POTENTIAL ERRORS](https://github.com/asadprodhan/How-to-automatically-download-reads-from-the-NCBI-SRA/blob/main/README.md#potential-errors)


<br />


## **Step 1: Download and Setup the SRA Tool Kit**


<br />


- Create a directory on your Linux Desktop


```
mkdir sratoolkits
```


- cd to sratoolkits and download the sra tool kit using the following link:


```
sudo wget https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/current/sratoolkit.current-ubuntu64.tar.gz
```


Visit the NABI SRA Toolkit[^SRA] manual (https://github.com/ncbi/sra-tools/wiki/01.-Downloading-SRA-Toolkit) 


- Move the sratoolkits directory in your /usr/bin directory


- cd to the sratoolkits/sratoolkit.3.1.1-ubuntu64/bin directory


- Find out the path by running the following command


```
pwd
```


- Now, add this path to your PATH variable as follows:


What is a PATH variable? See an explanation here[^PATH]


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


## **Step 2: Collect SRA Accession Numbers**


<br />


Here, I am going to use BioProject PRJNA340941[^Hakim] for demonstration purpose. This BioProject contains Illumina sequencing of 16S rRNA from a root microbiome study[^Hakim]. You can try downloading reads from any study such as transcriptomics[^RNAseq], mitochondrial genomics[^Mitogenomics] etc that has a BioProject number.


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

 

## **Step 3: Download Reads**


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


[2] Put the above script and your Accession List in the same directory


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



## **REFERENCES**


[^SRA]: NCBI SRA Toolkit. [cited 2 Jul 2024]. Available: https://github.com/ncbi/sra-tools/wiki/01.-Downloading-SRA-Toolkit



[^PATH]: Prodhan MA. About the PATH. Zenodo. 2024 [cited 26 Apr 2024]. doi:https://doi.org/10.5281/zenodo.11068991


[^Hakim]: Hakim S, Mirza BS, Imran A, Zaheer A, Yasmin S, Mubeen F, et al. Illumina sequencing of 16S rRNA tag shows disparity in rhizobial and non-rhizobial diversity associated with root nodules of mung bean (Vigna radiata L.) growing in different habitats in Pakistan. Microbiol Res. 2020;231: 126356. doi:10.1016/j.micres.2019.126356


[^RNAseq]: Prodhan MA, Pariasca-Tanaka J, Ueda Y, Hayes PE, Wissuwa M. Comparative transcriptome analysis reveals a rapid response to phosphorus deficiency in a phosphorus-efficient rice genotype. Sci Rep. 2022;12: 9460. doi:10.1038/s41598-022-13709-w


[^Mitogenomics]: Prodhan MA, Widmer M, Kinene T, Kehoe M. Whole mitochondrial genomes reveal the relatedness of the browsing ant incursions in Australia. Sci Rep. 2023;13: 10273. doi:10.1038/s41598-023-37425-1



