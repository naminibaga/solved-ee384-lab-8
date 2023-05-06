Download Link: https://assignmentchef.com/product/solved-ee384-lab-8
<br>
<ul>

 <li>Time Domain P410 radar  MRM RET software</li>

 <li>USB 2.0 A to Micro-B cable.</li>

 <li>Targets</li>

 <li>Tape measure</li>

</ul>

<strong>Introduction: </strong>

In this laboratory we will further explore the operation of the MRM and some basic radar functions.  As you saw in Lab 1, it can be difficult to see targets just by looking at a radar scan.  The raw signal looks very “noisy” to us.  By some simple processing of the raw signals we will be able to better determine target properties.

The main source of what looks like “noise” in the raw scans are actually echoes from other objects and people in the room.  These echoes are called <em>clutter</em> since they can “clutter” the signal display.  When an electromagnetic pulse is transmitted objects will reflect part of that energy back towards the radar unit.  The amount of signal energy returning to the radar from an object depends on the “size” of the object and the distance from the object to the radar.  Here

“size” does not refer to a physical size, but instead refers to the object’s radar cross-section (RCS), which is a measure of how detectable the object is to the radar.  The RCS of an object depends on material of the object, the absolute size of the object, the relative size of the object to the signal wavelength, the incident angle, the reflected angle, and the polarization of the transmitted and received radiation with respect to the orientation of the target.

For the purposes of this experiment, we do not need to concern ourselves with the RCS of objects.  We just need to realize that every object in the room (including yourself and your classmates) will act as targets for the radar and may provide reflections that are not necessarily what we want to see in our scans.  In this experiment we will develop simple methods of reducing the clutter seen in the scans so that we can better determine targets.

The first method for clutter reduction we will employ is to adjust the scan length, thus eliminating returns from objects outside our window of interest.  The MRM RET allows you set the <strong>Scan Start</strong> and <strong>Scan Stop</strong>.  Basically the MRM will issue a pulse from its pulse generator at Time=0.  It will start listening for returns at Time=<strong>Scan Start</strong> and top listening at Time=<strong>Scan Stop</strong>.  By converting the distance of interest to the length of time it will take a pulse to travel that distance and return, the <strong>Scan Stop</strong> can be set.  Pulses that arrive later from more distant object reflections will not be part of the scan.

If the target of interest is moving, then stationary clutter can be removed by taking the difference between successive scans.  As long as the radar unit is held stationary in between scans, the reflection from stationary objects will not change from one scan to the next.  Therefore, the signal due to those objects will be removed when the difference between scans is formed.  Any object that has moved will have a signal that occurs in different range bins, and will not be cancelled.

<strong>Experiment: </strong>

For this experiment we will limit the scan range to eliminate reflections from other people in the room.  Then we will perform some basic scan subtraction to remove clutter.  We will also calibrate the start time to give correct range measurements.

<ol>

 <li>Apply power to the MRM, start MRM RET and connect to the MRM.</li>

 <li>Set the <strong>Transmit Gain</strong> to 0 so that signals due to close targets are not saturated.</li>

 <li>Set the <strong>Scan Start</strong> time to 10000 ps. The start time should be set to the time that the pulse leaves the antenna.  We will refine this value later to give us correct distance measures.</li>

 <li>Determine the <strong>Scan Stop</strong>

  <ol>

   <li>You will limit the scan range to approximately 2 meters. This will help to prevent the motion from other users in the room affecting your radar scans.  With this limit in range, how long should a scan last?  (Hint: this is the time required for the pulse to travel out 2 meters and back to the radar at the speed of light.)</li>

   <li>Update the <strong>Scan Stop </strong>value. You must take into account the <strong>Scan Start </strong>time; you want the scan duration to be equal to what you calculated.</li>

  </ol></li>

</ol>

Remember when you change the parameter settings you must <strong>Set </strong>

<h1>Configuration</h1>

<ol>

 <li>Test your scan stop time. Stand away from the MRM and slowly walk towards the radar. At what time do you begin to see your reflection?  If it is not at approximately the time associated with 2 m, then recalculate your value and repeat the previous steps.  Record your <strong>Scan Stop </strong>value.  You may have to increase gain to see the signal at 2m.</li>

 <li>Use the subtraction method to remove clutter. This post-processing will take place in Matlab.</li>

 <li>Make a background scan.</li>

</ol>

<ol>

 <li>Log the data: under <strong>Logging</strong>–<strong>Start Logging</strong>. Make sure the word</li>

</ol>

“background” is in the file name.  Make note of the file name and location.

<ol start="10">

 <li>Set the <strong>Scan Control</strong>–<strong>Count</strong> to 10. Make sure the scan interval is set to 500000ms.  This will record multiple scans in a single log</li>

</ol>

file at ½ second intervals.  We will only use the last one, but by taking extras you will have time to make sure you are not moving during the scans.

<ul>

 <li>Hit the Start Scanning button, and hold still for 5 seconds.</li>

</ul>

Remember motion cannot be removed from the scans.

<ol>

 <li>Close the log file by going to <strong>Logging</strong>–<strong>Stop Logging</strong>.</li>

 <li>Make a target scan.

  <ol>

   <li>Place a target about 1m from the MRM. Measure the distance using a tape measure from the front of the antennas to the target and record this exact distance.</li>

   <li>Repeat step a) above, adding the word “target” to the log file name.</li>

  </ol></li>

 <li>In Matlab open the <em>m</em> file and save the file as</li>

</ol>

<em>Experiment2.m</em>

<ol>

 <li>Change the code so that it will open and save the data from both of your log files. Save the data from your background scans into a variable <em>rawscansV_background</em> and the data from your target scans into <em>rawscansV_target.</em> ii. In separate figures, plot 1 scan from each of these files. Discuss the similarities and the differences in these plots.

  <ul>

   <li>In order to better see the differences between these scans, which should mostly be due to the presence of the target, form and plot a</li>

  </ul></li>

</ol>

difference scan:

<em>scan_difference</em>= abs(<em>rawscansV_background- rawscansV_target</em>) You should now see a pulse reflection at approximately the distance to the target.

<ol>

 <li>Determine the MRM’s measured distance to the target by finding the peak of the <em>scan_difference</em>. Use the max and find commands in Matlab to determine where in the <em>scan_difference</em> vector your peak is.  The value of <em>Rbin</em> at that vector index is the measured distance.  Record the measured distance.</li>

</ol>

<ol>

 <li>Your tape measured distance and the MRM measured distance are probably different. This is due to the setting of the <strong>Start Time</strong>.  We will now calibrate the MRM <strong>Start Time</strong> to give accurate measurements.

  <ol>

   <li>Convert the difference in measured distance and recorded distance to pulse flight time, in picoseconds. Use this flight time to adjust the <strong>Start Time</strong> in the MRM RET.</li>

   <li>Update the <strong>Stop Time</strong> so that your scan time will still give you a range window of about 2m.</li>

  </ol></li>

</ol>

<ul>

 <li>Repeat collecting your background and target scans and determine the radar measured distance. Repeat this process if necessary until</li>

</ul>

you get measurements that are within 3 cm of the tape measured values.

<strong>Questions: </strong>

<ol>

 <li>Examine your scan difference plot. The clutter was not completely eliminated.  Explain the causes of the residual reflections that remain in the plot.</li>

 <li>Matlab code (commands) for 5c(iv).</li>

</ol>