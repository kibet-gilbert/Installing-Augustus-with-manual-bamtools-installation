# Installing Augustus with manual bamtools installation in Ubuntu Lts 16.04
![alt text](http://bioinf.uni-greifswald.de/augustus/images/augustus.head.transparent.gif)
This workflow is adapted from the description provided in [Installing Augustus with manual bamtools installation](https://iamphioxus.org/2017/05/08/installing-augustus-with-manual-bamtools-installation/)

This is a step by step guide on how to install latest version of Installing Augustus  3.3.1 (with manual bamtools installation).
AUGUSTUS is an open source tool that predicts genes in eukaryotic genomic sequences.
For more information go to : http://bioinf.uni-greifswald.de/augustus/

Augustus auxiliary tools, bam2hints and filterBam, depend on the pre-installation of bamtools with proper library path configured.

## **Installing Dependancies**

The first installation step is installation bamtools
For more go to :https://github.com/pezmaster31/bamtools/wiki/Building-and-installing
```{r,eval=FALSE,error=FALSE,warning=FALSE,message=FALSE,echo=TRUE}
sudo apt-get install libboost-iostreams-dev
sudo apt-get install zlib1g-dev
sudo apt-get install libgsl-dev
sudo apt-get install libmysql++-dev
sudo apt-get install libsqlite3-dev
sudo apt-get install libboost-graph-dev
sudo apt-get install libsuitesparse-dev liblpsolve55-dev
sudo apt-get install bamtools libbamtools-dev

```

## Downloading and installing samtools ##
Install these tools in your home directory as follows:
```{r,eval=FALSE,error=FALSE,warning=FALSE,message=FALSE,echo=TRUE}
git clone https://github.com/samtools/htslib.git
  cd htslib
  autoheader
  autoconf
  ./configure
  make
  sudo make install
  cd ..
  
 git clone https://github.com/samtools/bcftools.git
  cd bcftools
  autoheader
  autoconf 
  ./configure
  make
  sudo make install
  cd ..

git clone https://github.com/samtools/tabix.git
  cd tabix
  make
  cd ..
  
git clone https://github.com/samtools/samtools.git
  cd samtools
  autoheader
  autoconf -Wno-syntax
  ./configure
  make
  sudo make install
  cd ..
```

When that is done,proceed with installation of augustus:
```{r,eval=FALSE,error=FALSE,warning=FALSE,message=FALSE,echo=TRUE}
cd augustus<version>
make
```

Congratulations!!! 
You are finally ready to compile Augustus. Get back to the “augustus-3.3.1” directory and type “make”

## **References**
http://bioinf.uni-greifswald.de/augustus/
https://iamphioxus.org/2017/05/08/installing-augustus-with-manual-bamtools-installation/
https://github.com/pezmaster31/bamtools/wiki/Building-and-installing
