# Term 03 _ Projet 01
Self-Driving Car Engineer Nanodegree Program
   
### Simulator.

I downloaded the Term3 Simulator which contains the Path Planning Project from Github repository.
The simulator is installed on a Linux (Ubuntu 18.04) machine, and run after conveting the file to be an application program.

### Goals

In this project the goal wss to safely navigate around a virtual highway with other traffic that is driving +-10 MPH of the 50 MPH speed limit. The car's localization and sensor fusion data is provided, and there is also a sparse map list of waypoints around the highway. The car is supposed to try to go as close as possible to the 50 MPH speed limit, which means passing slower traffic when possible. The simulator allows other cars to change lanes too. The car should be programmed to avoid hitting other cars at all cost as well as driving inside of the marked road lanes at all times, unless going from one lane to another. The car is supposed to make one complete loop around the 6946m highway. Since the car is trying to go 50 MPH, it should take a little over 5 minutes to complete 1 loop. Also the car should not experience total acceleration over 10 m/s^2 and jerk that is greater than 10 m/s^3.

#### The map of the highway is in data/highway_map.txt

Each waypoint in the list contains  [x,y,s,dx,dy] values. x and y are the waypoint's map coordinate position, the s value is the distance along the road to get to that waypoint in meters, the dx and dy values define the unit normal vector pointing outward of the highway loop. The highway's waypoints loop around so the frenet s value, distance along the road, goes from 0 to 6945.554.

### Basic Build Instructions

The Repo was cloned and the project was built using the Cmake and make file provided 

The following data is sent from the Simulator to the C++ Program

#### Main car's localization Data (No Noise)

["x"] The car's x position in map coordinates
["y"] The car's y position in map coordinates
["s"] The car's s position in frenet coordinates
["d"] The car's d position in frenet coordinates
["yaw"] The car's yaw angle in the map
["speed"] The car's speed in MPH

#### Previous path data given to the Planner

//Note: Return the previous list but with processed points removed, can be a nice tool to show how far along
the path has processed since last time. 

["previous_path_x"] The previous list of x points previously given to the simulator
["previous_path_y"] The previous list of y points previously given to the simulator

#### Previous path's end s and d values 

["end_path_s"] The previous list's last point's frenet s value
["end_path_d"] The previous list's last point's frenet d value

#### Sensor Fusion Data, a list of all other car's attributes on the same side of the road. (No Noise)

["sensor_fusion"] A 2d vector of cars and then that car's [car's unique ID, car's x position in map coordinates, car's y position in map coordinates, car's x velocity in m/s, car's y velocity in m/s, car's s position in frenet coordinates, car's d position in frenet coordinates. 

## Reflection with respect to the Rubric Points

### Compilation

1. The code compiles correctly using the provided make file.

### Valid Trajectories

1. The car is able to drive the complete loop without any incident.
2. The car doesn't drive faster than the speed limit at any point of time. Also the car isn't driving much slower than speed limit unless obstructed by traffic.
3. The car does not exceed a total acceleration of 10 m/s^2 and a jerk of 10 m/s^3. However, while running in my local machine, it sometime showed "maximum acceleration exceeded" message may be due to slow processing.
4. The car never came into contact with any of the other cars on the road.
5. The car never spent more than 3 seconds out side the lane lanes during changing lanes, and every other time the car stays inside one of the 3 lanes on the right hand side of the road.
6. The car is able to smoothly change lanes when it makes sense to do so, such as when behind a slower moving car and an adjacent lane is clear of other traffic.

### Reflections

I started with the code provided in the repository. Initially I tried to write the whole thing on my own. It didn't work. Then, I followed the "Project Q&A" video. It was a real helping piece. I completely followed the method of spline interpolation as discussed in the video.

This was the most difficult portion of the code. Once the car was able to change lane on obstruction, the only job remained was to check for appriopriate conditions for lane change as that in a finite state machine.

The conditions are judged based on the fusion data of other cars. It is checked whether a safe distance is available between the cars that are ahead or at back of our car in our lane or in the lanes to our left or to our right. The safe distance has been take as a function of the speed of the car. Because, as the speed is reduced, the safe distance between the cars also is reduced. This increases the efficiency of lane change requirements.

Once the lane change dicission is made, the speed is checked for its maximization. Here the acceleration limit is used to increase or decrease the speed of the car appropriately. This was beautifully explained in the "Project Q&A" video.

The most beautiful part of the code is the use of the spline interpolation using two of the end points from the previous path. That provided a very smooth transition from one lane to the other.
