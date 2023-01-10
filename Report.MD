<p align="center">
    <h3 align="center"> Mantis Report </h3>


<p align="left">
first we create a git action yaml file

workflows managed by github and run on them
each job in a workflow runs in a fresh virtual environment.
by default the jobs will run in parallel
so to overide this and wait for the first job to end
we use needs: build


there is a build in template called build and test python app
<br />

  </p>
</p>


Yaml Gifhub Workflow File:
==========================


**checkout@v1** - which checks-out to the repo under $GITHUB_WORKSPACE so your workflow can access it .


 **action.yml/setup-python1 - 2** - which provide the following funcitionaly for github action users
                           Installs a version of Python of PyPy and (by default) adding it to the PATH
                           Optionally caching dependecies for pip,pipenv and poetry.
                           Registering problem matces for error output.

 **actions/syphar/restore-virtualenv@v1** 
 **syphar/restore-pip-download-cache@v1**
                           which provide python virtual environment
                           gives you either an new virtualenv, or restores an old one based on the requirements-file
                           sets $VIRTUAL_ENV and $PATH environment for the virtualenv
                           Restore keys take the OS into account, and the major and minor python version. for patch-updates the virtualenv can be reused.
                           will use any typical requirements file to build the cache key (poetry, pipenv, pip-requirements-txt)

**actions/upload-artifact@v3** - 
                           This uploads artifacts from your workflow allowing you to share data between jobs and store data once a workflow is complete.
 

**actions/download-artifact@v3** -
                           download all artifacts in a workflow run by not specifying a name. This can be useful if you are working with lots of artifacts.


## Workflow or any problems i encountered 

* i've came acrros a probelem with windows access violations when running pytest -

  i've tried to change the permissons locally without success on windows os, 
  however with ubuntu, the permissons changed perfectly so the test should run fine

* also added the module Path from pathlib due to mistakely deleteing it .


* in addition for now i've skipped the tests job , in order to check the build stage

* the build stage works perfectly create 2 spec files 
  MvxGraph.spec
  mvpy_rest_server.spec

  the spec file named after the python files - which can be used as a template to create exeutables
  the spec file tells Pyinstaller how to process our script .
  it encodes the script names and most of the options you give to the pyinstaller commands,
  Pyinstaller builds the app by executing the contents of the SPEC file.


* a build folder also created where pyinstaller put most of the metadata and internal
  bookkeeping for building our executable . it also can be used for debugging.

  dist folder - contains the final arificat that we want ship out our users.
  which contains all the dependencies and executable for our application .
  You’ll also find lots of files with the extension .so, .pyd, and .dll depending on your Operating System.

  These are the shared libraries that represent the dependencies of your project that PyInstaller created and collected.

  build stage :
  Pyinstaller create 2 EXE files on /dist folder . and Create Artifact avaliable for download.


## Notes


  in order to use  github customs made workflows
  we add them to the repo settings on the line:
  "Allow specified actions and reusable workflows.










