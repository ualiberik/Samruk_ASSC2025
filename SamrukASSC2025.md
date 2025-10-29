# Samruk Station

## Team members

## Abstract

## Table of contents

## Location and mission
Our team chose the polar orbit of the Moon as the location of our space settlement.
##### “...But why, some say the moon? Why choose this as our goal?...” 
We are not limited in the scale of the project, but we want it to be as realistic and achievable as possible. 
Moon — is the closest and most thoroughly explored celestial body, but still not settled. In our opinion, we need to overcome this frontier, before we will move beyond.
A station in the orbit of the Moon can be a transhipment point or spaceport in long-distance missions, such as missions to Mars, Venus, Mercury and the outer solar system, where spacecrafts can refuel and have repair. Thus, settlement in the orbit of the Moon would be a very important step toward the colonizing of the solar system.
![Picture1. Stationʼs orbit.](/location-01.jpg)
### Station will be located in 600km polar orbit, because:
- Polar orbit allows near-continuous exposure to sunlight. The moon’s axial tilt is only 5.145° [1], which means the poles are constantly illuminated by the Sun.
- Polar orbit and rotation of the moon around its axis allows to land on any point on the surface.
- 600km altitude is more stable and requires less amount of corrections, but still close enough to the surface.
### Space settlement can be fully autonomous.
- The moon surface consists not very much, but enough water [2] to provide for the needs of the biosphere and infrastructure in the settlement.
- The surface of the moon have a lot of Helium-3 [3] — which can cover the fuel and energetics needs of the station.
- Lunar regolith is very similar to the Earth rock by the chemical compound (and consists of silicon, iron, aluminum, calcium etc.) [4] which can be used as building material for the new modules of the station.
- Space near the Moon has dozens of times less radiation than, for example, near gas giants. About 0.96-1.24 мSv/day at the Moon's orbit [5].

