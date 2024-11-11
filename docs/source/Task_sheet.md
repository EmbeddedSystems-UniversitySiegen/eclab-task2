# Tasks

## Task 1

Model car and pedestrian traffic lights at a city crossroad, where one road runs along the North-South direction and other along the East-West. Each road has a pedestrian crossing.

**Car Traffic Lights:** Model two traffic lights for cars-- one for each direction. Each traffic light should have the standard three states: Red, Yellow, and Green. Ensure synchronization such that at any point, both car traffic lights aren't green simultaneously to avoid accidents.

**Pedestrian Traffic Lights:** Model two pedestrian lights, one for each crossing. Lights should have two states: Green and Red.
Synchronize it with car traffic lights to ensure pedestrian safety. For instance, when cars have a green light, the corresponding pedestrian light should be red .

The key challenge is to synchronize the four lights to ensure smooth traffic flow and maximum safety. Make sure to properly configure the intial states of four traffic lights.

**Simulation and Verification**: Once the model is set up, use UPPAAL simulator to observe the behavior of your traffic light system.

Formulate verification queries in UPPAAL to ensure the following:

- There is never a deadlock
- Car traffic lights are **never** green at the same time.
- When car lights are green, corresponding pedestrian lights should indicate red.
- When pedestrian lights are green, corresponding car lights should indicate red.
- Both pedestrian and car lights should eventually turn green
- All lights should never be red at the same time.

## Task 2

Model two elevator system where the elevators services requests from six floors. The elevators maintains a queue of requests and efficiently travel between floors to service these requests.

### a. Elevator Template

**States**

- **Idle**: The elevator is not in motion and is waiting for a request.
- **MovingUp**: The elevator is in motion, moving to a floor above.
- **MovingDown**: The elevator is in motion, moving to a floor below.
- **Loading/Unloading**: The elevator is stationary, allowing passengers to enter or exit.

**Transitions**

- From **Idle** to **MovingUp** or **MovingDown** based on the request queue.
- From **MovingUp** or **MovingDown** to **Loading/Unloading** once the elevator reaches the target floor.
- From **Loading/Unloading** back to **Idle** once the operation is complete.

**Variables**

- **int currentFloor**: To keep track of the elevator's current floor.
- **int targetFloor**: The next floor the elevator is heading to.
- **int requestQueue**: A queue to maintain the floor requests.

**Constraints**

- Elevator moving up should only accepts up request from floors above its current floor and likewise elevator moving down should only accepts down requests only from the floors below its current floor level.
- Fairness check to ensure that floor requests are handled alternately by the elevators , for example, if first elevator receives the a request from any of the floors, then next request should go to the second elevator.
- Elevators should not stay for more than 60 seconds in MovingUp or MovingDown states.

### b. Floor Template

Since there are nine floors, model the floors as a template in UPPAAL, parameterized by a floor number.

**States**

- **Idle**: No request has been made from this floor.
- **UpRequest**: A request to go up has been made.
- **DownRequest**: A request to go down has been made.

**Transitions**

- **Idle** to **UpRequest** when an upward request is made.
- **Idle** to **DownRequest** when a downward request is made.
- Return to **Idle** after the request has been serviced.

**Synchronization Channels:**

- **request_up[floorNumber]!** : To send an upward request from a floor.
- **request_down[floorNumber]!** : To send a downward request from a floor.
- **ack[floorNumber]?** : To receive acknowledgement that request has been serviced

**Constraints**

- Ground floor should not be able to make a down request and likewise the top floor should not be able to make a up request.
- Once a floor makes a request it should be served within 60 seconds.

### Simulation and Verification

Once the model is set up, use UPPAAL simulator to observe the behavior of your elevator system and Formulate verification queries in UPPAAL to ensure the following:

- There is never a deadlock.
- When a floor is in UpRequest/DownRequest state, it eventually returns to Idle state.
- When an elevator in MovingUp/MovingDown state, it eventually goes to Loading/Unloading state.
- Each elevator eventually services every floor.

## Deliverables

1. UPPAAL files for each task.
2. Report describing your approach, understanding of state machines modelling, simulation results from UPPAL, the verification queries, and outcomes.

## Evaluation Criteria

- Model Complexity and Accuracy
- Simulation Behavior
- Verification Outcomes: All your verification queries should return "Satisfied."
- Quality of report.
