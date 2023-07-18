# Brief
Generally, try to keep everything as small as possible, then wrap it accordingly.

If we need to use an axis component, create it as you normally would, adding tests and interfaces as you go. Then wrap it with a PackML component at the last moment. As long as all of our small bits are always assessed for their state, then we shouldn't miss anything that is requested of them by the PackML component or module basis.

### Example class

Below shows the expected vairables for a Cartesian robot

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

productionMode : T_ProductionMode;
maintenanceMode : T_MaintenanceMode;
manualMode : T_ManualMode; 

```
### Example Initialise

Below demonstrates how the module should be set up in an initialise method. Not to be confused with the PackML Initialize method this should be separate. 

``` pascal
// Set PackML Collections
ComponentsCollection.AddComponent(xAxis);
ComponentsCollection.AddComponent(yAxis);
ComponentsCollection.AddComponent(zAxis);
SubModulesCollection.AddModule(grabber);

// Set Cartesian Items
cartesianRobot.AddModulesAndComponents(
  xAxis := xAxis.GetRawAxis(),
  yAxis := yAxis,
  zAxis := zAxis,
  grabber := grabber);
  

myProdMode.init(THIS^);

// Set PackML modes
ModeManager.AddPackModes(productionMode,
    maintenanceMode,
    manualMode);

// Go to Production mode
ModeManager.ChangeMode(E_PMLUnitMode.ePMLUnitMode_Production);


```


