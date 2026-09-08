# Thought Process behind Double Pendulum
A map of my thoughts about how I should go about building the system and the questions that have to be asked and answered in order to code.
(As this is my first project and first real attempt at coding AI did assist me)

## Modelling Philosophy
A simulation is not a recreation of reality itself, but a mathematical model based on assumptions. 
Objects are defined by their properties and interactions.
The complexity of the simulation depends on what assumptions are included or removed.

## Questions

### 1. At any given time, what information must the computer know to completely describe the double pendulum ?

I began by imagining empty space and attempted to list all that would be needed for me to create the pendulum in space and know its behaviour in the current instance.

Potential quantities:
- Masses of the bobs
- Length of the rods
- Gravitational Field Strength
- Angular velocities of pendulums
- Angular positions of pendulums

Assumptions:
- Rods are massless and rigid
- No friction or air resistance
- Bobs act as point particles
- Motion is confined to a two dimensional plane

Then I realised that there are actually two categories of quantities that I have listed. One we may call parametres - the masses, lengths and gravity - the things that are invariant over time and the states - angular momentums and positions- the things that need to be defined at every instant.



### 2. Physically, perhaps in terms of forces, how is the system acting ?

Bob 1 is constrained by rod 1 (motion is limited as rod is inextensible) and has forces acting on it from rod 1, gravity and rod 2

Bob 2 is contrained by rod 2 relative to bob 1 (depending on the location and motion of bob 1 the area where bob 2 can move while constrained by rod 2 is subhject to change. But of course it still must be L metres away from bob 1, where L is the length of rod 2)



### 3. We know what the computer needs to describe the current instant but a double pendulum is a dynamic system evolving over time, so what information must the computer know in order to describe how the system will evolve in the next instant ?

Derivatives are the standard method of describing the rates of change of quantities and hence they could be used to determine how the current state of the pendulum will change over time.

The derivatives of the state variables would be the angular velocities and angular accelerations. Seeing as we already have the angular velocities, the angular accelerations are what we need to be able to determine.

From the assigned positions / displacements of each bob ( x1 = L1sintheta1, y1 = L1costheta1, x2...) we can determine the linear accelerations by taking the 2nd derivatives of these displacements. We can then, by establishing the forces acting on the bobs, use Newtons 2nd Law to substitute in our expressions for the linear acceleration and determine what we actually want, the angular accelerations.


