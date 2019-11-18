# SGBA_code_SR_2019

This section presents all the repositories used for the simulation and the real-world experiments done in the following publication:
> K.N. McGuire, C. De Wagter, K. Tuyls, H.J. Kappen, G.C.H.E. de Croon,
> 'Minimal navigation solution for a swarm of tiny flying robots to explore an unknown environment'
> Science Robotics, 23 October 2019 
> DOI: http://robotics.sciencemag.org/lookup/doi/10.1126/scirobotics.aaw9710

**The algorithm developed for the paper above is currently being cleaned up and ported to the latest firmware of the Crazyflie 2.1. Please go to for updates to https://github.com/knmcguire/SGBA_CF2_App_layer**


## Simulation

This section explains the git-repositories for the simulation experiments. 
Elements have been reused of the simulation used in:
> K.N. McGuire, G.C.H.E. de Croon, K. Tuyls, 
> 'A comparative study of bug algorithms for robot navigation',
> Robotics and Autonomous Systems, Volume 121, 2019, 103261
> DOI: https://doi.org/10.1016/j.robot.2019.103261

Repositories (also shown as submodules in this repository)
- ARGoS_bridge (ROS kinetic): https://github.com/tudelft/ARGoS_bridge (branch: gradient_bug_testing)
	- The node to port ROS twist-commands to the foot-bot and returns the laser-range finder measurements.
- Indoor_environment_generator (ROS kinetic): https://github.com/tudelft/indoor_environment_generator (branch: master)
	-The ROS package contains the procedural random indoor environment generator and provides the simulated RSSI measurements for the ARGoS’s foot-bot.
- ARGoS: https://github.com/tudelft/ARGoS3 (branch: ARGoS3_mod_tudelft)
	- Contains the modified foot-bot model.
- Bug_Algorithms (ROS kinetic): https://github.com/tudelft/bug_algorithms (branch: master)
	- Contains the finite state machine for the standard bug algorithms.
-Gradient_bug (ROS kinetic): https://github.com/tudelft/gradient_bug (branch: master)
 	-Contains the state machine for the swarm gradient bug algorithm.
### Launch
How to start the tests with ROS kinetic: 
- In a terminal, type “roslaunch bug_algorithms launch_bug_algorithm.launch”
- In another terminal, type “python multiple_environments_test.py” to supervise the tests.


## Real-World Testing
This section shows all the github-repositories used for the real-world experiments, for which a *Crazyflie 2.0, Multiranger and Flowdeck* was used as explained in the paper. These repositories represent the firmware of the microprocessors on this small quadcopter:
- Crazyflie_firmware: https://github.com/tudelft/crazyflie-firmware-private  (branch: systemtest_gradientbug)
	- This repository contains all the necessary changes to the Crazyflie firmware in order to make the SGBA work onboard
- Crazyflie2-nrf-firmware: https://github.com/tudelft/crazyflie2-nrf-firmware   (branch: systemtest_gradientbug)
	- This repository contains the firmware of the NRF51 chip on the Crazyflie 2.0, in order to enable inter-drone communication.

### Launch
How to start up the experiment:
- Give the Crazyflie a unique ID: E7E7E701, E7E7E702, etc.
- First flash the NRF and STM chips of all the Crazyflie with the following bashscript: ‘gradient_bug/bashscripts/flash_all_crazyflies.sh’
- Start the real-world testing with the following bashscript: ‘gradient_bug/bashscripts/start_swarm_exploration_experiment.sh’
- If something goes wrong, close the last bashscript and run ‘land_all.sh’
