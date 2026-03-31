Model car and pedestrian traffic lights at a city crossroad, where one road runs along the North-South 
direction and other along the East-West. Each road has a pedestrian crossing.   

Car Traffic Lights: Model two traffic lights for cars– one for each direction. Each traffic light should 
have the standard three states: Red, Yellow, and Green. Ensure synchronization such that at any point, 
both car traffic lights aren’t green simultaneously to avoid accidents.   

Pedestrian Traffic Lights: Model two pedestrian lights, one for each crossing. Lights should have two 
states: Green and Red. Synchronize it with car traffic lights to ensure pedestrian safety. For instance, 
when cars have a green light, the corresponding pedestrian light should be red.   

The key challenge is to synchronize the four lights to ensure smooth traffic flow and maximum safety. 
Make sure to properly configure the initial states of four traffic lights.   

Simulation and Verification: Once the model is set up, use UPPAAL simulator to observe the behavior. 
of your traffic light system   

Formulate verification queries in UPPAAL to ensure the following:   

There is never a deadlock 
Car traffic lights are never green at the same time 
When car lights are green, corresponding pedestrian lights should indicate red. 
When pedestrian lights are green, corresponding car lights should indicate red. 
Both pedestrian and car lights should eventually turn green 
All lights should never be red at the same time.   

 
Naming Requirements 
Car traffic lights should be named as Car_NS and Car_EW for North-South and East-West directions 
respectively. 
Pedestrian traffic lights should be named as Ped_NS and Ped_EW for North-South and East-West 
directions respectively. 
States should be named as Red, Yellow, Green for car traffic lights and Red, Green for pedestrian traffic 
lights.  

####  Objective  

The goal of Task 1 is to design, model, and simulate a traffic control system at a busy city intersection 
using the UPPAAL tool. The primary aim is to ensure safe and orderly traffic flow by synchronizing 
the operation of car traffic lights and pedestrian signals. The task emphasizes pedestrian safety by 
allowing pedestrian crossings only when it is safe to do so, thereby preventing potential conflicts 
between vehicles and pedestrians. This synchronization ensures that car and pedestrian signals operate 
in a coordinated manner, promoting safety and efficiency.   

Key Components   

The task is divided into two essential components that need to be carefully modeled and 
synchronized:   

1. Car Traffic Lights: 
• The car traffic lights are modeled for two primary directions: North-South (NS) and East
West (EW). 
• These traffic lights follow a standard three-state system: 
Red: Vehicles must stop. 
Yellow: Warning phase, indicating the light is about to turn red. 
Green: Vehicles are allowed to move. 
• The lights for the North-South and East-West directions must be synchronized to ensure that 
conflicting green signals do not occur simultaneously, which could lead to accidents.

 
2. Pedestrian Signals: 
• Pedestrian signals are modeled to work in alignment with the car traffic lights. 
• Pedestrians are allowed to cross the intersection only when it is safe, meaning when the car 
traffic lights for the corresponding direction are red. 
• The pedestrian signals will typically have two states: 
Red: Pedestrians must wait. 
Green: Pedestrians are allowed to cross. 
• The pedestrian signals need to be synchronized with the car traffic lights to ensure that 
pedestrians are never given a green light when vehicles are allowed to move through the 
intersection.

Modelling Approach 
In UPPAAL, the traffic control system will be represented using state machines, which are an effective 
way to model discrete states and transitions. Each component (car traffic lights and pedestrian signals) 
will have a corresponding state machine with well-defined states and transitions that adhere to safety 
and synchronization rules. The following aspects will be included in the modelling approach:   

State Definitions:   

For car traffic lights, the states will be: Red, Yellow, and Green. 
For pedestrian signals, the states will be: Red and Green. 
 
Transitions and Conditions:   

Transitions between states will be governed by predefined rules that ensure synchronized operation. 
For example, the North-South traffic lights will turn green while the East-West lights remain red, and 
vice versa. 
Pedestrian signals will transition to green only when the corresponding car traffic lights are red, 
ensuring a safe crossing period.  

Timing Constraints:   

Each transition will incorporate timing constraints to simulate realistic durations for each traffic light 
phase (e.g., red light duration, green light duration). 
Timed automata in UPPAAL will be used to enforce these constraints, ensuring that the timing behavior 
of the system is accurate. 
 
Synchronization Mechanisms:   

UPPAAL’s synchronization channels will be used to coordinate transitions between car and pedestrian 
signals. 
For example, when the car traffic light transitions to red, it can trigger the pedestrian signal to transition 
to green. 
 
Simulation and Verification   
 
The UPPAAL simulator is used to run the traffic light model step-by-step, allowing designers to observe 
the real-time interactions between the car traffic lights and pedestrian signals. During simulation, users 
can visualize how the system transitions between different states (e.g., from green to yellow to red) and 
how these transitions are synchronized between cars and pedestrians. 
 
Key points observed during simulation include:   
 
State Transitions:   

• How the car traffic lights for the North-South (NS) and East-West (EW) directions move 
through their states (Red, Yellow, Green). 
• How the pedestrian signals change states (Red, Green) in coordination with the car lights.   

 
Timing Constraints:   

