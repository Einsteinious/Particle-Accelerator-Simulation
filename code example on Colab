#Particle Collision Simulation (LHC-like)
#Description:
#This simulation visualizes particle collisions inspired by the Large Hadron Collider (LHC). It demonstrates the behavior of particles (e.g., protons, neutrons, and pions) as they collide, bounce off walls, and create new particles. The simulation includes realistic physics-based collisions, energy conservation, and visual effects such as particle trails, explosions, and dynamic labels.

#Key Features:
#Particle Types:
#Protons: Red particles with positive charge.
#Neutrons: Cyan particles with no charge.
#Pions (π⁺): Magenta particles with positive charge.
#Collision Dynamics:
#Particles collide and create new particles (e.g., proton + proton → proton + neutron + π⁺).
#Momentum and energy are conserved during collisions.
#Visual Effects:
#Trails: Particles leave fading trails to visualize their paths.
#Glow Effect: Particles have a glowing outline for better visibility.
#Interactive Counters:
#Displays the number of particles and collisions in real-time.
#Boundary Conditions:
#Particles bounce off the walls of the simulation area.
#Customizable Parameters:
#Maximum number of particles (max_particles).
#Maximum number of collisions (max_collisions).
#How It Works:
#Initialization:
#Two protons are created and set in motion toward each other.
#The simulation area is set up with a dark background, grid lines, and a circular boundary to mimic the LHC.
#Collision Handling:
#When particles collide, they are removed, and new particles (proton, neutron, and π⁺) are created.
#Animation:
#The FuncAnimation class updates the positions of particles and handles collisions in real-time.
#The animation runs until the maximum number of particles or collisions is reached.
#Code Structure:
#Particle Class:
#Represents a particle with properties like position, velocity, radius, color, mass, charge, type, and label.
#Includes methods to update the particle's position and handle fading trails.
#Collision Functions:
#are_colliding(): Checks if two particles are colliding.
#handle_collision(): Handles the collision logic, including creating new particles and displaying explosion effects.
#Animation:
#The update() function updates the positions of all particles, checks for collisions, and updates the counters.
#The FuncAnimation class creates the animation and embeds it in the notebook.
#Usage:
#Run the Simulation:
#Execute the code in a Jupyter Notebook or Python environment.
#The animation will display in the notebook or a separate window.
#Customize Parameters:
#Adjust max_particles and max_collisions to control the simulation's duration and complexity.
#Modify particle properties (e.g., mass, charge, color) to simulate different scenarios.
#Dependencies:
#Python Libraries:
#numpy: For numerical computations.
#matplotlib: For visualization and animation.
#IPython.display: For embedding the animation in a notebook.
#Animation Control Buttons in FuncAnimation
#Speed Controls (+) & (-)
#Adjust the speed of the animation.
#(+): Increases the speed, making the animation run faster.
#(-): Decreases the speed, making the animation run slower.
#Known Issue (when increasing frames):
#When increasing frames from 1000 to 2000, you might get the following error:

#"Animation size has reached 21143965 bytes, exceeding the limit of 20971520.0. If you're sure you want a larger animation embedded, set the animation.embed_limit rc parameter to a larger value (in MB). This and further frames will be dropped."

#To resolve this, simply increase the limit in the following code:

import matplotlib.pyplot as plt
plt.rcParams['animation.embed_limit'] = 500  # Increase the limit to 500 MB
#Increasing the limit to 500 MB shall do the trick, but it will also increase execution time (~ 5 minutes).

import numpy as np
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation
from IPython.display import HTML
import matplotlib.patheffects as path_effects  

# Increase animation embed limit
plt.rcParams['animation.embed_limit'] = 200  # Increase the limit to 200 MB

max_particles = 100  # Maximum number of particles allowed
max_collisions = 100  # Maximum number of collisions allowed
collision_counter = 0  # Track the number of collisions

# Set up the figure and axis
fig, ax = plt.subplots()
ax.set_xlim(-10, 10)
ax.set_ylim(-10, 10)
ax.set_aspect('equal')

plt.close(fig)  # Close the figure to prevent it from being displayed as a static image

# Add a circular grid to mimic the LHC structure
circle = plt.Circle((0, 0), radius=10, edgecolor='gray', facecolor='none', linestyle='--', alpha=0.5)
ax.add_patch(circle)

