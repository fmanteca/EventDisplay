# EventDisplay with ISPy (takes AOD or RECO format as input)

Note from 21st of June, 2022: several AOD productions are only stored in TAPE, while we can only read those written in DISK from cms-xrd-global.cern.ch. Probably using Fireworks is a better option (see below)

## Step 1 is to get your AOD events ####

##### Release needs to be >= than the one used for data re-reco, 10_6_X is good for all preUL data

    cmsrel CMSSW_10_6_0
    cd CMSSW_10_6_0/src/
    cmsenv
    voms-proxy-init2 --voms cms

##### Get the miniAOD 

    edmPickEvents.py "DAS dataset name" run:luminostiyBlock:event --runInteractive 
    
 - If you don't know the DAS dataset name, use dasgoclient --query="dataset=/*[Something that should resemble it]*/*/MINI*"
 - Multiple events can be requested run1:luminostiyBlock1:event1,run2:luminostiyBlock2:event2,...

## Step 2 is to go from root to ig file 

##### On top of CMSSW_10_6_X install iSpy

    git clone https://github.com/cms-outreach/ispy-analyzers.git ISpy/Analyzers 
    git clone https://github.com/cms-outreach/ispy-services.git ISpy/Services
    scram b -j 8
    cd ISpy/Analyzers/python

- Open ispy_10_X_X_cfg.py and edit the input root file to the one you got in step 1.

    cmsRun ispy_10_X_X_cfg.py (nets you the .ig file you can use for plotting)

## Step 3 is uploading to the webpage (it seems that technically you can host it locally but it worked nicely for me online) ####

Go to: http://ispy-webgl-dev.web.cern.ch/# 

Click Open File (top left corner) => Examine => Select the .ig you had => Click the file name => Select the event =>  Play with the interface to make it seem nicer :)
Only caveat is that screenshots would be taken at your own screen resolution, I change it to 4K to get them "look nicer"

More information can be found in: http://cms-outreach.github.io/ispy/


# Using Fireworks (takes miniAOD/AOD/RECO formats as input)

Use edmPickEvents.py to pick the miniAOD events.

Copy the output to a public /eos/ path.

Use that path here: https://fireworks.cern.ch/cmsShowWeb/revetor.pl

Additional information can be found in:
- https://twiki.cern.ch/twiki/bin/viewauth/CMS/SWGuideCMSDataAnalysisSchoolLPC2022EventDisplayExerciseBackup
- https://indico.cern.ch/event/1155896/
