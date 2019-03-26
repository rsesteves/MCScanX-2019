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

    wget http://chibba.pgml.uga.edu/mcscan2/MCScanX.zip
    unzip MCScanX.zip
    cd MCScanX
    make

The following errors could occur:
- Error 1
    msa.cc: In function ‘void msa_main(const char*)’:
    msa.cc:289:9: error: ‘chdir’ was not declared in this scope
     if (chdir(html_fn)<0)
         ^~~~~
    msa.cc:289:9: note: suggested alternative: ‘mkdir’
     if (chdir(html_fn)<0)
         ^~~~~
         mkdir
    makefile:2: recipe for target 'mcscanx' failed
    make: *** [mcscanx] Error 1

Solution:
Add this to top of msa.cc.
    nano msa.cc
    #include <unistd.h>
    /* Author: Yupeng Wang <wyp1125@uga.edu> March 31, 2011
    * This is the new code for generating and printing multiple alignment based on progressive alignment
    */
    #include "msa.h"
    ...
Save
    $make

- Error 2
    hemzy@DESKTOP-J3FNUQU:~/MCScanX$ make
    g++ struct.cc mcscan.cc read_data.cc out_utils.cc dagchainer.cc msa.cc permutation.cc -o MCScanX
    g++ struct.cc mcscan_h.cc read_homology.cc out_homology.cc dagchainer.cc msa.cc permutation.cc -o MCScanX_h
    g++ struct.cc dup_classifier.cc read_data.cc out_utils.cc dagchainer.cc cls.cc permutation.cc -o duplicate_gene_classifier
    g++ dissect_multiple_alignment.cc -o downstream_analyses/dissect_multiple_alignment
    dissect_multiple_alignment.cc: In function ‘int main(int, char**)’:
    dissect_multiple_alignment.cc:252:17: error: ‘getopt’ was not declared in this scope
        while ((c = getopt(argc, argv, "g:c:o:")) != -1)
                    ^~~~~~
    dissect_multiple_alignment.cc:252:17: note: suggested alternative: ‘getpt’
        while ((c = getopt(argc, argv, "g:c:o:")) != -1)
                    ^~~~~~
                    getpt
    dissect_multiple_alignment.cc:257:32: error: ‘optarg’ was not declared in this scope
                sprintf(gpath,"%s",optarg);
                                    ^~~~~~
    dissect_multiple_alignment.cc:257:32: note: suggested alternative: ‘opath’
                sprintf(gpath,"%s",optarg);
                                    ^~~~~~
                                    opath
    dissect_multiple_alignment.cc:269:17: error: ‘optopt’ was not declared in this scope
                if (optopt!='g' || optopt!='c' || optopt!='o')
                    ^~~~~~
    dissect_multiple_alignment.cc:269:17: note: suggested alternative: ‘getpt’
                if (optopt!='g' || optopt!='c' || optopt!='o')
                    ^~~~~~
                    getpt
    makefile:2: recipe for target 'mcscanx' failed
    make: *** [mcscanx] Error 1
 
 Solution:
 Add #include <getopt.h> to  detect_collinear_tandem_arrays.cc and dissect_multiple_alignment.cc, then add #include <unistd.h> to msa.cc.

    nano detect_collinear_tandem_arrays.cc
    #include <getopt.h>

    nano dissect_multiple_alignment.cc
    #include <getopt.h>

Save

    $make

Issues did not come up, but for some users it may. Solutions can be found via MCScanX github.

Getting Started
---------
**Datasets of Interest**
- Arabidopsis Thaliana and Lyrata
Arabidopsis Thaliana(ATH) and Arabidopsis Lyrata(ALY) were downloaded through Phytozome. An account was created to access the Phytozome data. The following data sets were downloaded, as mentioned in the reference, to the windows system:

Athaliana_447_Araport11.gene.gff3.gz
Athaliana_447_Araport11.protein_primaryTranscriptOnly.fa.gz
Alyrata_384_v2.1.gene.gff3.gz
Alyrata_384_v2.1.protein_primaryTranscriptOnly.fa.gz

A directory was made in MCScanX/data/ directory called ATHpALYp, and another folder named results was made with the lines below (assuming to be in the data folder).

    mkdir ATHpALYp
    cd ATHpALYp
    mkdir results

The files were then copied into Ubuntu with the line used below (assuming to be in the ATHpALYp folder):

    cp /mnt/c/Users/Dumbo/Downloads/*.gz ./

The files above were gunziped by the lines below:

    gunzip *.gz

The set-up looked like the below:

    hemzy@DESKTOP-J3FNUQU:~/MCScanX/data/ATHpALYp$ ls
    Alyrata_384_v2.1.gene.gff3                         Athaliana_447_Araport11.gene.gff3
    Alyrata_384_v2.1.protein_primaryTranscriptOnly.fa  Athaliana_447_Araport11.protein_primaryTranscriptOnly.fa

- Making a database
The FASTA files were concatenated together to be used as a protein database, soon to be used for blasting RNAseq data to itself. The lines were used below.

    cat Athaliana_447_Araport11.protein_primaryTranscriptOnly.fa Alyrata_384_v2.1.protein_primaryTranscriptOnly.fa > ATHpALYp.fa

    makeblastdb -in ATHpALYp.fa -dbtype prot

The FASTA files were then "blasted" against the created database and will be aligned. The line below was used and ran overnight, or approximately 2-4 hours (on my machine).

    blastp -query ATHpALYp.fa -db ATHpALYp.fa -evalue 1e-10 -max_target_seqs 5 -outfmt 6 -out ATHpALYp.blast -num_threads 2





The Works
---------
****
- ATH and ALY orthologs.
We will be comparing the ready-made files for synteny using the ortholog command from jcvi.compara.catalog. Last is used to compare the data, and the option ``--no_strip_names`` was used in order to remove the isoform mark. Wi