# Add a grid to the background
ax.grid(True, linestyle='--', alpha=0.3, color='gray')

# Set a dark background
fig.patch.set_facecolor('black')
ax.set_facecolor('black')

# Add a beamline effect
ax.axhline(0, color='deepskyblue', linestyle='--', alpha=0.3, linewidth=2)
ax.axvline(0, color='deepskyblue', linestyle='--', alpha=0.3, linewidth=2)

# Add a title and labels
ax.set_title("Particle Collision Simulation (LHC-like)", color='white', fontsize=14, pad=20)
ax.set_xlabel("X Position", color='white', fontsize=10)
ax.set_ylabel("Y Position", color='white', fontsize=10)

# Adjust tick colors for better visibility
ax.tick_params(axis='x', colors='white')
ax.tick_params(axis='y', colors='white')

# Define the Particle class
class Particle:
    def __init__(self, pos, velocity, radius, color, mass=1, charge=1, type='proton', label=''):
        self.pos = np.array(pos, dtype=float)
        self.velocity = np.array(velocity, dtype=float)
        self.radius = radius
        self.color = color
        self.mass = mass
        self.charge = charge
        self.type = type  # Particle type
        self.label = label  # Add label parameter
        self.circle = plt.Circle(self.pos, self.radius, color=self.color)
        self.trail = ax.plot([], [], color=self.color, lw=1, alpha=1)[0]
        self.collision_count = 0
        self.trail_alpha = 1
        self.text = ax.text(self.pos[0], self.pos[1], self.label, fontsize=8, ha='center', va='center', color='white')

    def update(self, dt):
        self.pos += self.velocity * dt
        x, y = self.trail.get_data()
        self.trail.set_data(np.append(x, self.pos[0]), np.append(y, self.pos[1]))
        
        # Gradient fading for trails
        self.trail_alpha = max(0.3, self.trail_alpha - 0.02)  # Adjust fading rate
        self.trail.set_alpha(self.trail_alpha)
        
        # Update text position
        self.text.set_position((self.pos[0], self.pos[1]))

# Create two protons
particle1 = Particle(pos=[-5, 0], velocity=[3, 0], radius=1.0, color='red', mass=1, charge=1, type='proton', label = 'proton')
particle2 = Particle(pos=[5, 0], velocity=[-3, 0], radius=1.0, color='blue', mass=1, charge=1, type='proton', label = 'proton')

# List to store all particles
particles = [particle1, particle2]

# Add particles to the plot
for p in particles:
    ax.add_patch(p.circle)
# Add a glow effect to particles
for p in particles:
    p.circle.set_path_effects([path_effects.withStroke(linewidth=3, foreground='lightgray', alpha=0.3)])

# Adjust particle and text colors for better visibility
for p in particles:
    p.circle.set_edgecolor('white')  # Add edge color for better visibility
    p.text.set_color('white')  # Make labels white

# Function to check for collisions
def are_colliding(particle1, particle2):
    distance = np.linalg.norm(particle1.pos - particle2.pos)
    return distance <= (particle1.radius + particle2.radius)

