# shutter_speed_tester

A project that goal is to design and build a tool that allows to test the shutter speed accuracy of a film camera

## Introduction

When people passionated of old film cameras want to use their camera to shoot film, this sometimes result in an over or an under exposed film.  
This is usualy due to the speed of the camera shutter that is not any more accurate. In order to check the shutter speed accuracy, the camera owner have to compare the actual opening time of the shutter with the expected one.  
This is the purpose of the shutter speed tester : measure the accuracy of shutter speed. 

## Principle

![Shutter speed tester principle schema](./design/images/principle.svg)

## Usage

1. Put the enlighting light in front of the camera
2. Put the light sensor at the open back of the camera
3. Switch the device on
4. Press the camera shutter button
5. Read the measured camera speed (displayed as a time (t) and as a speed (1/t)), and compare it to the setting of the camera (1/60, 1/125, etc)
6. To perform the measure again, maybe with another camera setting, press the Reset button on the device, and go to 4.

## State Diagram

![State diagram](design/images/states.svg)

## Project scope

The project scope is to describe how to build a shutter speed tester tool.
The outputs of the project are :
- design documents, including the design process itself
- build description

## Preliminary design

The system is very small and is not interfaced with other systems, except
- The user
- The camera

Thus we will not write a complete system analysis of this. We will jump directly to the physical architecture design of our tool :

![Physical Architecture](design/images/physicalArchitecture.svg)

|Component role | Component choice | Comment |
|---------------|------------------|---------|
| Main unit     | Compound         | The main unit is composed of several other components.</br> A specific casing has to be be designed for it |
| Control unit (hardware) | Arduino Nano | An arduino nano microcontroler would fullfill all the needs : </br>- low price</br>- low dimensions</br>- low electric cosumption</br> - capacity to interact with simple electronic components |
| **Control unit (software)**| Specific code| This will be one of the subjects of this project. It has to make the link between the differents componetns of the tool |
| Electrical power | Battery | The detailed design of the battery part has to be defined later. </br>The use of battery allow a more practical usage of the tool. </br>The low consumption of the arduino allow to use it without a to high battery consuption |
| Power switch | Flip flop switch | A "hard" power switch will be preferred rather than a standby push button, in orther to not use the battery at all when not in use |
| Reset button | Push button | The Reset button will be able to erase the previous result and start a new measure |
| Control led| Led | the control led will help the operator to see that the light sensor is currently detecting light (when the shutter is open, if the light source and the light sensor are correctly positionned)|
|Display| 2x16 LCD| A 2x16 LCD is very common, low price and easy to control with an Arduino|
|Light source| Led| The light source has to be chosen in accordance with the light sensor sensitivity (intensity and even maybe wavelength).</br>It has to be mounted preferably on a physical support that allows to adjust the position according the tested camera.</br>There is two options for the light source : </br>  1. Use an independent light source, maybe even don't include it in the package and let the user choose it by himself</br>  2. Use a light source powered by the tool</br>The option 2 is prefered because it allow to have a real control on the quality of the light source. Indeed much of commercial led lamps are quickly blinking when used in eco mode and cannot be used for our purpose.</br>The challenge is to have a light source that <br/>  - is bright enough to allow the light sensor to detect the opening of the shutter</br>  - does not use too much electrical power and does not drain the battery too fast|
| Light Sensor | Phototransistor | A phototransistor is a good compromise between a low price, a good sensitivity and a low reaction time.</br> A specific support has to be designed, maybe according different film formats, in order allow a good position on the camera back, in order to easily detect the source light and not be influenced by environment light |

## General design process

The design process will be split in multiple steps. The idea is to first derisk all that may be tricky.  
At first the electrical circuits design and software components will be tested using a solderless breadboard.  
When all work well, a dedicated motherboard will be designed and manufactured.  
A dedicated casing and mecanical support will be draw and 3D printed.

## Design & development tools

The design & development tools are the following
| Tool name      | Version  | Purpose     | link                            |
| -------------- | -- | ----------- | ------------------------------- |
| Fritzing      | 0.9.3 | Electronic component & circuit design       | https://fritzing.org/ |
| Arduino IDE   | 1.8.16 |Arduino cross development IDE    | https://www.arduino.cc/en/software |
| VSCode | 1.62.0 | General purpose code editor | https://code.visualstudio.com/ |
| Drawio integration | 1.6.201 | Integration of Drawio tool into VSCode IDE |

## Developpement steps description

[Development steps](DevelopmentStories.md)

## Part list
| Name | Description | Aprox. Price | Reference |
| ----- | -------------| ---------- | ------ |
| High power Led | A 8000 mcd red led | 0.62 € | https://www.conrad.fr/p/kingbright-l-7113sec-j3-led-rouge-rond-5-mm-8000-mcd-20-20-ma-22-v-1050453 |
|JST XH connector|    |   |   |


