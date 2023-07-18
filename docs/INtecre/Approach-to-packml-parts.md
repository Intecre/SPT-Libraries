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


