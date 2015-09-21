
Background: 
  Running R script on HTCondor

Problem: 
  R packages are not installed on the submit and excutable node.

Solution:

  [how to use R]<http://chtc.cs.wisc.edu/howto_overview.shtml>
  Three steps:
  1. Compiling: http://chtc.cs.wisc.edu/howto_overview.shtml : `chtc_buildRlibs --rversion=sl6-R-2.10.1 --rlibs=lme4_0.999375-39.tar.gz,pedigreemm_0.2-4.tar.gz`
  Remember to download all the R package tar.gz files in the same directory.
  2. Prepare to submit: http://chtc.cs.wisc.edu/DAGenv.shtml : `wget http://chtc.cs.wisc.edu/downloads/ChtcRun.tar.gz; tar xzf ChtcRun.tar.gz`;

  Modify Rin(or create another folder using the same structure of Rin: Rin/shared; Rin/0; Rin/1(if you just want to run it once just create another folder apart from "shared")). Change the R script in the shared folder and put the compiled R package zip file here. 

  Modify process.template.
  3. Submit the R script:
	
    `./mkdag --data=Rinputdir --outputdir=Routputdir(will create for you) --cmdtorun=RscriptName --type=R --version=SameRversionAsCompilingLikeR-3.0.1 --pattern=OutPutFileNamePattern`
	(If you would like to pass argument to R, add `--parg=xxx` to it.
	
   It will create the Routputdir folder. cd into it and run   `condor_submit_dag mydag.dag`
	

