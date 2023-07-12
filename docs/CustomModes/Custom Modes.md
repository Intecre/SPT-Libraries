# PML State Custom Modes

Machines may have unit modes other than "Production", "Maintenance" and "Manual". This function block enables the user to configure further models (UnitModes).
[Unit Mode Config](https://infosys.beckhoff.com/english.php?content=../content/1033/tcplclib_tc3_packml_v2/1335962123.html&id=)

eMode: Number of the new PML UnitMode [4..31].
sName: Name of the new PML UnitMode.

Parameters of Unit Mode Config must be set and that will reference to Global Variables stPMLUnitModeConfigurationArray.

![Unit mode Global Variables](GlobalVariables.jpg)

![Unit mode Structures](Structures.jpg)
