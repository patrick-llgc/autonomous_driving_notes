# Sensor fusion
Notes on sensor fusion


## Sensor fusion
### Why do we need sensor fusion?
- Each sensor provides different types of information about the tracked object position with differing accuracies especially in different weather conditions. 
- Algorithms used in sensor fusion have to deal with temporal, noisy input and generate a probabilistically sound estimate of kinematic state
- Sensors are lacking
	- Camera: HD, but detection not reliable enough
	- Lidar: 3D but too expensive and short on specs
	- Radar: Reliable but low resolution
- In object level fusion, each sensor has a cognition engine, and fusion is performed on objects, processed sensor results. So it may be more robust to generate rich combined high resolution model and perform perception on top of it. ([source from vayavision](https://www.youtube.com/watch?v=sNaENlLZYSo))
- Merge raw sensor data: calibration, parallax, timing synchronization. (synchronized RGBD data) But the resolution is different (HD camera, lower resolution lidar)
- But we do not need high resolution everywhere! Point and shoot lidar. This need collaboration of cognition and sensors. Use camera data to upsample lidar data for better prediction.
- Upsample lidar to get distance of every pixel. **We can do similar stuff with radar data to ([this](https://youtu.be/sNaENlLZYSo?t=1122)) as well!** 

### Kalman filter, Extended Kalman filter
- [Review on Medium](https://medium.com/@wilburdes/sensor-fusion-algorithms-for-autonomous-driving-part-1-the-kalman-filter-and-extended-kalman-a4eab8a833dd)
- **Kalman filter** is one of the most powerful technique to smooth noisy input data and estimate state. The Kalman filter takes in a stream of information and uses the state prediction and measurement to update its belief about the state of the tracked object. 
- Predicted state (with uncertainty) + Measurement (with noise) --> updated state and uncertainty.
- Lidar data usually contains position information (x, y), but radar data usually contains (range rho, bearing theta and range rate rho').
- **Extended Kalman filter **is used to process radar data or other data that does not fit into cartesian coordinate. The mapping of different coordinate system is nonlinear and thus violate the linear system state of Kalman filter (that measurement and process models are Gaussian, as non-linear transform of Gaussian is not Gaussian). The extended Kalman filter approximates the nonlinear model by a first order Taylor expansion.

### Unscented Kalman Filters and Particle filters
- TODO


