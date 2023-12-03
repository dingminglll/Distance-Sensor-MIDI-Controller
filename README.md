# Distance Sensor MIDI Controller
This project is built using an Arduino and a VL53L0X distance sensor. The VL53L0X chip sends distance information back to the Arduino, which then converts these distances into different MIDI signals, transmitting them to the host software.

## Airdrum
Set the MIDI parameters to be transmitted in the Arduino.

Different distances correspond to different signals, representing different sounds, as shown below:
``` C++
void loop()
{
  int distance = sensor.readRangeSingleMillimeters();
  if(distance<500){
    
    if(distance<200){
      //basedrum
      noteOn(0, 36, 64);   // Channel 0, middle C, normal velocity
      MidiUSB.flush();
      delay(100);
    }
    
    if(distance > 200 && distance < 350){
      //snare
      noteOn(0, 38, 64);   // Channel 0, middle C, normal velocity
      MidiUSB.flush();
      delay(100);
    }
    
    if(distance>=350){
      //crash
       noteOn(0, 42, 64);   // Channel 0, middle C, normal velocity
      MidiUSB.flush();
      delay(100);
    }
    Serial.print(distance);
  }
  
  if (sensor.timeoutOccurred()) { Serial.print(" TIMEOUT"); }

  Serial.println();
}
```

Upload the code to the Arduino control board.

Open the host software (e.g., Ableton Live 11) and select Arduino Leonardo as the MIDI device.![Alt text](/img/image3.png)

In the host software, select the desired drum machine sounds.

The code sets three distance ranges, corresponding to the sounds of a bass drum, a snare drum, and cymbals. By changing the distance from the device, different sounds can be played. Combining different sound combinations and the rhythm of hand waving can create a variety of rhythmic patterns.

## CC Controller
Change the sound waveforms in real-time to achieve real-time changes in sound effects, as shown in the figure below:
![Alt text](/img/image2.png)

Diagram of real-time adjustment of sound waveforms

Edit MIDI mapping in the host software, using different distances to control different knobs, buttons, etc.

By choosing to control the waveform of the sound, you can change the sound effects in real-time during performance by changing the distance to the device.
