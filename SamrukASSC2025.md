# Samruk Station

## Team members
- Uali Berik – Mission of the station, Location of the station, General structure, Resource extraction, 3D modeling, Visual design.
- Nurzhan Kunakbayev – Demographic aspects, Political aspects, Financial aspects, Economical aspects, Infrastructure.
- Amina Toxankyzy – Demographic aspects, Social aspects, Infrastructure, Design.
- Arlan Tairov – Thermal regulation of the station, Food supply of the station, Medicine and healthcare, Atmosphere and climate.
- Arman Temirbulatov – Radiation protection, Energy systems of the station, Transportation system, Waste management.

## Abstract
SamrukStation is the space settlement in the Earthʼs Moon polar orbit.
Mission of the SamrukStation is being experimental platform of building large fully autonomous orbital settlements, being transhipment point for spacecrafts that have long-distance missions and being industrial complex.
It will have population of 120000 people after 80 years of operation, having 25200 people at the start. The settlement can be fully autonomous and doesnʼt need constant support from the Earth. Living conditions of the settlement are close to the Earthʼs conditions, having imitation of Earthʼs gravity, biodiversity and social/cultural life.
In our project, we try to maintain balance between realism and innovations.

## Table of contents

## Location and mission
Our team chose the polar orbit of the Moon as the location of our space settlement.
##### “...But why, some say the moon? Why choose this as our goal?...” 
We are not limited in the scale of the project, but we want it to be as realistic and achievable as possible. 
Moon — is the closest and most thoroughly explored celestial body, but still not settled. In our opinion, we need to overcome this frontier, before we will move beyond.
A station in the orbit of the Moon can be a transhipment point or spaceport in long-distance missions, such as missions to Mars, Venus, Mercury and the outer solar system, where spacecrafts can refuel and have repair. Thus, settlement in the orbit of the Moon would be a very important step toward the colonizing of the solar system.
![Picture1. Stationʼs orbit.](/location-01.jpg)
### Station will be located in circular (eccentricity about 0) 600km polar orbit, because:
- Polar orbit allows near-continuous exposure to sunlight. The moon’s axial tilt is only 5.145° [1], which means the poles are constantly illuminated by the Sun.
- Polar orbit and rotation of the moon around its axis allows to land on any point on the surface.
- 600km altitude is more stable and requires less amount of corrections, but still close enough to the surface.
### Space settlement can be fully autonomous.
- The moon surface consists not very much, but enough water [2] to provide for the needs of the biosphere and infrastructure in the settlement.
- The surface of the moon have a lot of Helium-3 [3] — which can cover the fuel and energetics needs of the station.
- Lunar regolith is very similar to the Earth rock by the chemical compound (and consists of silicon, iron, aluminum, calcium etc.) [4] which can be used as building material for the new modules of the station.
- Space near the Moon has dozens of times less radiation than, for example, near gas giants. About 1.37 мSv/day at the Moon's orbit [5].

