---
layout: post
title: "Change the status of a Private MC dataset published in the CMS DAS to INVALID"
date: 2023-04-11 13:03:00 -0000
---

It is not possible to delete a published dataset in CMS. You can always change delete the data fom your local grid memory. However the dataset will still show upon a CMS DAS search. Changing the status to invalid is one way of making sure that the dataset doesn't show up. This is acheived through the DBS client. For the most recent use case, `python3` based client has been used in conjunction with `CMSSW` version >12.

### Setup the environment

```
cmsrel CMSSW_12_4_11
cd CMSSW_12_4_11/src
cmsenv
git cms-init
scram b -j
```

Make sure to not source the crab config. 

### Clone DBS Client

```
git clone git@github.com:dmwm/DBSClient.git
```

### Set status to invalid

List the dataset using `dasgoclient`.

```
dasgoclient --query="dataset=/JPsiToEE_Pt2To30*/*/USER instance=prod/phys03"
```

> /JPsiToEE_Pt2To30_13p6TeV_TuneCP5_pythia8/asahasra-PrivateMC_CMSSW12410patch1_221019DIGIRAW-a74b34b0dcd2a29d9f812d56a0b763dd/USER
> /JPsiToEE_Pt2To30_13p6TeV_TuneCP5_pythia8/asahasra-PrivateMC_CMSSW12410patch1_221024ScoutingReRun200k-105fd880305ee5bab10a714fe2eee19e/USER
> /JPsiToEE_Pt2To30_13p6TeV_TuneCP5_pythia8/asahasra-PrivateMC_CMSSW12410patch1_221102ScoutingReRun-7657a045544b9145636eaa01965dcc38/USER
> /JPsiToEE_Pt2To30_13p6TeV_TuneCP5_pythia8/asahasra-PrivateMC_CMSSW12410patch1_230228ScoutingReRun-22ef6f9ee5470c9936184150b3154ec2/USER
> /JPsiToEE_Pt2To30_13p6TeV_TuneCP5_pythia8/asahasra-PrivateMC_CMSSW12410patch1_230301ScoutingReRun-22ef6f9ee5470c9936184150b3154ec2/USER
> /JPsiToEE_Pt2To30_13p6TeV_TuneCP5_pythia8/asahasra-PrivateMC_CMSSW12410patch1_230301_mod_ScoutingReRun-c977861fac258f312614ec5b6ce7a8d5/USER
> /JPsiToEE_Pt2To30_13p6TeV_TuneCP5_pythia8/asahasra-PrivateMC_CMSSW12411_221109RECOsmallSet20k-002c5a5c6f36a7e77cfefce375c6d71e/USER
> /JPsiToEE_Pt2To30_13p6TeV_TuneCP5_pythia8/asahasra-PrivateMC_CMSSW12411_221110RECO-002c5a5c6f36a7e77cfefce375c6d71e/USER
> /JPsiToEE_Pt2To30_13p6TeV_TuneCP5_pythia8/asahasra-PrivateMC_CMSSW1245_220818GEN-43c9dace3a34c0f8b74c4929d9df9898/USER
> /JPsiToEE_Pt2To30_13p6TeV_TuneCP5_pythia8/asahasra-PrivateMC_CMSSW1245_220823GEN-f81fd232652d72612e99f39f9c293b6e/USER
> /JPsiToEE_Pt2To30_13p6TeV_TuneCP5_pythia8/asahasra-PrivateMC_CMSSW1245_221014DIGIRAW-3d22687742b6ba3b82aa980bed41060b/USER
> /JPsiToEE_Pt2To30_13p6TeV_TuneCP5_pythia8/asahasra-PrivateMC_CMSSW1245_221014DIGIRAW_smallSub7p4kevents-3d22687742b6ba3b82aa980bed41060b/USER
> /JPsiToEE_Pt2To30_13p6TeV_TuneCP5_pythia8/asahasra-PrivateMC_CMSSW1300pre3_230206ScoutingReRun100k-00e0ebb55839142965ba630340eca14d/USER
> /JPsiToEE_Pt2To30_13p6TeV_TuneCP5_pythia8/asahasra-PrivateMC_CMSSW1300pre3_230207ScoutingReRun-00e0ebb55839142965ba630340eca14d/USER

Change the status of a dataset.

```
python3 DBSClient/utils/DataOpsScripts/DBS3SetDatasetStatus.py --dataset=/JPsiToEE_Pt2To30_13p6TeV_TuneCP5_pythia8/asahasra-PrivateMC_CMSSW1245_220818GEN-43c9dace3a34c0f8b74c4929d9df9898/USER --url=https://cmsweb.cern.ch/dbs/prod/phys03/DBSWriter --status=INVALID --recursive=False
```
> Done

List the datasets again to cross-check.