# GloVe
My software written in PureData for Bela microcontroller hardware to power a generative glove instrument I built and designed
   Simo Suoheimo
MusiGlove
A new musical instrument for vocalists and live performers

7th December 2022
 
Table of Contents
Table of Contents 2
Overview 3
Project Plan and Design 3
Goals 3 Design and Sketching Phase 3 Bill of Materials 6
Software implementation with PD 7
Bela & Pure Data 7 
Inputs from interface, Chordifyer with Sigmund pitch analyzer object, Osc’s and phasors 8 
Vocal pitch-following FM Synth with chords and chorus 9 
Reverb 10
Hardware implementation and construction the instrument 11
Electronics and Glove Design 11 Flex Sensors 13
Playing the MusiGlove and Lessons Learned 15
Design Principles: Simplicity reigns supreme 15
The value of testing code and sensors in small batches is immense and makes it easier to focus on the right features 15
New electronic instruments can be fun and intuitive when they are designed around the performers’ natural movement 16

Overview

I developed and created hardware and software for a novel musical instrument, MusiGlove, merging live synthesis run PureData on a Bela microcontroller (other MC's eg. Raspberry Pi w/ audio interface HW w/ PD support are alternative options), effects, and using the performer’s natural finger movements as a starting point to accompany vocals and other musical performances was designed.
The design choices, building process, challenges, lessons and insights from creating and finally playing the instrument are discussed in this project and learning diary.
Project Plan and Design
Goals
The goal was to design, develop and create a working, playable prototype of novel musical instrument using my knowledge as a musician, learning key skills in electronics, electronic instrument design, programming a Bela microcontroller environment, and creating patches in PureData that enable live synthesis and effects. In addition to the working instrument, documenting lessons and challenges of using a human-computer interaction-centered approach to a musical interface, working with electronics and sensors, physical and software design lessons and limitations, learning the Bela platform, and working with PureData are also key outcomes.

Design and Sketching Phase (insp. by Agile, Lean Product Dev philosophy)

Initial designs included a pre-glove iteration that was used as a testbed while creating the PureData (PD) patches, and to test electronics, calibrate sensors, and to get to know the Bela environment.
I approached the design phase and building phase as an iterative process that would loop back to the designs and a new iteration of sketches based on the learnings, challenges and limitations faced with the physical, PD and glove designs.
User-centered design, experience and recordings from live vocal perfomance situations, my own musical inspirations as a vocalist and performer, and Human-computer interaction knowledge were used as a starting point for designing the new instrument.
Initial design sketch of the instrument, its capabilities and its design affordances
 
  1. Identifying the key features and characteristics (Week 2-3 of 6): Glove interface for a vocalist that produces live FM synthesis sounds corresponding to vocal pitch through a microphone input, controlled by hand and finger movements. I wanted to make sure the instrument corresponds to a performers’ natural, personal hand movements during a live performance. Furthermore, the sound input should not be limited to a microphone, but could also be used with any other non-percussive musical instrument, although monotonal instruments would be best suited as inputs.
The musical characteristics should allow for real-time synthesis and effects that the vocalist could use to play the instrument that could also be recorded separately - not a mere vocal effect or controller that most existing glove controllers essentially provide, but a real instrument that allows for stand-alone expression in live and recorded performances. The instrument should also be able to produce soundscapes without vocal or instrument signal inputs.
I modelled my own on-stage movements through me own real live performance videos to make sure the instrument would fit those well, reducing the barrier to learn and use the instrument, and to make its incorporation into my own performances natural and effortless, even for the first prototype.
2. Researching existing musical instruments and their designs (Week 2-3), with attention paid to how they are used and what makes them effective or user-friendly. This step was used to identify best practices and avoiding common pitfalls. These included DIY glove projects that are usually designed to activate effects such as pitch, reverb and vocoders, VR glove designs, and the MiMu glove used by musician Imogen Heap. Key issues include natural movement, learning threshold, lack of live synthesis as most are basically midi controllers in glove form, ease of use, and durability.
3. The development of a concept for the instrument (Week 2), including a detailed description of its features and sketches. Eg. an early sketch of functionalities and an idea of having an instrument in-feature as an additional microphone or piezo as well as a glove and vocal feature, that was simplified into the final design of a glove.
4. The creation of a prototypes of the instrument on PD 0.52-2, Mac, Bela, and breadboard (week 3-4) helped me test and refine the design, as well as identify any challenges or limitations

  that needed to be addressed. These included limiting the complexity of the code, features, and sensors, and eg. replacing problematic PD objects with simpler ones, and working with the sonics and sounds in PD to make them more user-friendly and to limit eg. unwanted signals from sensors.
5. The testing and refinement phase was repeated during weeks 4-6. I had no experience with PD and Bela or microcontroller programming before the project, which taught humility and realism in debug code, understanding the inner workins of PD objects and programming, as well as numerous aspects of using sensors and microphone audio inputs with Bela running on PD. A key lesson was to be flexible with the components available, which was critical to adapt to the availability of components as well as a few component failures on the final week.
I used a Lean Product Development workflow of building, measuring, learning and implementing the lessons into the next design iteration. These were:
1. Initial playable design running on Mac and breadboard without glove and final components 2. Simplified version with actual sensors (only one flex sensor was available before the final
week, as parts delivery took time) running on Bela
3. Final version with the MusiGlove interface running as a stand-alone on Bela
Key lessons from a design perspective included the value of iterative design and building minimum viable product (MVP) versions of the instrument, while documenting learnings and updating the next design iterations, and solving problems rapidly with fast light prototypes.
Lessons along the way and their solutions involved understanding PD, Bela, interface and sensor issues, such as sensitivity to movement, stability issues of code on Bela, and scaling down initial design specifications and expectations on the side of processing power-hungry code such as the initial FM synth patch that was developed but seemed to cause potentially memory-related Bela problems even while running flawlessly on a Mac laptop in PD Vanilla 0.52.2, limiting and removing problematic versions of reverb and chorus effects, and other tweaks.
Furthermore, the initial ambition of several sensors and their interaction was scaled down to individual sensors and simplified logic in PD, to ensure robustness and playability of the prototype during the final assembly, as several components did not arrive, and the ones that did arrived four days before the final project presentation.

  Bill of Materials
Based on the designs and sketches, I planned a bill of materials and listed the tools needed to create the first iterations of the instrument, sensors, and glove. Careful planning helped, but not all components were available, resulting in a last-week redesign of the final prototype around less sensors and implementing basic switching features in PD instead.
Bela Board microcontroller
Breadboard
5 Flex Sensors (Final design works with two)
Wiring and straps
Gloves: kitchen rubber gloves and surgical gloves for first rough prototypes, leather inner and outer gloves for final prototype
Felt and plastic reinforcements
2 Potentiometers (for pre-glove iteration on breadboard)
Flexible potentiometers
Resistors
Power source (LiPo battery)
Accelerometer (Not used in final version)
Capacitive touch sensor (Replaced with flex sensor programming) ESP32 Dev kit (Did not arrive, can be used in v2.0 wireless version) Memory card
1⁄8 stereo plug input and output, female
Basic battery powered loudspeaker for testing
Zoom H5 audio interface
Dynamic Rode microphone
XLR cable

  Software implementation with PD
Bela & Pure Data
Learning, creating and experimenting with PD 0.52-2 Vanilla and Bela was an entirely new challenge for me. After the course introduction and coding exercises, I studied PD documentation, open source projects and new objects online, on forums, in PD help sections and Youtube tutorials. A key lesson was the depth of PD and the value of getting features working in small batches, often one by one on the Bela, instead of trying to run complex patches that worked on a Mac laptop and uploading them to Bela, as this made troubleshootin the code very complex. Unexpected errors occurred throughout the project, and many couldn’t be solved even with hours of studying documentation, rare error messages and the generous help of our course's great teaching assistant Anssi and teacher Koray Tahiroglu, which lead to dozens of hours of rewriting and simplifying the patches designed in the previous design phase during the project and running them one by one to ensure stability. The ability to troubleshoot and modify variables live on Bela would have been a great asset in this phase, but instead, surprising amounts of time trickled into uploading small batches of code onto Bela to identify and solve PD problems that did not present themselves on a laptop.
I used analog inputs from the flex sensors in the glove’s fingers to control and stack the FM synth, “Chordifyer” and reverb. Initially, I designed these to be dynamic and to also control the FM synth attack and other variables but decided to cut these features for the time being to ensure smooth performance, to limit error and stability issues, and to make sure a working stable prototype would be produced by the end of Week 6 of the project.
A key lesson was to run small parts of the PD programming at a time, as problems could not be identified in a Mac environment, which was a slight surprise considering Bela’s capability of running PD vanilla. Some issues could not even be fixed by changing Bela’s data rate, and had to be solved by simplifying the code and features.
Cleaning signals from the analog inputs was a useful universal lesson on running sensors and code on a microcontroller, and was became a key skill during the project. Overall, the value of simplicity in code and sensor functionality, instead of sophisticated sensor interaction with “if-else” logic was highlighted during the project.

  Inputs from interface, Chordifyer with Sigmund pitch analyzer object, Osc’s and phasors
Initial designs had PD patches oranized in sub patches, but these turned out challenging to debug on Bela, even when no error were produced on PD on a Mac. During the last week, I rewrote the patches and refrained from using sends and mix objects to streamline troubleshooting and to account for the very limited time of working with the components as they arrived on the last week of the project.
The Sigmund object documentation and online examples took considerable time to understand, and worked out in the end in spite of several questions on the way. Some flags could not be implemented even when used as documented, which might be a problem with the actual object, and reported by other PD users online.
To calibrate the sensors’ analog output and to account for mechanical errors caused by their nature as flexible resistors, the oscilloscope in Bela proved invaluable.
I explored several options for the Chrodifyer, and chose phasors and osc objects arranged in chords and omitted modulation features for simplicity and to account for the sensors that did not arrive in time. These features are simple to add in a future v2 prototype, but testing the instrument in real life suggests may be excessive given the sonic character of the instrument.
 
  Vocal pitch-following FM Synth with chords and chorus
An FM synth patch is fed midi notes from the audio input through a microphone, routed through Sigmund’s pitch analyzer to produce a rich live synthesis that can be used to accompany the vocalist’s pitch, or to produce ambient soundscapes. Testing revealed the sonics gained desired richness from a delicate chorus effect, but also confirmed suspicions that excessive chorus and delay on the code level can cause unwanted muddiness, as well as stability issues when run on Bela. Furthermore, controlling effects and the release, attack and FM amount on a third finger while performing live was rather inaccurate, while controlling the Chordifyer and and FM synth on the first and second finger, revealing the limitations in finger accuracy and control while singing live, and allowing for simplicity on the sensor input and PD code level without sacrificing essential features or stability in a live setting.
 
  Reverb
The reverb initially designed was a more complex patch with additional controls, which was simplified into a smoothly running simple version to ensure stability and to remove the need for a discrete dedicated sensor. Adc5 in the main patch could be used to modulate the reverb in a future version, but the flex sensors available on Week 6 would not allow this in the prototype. However, through experimentation, the right settings on the reverb proved more than sufficient for the instrument in a live musical setting in the end, and deeper control would be a bonus rather than a necessity. Bela experience during the project taught me that it rewards simplicity over complexity.
 
  Hardware implementation and construction of the instrument
Electronics and Glove Design
A leather glove inner with a larger, rigid leather glove outer, with the sensors mounted in between, was chosen after testing prototypes attached directly to fingers and to kitchen and surgical gloves. This allowed for more control thanks to the added rigidity and structure of the gloves, and added protection to the sensors for durability in live situations where the musician moves freely and sometimes rapidly. It also allowed for a simplistic aesthetic that doesn’t distract from the musicians’ performance, movement and expression in a performance situation.
First and middle finger were chosen as the main fingers for the flex sensors to control the PD patch main functions, taking my personal finger movement habits into account through observing my own performance videos.
Prototyping with a flex sensor attached to bear hands to experience the sensitivity of the sensor directly and to allow for a better design of the glove construction
 
  A sturdy Black Diamond Guide leather glove was chosen as the outer glove for its rigidity. It covers the sensors and the inner glove, providing protection for the sensors, a better feel for the player, and rigidity for controlling individual finger movements without triggering other sensors unintentionally. 8.2kOhm and 1MOhm resistors were used on the breadboard for rapid prototyping. Analog signals are routed into adc3, 4 and 5 on Bela. The dynamic microphone signal is routed through a Zoom H5 into Bela.
 
  Flex Sensors
12 cm flexible resistor-based flex sensors were used in the first and second fingers of the glove. The flex sensors were soldered carefully and secured from direct pulling with an attachment loop between the gloves in the second iteration, after noting they were subject to force during hand movements.
The mechanical wear was an issue that broke one sensor during testing, and was tackled by choosing to use fit them between an inner and outer glove within a plastic pocket, providing rigidity, robustness, preventing breakdowns and adding stiffness and accuracy to the control for the performer.
 Careful soldering was essential to ensure the robustness of the instrument.
One flex sensor broke due to mechanical wear during prototyping before the double glove structure was introduced.
  
  The breadboard setup with regular potentiometers allowed for rapid prototyping and initial calibration of analog signals before constructing the glove.
 
  Playing the MusiGlove and Lessons Learned
Simplicity reigns supreme
PD offers almost endless options for creating elaborate musical instruments and ways to generate, modulate and control sound. However, building a robust, stable and fun-to-play instrument merging together the physical UX of the glove, the electronics, and code running on Bela requires pragmatism and streamlining in design choices and affordances. This requires smart prioritization and humility: developing elaborate patches first without the ability to test them with a physical prototype is often counterproductive, and many features such as deeper parameter control of reverb, delay, and the FM synth parameters turned out to be excessive and more on the side of “nice-to-have” compared to vital in most performance situations with the instrument. Furthermore, these would typically be redundant in both live and studio settings.
Overcoming countless issues on the hardware and code level, from breaking sensors and solder, to reinforcing the glove, and to simplifying the PD code to account for Bela limitations and instability was a key part of the learning process, and could in many cases have been avoided by more experience with the sensors’ capabilities and eg. analog signal quality, Bela’s limitations, and a slower step-by-step approach testing small features in batches, which was a key lesson on the realities of design and implementation of electronics, hardware and code when creating a musical instrument. In this sense, my experience with PD and Bela required a different approach and more step-by-step testing and debugging compared to eg. Python development in my other projects.

  The value of testing code and sensors in small batches is immense and makes it easier to focus on the right features
The simplicity on the code, user interface and instrument UX level were key lessons learned during the project: When creating a novel electronic instrument running live synthesis and effects on a microcontroller with the goal of using it in a live performance, simplicity reigns supreme, performer inputs should be calibrated carefully and to require less precision, and with the philosophy of “less is often more”. The artistic expression, ease of adoption, learning curve and enjoyment of use afforded by the pre-made design choices of the instrument gain from simplicity and limiting depth of adjustment, where not absolutely crucial for the core features of the instrument.
New electronic instruments can be fun and intuitive when they are designed around the performers’ natural movement
Performing music and composing with MusiGlove has proven to be an easily accessible and enjoyable experience that allows for a lot of creativity with a few minutes of use even for new users. Several features in the initial designs were probably excessive, and usability turned out to be more important than the ability to fine-tune parameters of the effects, the Chordifyer and the FM synth in a live situation, given the complexity of fine motor control of several fingers individually. The project and testing the usable prototype in musical performance settings highlighted the importance of intuitiveness in using hand movements while singing and playing the instrument over the value of deeper tinkering of parameters in a live situation. With the simpler design, the MusiGlove allows for deep creativity with live synthesis for players without any previous experience with the instrument, while rewarding more thorough learning with rich musical expression in a fun and intuitive way, whether performing solo or accompanied by other musicians.

   
   
   
