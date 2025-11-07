# Lab 6
In this lab, we are creating a Ring Oscillator, a 3-phase Charge pump and a regulator in order to put them together and design a 2V voltage generator.

In all the components, the capacitor and resistor values are too large to be placed in the layout since they would take up too much area, so they are 
replaced with symbols to represent where they should be connected. In a real situation, there could be pads placed that connect to the top metal layer 
(metal 3) to allow the resistors and capacitors to be added to a PCB which can connect the built-in connectors to the actual passive devices.

## 3-Phase Charge Pump

Figure 1 shows the schematic and icon of the 3 Phase Charge Pump gate.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/Charge_Pump_Schematics_and_Icon.png" alt="Charge Pump Schematic and Icon" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 1: Charge Pump Schematic and Icon </em></figcaption>
</div>
<br><br>

The charge pump schematic was the simulated as follows in Figure 2.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/Charge_Pump_Sim_Schematics.png" alt="Charge Pump Sim Schematic" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 2: Charge Pump Sim Schematic </em></figcaption>
</div>
<br><br>

The simulation results can be seen in Figure 3

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/Charge_Pump_Sim_Results.png" alt="Cahrge Pump Simulation Results" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 3: Charge Pump Simulation Results </em></figcaption>
</div>
<br><br>

Next, the layout was created as can be seen in Figure 4.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/Charge_Pump_Layout.png" alt="Charge Pump Layout" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 4: Charge Pump Layout </em></figcaption>
</div>
<br><br>

The 3D view of the layout can be seen below in Figure 5.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/Charge_Pump_Layout_3D.png" alt="Charge Pump 3D View" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 5: Charge Pump 3D View </em></figcaption>
</div>
<br><br>

## Ring Oscillator

Figure 6 shows the schematic and icon of the Ring Oscillator gate.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/Ring_Oscillator_Schematics_and_Icon.png" alt="Ring Oscillator Schematic and Icon" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 6: Ring Oscillator Schematic and Icon </em></figcaption>
</div>
<br><br>

The schematic was the simulated as follows in Figure 7.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/Ring_Oscillator_Sim_Schematics.png" alt="Ring Oscillator Sim Schematic" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 7: Ring Oscillator Sim Schematic </em></figcaption>
</div>
<br><br>

The simulation results can be seen in Figure 8.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/Ring_Oscillator_Sim_Results.png" alt="Ring Oscillator Simulation Results" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 8: Ring Oscillator Simulation Results </em></figcaption>
</div>
<br><br>

Next, the layout was created as can be seen in Figure 9.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/Ring_Oscillator_Layout.png" alt="Ring Oscillator Layout" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 9: Ring Oscillator Layout </em></figcaption>
</div>
<br><br>

The 3D view of the layout can be seen below in Figure 10.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/Ring_Oscillator_Layout_3D.png" alt="Ring Oscillator 3D View" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 10: Ring Oscillator 3D View </em></figcaption>
</div>
<br><br>

## Regulator

Figure 11 shows the schematic and icon of the Regulator.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/Regulator_Schematic_and_Icon.png" alt="Regulator Schematic and Icon" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 11: Regulator Schematic and Icon </em></figcaption>
</div>
<br><br>

The Regulator schematic was the simulated as follows in Figure 12.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/Regulator_Sim_Schematics.png" alt="Regulator Sim Schematic" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 12: Regulator Sim Schematic </em></figcaption>
</div>
<br><br>

The simulation results can be seen in Figure 13

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/Regulator_Sim_Results.png" alt="Regulator Simulation Results" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 13: Regulator Simulation Results </em></figcaption>
</div>
<br><br>

Next, the layout was created as can be seen in Figure 14.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/Regulator_Layout.png" alt="Regulator Layout" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 14: Regulator Layout </em></figcaption>
</div>
<br><br>

## Combined Blocks

Finally, the blocks are combined in a schematic as shown below in Figure 15.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/TopModule_Schematics.png" alt="Combined Circuit Schematic" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 15: Combined Circuit Schematic</em></figcaption>
</div>
<br><br>

The schematic was the simulated as follows in Figure 16.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/TopModule_Sim_Schematics.png" alt="Combined Circuit Sim Schematic" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 16: Combined Circuit Sim Schematic </em></figcaption>
</div>
<br><br>

The simulation results can be seen in Figure 17.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/TopModule_Sim_Results.png" alt="Combined Circuit Simulation Results" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 17: Combined Circuit Simulation Results </em></figcaption>
</div>
<br><br>

Next, the layout was created as can be seen in Figure 18.

<br> <br>
<figure>
  <div align="center">
    <img src="imgs_and_videos/TopModule_Layout.png" alt="Combined Circuit Layout" width="500">
  </div>
</figure>

<div align="center">
  <figcaption><em>Figure 18: Combined Circuit Layout </em></figcaption>
</div>
<br><br>