## Structure of the station
The orbital station consists of a central not-rotating cylinder — a central hub, two artificial gravity rings rotating in different directions and engines. The central hub is used for experiments with weightlessness, industry and docking. Living modules rotate by magnetic forces and the whole biosphere lives there. Engines are placed on the end face of the central hub and used for maneuvers and orbital corrections.
### Central hub
The central hub is a cylinder with 40m diameter that doesn't rotate and has no artificial gravity. It has docking ports, engines, magnetic elements and flywheels. The central hub is used as adapter between two rings, for docking, for industrial complexes and for experiments with weightlessness. It is connected with living modules (through magnetism, without contact) and gives them a rotation.
### Living modules
Each "ring" has 3 pairs of living modules, that is, in total station has 12 living modules. Living modules are separated to increase safety and fault tolerance (in case of accident in one or several living modules, the others will be safe), but they are also connected with each other through tunnels with gateways. Each living module is connected with rotor through two cylinder tunnels.
Each living module is segment of ring and has height of 60m and width of 120m. 
Living modules have angle of 12° between them.
Whole living area consists of two parts:
- Humans living area — 7 800 000m^2 (including personal and public areas, calculated in next chapters).
- Another biosphere (plants and farms) living area — 980 407m^2 (calculated in next chapters).
Therefore, total living area — 8 780 407m^2, 8 780 407m^2 / 2 = 731 700m^2 — for each module.
2714.688mR - 74653.92m^2 = 731700m^2
R = (731700m^2 + 74653.92m) / 2714.688m = 297m.
r = R - 60m = 237m.
### Artificial gravity
In order for the biosphere to be able to inhabit the station for a long time, it is necessary to recreate conditions on Earth as closely as possible, including imitating of the Earthʼs gravity. Artificial gravity will be made by centrifugal force by rotation of the living modules. Acceleration in living modules will be equal about 1 Earthʼs g.
a = w^2 * Rav = g
w = sqrt(g / Rav)
w = sqrt(9.81m/s^2 / 267m) = 0.1917rad/s = 10.96°/s (267 is average radius)
T = 360° / 10.96°/s = 32.84s
RPM = 60s / 34.29s = 1.83 — rotation frequency to maintain g
#### Rotation method
The inner rim of rotor has 64 of permanent magnets that alternate poles. The outer rim of central hub has 64 of electromagnets (that create a field when current is passed through them and polarity is depend on direction of the current). Each electromagnet is turned on in the certain moment, which is controlled by speed controller (ESC). The ESC receives angular position data from Hall sensors along the rim. By sequentially energizing electromagnets with a phase shift of 120°, continuous rotation of the ring is achieved, similar to a 3-phase BLDC system. Thus, the rotation of the living modules is made by the same construction as rotation in brushless motors.
#### Torque compensation
To avoid the rotation of the central hub, the torque must be fully compensated, that is, the sum of torque must be equal to zero. To compensate the most of the torque two rings with 6 living modules each will rotate in different directions. 
L = m * r^2 * w, where
L — torque, r - raduis, w - angle speed.
According to this formula, the torque depends not only on speed of rotation, but on mass too. The mass of each ring can be different, but we canʼt change the speed of rotation of the rings (to keep centrifugal force) to compensate the torque. There will be residual uncompensated torque and thatʼs why central hub will have flywheels. Flywheels will be rotated by motor. Their mass and radius are constant, therefore, it is enough to rotate them with certain speed (which will be calculated by PID or more developed controllers) to compensate residual torque.
#### Flywheelsʼ saturation
However, the station will have a lot of microdisturbances: micrometeorites, solar pressure, gravity gradients, orbital corrections, reaction during docking of ships — they all give an extra torque. Thus, overtime, flywheels will accumulate too much, not safe speed — which is called flywheelʼs saturation. To solve this problem, the station will make desaturation — removal of the torque, when flywheels accumulate too dangerous speed. The station will use RCS to shed excess torque and desaturate flywheels. 
mp0 — propellant mass for one desaturation, mp — propellant per day, m — mass of central hub, m-dot — propellant mass flow rate, L — torque, r — radius, w — angular speed, F — force, T — instantaneous torque, t — time, ve — exhaust rate, Isp - specific impulse.
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
mp = 
### Magnetic suspensions
To avoid mechanical contact and increase the service life of the station, the rotor will be stabilized by active magnetic bearing (AMB). Supports with electromagnets will be placed on the central hub. Controller takes data about the location of the ring and applies certain current to the matching electromagnets to stabilize it. In case of failure of AMB, spare mechanical bearing will be used.
### Transport system
Central hub doesnʼt rotate, while living modules and rotor do. Thatʼs why station needs special system to transfer humans and cargo between them — transport rings.
Transport rings work like "elevator". Transport rings rotate the same way as the rotors and living modules.
At first, transport ring synchronizes with rotation of point A.
Then, it docks to point A through tunnel, humans and cargo move to the ring.
Then, it undocks and changes its rotation speed to synchronize with rotation of point B.
Then, it docks to point B in the same way.
Finally, it undocks and synchronizes with rotation of point A and process repeats.
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

## Zoning

