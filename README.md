# Notes on autonomous driving

## Building blocks
- [Radar and Lidar](radar_lidar.md)
- [Localization](localization.md)
- [Sensor fusion](sensor_fusion.md)

## Levels of autonomous driving
- Nice way to visualize L1-L5 from NXP. ADAS for L1-L2, and autonomous driving for L3-L5.
![](assets/levels.png)

- Comparison of different sensors. OEM and tier-1 are asking for more resolution from radars for L3, L4 autonomous driving.
![](assets/comparison_sensors.png)

- [Automotive supply chain explained](https://medium.com/self-driving-cars/the-automotive-supply-chain-explained-d4e74250106f). Manufactures are OEMs. Direct part suppliers are tier-1.


## sensor setup
- Voyage
![Voyage](https://cdn-images-1.medium.com/max/2400/1*VZMUdPFniGA3X7urHi6f4w.png)
- Tesla
![Tesla](https://electrek.co/wp-content/uploads/sites/3/2016/10/tesla-second-gen-autopilot-sensors-suite.png)

## New ideas
- Reconstruct high resolution radar image from lidar
- Reconstruct higher resolution model of the world with radar (or low cost one-line lidar) and high resolution RGB image
