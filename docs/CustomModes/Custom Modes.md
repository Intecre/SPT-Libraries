# PML State Custom Modes

Machines may have unit modes other than "Production", "Maintenance" and "Manual". This function block enables the user to configure further models (UnitModes).
[Unit Mode Config](https://infosys.beckhoff.com/english.php?content=../content/1033/tcplclib_tc3_packml_v2/1335962123.html&id=)

eMode: Number of the new PML UnitMode [4..31].
sName: Name of the new PML UnitMode.

![Custom mode setup](CustomModeSetup.jpg)

Parameters of Unit Mode Config must be set and that will reference to Global Variables stPMLUnitModeConfigurationArray by twincat itself. No Additional action required.

![Unit mode Global Variables](GlobalVariables.jpg)

![Unit mode Structures](Structures.jpg)


## Changing the states 

There are two ways for change the state 

1- StateComplete() method 

2- State Change Commands 

On reduced modes like manual, i.e. if state in Execute, StateComplete() method doesn't have any effect. The only way from getting out of Execute state is request Abort Command.  

That will be the same case for custom modes, we have to define the states on custom mode and exit methods from states. 


![Manual Mode States](ManualModeStates.jpg)