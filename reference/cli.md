# CLI

## Introduction

Ritchie works through files stored inside the **.rit** folder in the _HOME_ of the user's machine. This folder is **manipulated** by the CLI as commands are executed.

In this folder are stored: 

* the **tree.json** files from the formula repositories accessible on the user's machine 
* the **executable** files of the formulas 
* the **temporary** files used in Ritchie 
* **passphrase** and **session** files for the **Single** version

{% hint style="info" %}
To get to know more about our CLI repository, access [**ritchie-cli**](https://github.com/ZupIT/ritchie-cli) on Github. 
{% endhint %}

## Composition of the .rit folder

### Repo folder

The **repo** folder contains all the files necessary for the CLI to know the commands and formulas it can execute. 

It is made up of other folders: 

* a **cache** folder that will contain the tree.json files from the formula repository that the user has access to \(according to the version of Ritchie he is using\). 
* a **local** folder that will contain the tree.json of the repository where the user is developing and testing formulas locally. 

In addition to these folders, there is also a **repositories.json** file. This file contains a list of tree.json for the CLI to identify which trees it has access to, and what their priorities are, in order to avoid duplicate commands if they appear in more than one formula repository.

### Formulas folder

The **formulas** folder contains all the files necessary for the CLI to execute the formulas.

It is composed of several folders, one per formula, containing the formula executable according to the operating system used, as soon as the associated config.json is used to identify the necessary input parameters for the formula to be executed correctly.

These files are downloaded, and these folders are created when the CLI executes a formula command for the [first time](https://docs.ritchiecli.io/key-concepts#formulas-on-demand) \(they are fetched through the formula's repoUrl informed in the associated tree.json\).

When the user tests a formula he implemented locally, the _Makefile_ file contained in the formula repository used will add the formula's executables inside that folder, creating the same structure that would be created if the formula were downloaded from a server.

### tmp folder

The **tmp** folder is where temporary files are stored. Those files can be created or manipulated during the execution of some formulas or core commands. These temporary files can be templates, certificates, or other single-use files.

### Passphrase & Session

The **passphrase** & **session** files are encrypted files used in the Single version to be able to define datas that will repetitively be used through Ritchie. Those datas can be _credentials_ of some tools manipulated in the formulas, or even the definition of the _context_ used to perform some automations.