## Structure of the station
The orbital station consists of a central not-rotating cylinder — a central hub, two artificial gravity rings rotating in different directions and engines. The central hub is used for experiments with weightlessness, industry and docking. Living modules rotate by magnetic forces and the whole biosphere lives there. Engines are placed on the end face of the central hub and used for maneuvers and orbital corrections.
### Central hub
The central hub is a cylinder that doesn't rotate and has no artificial gravity. It has docking ports, engines, magnetic elements and flywheels. The central hub is used as adapter between two rings, for docking, for industrial complexes and for experiments with weightlessness. It is connected with living modules (through magnetism, without contact) and gives them a rotation.
### Living modules
Each "ring" has 3 pairs of living modules, that is, in total station has 12 living modules. Living modules are separated to increase safety and fault tolerance (in case of accident in one or several living modules, the others will be safe), but they are also connected with each other through tunnels with gateways. Each living module is connected with rotor through two cylinder tunnels.
### Artificial gravity
In order for the biosphere to be able to inhabit the station for a long time, it is necessary to recreate conditions on Earth as closely as possible, including imitating of the Earthʼs gravity. Artificial gravity will be made by centrifugal force by rotation of the living modules. Acceleration in living modules will be equal about 1 Earthʼs g.
#### Rotation method
The inner rim of rotor has 64 of permanent magnets that alternate poles. The outer rim of central hub has 64 of electromagnets (that create a field when current is passed through them and polarity is depend on direction of the current). Each electromagnet is turned on in the certain moment, which is controlled by speed controller (ESC). The ESC receives angular position data from Hall sensors along the rim. By sequentially energizing electromagnets with a phase shift of 120°, continuous rotation of the ring is achieved, similar to a 3-phase BLDC system. Thus, the rotation of the living modules is made by the same construction as rotation in brushless motors.
#### Torque compensation
To avoid the rotation of the central hub, the torque must be fully compensated, that is, the sum of torque must be equal to zero. To compensate the most of the torque two rings with 6 living modules each will rotate in different directions. 
L = m * r^2 * w, where
L — torque, r - raduis, w - angle speed.
According to this formula, the torque depends not only on speed of rotation, but on mass too. The mass of each ring can be different, but we canʼt change the speed of rotation of the rings (to keep centrifugal force) to compensate the torque. There will be residual uncompensated torque and thatʼs why central hub will have flywheels. Flywheels will be rotated by motor. Their mass and radius are constant, therefore, it is enough to rotate them with certain speed (which will be calculated by PID or more developed controllers) to compensate residual torque.
#### Flywheelsʼ saturation
However, the station will have a lot of microdisturbances: micrometeorites, solar pressure, gravity gradients, orbital corrections, reaction during docking of ships — they all give an extra torque. Thus, overtime, flywheels will accumulate too much, not safe speed — which is called flywheelʼs saturation. To solve this problem, the station will make desaturation — removal of the torque, when flywheels accumulate too dangerous speed. The station will use RCS to shed excess torque and desaturate flywheels. 
mp0 — propellant mass for one desaturation, mp — propellant per day, m — mass of central hub, m-dot — propellant mass flow rate, L — torque, r — radius, w — angular speed, F - force, T — instantaneous torque, t — time, ve — exhaust rate, Isp - specific impulse, n — number of desaturations per year.
- L = 1/2 * m * r^2 * w (assume that the central hub is a solid cylinder)
- T = Fr
- dL = T * t
- F = m-dot * ve
- ve = Isp * g0
- mp0 = m-dot * t
Therefore,
dL = F * r * t
Ft = dL / r
mp0 = (F * t) / ve
mp0 = dL / (r * ve)
mp0 = dL / (r * Isp * g0) = (1/2 * m * r^2 * dw) / (r * Isp * g0) — mass of propellant needed for one desaturation.
mp = ((1/2 * m * r^2 * dw) / (r * Isp * g0)) * 12 / 365 * 1.2 — mass of propellant per day (assume that there are 12 desaturations per year, 1.2 for reserve)
### Magnetic suspensions
To avoid mechanical contact and increase the service life of the station, the rotor will be stabilized by active magnetic bearing (AMB). Supports with electromagnets will be placed on the central hub. Controller takes data about the location of the ring and applies certain current to the matching electromagnets to stabilize it. In case of failure of AMB, spare mechanical bearing will be used.
### Transport system
### Communication and power transmission
Central hub and rotor donʼt contact, thatʼs why, living modules will be powered by inductive wireless transmission, through magnetic coils. 
n = n0 * ​(r0 / r​​)^3, where
n — current efficiency, r — current distance, r0 — minimal distance, n0 — r0 efficiency
Efficiency of this power transmission method is approximately proportional to the cube of the distance between coils, which means that efficiency drops sharply with increasing distance.
To increase efficiency of power transmission, resonant inductive transmission and HTS superconductors will be used. 
n = (k^2 * Q1 * Q2) / (1 + k^2 * Q1 * Q2) — efficiency with resonant inductive transmission, where
n — efficiency, k — connection coefficient (>0, <1), Q1, Q2 — quality coefficient of coils.
k = (R / r)^3, where
R ​— coil radius, r ​— distance between coils.
if R = 5m, Q1 = Q2 = 10^3 (for HTS superconductors), n = 0.99 (for maximum efficiency)
k^2 * Q1 * ​Q2​ = 99
k = sqrt(99 / Q1 * Q2) = sqrt(99 / 10^6) = 0.00994
r = R * (1/k)^1/3 = 5m * (1 / 0.00994)^1/3 = 20m
According to this calculation, distance between rotor and cental hub could be 20m, keeping 99% efficiency. To support work of HTS superconductors, their temperature must be about 80K. A backup laser-based power transmission system provides emergency power if inductive coupling fails.
Each ring consumes about 200MW of energy, therefore,
Ploss = 200MW * 0.01 = 2MW — of extra energy.
To transmit data radio communication will be used.

## Energy production

## Radiation shield

