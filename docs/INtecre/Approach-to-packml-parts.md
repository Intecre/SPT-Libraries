# Brief
Generally, try to keep everything as small as possible, then wrap it accordingly.
i.e. if we need to use an axis component, create it as you normally would, adding tests and interfaces as you go. Then wrap it with a PackML component at the last moment. As long as all of our small bits are always assessed for their state, then we shouldn't miss anything that is requested of them by the PackML component or module basis.

``` pascal

T_CartesianRobotModule EXTENDS PackMLbase

xAxis,yAxis,zAxis : T_Axis;
gripper : T_Gripper;
cartesianRobot : T_CartesianRobot(xAxis,yAxis,zAxis,gripper);

xAxisComponent : T_AxisComponent(xAxis);
yAxisComponent : T_AxisComponent(yAxis)
zAxisComponent : T_AxisComponent(zAxis);
components : T_ComponentsCollection := [xAxisComponent, yAxisComponent,zAxisComponent];
gripperModule : T_GripperModule(gripper);
subModules : T_ModulesCollection := [ gripperModule ];

prodmode 
maintmode
manualmode


-----------------------------------------------

code about init 


```


------------------

Another Approach:

```pascal

DECLARATION

FUNCTION_BLOCK T_CartesianRobotModule EXTENDS FB_PackML_BaseModule
VAR
	_xAxis, _yAxis, _zAxis : I_Axis;
	_gripper : I_Gripper;
	_cartesianRobot : I_CartesianRobot;
	
	xAxisComponent : T_AxisComponent;
	yAxisComponent : T_AxisComponent;
	zAxisComponent : T_AxisComponent;
	gripperModule : T_GripperModule;
	
	productionMode : T_CartesianRobotProductionMode;
	maintenanceMode : T_CartesianRobotMaintenanceMode;
	manualMode : T_CartesianRobotManualMode;
END_VAR

-----------------


Initialise Method

// down side of this method, we need to pass submodule components details to cartesian robot module 
//i.e. Cartesian robot doesn't needs to know about cylinder, but module in module cases force this.
//Therefore, any object use within cartesian robot (all sensors, everything) needs to be passed in initialise method 

DECLARATION
METHOD GenericInitialise
VAR
	CartesianRobot : I_CartesianRobot;
	xAxis, yAxis, zAxis : I_Axis; 
	Gripper : I_Gripper;
	Cylinder : I_Cylinder; // cylinder belongs to Gripper, so needs to be passed into gripper module
END_VAR

_xAxis := xAxis;
_yAxis := yAxis;
_zAxis := zAxis;
_gripper := Gripper;
_cartesianRobot := CartesianRobot;

xAxisComponent.GenericInitialise(_xAxis);
yAxisComponent.GenericInitialise(_yAxis);
zAxisComponent.GenericInitialise(_zAxis);
gripperModule.GenericInitialise(gripper, Cylinder);

_cartesianRobot.GenericInitialise(xAxis, yAxis, zAxis, gripper);
productionMode.Initialise(THIS^);
maintenanceMode.Initialise(THIS^);
manualMode.Initialise(THIS^);

ComponentsCollection.AddComponent(xAxisComponent);
ComponentsCollection.AddComponent(yAxisComponent);
ComponentsCollection.AddComponent(zAxisComponent);
SubModulesCollection.AddModule(gripperModule);

```