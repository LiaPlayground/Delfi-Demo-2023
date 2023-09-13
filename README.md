<!--
author:   Sebastian Zug; André Dietrich

email:    sebastian.zug@informatik.tu-freiberg.de

version:  0.0.2

language: de

narrator: Deutsch Female

icon:     https://media.aubi-plus.com/institution/thumbnail/3f3de48-technische-universitaet-bergakademie-freiberg-logo.jpg

-->

[![LiaScript](https://raw.githubusercontent.com/LiaScript/LiaScript/master/badges/course.svg)](https://liascript.github.io/course/?https://raw.githubusercontent.com/LiaPlayground/Edrys-Demo-2023/main/README.md#1)

# Modulare und konfigurierbare Remote-Labs mit Edryss
<h2>Challenges and Solutions </h2>

<div style="width: 46%; float: left">

André Dietrich, Sebastian Zug

Institute of Computer Science

TU Bergakademie Freiberg

</div>

![partner_map](https://github.com/Cross-Lab-Project/presentations/blob/main/GeCon_2022_Adaptability/Partners.png?raw=true)<!-- style="width: 50%; float: right" -->


## Motivation

     {{0-1}}
<section>

> __Traditionelle Remote-Labore sind geschlossene Strukturen, die individuelle Lernziele repräsentieren.__

``` ascii

  Laboratory Level                   Monolithic
                          Server-Infrastructure          Learner's View
  n Instances   .--------------------------------.
                |                                |         m Instances 
                                                                 .
      +-----------------+         +-----------------+            .  
      | Instrumentation |░        |    Management   |░           .
      +--------.        |░        +--------.        |░  
 +-----------+  \       |░   +-----------+  \       |░   +----------------+
 | 👩🏻‍🔬 Actual  \  \      |--->|  Gateway   \  \      |--->|  Web Browser   |
 | Laboratory /  /      |<---|     🖥     /  /      |<---|      🧑‍💻        |
 +-----------+  /       |░   +-----------+  /       |░   +----------------+
      +--------'        |░        +--------'        |░   Student's Computer
      |                 |░        |                 |░
      +-----------------+░        +-----------------+░           .
        ░░░░░░░░░░░░░░░░░░          ░░░░░░░░░░░░░░░░░░           .
                   .                                             .
                   .
                   .                                             
```

</section>


     {{1-2}}
<section>

> __Crosslab zielt auf die übergreifende, interdisziplinäre Nutzung von Remote-Laboren.__


```ascii

                             .--------------.   .--------------.   .--------------.
                             | technical    |   | didactical   |   |organisational|
                             |              |   |              |   |              |
                            +--------------------------------------------------------+
         +-->    elements   | composition of varying laboratory objects              |
         |                  +--------------------------------------------------------+
         |                   |              |   |              |   |              |
         |                  +--------------------------------------------------------+
         +-->        types  | mixture of different types of laboratories             |
         |                  +--------------------------------------------------------+
CROSS ---+                   |              |   |              |   |              |
         |                  +--------------------------------------------------------+
         +->  disciplinary  | sharing laboratories between different disciplines     |
         |                  +--------------------------------------------------------+
         |                   |              |   |              |   |              |
         |                  +--------------------------------------------------------+
         +-->   university  | formation of a laboratory cluster                      |
                            +--------------------------------------------------------+
                             |              |   |              |   |              |
                             .--------------.   .--------------.   .--------------.
```

<!-- class="highlight" -->
> __Project:__
> [Crosslab](https://stiftung-hochschullehre.de/projekt/crosslab/) - Flexibel kombinierbare Cross-Reality Labore in der Hochschullehre: zukunftsfähige Kompetenzentwicklung für ein Lernen und Arbeiten 4.0, Stiftung Innovation in der Hochschullehre (2021 - 2024) - TU Bergakademie Freiberg, TU Illmenau, TU Dortmund, Nordakademie


<!-- class="reference" -->
> __Reference:__
> Ines Aubel et al
> _Adaptable Digital Labs - Motivation and Vision ofthe CrossLab Project_
> GeCon 2022
> [Link](https://www.researchgate.net/publication/365384986_Adaptable_Digital_Labs_-Motivation_and_Vision_of_the_CrossLab_Project)

</section>


## Edrys - Konzept und Implementierung

     {{0-1}}
<section>

> _Divide and Conquer_ Differenzierte Module statt atomarer Impementierungen
  

``` ascii

                                        Existing
                                 Module Implementations
                                     from the Web
                                           |
                                           v    
      +-----------------+         +-----------------+            .  
      | Instrumentation |░        |    Management   |░           .
      +--------.        |░        +--------.        |░  
 +-----------+  \       |░   +-----------+  \       |░   +----------------+
 | 👩🏻‍🔬 Actual  \  \      |--->|  Gateway   \  \      |--->|  Web Browser   |
 | Laboratory /  /      |<---|     🖥     /  /      |<---|      🧑‍💻        |
 +-----------+  /       |░   +-----------+  /       |░   +----------------+
      +--------'        |░        +--------'        |░   Student's Computer
      |                 |░        |                 |░
      +-----------------+░        +-----------------+░           .
        ░░░░░░░░░░░░░░░░░░          ░░░░░░░░░░░░░░░░░░           .
      |                        | |                     |         .
      '------------------------' '---------------------'
             Edrys Station           Edrys Classroom
          PC in the Browser!              Server
```

</section>


    {{1-2}}
<section>

```ascii
                                        Existing
                                 Module Implementations
                                     from the Web
                                           |
                                           v                     .
      +-----------------+         +-----------------+            .  
      | Instrumentation |░        |    Management   |░           .
      +--------.        |░        +--------.        |░  
 +-----------+  \       |░   +-----------+  \       |░   +----------------+
 | 👩🏻‍🔬 Actual  \  \      |--->|  Gateway   \  \      |--->|  Web Browser   |
 | Laboratory /  /      |<---|     🖥     /  /      |<---|      🧑‍💻        |
 +-----------+  /       |░   +-----------+  /       |░   +----------------+
      +--------'        |░        +--------'        |░   Student's Computer
      |                 |░        |                 |░
      +-----------------+░        +-----------------+░           .
        ░░░░░░░░░░░░░░░░░░          ░░░░░░░░░░░░░░░░░░           .
      |                        | |                     |
      '------------------------' '---------------------'
                     ^               +-----------+
                     |               | * ...     |\
                     |               | * ...     +-+
                     |               | * Module 1  |     Classroom 
                     |               | * Module 2  |     configuration
                     |               |             |
                     | .yaml / .json |             |
                     +---------------| * Station 0 |
                                     | * ...       |
                                     +-------------+
```

<!-- class="reference" -->
> __Reference:__
> OER and Digital Laboratories,
> GeCon 2023
> [Link](https://liascript.github.io/course/?https://raw.githubusercontent.com/Cross-Lab-Project/presentations/main/GeCon_2023_Keynote/CrossLab_GeCon2023.md)

</section>

### Umsetzung

![](https://github.com/Cross-Lab-Project/presentations/blob/main/HDF_CommunityGroup_2022/Screenshot.png?raw=true "Remote Laboratory")

### Existierende Module 

| [Modules](https://github.com/topics/edrys-module) | [Classrooms](https://github.com/Cross-Lab-Project/openLabs) |
| ------------------------------------------------- | ----------------------------------------------------------- |
| Collaboration (Chat, Video Call)                  | Micro-controller (based on arduino-cli)                     |
| Interaction (Whiteboard, Editors)                 | Programming environments for various languages              |
| Input/Output (Video stream, Console)              |                                                             |
| Teaching Materials (LiaScript)                    |                                                             |

### Exemplary Edrys course as OER 

> __Exemplarischer Arduino-Kurs als OER für Edrys [Link](https://github.com/LiaPlayground/Edrys-Demo-2023/blob/main/class/Arduino-Lab.yml).__

```` yaml   edrys_arduino_example.yaml
id: aGLUUb8kSI9yFmY6GYcLx
createdBy: andredietrich@web.de
dateCreated: 1689064662293
name: Real Labs
meta:
  logo: >-
    https://raw.githubusercontent.com/TUBAF-IfI-LiaScript/VL_EAVD/master/excercise/images/excercise_04.png
  description: >-
    Die Studierenden setzen eine Anwendung um, die zwei existierende Klassen für
    die Verwendung von peripheren Bauteilen - Ultraschallsensor und LCD-Display
    - um. Im Ergebnis steht eine Applikation die kontinuierlich die Distanz zu
    einem Hindernis vermisst. Die Daten werden zudem über die Serielle
    Schnittstelle ausgegeben und analysiert.
  selfAssign: true
members:
  teacher:
    - andredietrich@web.de
    - sebastian.zug@informatik.tu-freiberg.de
  student:
    - passe.partout@web.de
modules:
  - url: https://edrys-org.github.io/module-liascript/
    config:
      course: >-
        https://raw.githubusercontent.com/TUBAF-IfI-LiaScript/VL_EAVD/master/excercise/04_OOP_stud.md
    showInCustom: Lobby
    width: full
    height: tall
  - url: https://cross-lab-project.github.io/edrys_module-station-stream/index.html
    stationConfig:
      video: true
      audio: false
    showInCustom: station
    width: full
    height: tall
  - url: https://cross-lab-project.github.io/edrys_module-editor/index.html
    config:
      editorText: |
        #include <LiquidCrystal.h>
        #include <NewPing.h>

        const int triggerPin = 51;   
        const int echoPin = 53;     
        const int maxDistance = 400;
        const int ledPin =  13;

        //Pin assignments for SainSmart LCD Keypad Shield
        LiquidCrystal lcd(8, 9, 4, 5, 6, 7); 
        NewPing sonar(triggerPin, echoPin, maxDistance);

        void setup() 
        { 
          lcd.begin(16, 2);
        }

    ....
````

## References

| Reference                | Link                                                                         |
| ------------------------ | ---------------------------------------------------------------------------- |
| Crosslab Projekt Website | [https://cross-lab.org/](https://cross-lab.org/)                             |
| Project Repository       | [https://github.com/Cross-Lab-Project](https://github.com/Cross-Lab-Project) |
| Edrys Repository         | [https://edrys.org/](https://github.com/edrys-org/edrys)             |
| LiaScript                | [https://LiaScript.github.io](https://LiaScript.github.io)                   |



> Presentation materials:
>
> + https://github.com/LiaPlayground/Edrys-Demo-2023/
> + https://liascript.github.io/course/?https://raw.githubusercontent.com/LiaPlayground/Edrys-Demo-2023/main/README.md#1