• The duration for which each light stays in a particular state (e.g., how long the green light 
lasts before transitioning to yellow). 
• The timing behavior ensures that lights change at appropriate intervals to maintain smooth 
traffic flow and pedestrian safety.   

 
Synchronization:   

Whether the pedestrian signals are only green when the corresponding car traffic lights are red. 
Ensuring that conflicting green lights (where cars and pedestrians are both given the right of way) do 
not occur.   

Simulation helps identify potential issues such as incorrect timing, conflicting signals, or missed 
synchronization, allowing for adjustments to the model before verification.    


#### Modeling  

The traffic control system for managing vehicle and pedestrian traffic at a city intersection is modeled 
in UPPAAL under the system name Traffic Control System. This system uses state machines to 
represent the dynamic behavior of car traffic lights and pedestrian signals in both North-South (NS) and 
East-West (EW) directions. The following sections provide a detailed explanation of how this system 
is constructed, including defining states, specifying transitions, assigning temporal parameters, and 
ensuring synchronization.   

Initiating Car Traffic Lights Template   

• Car Traffic Lights for North-South Direction (Car_NS):   

 Initial State: Green 
 The traffic light starts in the Green state, allowing cars to move through the intersection. 
 From the Green state, the light transitions to Yellow after a specified duration (e.g., 30  
 seconds). 
 After the Yellow state (which lasts for 5 seconds), it transitions to Red. 
 The Red state remains active for a defined period (e.g., 30 seconds) before cycling back to 
 Green.     
 
 
• Pedestrian Lights for North-South Direction (Ped_NS):   

Initial State: Red 
The pedestrian signal starts in the Red state to ensure that pedestrians do not cross while cars 
are allowed to move. 
It transitions to Green when the Car_NS transitions to Red, allowing pedestrians to cross safely. 
This transition occurs through synchronization channels (e.g., pedes_ew_green!).   


 
• Car Traffic Lights for East-West Direction (Car_EW):   

 Initial State: Red 
 The traffic light starts in the Red state to allow the North-South direction to proceed. 
 It transitions to Green after the North-South lights complete their cycle and go to Red. 
 The light then transitions to Yellow before returning to Red, following a similar timing 
 pattern as the North-South direction. 
 
• Pedestrian Lights for East-West Direction (Ped_EW):   

 Initial State: Green 
 The pedestrian signal starts in the Green state when the Car_EW is in Red. 
 It transitions to Red when the Car_EW changes to Green, synchronized via channels (e.g., 
 pedes_red!). 
 
Defining States 
The model clearly defines the states for the traffic lights in both directions:   

• Car Traffic Light States:   

Green: Vehicles are allowed to pass. 
Yellow: A warning state indicating the light is about to change to red. 
Red: Vehicles must stop. 
• Pedestrian Signal States:   

Green: Pedestrians are allowed to cross. 
Red: Pedestrians must wait. 
These states are visually represented in UPPAAL to provide an intuitive understanding of the 
system’s behavior.   

Transition Specification   

The transitions between states are defined based on timing constraints and synchronization events: 
Car Traffic Lights: 
Green to Yellow: 
Condition: The timer t exceeds 30 seconds (t > 30). 
Action: Reset the timer (t = 0).   

 
Yellow to Red:   

Condition: The timer t exceeds 5 seconds (t > 5). 
Action: Trigger the pedestrian signal to turn green (pedes_green!) and reset the timer (t = 0). 
 
Red to Green:   

Condition: The timer t exceeds 30 seconds (t > 30). 
Action: Trigger the pedestrian signal to turn red (pedes_red!) and reset the timer (t = 0). 
 
Pedestrian Signals:   

Red to Green for North to South: Synchronized with the car light turning red (pedes_green!). 
Green to Red for North to South: Synchronized with the car light turning green (pedes_red!).   
Red to Green for East to West: Synchronized with the car light turning red (pedes_green!). 
Green to Red for East to West: Synchronized with the car light turning green (pedes_red!). 
 
Temporal Parameters Assignment 
Timing constraints are assigned to each state to simulate real-world traffic flow dynamics: 
Green State: The car traffic light remains green for a duration of 30 seconds (t ≤ 30). 
Yellow State: The car traffic light remains yellow for a duration of 5 seconds (t ≤ 5). 
Red State: The car traffic light remains red for a duration of 30 seconds (t ≤ 30). 
These time durations are implemented in UPPAAL using clock variables (e.g., t), and conditions are 
placed on transitions to enforce these constraints. 
 
Ensuring Synchronization 
Synchronization is crucial to ensure that the North-South and East-West traffic lights operate 
coherently, preventing conflicting signals and ensuring pedestrian safety. This is achieved using 
synchronization channels in UPPAAL: 
For Pedestrian Signals: 
When the car traffic light transitions to red, the pedestrian signal transitions to green using a 
synchronization channel (pedes_green!). 
Similarly, when the car traffic light transitions to green, the pedestrian signal turns red using another 
synchronization channel (pedes_red!). 
Coordination Between Directions: 
The North-South and East-West traffic lights are synchronized to ensure that while one direction has a 
green light, the other direction remains red. 