## Energy production
To calculate the station's approximate energy consumption, we'll assume 2.5 kW per person [1].
Powering the entire station will require the use of several energy sources.
### Solar energy
Since the Moon is close to the Sun, solar energy is suitable for solar panels on the station. Also, since the station is in polar orbit, the time in the shadows is limited, improving efficiency. At lunar orbit, the solar flux is approximately 1360W per square meter (approximately the same as on Earth).
To increase solar cell efficiency, we propose using IMMs, which provide 33% [2] of the total energy. The settlement will also use solar concentrators, including movable mirrors, to focus and magnify sunlight, guaranteeing sufficient power output for long-term viability. To avoid reducing cell efficiency as they heat up, we propose using photonic crystal coatings, which transmit light but not infrared radiation.
If the station has a total of 120,000 people, then 2.5 kW * 120,000 = 300 MW. Let's add another 30% for other processes and, as a reserve, let's assign this task to thermonuclear fusion.
The solar panel area can be calculated using the formula:
A = P/(E × η × k)
where:
A — the required panel area, P — the required electrical power, E — the solar constant, η — the solar panel efficiency, k — the system loss coefficient (taking into account inverters, temperature, pollution, etc.).
Substituting the values: η = 0.33, k = 0.95 (approximate value taking into account the station's technology and the insignificant shadow in polar orbit), the effective power per square meter is then:
P_(1"m"^2) = 1361 × 0.33 × 0.95 ≈ 427" W/m²".
Therefore, the formula for the area becomes:
A = P/427.
If the station requires 300 MW, the panel area will be:
A = (300000000)/427 ≈ 702576m².
Thus, with an efficiency of 33% and system losses of 5%, approximately 702576m² will be required to generate 300 MW.
### Thermonuclear fusion
Thermonuclear fusion — a technology not yet in use today, but one that will be highly effective in the future and is being actively studied. Thermonuclear fusion is very promising due to its incredible power (one reactor produces the equivalent of thousands of solar panels), its non-polluting properties, and its ability to operate continuously for decades. In our case, D-He3 can be used for thermonuclear fusion. Both of these components can be extracted from the Moon, but since this technology is not yet fully developed, we will not consider it as a basis for this study.
Its efficiency is 40% [3], which means the reactions should release not 90, but 225 MW:
Reaction energy E_D3≈18.3" MeV"=2.93×10^(-12) " J".
Required number of reactions:
R_D3=(225×10^6)/(2.93×10^(-12) )≈7.68×10^19 " reactions/s".
Mass per reaction: D+³He ≈5.03 u ≈ 8.35×10^(-27)kg →
m ̇≈7.68×10^19×8.35×10^(-27)≈6.41×10^(-7) kg/s.
→ ~0.055 kg/day ≈ 20 kg/year (sum of D+³He).
For a mixture of deuterium and helium-3 (reaction D + He-3 → He-4 + p) with a total fuel of 20.2 kg and a molar ratio of 2:1 (deuterium: helium-3), the calculation is as follows: total mass m=2.014×2x+3.016×x=7.044x, where 2.014 g/mol is the molar mass of the deuterium isotope (²H, one proton and one neutron), and 3.016 g/mol is the molar mass of the helium-3 isotope (³He, two protons and one neutron). From the equation x=20200/7.044≈2869mol. 
Then the mass of deuterium = 2 x 2.014 x 2869 ≈ 11.55 kg, 
the mass of helium-3 = 3.016 x 2869 ≈ 8.66 kg per year
### Energy storage
To store energy and distribute it during necessary and emergency situations, lithium-ion battery modules will be used. Let's say we want a 7-day energy reserve, then we need to calculate how much energy this is.
E = P * N * t * 130% where E is energy, P is Power for 1 human, N is the number of humans, t is time (7 days)
2.5 * 1000 * N * 24 * 3600 * 1.3 * 7 = 181 440 000 000 000 Joules
Various mirrors and other components will also redirect light into special "ovens," where the temperature will be approximately 1500 degrees Celsius. To store all this energy, the batteries have a capacity, which is subtracted by the product of voltage and capacity in ampere-hours. In other words, if the station has 10,000 A*h batteries with a voltage of 400 volts, their number will be equal to the energy divided by the capacity of one battery module.
181,440,000,000,000 Joules = 50,400 MWh; 50,400 MWh: (10,000 * 400) = 12,600 such modules, which will be distributed evenly across all units.
FES (flywheel energy storage system) and SMES (superconducting energy storage system) systems will also be used as backup options.
Food processing will also produce methane, which can be burned to generate energy or stored as fuel for the engines. Combustion energy is calculated by multiplying the efficiency by the specific heat of combustion of the fuel and by the mass of the fuel. However, this energy will be considered reserve and additional in certain cases, as it accounts for less than 1 percent of the total. (For more details on the operating principle, see the waste section)

## Shielding
### Radiation
Since the Moon has neither a magnetic field nor an atmosphere similar to Earth's, nearly 100% of cosmic rays reach its surface. Therefore, the station itself requires reliable protection from radiation, which is extremely harmful to humans.
According to studies, radiation levels in lunar orbit reach approximately 1.37 mSv [1] per day, equivalent to 500 mSv per year. For humans, this exceeds the natural background radiation on Earth, which is approximately 3 mSv per year. [2] For long-term habitation and life extension, the dose should be reduced to 20 mSv per year, and for pregnant women, to 6.6 mSv per year. In other words, the crew should receive only about 4% of external radiation. [3]
### Mechanical Damage
Since small space objects, such as micrometeorites, could collide with the station, structural protection is necessary. Space is filled with debris, and avoiding every collision is impossible, so even minor collisions will occur.
### Temperatures
To prevent the station from overheating due to solar radiation and internal heat generation, thermal protection and heat dissipation systems (such as radiators and ammonia-based heat pipes) are required. About half of solar energy is infrared, about 40% is visible light, and the rest is ultraviolet radiation. Additionally, the station is exposed to charged particles from the solar wind.
Without reflective coatings (such as aluminized Kapton, white paint, or photonic crystals), the station's hull would quickly heat up—like a sheet of metal exposed to the sun.
### Protective layers
1. The outer layer is the white "Beta" fabric used on the ISS. It provides thermal resistance, reflects light, and protects the surface from degradation. [4]
2. Multilayer insulation (MLI) made of aluminized Kapton, approximately 0.05 cm thick and with a surface density of 0.007 g/cm². It reflects solar radiation and minimizes thermal fluctuations. This material reflects more than 90% of light and prevents overheating. It is widely used on the ISS, the James Webb Space Telescope, and other space missions. [5]
3. Self-healing composite panel made of Dyneema fibers filled with polyethylene glycol and silicon particles, 6.5 cm thick and with a density of 11.8 g/cm². When punctured by micrometeoroids, the layer seals almost instantly. Capillary and shear forces drive solid microspheres toward the impact site, where the thickening of the liquid filler leads to hardening and sealing. The Dyneema mesh redistributes stress, allowing the layer to withstand multiple impacts without failure. This innovative material enables long-term missions by reducing the need for external repairs. [12]
4. Boron nitride nanotube (BNNT) composite with a thickness of 10 cm and a density of 14 g/cm². BNNTs have exceptional mechanical strength, thermal stability, and radiation attenuation properties, making them ideal for lightweight yet strong space structures. [6]
5. Water shield with a thickness of 40 cm and a density of 40 g/cm². Due to its hydrogen content, water effectively absorbs protons and neutrons; NASA recognizes it as an excellent material for radiation shielding. [7]
6. Kevlar with a thickness of 0.5 cm and a density of 0.72 g/cm². Kevlar is five times stronger than steel by weight, intercepts micrometeorite fragments, and is resistant to tearing. Often used in Whipple shields for impact protection. [9]
7. 30 cm thick, 28.5 g/cm² high-density polyethylene (HDPE) layer, providing hydrogen-containing shielding to attenuate protons and neutrons. [7]
8. The final layer is a 0.35 cm thick, 0.945 g/cm² anodized aluminum housing, providing a hermetic seal and mechanical strength. [8]
### Windows
For space observation without compromising radiation shielding, multilayer transparent windows are offered: borosilicate glass (17.5 mm) [9], transparent polycarbonate (10 mm), transparent ceramic (25 mm) [12], a thin layer of barium or lead glass (4 mm) [10], and external louvers made of aluminum alloy and Kapton (2 cm thick). This combination provides transparency while blocking most harmful radiation.
Radiation Attenuation Calculation:
Attenuation follows an exponential law:
D = D₀ e^(-x/λ), where λ ≈ 30 g/cm² for hydrogen-rich materials such as HDPE or water, D₀ = 500 mSv/year, and the total thickness of the protective mass x ≈ 95 g/cm². [6]
Therefore, D ≈ 20 mSv/year, which corresponds to the recommended safe level for long-term use.
This multilayer system provides impact resistance, excellent heat dissipation, and reliable radiation protection. Innovative materials such as BNNT composites and self-healing polymers enable durable, lightweight, and self-sustaining station designs suitable for long-term lunar orbit missions.
## Thermal control system

## Nutrition
To sustain a lunar orbital colony with an expanding population over 80 years, food production must be entirely self-sufficient, reliable, and regenerative. The system should operate in a closed ecological cycle, combining biological, technological, and automated processes. Early years (0–10) will rely on starting reserves and system activation, while later decades will be maintained through autonomous, modular farms capable of adapting to demographic and
environmental changes. [1][2][3]
### Diet composition
The astronauts’ and colonists’ diet must be carefully balanced to sustain muscle mass, bone
strength, immune stability, and cognitive performance in reduced gravity. According to NASA’s
Human Research Program and ESA nutrition protocols, the daily intake per person should
include approximately:
#### Proteins: 100–120 g/day [4]
  Proteins maintain muscle tissue, repair cells, and regulate enzymatic activity. In low gravity,
muscle atrophy occurs faster; therefore, protein consumption is vital. Sources include
freeze-dried poultry, soy protein isolates, lentils, and microalgae such as Spirulina and Chlorella.
Insect-based protein powders derived from crickets (Acheta domesticus), mealworms (Tenebrio
molitor), and black soldier fly larvae (Hermetia illucens) provide a renewable, high-density
source of essential amino acids. [5]
#### Fats: 110–130 g/day [4]
  Fats serve as compact energy sources and enable absorption of vitamins A, D, E, and K.
Omega-3-rich algae oils will be the primary source, along with nuts, powdered dairy, and
vegetable oils (olive, flaxseed). These fats play a key role in keeping the cardiovascular system
healthy and maintaining immune balance during space missions.
#### Carbohydrates: 350–400 g/day [4]
  Carbohydrates provide the primary source of energy and stabilize blood glucose levels critical
which are essential for concentration and mental performance. Main sources include dehydrated
fruits, potatoes, whole-grain pasta, and long-storage bread mixes that can be rehydrated with
purified water.
#### Vitamins and Micronutrients
Because sunlight exposure is limited in space, vitamin D must be supplied through synthetic
sources. Calcium, phosphorus, and magnesium maintain bone mineral density; iron and vitamin
B12 sustain oxygen transport and cognitive health. These micronutrients will be included in
fortified foods, microalgae supplements, and compact multivitamin tablets to ensure a balanced
diet. [6]
These macronutrients are complemented by essential vitamins and minerals to prevent bone loss,
anemia, and neurocognitive decline.
### Food Production Infrastructure
To ensure sustainable nutrition, four major agricultural modules will form the core of the closed-loop food system.
#### Hydroponic Vertical Farms
- Main crops: (minimum seven species): lettuce (Lactuca sativa), spinach (Spinacia oleracea), kale (Brassica oleracea var. sabellica), chard (Beta vulgaris subsp. cicla), basil (Ocimum basilicum) as an aromatic herb and antioxidant source, tomatoes (Solanum lycopersicum) for vitamins and lycopene, soybean / peas (Glycine max / Pisum sativum) for plant protein. Additionally: potato (Solanum tuberosum) in dedicated containers as a carbohydrate staple.
Inputs: purified recycled water, mineral nutrient solutions (N, P, K, Ca, Mg), CO₂ from cabin air, LED light energy.
Outputs: leafy vegetables, tomatoes, microgreens, and legumes (sources of vitamins A, C, K and plant protein); potatoes and grains for carbohydrates.
Conditions: 18–25 °C, 50–70% humidity, pH 5.5–6.5, LED spectra (blue 450 nm + red 660nm).
Area: 8m2/person.
Role: provides psychological comfort (fresh food), vitamins, and carbohydrates.
#### Microalgae Photobioreactors
Inputs: water, CO₂, minerals, artificial or solar light.
Outputs: biomass rich in proteins (50–60%), omega-3 fatty acids, vitamins B and E, and oxygen.
Conditions: 20–30 °C, pH 7–8, high light intensity, continuous mixing.
Volume: 1–5 L per person.
Area: 1m2/person.
Role: protein and lipid source, oxygen generation, and CO₂ recycling.
#### Insect Farms
Inputs: plant residues from hydroponics, processed algae biomass, sterilized food waste.
Outputs: insect powder with 50–70% protein, 15–30% fat, vitamin B12, iron, zinc.
Conditions: 25–30 °C, 50–70% humidity, automated trays and dryers.
Area: 0.5m2/person.
Role: main renewable source of animal protein and fat.
#### Microbial Fermentation Modules
Inputs: plant and insect waste, mineral salts, and nutrient media.
Outputs: B-vitamins, amino acids, probiotics, enzymes, and fermentation-derived food additives.
Conditions: sterile bioreactors, 25–37 °C depending on strain.
Area: 0.05m2/person.
Role: nutrient recycling and synthesis of essential micronutrients (e.g., B12, K).
### Area calculations
- Initial population N(0)=25 200
- Final population after 80 years N(80) = 120000
- Scaling exponent α=0.9
8m2/person + 1m2/person + 0.5m2/person + 0.05m2/person = 9.55m2/person
A(0,i) = a(i) * N(0) = 9.55m^2 * 25200 = 240660m^2
A(N)=A(0)⋅(N/N(0))^α = 240660m^2 * 4.0738 = 980407m^2
### Longevity and Maintenance Plan (80 Years)
- Years 0–10: Initial phase with stored freeze-dried food, seeds, algal and insect cultures. Redundant energy and water reserves. Deployment of modular farm sections.
- Years 10–30: Full activation of hydroponic and photobioreactor systems. Implementation of automated nutrient monitoring and waste recycling. Robotic maintenance ensures continuity.
- Years 30-60: The colony reaches metabolic independence. Microbial fermentation modules and insect farms become major nutrient recyclers. Genetic seed banks and cryostorage safeguard biodiversity.
- Years 60-80: Self-sustaining ecosystem with AI-driven optimization, predictive nutrient modeling, and intergenerational genetic renewal of crops and insect species. Continuous adaptation to population growth from X₀ to N inhabitants.

## Atmosphere and climate
### Oxygen production
The Samruk station will employ Chlorella microalgae as a primary oxygen source. Chlorella is a powerful tool for generating oxygen in space, as it exhibits a high rate of photosynthesis and is compact and efficient. It has been used in space missions and has shown its potential. The photosynthetic process in Chlorella requires only fundamental inputs: water, carbon dioxide, light energy, and trace minerals (including potassium, phosphorus, and sodium) to sustain cellular reproduction. In the experimental facilities of the Institute of Biophysics in Krasnoyarsk, specifically BIOS-1, BIOS-2, and BIOS-3, a two-component closed-loop life support system has been implemented, consisting of humans and chlorella. Carbon dioxide is placed in a specialized container that contains water with specific minerals and chlorella. Under the influence of fluorescent light, the carbon dioxide undergoes a photosynthesis reaction, converting it into oxygen.
#### Stoichiometry and Key Constants (per person)
Daily oxygen requirement (24 h):
1.5 m^3 O₂ = 66.96 mol O₂.
1 mol = 10^15 fmol => 66.96 mol = 6.696 * 10^16 fmol.
Stoichiometrically, 1 mol of O₂ requires 1 mol of H₂O(for photosynthesis).
Thus, the reaction water mass ≈ 1.206 L/person/day (66.96 mol * 18.015 g/mol ≈ 1205.5 g).
This is a stoichiometric value; the actual circulating water volume in the reactor will be
significantly larger.
Chlorella cell parameters:
Average cell diameter: ≈5 μm => cell volume ≈ 65.45 μm^3 = 6.545 * 10^(-14) L.
Oxygen production rate: 25–400 fmol O₂/cell/hour.
#### Daily oxygen production per cell: 600–9,600 fmol/cell/day
High productivity (400 fmol/h => 9,600 fmol/day):
N(min) = (6.696 * 10^16 fmol) / (9.6 * 10^3 fmol/day) ≈ 6.98 * 10^12 cells
Low productivity (25 fmol/h => 600 fmol/day):
N(max) = (6.696 * 10^16 fmol) / (600 fmol/day) ≈ 1.12 * 10^14 cells
(Thus, 6.98 * 10^12 – 1.12 * 10^14 cells/day are required per person depending on productivity.)
####  Chlorella biomass volume per person (range)
High productivity:
V(min) = 6.98 * 10^12 cells * 6.545 * 10^(-14) L/cell = 0.4566 L
Low productivity:
V(max) = 1.12 * 10^14 cells * 6.545 * 10^(-14) L/cell = 7.309 L
(Thus, 0.457–7.31 L of biomass is required per person.)
#### Stoichiometric water mass/volume for photosynthesis (per person)
n(O₂) = 66.96 mol ⇒ requires ~66.96 mol H₂O⇒ water mass = 1,205.5 g ≈ 1.206 L.
(This is a stoichiometric value – the reactor will utilize and circulate significantly more water.)
#### Scaling for 120,000 people (final values)
O₂ and H₂O totals:
O₂: 1.5 m^3 * 120,000 = 180,000 m^3/day
Stoichiometric water: 1.206 L * 120,000 = 144,720 L/day = 144.72 m^3/day
Chlorella cells (total):
High productivity (400 fmol/h):
N(total,min) = 6.98 * 10^12 * 120,000 ≈ 8.37 * 10^17 cells
Low productivity (25 fmol/h):
N(total,max) = 1.12 * 10^14 * 120,000 ≈ 1.34 * 10^19 cells
Biomass volume (total):
High productivity: V(total,min) = 0.4566 L * 120,000 ≈ 54,792 L ≈ 54.79 m^3
Low productivity: V(total,max) = 7.309 L * 120,000 ≈ 877,080 L ≈ 877.08 m^3
(Summary: For 120,000 people, 8.37 * 10^17 – 1.34 * 10^19 cells are required, equivalent to
~54.8 m^3 of biomass under optimal conditions or ~877.1 m^3 under low productivity.)
### Reserve Oxygen Production Method
In emergency scenarios (e.g., bioreactor failure or sudden crew expansion), the Samruk station employs water electrolysis (Electrolysis is the process of decomposing water (H₂O) into oxygen (O₂) and hydrogen (H₂) through the application of direct electric current) as a reliable backup method for oxygen generation.
2H₂O → 2H₂ + O₂
- Oxygen — directed into the life support system.
- Hydrogen — stored as fuel for propulsion, power generation, or synthetic chemical
processes.
This method ensures 150% of daily oxygen demand and serves as a critical contingency capability under all non-nominal conditions.
### Atmosphere composition
The atmospheric composition aboard the Samruk station will be identical to that of Earth to ensure crew safety and comfort:
- Nitrogen (N₂) — 78%
- Oxygen (O₂) — 21%
- Carbon dioxide (CO₂) — 0,03%
Rationale for this composition:
- Pure oxygen increases fire hazards and can be toxic to humans at high concentrations.
- A nitrogen-dominated atmosphere would accelerate corrosion of the station's metal
components.
- The inclusion of water vapor is necessary to maintain comfortable air humidity levels
This atmospheric composition provides optimal conditions for both human habitation and
equipment operation aboard the station.
### Climate
#### Pressure
Nominal cabin pressure: approximately 101.3 kPa (1 atm), or slightly reduced (~90–101 kPa) depending on the station’s architectural design.
A near-Earth pressure level is preferred to prevent crew adaptation difficulties.
#### Temperature
Comfortable temperature range: 18–26 °C in inhabited modules.
Auxiliary modules (e.g., agricultural or technical compartments) maintain specific temperature ranges depending on equipment requirements.
Relative humidity:
- 40–60 % in living areas (for human comfort and respiratory health),
- lower in technical zones to reduce corrosion risk and prevent condensation.
#### Ventilation 
Continuous mechanical ventilation with balanced supply and exhaust airflow circulation.
Air treatment includes:
- HEPA filtration for particulates,
- adsorption of volatile organic compounds (VOC),
- catalytic purification for trace contaminants.

### Water needs calculations

## Healthcare

## Waste management

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
- Water. Water ice is concentrated at the south pole of the moon, in eternally darkened craters, such as Shackleton crater in which one of the regolith-extracting stations will be placed. According to LRO data, regolith in Shackleton consists about 5-10% of water by mass [1].
- Heluim-3. Unlike water, helium-3 is concentrated in illuminated regions, such as the lunar maria (Mare Tranquillitatis, Oceanus Procellarum or Mare Fecunditatis), in which regolith-extracting stations also will be placed. Regolith in these regions consist of about 50ppb of Helium-3 [2].
- Building materials. Metals will be extracted from the rest of the regolith that is mined by water and helium-3 extracting stations.
![Picture1. Complexes location](/Complexes location.jpg)
### Transportation
As stated above, lunar regolith will be transported to the orbital settlement by large amounts of delivering rockets. Rockets are docked to the tank in the base and fly to orbit when the tank is full and orbital settlement's trajectory is above. Delivering rockets have 4 thrust-vectoring engines and RCS to perform maneuvers. After approaching the orbital station, rockets attach the tank to the station and refuel to deorbit and ereturn empty tanks back and lift other tanks.
![Picture1. Delivering rocket 3D-model](/Delivering rocket.jpg)
### Processing
On the orbital settlement regolith will be heated and melted in vacuum furnaces to separate volatile components of it. 
- Water. Most of the water will be used by the biosphere of the settlement and thermoregulation systems. Another part will be electrolyzed to gain hydrogen and oxygen that can be used as fuel pair for rocket engines and for production of  “heavy water” that is used in thermonuclear energetics.
- Building materials. Metals are then refined from the rest of metals-consisting regolith by electromagnetic separation and used in building of new modules, repairing, manufacturing etc.
- Heluim-3. Helium-3 will be extracted from regolith and used in thermonuclear energetics in pair with heavy hydrogen.

## Demography aspects

## Political aspects

## Social aspects

## Economical aspects

## Risks and assumptions

## Bibliography
### Location and mission of the settlement
1. https://books.google.kz/books?id=S4xDhVCxAQIC&pg=PA184&redir_esc=y#v=onepage&q&f=false
2. https://cfpl.ae.utexas.edu/wp-content/uploads/2010/10/science_article.pdf
3. https://www.sciencedirect.com/science/article/abs/pii/S0019103507001285
4. https://www.lpi.usra.edu/lunar/missions/apollo/apollo_11/samples
5. https://www.nature.com/articles/s41586-024-07927-7
### Shielding
1. https://pmc.ncbi.nlm.nih.gov/articles/PMC10427620/?
2. https://www.cdc.gov/radiation-health/about/how-to-measure-radiation
3. https://nss.org/wp-content/uploads/2018/01/NSS-JOURNAL-Orbital-Space-Settlement-Radiation-Shielding.pdf
4. https://ntrs.nasa.gov/api/citations/19930015285/downloads/19930015285.pdf
5. https://ntrs.nasa.gov/api/citations/20080045503/downloads/20080045503.pdf
6. https://www.nasa.gov/wp-content/uploads/2017/07/niac_2011_phasei_thibeault_radiationshieldingmaterials_tagged.pdf
7. https://ntrs.nasa.gov/api/citations/20090020691/downloads/20090020691.pdf
8. https://www.nasa.gov/wp-content/uploads/2023/03/prc-5006-current.pdf
9. https://hvit.jsc.nasa.gov/shield-development/materials.html
10. https://www.sciencedirect.com/science/article/abs/pii/S0969806X22007393
11. https://marshield.com/publications/Medical_RadiationShieldingLeadGlass.pdf
12. https://www.dyneema.com/media/jhrmt0j4/dyneema-composites.pdf
https://www.researchgate.net/publication/325021854_Shear_thickening_effect_of_the_suspensions_of_silica_nanoparticles_in_PEG_with_different_particle_size_concentration_and_shear
13. https://digitalcommons.unl.edu/nasapub/121
### Nutrition
1. https://pmc.ncbi.nlm.nih.gov/articles/PMC8747021/
2. https://www.acorecycling.com/from-earth-to-mars-sustainability-lessons-for-space-colonies/
3. https://www.nasa.gov/exploration-research-and-technology/growing-plants-in-space/
4. https://pmc.ncbi.nlm.nih.gov/articles/PMC8747021/ (3.1.1. Key Components of Space Nutrition)
5. https://www.airbus.com/en/newsroom/press-releases/2019-04-photobioreactor-oxygen-and-asource-of-nutrition-for-astronauts
6. https://spacefood.competitionsciences.org/wp-content/uploads/2024/11/Astronaut-NutritionalNeeds-Guide-SFDC.pdf
7. https://www.space.com/astronaut-pee-iss-water-recycling-98-percent-milestone
8. https://www.aquatechtrade.com/news/water-reuse/how-is-water-recycled-in-space
### Resource industry
1. https://agupubs.onlinelibrary.wiley.com/doi/full/10.1029/2012GL052119
2. https://agupubs.onlinelibrary.wiley.com/doi/pdf/10.1029/1998GL900305

## Methods/instruments