## Thermal control system

## Resource industry
To maintain its existence, the settlement needs to have a constant flow of resources, such as water, building materials, rocket and energy fuel.
The closest place to extract these resources — Surface of the Earth's Moon.
### Extraction
The three types of raw materials that will be extracted from the surface: building materials, water ice and helium-3. All of them are found in lunar regolith. Several resources-extracting complexes will be placed across the surface of the Moon. Each complex will be specialized for a particular resource (water, metals or helium-3).
#### Structure of the resources-extracting stations
- Resource storage (base). Each station has a large building with tanks that store lunar regolith. Lunar regolith will be pressurized in tanks to store it as effectively as it's possible. Each tank has docking ports for delivering rockets.
  ![Picture1. Storage 3D-model](/Storage.jpg)
- Mining rovers. Each station has a large amount of autonomous rovers that mine lunar regolith and deliver it to storage. They use tracks to move and regolith digging devices.
  ![Picture1. Rover 3D-model](/Rover.jpg)
- Delivering rockets. Rockets that are docked to the storage and lift full tanks to the orbital settlement. They have 4 free-rotating rocket engines and RCS to perform maneuvers and for docking.
  ![Picture1. Delivering rocket 3D-model](/Delivering rocket.jpg)
- Power supply. All described earlier structures have solar panels to power themselves. The complexes also will be supplied by solar batteries and energy from the orbital station that will be transfered through laser rays, microwaves and delivering rockets.
#### Resources
- Water. Water ice is concentrated at the south pole of the moon, in eternally darkened craters, such as Shackleton crater in which one of the regolith-extracting stations will be placed. According to LRO data, regolith in Shackleton consists about 5-10% of water by mass.
- Heluim-3. Unlike water, helium-3 is concentrated in illuminated regions, such as the lunar maria (Mare Tranquillitatis, Oceanus Procellarum or Mare Fecunditatis), in which regolith-extracting stations also will be placed. Regolith in these regions consist of about 50ppb of Helium-3.
- Building materials. Metals will be extracted from the rest of the regolith that is mined by water and helium-3 extracting stations.
![Picture1. Complexes location](/Complexes location.jpg)
### Transportation
As stated above, lunar regolith will be transported to the orbital settlement by large amounts of delivering rockets. Rockets are docked to the tank in the base and fly to orbit when the tank is full and orbital settlement's trajectory is above. Delivering rockets have 4 thrust-vectoring engines and RCS to perform maneuvers. After approaching the orbital station, rockets attach the tank to the station and refuel to return empty tanks back and lift other tanks.
![Picture1. Delivering rocket 3D-model](/Delivering rocket.jpg)
### Processing
On the orbital settlement regolith will be heated and melted in vacuum furnaces to separate volatile components of it. 
- Water. Most of the water will be used by the biosphere of the settlement and thermoregulation systems. Another part will be electrolyzed to gain hydrogen and oxygen that can be used as fuel pair for rocket engines and for production of  “heavy water” that is used in thermonuclear energetics.
- Building materials. Metals are then refined from the rest of metals-consisting regolith by electromagnetic separation and used in building of new modules, repairing, manufacturing etc.
- Heluim-3. Helium-3 will be extracted from regolith and used in thermonuclear energetics in pair with heavy hydrogen.

## Food

## Atmosphere and climate

## Medicine

## Waste management

## Demography aspects

## Political aspects

## Social aspects

## Economical aspects

## Bibliography
### Location and mission of the settlement
1. https://books.google.kz/books?id=S4xDhVCxAQIC&pg=PA184&redir_esc=y#v=onepage&q&f=false
2. https://cfpl.ae.utexas.edu/wp-content/uploads/2010/10/science_article.pdf
3. https://www.sciencedirect.com/science/article/abs/pii/S0019103507001285
4. https://www.lpi.usra.edu/lunar/missions/apollo/apollo_11/samples
5. https://www.nature.com/articles/s41586-024-07927-7
