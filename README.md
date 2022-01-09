# Sense-of-independence

Python code to be run on Rasperry Pi. Sets up virtual emulator and uses emulator funcitonality to simulate electromyography (EMG) to detect patient tonic and clonic seizures

- Jack Fujita and Lara Al Barbarawi

This computer program will be able to detect the type of seizure, length of seizure and time of seizure, in the presence of one, in infants.
	- It will detect two main types of seizures; Clonic and Tonic.
		Clonic Seizure: Jerking/Twitching of the muscles
		Tonic Seizure: Stiffening of the muscles
	- The program will write to two different files: 
		1- raw_data: includes the raw data, rolling average, type of seizure (if occuring).
		2- seizure details: inlcudes the list of rolling averages of the past 30 seconds, Seizure status (Type of seizure), time of day & length of seizure.
			This file will be used for detailed analysis of the infants condition. 
	- If the length of the seizure is greater than 5 minutes (300s), the program warns the parents with a medical emergency.

Note: Length of seizure can only be determined once the seizure has come to an end.
Note: Datetime library may need to be installed.

The MYoware EMG sensor will be located in a wearble device attached to the infant's back with the reference electrode attached to the backbone.
The program will communicate the output data in the form of four different combinations LED lights and a buzzer via a pager that the parents will carry around.


Setting up the emulator:
	- GPIO18: Buzzer 
	- GPIO24: Red LED
	- GPIO25: Yellow LED
	- GPIO12: Green LED
	- GPIO16: Blue LED
	- Sensor: EMG

Note: You will notice that the yellow LED is on. This is because the device is still not connected


Test Cases:
   1. Tonic Seizure:
	Increase the value from 0 to above threshold_1 (=150)
	Buzzer, Yellow & Green LEDs lights will turn on because the type of seizure is yet to be identified
	After roughly 30 seconds, a tonic seizure will be detected and Blue LED light will turn on
   2. Clonic Seizure:
	Quickly fluctuate between 0 and 255
	Buzzer, Yellow & Green LEDs lights will turn on because the type of seizure is yet to be identified
	After roughly 30 seconds, a Clonic seizure will be detected and Red LED light will turn on
   3. Unable to identify:
	Start off with tonic, and end with clonic, or vice versa ( OR any abnormal patterns of flucuations that haven't been defined above in clonic and tonic seizures.)
	Buzzer, Yellow & Green LEDs lights will turn on because the type of seizure is yet to be identified.
	After roughly 30 seconds, Seizure Unidentified will be displayed. Green and Yellow LED lights will turn on.
   4. False Alarm:
	Increase the value from zero to well over 150 and return back to below 150
	Buzzer, Yellow & Green LEDs lights will turn on because the type of seizure is yet to be identified.
	After roughly 30 seconds, False alarm will be displayed. Green LED light will turn on.
   5. Medical Emergency:
	Stimulate one of the above seizures and leave for over 5 minutes.
	The Buzzer will turn on and blue and red lights will flash to warn the parents of a medical emergency.
