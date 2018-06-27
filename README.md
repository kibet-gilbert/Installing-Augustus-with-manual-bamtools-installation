# Installing Augustus with manual bamtools installation in Ubuntu Lts 16.04

This workflow is adapted from the description provided in https://iamphioxus.org/2017/05/08/installing-augustus-with-manual-bamtools-installation/

This is a step by step guide on how to install latest version of Installing Augustus  3.3.1 (with manual bamtools installation).
AUGUSTUS is an open source tool that predicts genes in eukaryotic genomic sequences.
For more information go to : http://bioinf.uni-greifswald.de/augustus/

Augustus auxiliary tools, bam2hints and filterBam, depend on the pre-installation of bamtools with proper library path configured.

## **Installing bamtools**

The first installation step is installation bamtools
For more go to :https://github.com/pezmaster31/bamtools/wiki/Building-and-installing
```{r,eval=FALSE,error=FALSE,warning=FALSE,message=FALSE,echo=TRUE}
sudo apt-get install bamtools libbamtools-dev
```
If working with on a shared server (like a cluster) and we do not have the root permission,
install bamtools under our local directory as follows:
```{r,eval=FALSE,error=FALSE,warning=FALSE,message=FALSE,echo=TRUE}
git clone git://github.com/pezmaster31/bamtools.git
mkdir build
cd build
cmake ..
make
```

## **Downloading and installing Augustus**

Augustus source files can be found on http://bioinf.uni-greifswald.de/augustus/binaries/
N/B : CHECK THE LATEST VERSION OF AUGUSTUS TO INSTALL (only change the versions if need be)
```{r,eval=FALSE,error=FALSE,warning=FALSE,message=FALSE,echo=TRUE}
wget http://bioinf.uni-greifswald.de/augustus/binaries/augustus-3.3.1.tar.gz
tar xvzf augustus-3.3.1.tar.gz
cd augustus-3.3.1
make
```
## **Adapting bam2hints and filterBam**

You need to modify the Makefiles of bam2hints and filterBam to adapt them to your manually installed bamtools as follows:
Go to the “augustus-3.2.3/auxprogs/bam2hints” directory and make the following changes for the Makefile as follows:
```{r,eval=FALSE,error=FALSE,warning=FALSE,message=FALSE,echo=TRUE}
cd auxprogs/bam2hints
```
Open the the Makefile in a txt editor of your choice.
In this case we will use VIm (Vi Improved)
```{r,eval=FALSE,error=FALSE,warning=FALSE,message=FALSE,echo=TRUE}
vim Makefile
```

Replace:
INCLUDES = /usr/include/bamtools
By:
INCLUDES = $(BAMTOOLS)/include

Replace:
LIBS = -lbamtools -lz
By:
LIBS = $(BAMTOOLS)/lib/libbamtools.a -lz

To save and go back to terminal use (in command mode by esc key) ":wq"

Go to the “augustus-3.3.1/auxprogs/filterBam/src” directory and make the following changes for the Makefile:
```{r,eval=FALSE,error=FALSE,warning=FALSE,message=FALSE,echo=TRUE}
cd ~/augustus-3.3.1/auxprogs/filterBam/src
```

Open the the Makefile in a txt editor of your choice.
In this case we will use VIm (Vi Improved)
```{r,eval=FALSE,error=FALSE,warning=FALSE,message=FALSE,echo=TRUE}
vim Makefile
```

Replace:
INCLUDES = -I$(BAMTOOLS) -Iheaders -I./bamtools
By:
INCLUDES = -I$(BAMTOOLS)/include -Iheaders -I./bamtools

Replace:
LIBS = -lbamtools -lz
By:
LIBS = $(BAMTOOLS)/lib/libbamtools.a -lz

To save and go back to terminal use (in command mode by esc key) ":wq"

Congratulations!!! 
You are finally ready to compile Augustus. Get back to the “augustus-3.3.1” directory and type “make”

## **References**
http://bioinf.uni-greifswald.de/augustus/
https://iamphioxus.org/2017/05/08/installing-augustus-with-manual-bamtools-installation/
https://github.com/pezmaster31/bamtools/wiki/Building-and-installing
