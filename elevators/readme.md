Model two elevator system where the elevators services requests from six floors. The elevators 
maintains a queue of requests and efficiently travel between floors to service these requests. 


a. Elevator Template <br>
States <br>
Idle: The elevator is not in motion and is waiting for a request. <br>
MovingUp: The elevator is in motion, moving to a floor above. <br>
MovingDown: The elevator is in motion, moving to a floor below. <br>
Loading/Unloading: The elevator is stationary, allowing passengers to enter or exit. <br>



Transitions <br>
From Idle to MovingUp or MovingDown based on the request queue. <br>
From MovingUp or MovingDown to Loading/Unloading once the elevator reaches the target floor. <br>
From Loading/Unloading back to Idle once the operation is complete. <br>


 
Variables <br>
int currentFloor: To keep track of the elevator’s current floor. <br>
int targetFloor: The next floor the elevator is heading to. <br>
int requestQueue: A queue to maintain the floor requests. <br>


 
Constraints <br>
Elevator moving up should only accepts up request from floors above its current floor and likewise 
elevator moving down should only accepts down requests only from the floors below its current floor 
level. 
Fairness check to ensure that floor requests are handled alternately by the elevators , for example, if 
first elevator receives the a request from any of the floors, then next request should go to the second 
elevator. 
Elevators should not stay for more than 60 seconds in MovingUp or MovingDown states. 


 
b. Floor Template <br>
Since there are nine floors, model the floors as a template in UPPAAL, parameterized by a floor number. <br>
States <br>
Idle: No request has been made from this floor. <br>
UpRequest: A request to go up has been made. <br>
DownRequest: A request to go down has been made. <br>


 
Transitions <br>
Idle to UpRequest when an upward request is made. <br>
Idle to DownRequest when a downward request is made. <br>
Return to Idle after the request has been serviced. <br>


 
Synchronization Channels: <br>
request_up[floorNumber]! : To send an upward request from a floor. <br>
request_down[floorNumber]! : To send a downward request from a floor. <br>
ack[floorNumber]? : To receive acknowledgement that request has been serviced. <br>

Constraints <br>
Ground floor should not be able to make a down request and likewise the top floor should not be able 
to make a up request. <br>
Once a floor makes a request it should be served within 60 seconds. <br>

Simulation and Verification <br>
Once the model is set up, use UPPAAL simulator to observe the behavior of your elevator system and 
Formulate verification queries in UPPAAL to ensure the following: <br>
There is never a deadlock. <br>
When a floor is in UpRequest/DownRequest state, it eventually returns to Idle state. <br>
When an elevator in MovingUp/MovingDown state, it eventually goes to Loading/Unloading state. <br>
Each elevator eventually services every floor. <br>

Naming Requirements <br>
Elevator template should be named as Elevator. <br>
Floor template should be named as Floor. <br>
Elevator states should be named as Idle, MovingUp, MovingDown, Loading_Unloading. <br>
Floor states should be named as Idle, UpRequest, DownRequest <br>
Variables should be named as curr_floor, dest_floor to represent current and destination floor 
respectively in Elevator template. <br>

 
#### Description <br>
 
The objective of this task is to design and simulate a model of a two-elevator system serving requests 
from six floors using UPPAAL. The elevators must efficiently handle a queue of requests and travel 
between floors to provide timely service. Each elevator operates with four key states: Idle, MovingUp, 
MovingDown, and Loading/Unloading. The elevators transition between these states based on the 
current requests, ensuring they only accept upward requests from floors above and downward requests 
from floors below their current position. Fairness is a crucial aspect of this system, requiring the 
elevators to handle floor requests alternately to balance the load. Additionally, constraints ensure that 
no elevator remains in the MovingUp or MovingDown state for more than 60 seconds. <br>
 
The system also includes a Floor template representing the six floors, each capable of generating upward 
or downward requests based on its position. The ground floor can only make upward requests, while 
the top floor can only make downward requests. Synchronization channels are used to manage 
communication between floors and elevators, ensuring that requests are acknowledged and serviced 
within the specified time frame. The overall objective is to simulate the behavior of the elevators in 
UPPAAL and verify key properties, including the absence of deadlocks, the eventual servicing of all 
requests, and the efficient transition of elevators through their states. By achieving these goals, the 
model demonstrates how state machines can be employed to ensure the reliability, efficiency, and 
fairness of real-world elevator systems. <br>
