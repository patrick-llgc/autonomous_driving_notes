# Radar and Lidar
Notes on radar and lidar sensors and data

## Lidar Working principles
- Different methods to measure distance with light ([youtube](https://www.youtube.com/watch?v=ddxguAzzzJE))
- A lidar has its own source of light, so it works at night.
- Lidar requires less power and generates less heat than 2D camera system.
- 360 degree views (from spinning a linear laser source), no blind spot.
- Lidar vs high resolution radar ([youtube video](https://youtu.be/NZKvf1cXe8s?t=181)). NXP also has a nice [comparison](https://semiengineering.com/wp-content/uploads/2017/10/fig4-2.png) according to [a 2017 report](https://semiengineering.com/here-comes-high-res-car-radar/).
- The current state-of-the-art Lidar from Velodyne is the Alpha Puck, with 300 m visible distance.
- Spinning radars have advantages over solid state lidars
	- 360 degree view. Solid state lidars have at most 120 degree view, and thus at least four are needed to cover the 360 degrees.
	- [Review](https://arstechnica.com/cars/2018/05/why-bulky-spinning-lidar-sensors-might-be-around-for-another-decade/) predicting that spinning lidars will be around for another decade.
- Velodyne laser specs
	- Wavelength: Velodyne lasers uses [905 nm](https://velodynelidar.com/newsroom/guide-to-lidar-wavelengths/), which falls in near infrared (NIR) range. (They also have 1550 nm version, which has more water absorption, operating at higher power and less safe to human eyes.)
	- Power: 2 mW. 
	- Safety: Belongs to Class I (safest) category according to IEC categorization.
	- Rotating speed: Velodyne lidars rotates at 10 Hz.



## Radar Working principles
-  A critical component of most self-driving cars
is a set of long-range (150m-250m) radar sensors that, along
with LIDAR and/or cameras, map the environment including
cars, obstacles, and pedestrians [5]. Automotive long-range
radars commonly in use today are based on Frequency Modulated Continuous Wave (FMCW) [2], [16], and operate in the
76-77 GHz band [3] with a total bandwidth of 1 GHz. (from [radarMAC paper](http://sci-hub.tw/10.1109/SAHCN.2016.7733011)) This corresponds to a wavelength of 4 mm.
- Radars are moving from 24 GHz to 77 GHz in automotive radars. The range resolution of a 77GHz system can be 4cm versus 75cm for 24GHz radar, allowing better detection of multiple objects that are close together. (...) as sensors move from 24GHz to 77GHz, velocity measurements can improve by 3x. (...) the total area needed for a 77GHz antenna is one-ninth the size of a similar 24GHz antenna.(from [Texas Instruments](https://e2e.ti.com/blogs_/b/behind_the_wheel/archive/2017/10/25/why-are-automotive-radar-systems-moving-from-24ghz-to-77ghz))
	- Historically short-range radars (SRR) used 24 GHz, and long range radars (LRR) are using 77 GHz.
- Excellent video from NXP on the [The latest developments in radar technology for automotive](https://youtu.be/MiVCee1UfJs?t=262).


## Interference of sensors
### Q: Will multiple lidars interfere?
tl;dr: Yes but very unlikely and easy to filter out.
> A1: From direct industry information. Yes, there is multi path errors, but they're so random (and limited) that they typically get filtered out. [reddit](https://www.reddit.com/r/robotics/comments/7gyswt/will_selfdriving_vehicle_lidar_interfere_with/) 

> A2: It took me a bit to understand that the laser spot that a lidar projects is tiny and moving really fast so the chances of your laser spot hitting another lidar's laser spot are tiny even with multiple lidar's nearby. This is in contrast to an ultrasound sensor for example, which generates a wide sound wave that any other sensor nearby will detect.

> A3: Laser range finding is done by firing a laser pulse, at a slight angle, and watching where the dot shows up linearly, and the timing at which it shows up, and possibly even the size of the dot.

> This allows you to use trigonometry to determine the distance to the point you aimed at. The lidar does this, but hundreds of time a second while spinning around in a circle changing its targeting angle constantly.

> At any given moment, Each lidar is only ever looking for a reflection from the spot it fired itself at, and is blind to everywhere else in it's range. So, it's unlikely that even with hundreds of lidars in a traffic jam that you'd have more than a few in range of each other, and even less likely that they'd be measuring the same ~1mm diameter spot. and even if they did interfere on a point, it'd likely be tossed out by a filtering algorithm, or even pulse modulation that allows the lidar to identify which pulses are it's own.

> So yes, it's a problem, but it's largely a solved one. Source: I did research previously on how to build a rangefinder from scratch.

### Q: Will multiple radars interfere?
tl;dr: Yes it is worse than lidar interference, and needs to be addressed.
> A1: Google and Raytheon has a [paper](http://sci-hub.tw/10.1109/SAHCN.2016.7733011) ([slides](https://slideplayer.com/slide/10904536/)) to talk about this. Uncoordinated assignment results in radar blindness when as few as 4 cars are within the transmission range.

> A2: Definitely there would be interference between the radar frequencies when most of the vehicles equipped with radar are close by. There are researchers happening around the world to tackle this problem termed as ‘interference mitigation'. Also there are papers published describing various methods to solve the interference problem. (from [Quora](https://www.quora.com/If-self-driving-cars-continue-to-use-radar-for-rangefinding-wont-they-have-problems-when-there-are-hundreds-of-them-on-the-same-stretch-of-road-all-using-the-same-frequencies))

> A3: the better solution is probably to use Spread spectrum - Wikipedia technology. This is how modern military radars work. It has huge advantages in that it produces no signal collisions, almost no interference with other users of the spectrum (including other cars), very secure and effectively impossible to spoof, and is very difficult to block. (from [Quora](https://www.quora.com/If-self-driving-cars-continue-to-use-radar-for-rangefinding-wont-they-have-problems-when-there-are-hundreds-of-them-on-the-same-stretch-of-road-all-using-the-same-frequencies))



## Radar providers
- [SmartMicro](https://youtu.be/MiVCee1UfJs?t=262): German company with footprint in China. 
- A number of companies include Arbe, Autoliv, Echodyne, Metawave, RADSee, Steradian and others are working on high resolution radars. In addition, NXP is pursuing it. Imec, an R&D organization, also is working on it.
- [INRAS/Radarlog](http://www.inras.at/en/products/new-radarlog.html) is an Austrian radar manufacturer who provides raw data
- MIMO has virtual channels. 3Tx/4Rx goes to 12Tx/16Rx.