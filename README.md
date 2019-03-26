# MCScanX-2019

Introduction
---------
MCScanX is a multi-alignment tool for a set of genomes to be compared and analyzed. This is a project introduced to me by Dr. Won Yim a professor at the University of Nevada, Reno. Arabidopsis Thaliana will be compared and anlayzed against itself and A. Lyrata. This repository will go more in-depth in the process of things.

Citations
---------
**MCScanX**

Wang Y, Tang H, DeBarry JD, Tan X, Li J, Wang X, Lee TH, Jin H, Marler B, Guo H, Kissinger JC, Paterson AH. (2012) MCScanX: a toolkit for detection and evolutionary analysis of gene synteny and collinearity. Nucleic Acids Res, 40(7): e49.

**Phytozome Data: Arabidopsis Thaliana, Araport**

Cheng CY, Krishnakumar V, Chan AP, Thibaud-Nissen F, Schobel S, Town CD, Araport11: a complete reannotation of the Arabidopsis thaliana reference genome., The Plant journal : for cell and molecular biology. 2017 Feb ; 89 4 789-804

**Phytozome Data: Arabidopsis Lyrata**

Rawat V, Abdelsamad A, Pietzenuk B, Seymour DK, Koenig D, Weigel D, Pecinka A, Schneeberger K, Improving the Annotation of Arabidopsis lyrata Using RNA-Seq Data., PloS one. 2015 ; 10 9 e0137391

Requirement/Dependencies
---------
**Computer**

Buy one or use a computer (come to Dr. Yim's lab, you can probably use one there!).

**Ubuntu**

A linux environment will be used through Ubuntu 18.04 from the windows store. Download the program and run it. Make an account prompted:

    Enter new UNIX username:
    Enter new UNIX password:

Note: the terminal will ask you to re-type the password, and when typing in the password, no text will show up. That is fine. When typing and finishing, hit Enter.

**javac**

Downloading this to the environment will help run some of the MCScanX programs. The following code was typed into terminal:

    sudo apt install -y openjdk-11-jdk-headless

**NCBI-Blast+**

NCBI blast program will help create the required files for alignment and ready for the MCScanX analysis. The NCBI program was retrieved using wget, then installed using the tar command, then exported to PATH to be available in the environment. The following code was typed into terminal: 

    wget ftp://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/2.2.31/ncbi-blast-2.2.31+-x64-linux.tar.gz
    tar zxvpf ncbi-blast-2.2.31+-x64-linux.tar.gz
    export PATH=$PATH:$HOME/ncbi-blast-2.2.31+/bin

**Installing MCScanX**
<s>


Python 2.7 will be used to run some of the modules in the protocol. Download python by typing the lines in the Ubuntu terminal.

    sudo apt install python2.7
    sudo apt-get install python-dev  \
     build-essential libssl-dev libffi-dev \
     libxml2-dev libxslt1-dev zlib1g-dev \
     python-pip -y
    sudo apt-get update -y



Getting Started
---------

The Works
---------
**Pairwise Synteny Search**
- ATH and ALY orthologs.
We will be comparing the ready-made files for synteny using the ortholog command from jcvi.compara.catalog. Last is used to compare the data, and the option ``--no_strip_names`` was used in order to remove the isoform mark. Wi
- ATH and ATH downstream analyses