# Function to handle collisions
def handle_collision(particle1, particle2):
    global particles, collision_counter

    collision_counter += 1

    # Create multiple scatter points for a more realistic explosion
    explosion_points = ax.scatter(
        [particle1.pos[0]] * 10,  # 10 points at the collision position
        [particle1.pos[1]] * 10,
        s=np.random.uniform(50, 200, size=10),  # Random sizes
        c=np.random.choice(['gold', 'darkorange', 'white'], size=10),  # Random colors
        alpha=0.8,
        zorder=10
    )
    fig.canvas.draw()
    plt.pause(0.05)
    explosion_points.remove()  # Remove the explosion effect after a brief pause

    # Remove the colliding particles from the plot
    particle1.circle.remove()
    particle2.circle.remove()
    particle1.text.remove()  # Remove label for particle1
    particle2.text.remove()  # Remove label for particle2
    
    particles.remove(particle1)
    particles.remove(particle2)
    
    total_momentum = particle1.velocity * particle1.mass + particle2.velocity * particle2.mass
    total_energy = 0.5 * particle1.mass * np.linalg.norm(particle1.velocity)**2 + \
                   0.5 * particle2.mass * np.linalg.norm(particle2.velocity)**2

    # Outcome 2: p + p → p + n + π⁺
    # Create a proton
    proton_velocity = np.random.uniform(-3, 3, size=2)
    proton_velocity = proton_velocity / np.linalg.norm(proton_velocity) * np.sqrt(2 * total_energy / 3)
    
    proton = Particle(
        pos=particle1.pos + np.array([1, 0]),  # Offset to avoid overlap
        velocity=proton_velocity,
        radius=0.3,
        color='orange',  # Proton
        mass=1,
        charge=1,
        type='proton',
        label=f'p{collision_counter}'
    )
    particles.append(proton)
    ax.add_patch(proton.circle)

    # Create a neutron
    neutron_velocity = np.random.uniform(-3, 3, size=2)
    neutron_velocity = neutron_velocity / np.linalg.norm(neutron_velocity) * np.sqrt(2 * total_energy / 3)
    
    neutron = Particle(
        pos=particle1.pos + np.array([0, 1]),  # Offset to avoid overlap
        velocity=neutron_velocity,
        radius=0.3,
        color='cyan',  # Neutron
        mass=1,
        charge=0,
        type='neutron',
        label=f'n{collision_counter}'
    )
    particles.append(neutron)
    ax.add_patch(neutron.circle)

    # Create a positively charged pion
    pion_velocity = np.random.uniform(-3, 3, size=2)
    pion_velocity = pion_velocity / np.linalg.norm(pion_velocity) * np.sqrt(2 * total_energy / 3)
    
    pion = Particle(
        pos=particle1.pos + np.array([-1, 0]),  # Offset to avoid overlap
        velocity=pion_velocity,
        radius=0.2,
        color='magenta',  # Positively charged pion
        mass=0.1,  # Pion mass (approximate)
        charge=1,
        type='π⁺',
        label=f'π⁺{collision_counter}'
    )
    particles.append(pion)
    ax.add_patch(pion.circle)

# Add a particle counter
particle_counter = ax.text(-9.5, 9.5, f'Particles: {len(particles)}', fontsize=10, color='white')
collision_counter_text = ax.text(-9.5, 8.5, f'Collisions: {collision_counter}', fontsize=10, color='white')

# Update the counter in the `update` function
def update(frame):
    global collision_counter

    if collision_counter >= max_collisions or len(particles) >= max_particles:
        return [p.circle for p in particles] + [p.trail for p in particles]

    dt = 0.05

    for p in particles:
        p.update(dt)

        # Circular boundary conditions
        distance_from_center = np.linalg.norm(p.pos)  # Distance from the center (0, 0)
        if distance_from_center + p.radius >= 10:  # If particle is outside the circle
            # Calculate the normal vector at the collision point
            normal = p.pos / distance_from_center
            # Reflect the velocity vector across the normal
            p.velocity = p.velocity - 2 * np.dot(p.velocity, normal) * normal

    # Check for collisions
    collided = False
    for i in range(len(particles)):
        for j in range(i + 1, len(particles)):
            if are_colliding(particles[i], particles[j]):
                handle_collision(particles[i], particles[j])
                collided = True
                break
        if collided:
            break

    # Update circle positions and labels
    for p in particles:
        p.circle.center = p.pos
        p.text.set_position((p.pos[0], p.pos[1]))

    # Update particle and collision counters
    particle_counter.set_text(f'Particles: {len(particles)}')
    collision_counter_text.set_text(f'Collisions: {collision_counter}')

    return [p.circle for p in particles] + [p.trail for p in particles] + [particle_counter, collision_counter_text]
    
# Add a Legend
legend_elements = [
    plt.Line2D([0], [0], marker='o', color='w', markerfacecolor='orange', markersize=8, label='Proton'),
    plt.Line2D([0], [0], marker='o', color='w', markerfacecolor='cyan', markersize=8, label='Neutron'),
    plt.Line2D([0], [0], marker='o', color='w', markerfacecolor='magenta', markersize=8, label='π⁺ Pion'),
]
ax.legend(handles=legend_elements, loc='upper right', fontsize=10, facecolor='black', edgecolor='white', labelcolor='white', bbox_to_anchor=(1.25, 1))

# Create the animation
ani = FuncAnimation(fig, update, frames=1000, interval=50, blit=True)

# Embed the animation in the notebook
HTML(ani.to_jshtml())
