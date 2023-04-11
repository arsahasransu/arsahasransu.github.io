---
layout: post
title: "Change the status of a Private MC dataset published in the CMS DAS to INVALID"
---

It is not possible to delete a published dataset in CMS. You can always change delete the data fom your local grid memory. However the dataset will still show upon a CMS DAS search. Changing the status to invalid is one way of making sure that the dataset doesn't show up. This is acheived through the DBS client. For the most recent use case, `python3` based client has been used in conjunction with `CMSSW` version >12.

### Setup the environment

> cmsrel CMSSW_12_4_11
> cd CMSSW_12_4_11/src
> cmsenv
> git cms-init
> scram b -j

Make sure to not source the crab config. 

### Clone DBS Client

> git clone git@github.com:dmwm/DBSClient.git

### Set status to invalid

List the dataset using `dasgoclient`.

> dasgoclient --query="dataset=/JPsiToEE_Pt2To30*/*/USER instance=prod/phys03"

Output