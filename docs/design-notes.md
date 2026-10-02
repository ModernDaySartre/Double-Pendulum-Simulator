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

Then I realised that there are actually two categories of quantities that I have listed. One we may call parametres - the masses, lengths and gravity - the things that are invariant over time and the states - angular velocities and positions- the things that need to be defined at every instant.

#### Why use angles and angular velocities over cartesian coordinates ? You could describe the system using x1,y1,x2 and y2.

I acknowledged the fact that angles weren't the only system of state variables that could be used to create this model.

However, in the choice of angles  there is simplicity for my code. Angles align with the idea of a minimal state description, they are a set of variables that can determine the future evolution of the model over time without involving variables that are constrained or redundant. For example, the cartesian coordinates, x1 and y1, used to describe the position of bob 1 have the imposed constraints of having to satisfy x1^2 + y1^2 = L^2, where L is the fixed length of the rod, and the equivalent constraint for x2 and y2. They contain redundant information. Why tell the computer to acknowledge thse 4 coordinates and remember that they must also satisfy the 2 constraints when I could instead choose two angles and the geometry satisfies the constraint.

### 2. Physically, perhaps in terms of forces, how is the system acting ?

Bob 1 is constrained by rod 1 (motion is limited as rod is inextensible) and has forces acting on it from rod 1 (We can label this force T1), gravity (g) and rod 2 (We can label this forec T2)

Bob 2 is contrained by rod 2 relative to bob 1 (depending on the location and motion of bob 1 the area where bob 2 can move while constrained by rod 2 is subhject to change. But of course it still must be L metres away from bob 1, where L is the length of rod 2)



### 3. We know what the computer needs to describe the current instant but a double pendulum is a dynamic system evolving over time, so what information must the computer know in order to describe how the system will evolve in the next instant ?

Derivatives are the standard method of describing the rates of change of quantities and hence they could be used to determine how the current state of the pendulum will change over time.

The derivatives of the state variables would be the angular velocities and angular accelerations. Seeing as we already have the angular velocities, the angular accelerations are what we need to be able to determine.

From the assigned positions / displacements of each bob ( x1 = L1sintheta1, y1 = L1costheta1, x2...), where theta1 and theta 2 are measured from the downward vertical with clockwise rotation being +ve, we can determine the linear accelerations by taking the 2nd derivatives of these displacements. We can then, by establishing the forces acting on the bobs, use Newtons 2nd Law to substitute in our expressions for the linear acceleration and determine what we actually want, the angular accelerations.


