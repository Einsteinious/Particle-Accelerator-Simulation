# Particle-Accelerator-Simulation
While not a perfect replication of real LHC physics, it incorporates fundamental concepts like energy and momentum conservation.
Models the collision of two protons (p + p) resulting in a proton (p), a neutron (n), and a positively charged pion (π⁺). It’s designed to reflect particle physics and it is mostly accurate, with momentum and energy conservation during collisions.

Used a circular boundary for the simulation, similar to a cyclotron. This boundary will likely lead to more collisions and thus take a bit more time to run (2-6 mins, depending on the number of particles).
#The particles are created at random speeds, so the patterns will always be unique. (which is really cool but sometimes it keeps colliding and produces like 100 particles!)

**In essence, this code provides a simplified yet visually appealing way to understand the basic concepts of particle collisions, similar to those that occur in high-energy physics experiments like the LHC.**
To see how it works open this that links to my work:
**[Particle Accelerator simulation](https://colab.research.google.com/drive/1qWvhOPAB6fdfmvo2OA1xGDwk-BUsavbl?usp=sharing)**


(Particle Class:
This defines what a particle is: its position, velocity, size, color, mass, charge, and type (proton, neutron, pion). It also handles how a particle moves and leaves a fading trail to show its path. 
Collision Detection and Handling:
The code checks if particles are close enough to collide. When a collision occurs, the colliding particles are removed, and new particles are created (a proton, neutron, and pion in this case). An explosion effect is briefly displayed to visually represent the collision. The code attempts to conserve momentum and energy during collisions. 
Animation:
The FuncAnimation function from Matplotlib is used to create a smooth, real-time visualization of the particles moving and colliding. The animation updates the particle positions, checks for collisions, and updates the counters. The code also handles the particles bouncing off the edges of the simulation area, giving a circular boundary to simulate the LHC. 
Visual Enhancements:
The simulation includes visual effects like particle trails, glowing outlines, and explosion animations to make it more engaging. It has a dark background with a grid and circular boundary to resemble the LHC. It also has particle labels, and particle and collision counters. 
Customization:
You can adjust parameters like the maximum number of particles and collisions to control the simulation's complexity and duration. You can also modify particle properties like mass, charge, and color to simulate different scenarios. The code also contains speed controls. 
Libraries:
It uses numpy for numerical calculations, matplotlib for plotting and animation, and IPython.display to embed the animation in a Jupyter Notebook.)
