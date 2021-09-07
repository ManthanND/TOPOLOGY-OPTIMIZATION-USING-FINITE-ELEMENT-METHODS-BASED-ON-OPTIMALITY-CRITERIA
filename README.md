# TOPOLOGY-OPTIMIZATION-USING-FINITE-ELEMENT-METHODS-BASED-ON-OPTIMALITY-CRITERIA
Optimization can be referred in many ways. People optimize like investors optimize for getting maximum return on investments, manufacturers optimize to seek maximum efficiency in their production process while the engineers optimize their designs by adjusting various parameter to seek maximum performance from the system.
Even it’s fascinating to note that Mother Nature optimizes. It optimizes various systems for minimum potential energy. Even during chemical reactions molecules react in such a way that the distance between the newly formed atomic interactions (bonds) has minimum total energy of reaction.
Optimization is an important tool for analysis of physical systems. Our goal is to find values of the variables that optimize (maximize or minimize) the objective of which the variables are either restricted or constrained by some ways.


## Topology Optimization:
Sizing, shape and topology address different aspects of structural design problem. In a typical sizing (parametric) problem, the goal may be to find the optimal thickness distribution of a linearly elastic plate or optimal thickness distribution of a linearly elastic plate or truss structure. The optimal thickness distribution minimizes (or maximizes) a physical quantity such as mean compliance (external work), peak stress, deflection, etc. while equilibrium and other constraints on the state and design variables are satisfied. The design variable is the thickness of the plate and the state variable may be its deflection. The main feature of the sizing problem is that the domain of the design model and state variables is known apriority and is fixed throughout the optimization process. On the other hand, in shape optimization problem, the goal is to find the optimum shape of the domain, that is the shape problem is defined on a domain which is now a design variable. Topology optimization of the solid structures involves the determination of features such as the number and location and shape of the holes and connectivity of the domain.

## Breakdown of Sigmund-Bendsoe Algorithm used for TO:
The 4 major parts required for topology optimization are as follows:
1. Problem definition and compliance minimization
2. Optimality Criteria based optimizer
3. Mesh Independency filter
4. Finite element part
The disadvantage of homogenization based approach mentioned above is that determining the optimal microstructures (material presence) is cumbersome if resolved, especially for non-compliance minimization problems. So we follow the second approach, power-law based method (SIMP), where material properties are assumed constant (isotropic) within each element. The material properties are defined as some power times material properties.


## Algorithm Description:
The main input arguments required to be specified by the user for topology optimization can be reduced to just 4 main arguments viz:
Topology (nelx, nely, volfrac, penal, rmin)
Where nelx and nely are number of elements in horizontal and vertical direction each of 1 unit, thus they also denote the horizontal and vertical dimensions.
Volfrac is the volume fraction required to be kept in the optimized structure.
Penal is the penalization factor incorporated because of the use of SIMP method and rmin is the filter size (radius about which a gradient effect is kept in, to avoid the checker-board effect).The remaining boundary conditions like force and fixed nodes are directly incorporated in the Finite element part of the code, which makes the code specific to the nature of problem addressing.
The code is divided into 4 parts as discussed earlier:
1. Main program (Objective function definition and iteration schemes):
It distributes the material evenly within the design space (which means equal stiffness throughout the geometry). It will make a function cal to FE function defined which returns a displacement vector. The element K function defined below is also called upon. For the assemblage of the element matrices, n1 and n2 are defined to obtain element displacement vector from Global displacement vector. The sensitivity analysis is followed by Mesh-Independency Filter
2. OC based optimizer (Optimality Criteria)
Here the langrange multiplier satisfying the volume constraint is obtained using bisection algorithm by initial guess of lower l1 and upper l2. The bisection continues until the convergence criteria is achieved.
3. Mesh independency filter:
The rmin radius defined in the argument, helps defining the mesh independency of the density distribution. For r>rmin the density value is set to 0. For r<rmin density value scales from 1 to 0 based on the location of centre of element
4. The finite element part makes use of MATLAB function called sparse, where it neglects the density 0 locations straight away by just storing non-zero elements
The FE part loops over element stiffness matrices to obtain a global stiffness matrix. Here the convention of node numbering used is Columnwise left to right.
Every node has 2 degrees of freedom ux and uy, thus a square element having four such nodes at each corner ill have total of 8 elements.
A Boundary condition in terms of force acting at the mid-span of 1 unit. This is given as F(2,1)=-1, which is a vertical force in upper left corner.
Supports (Zero displacements) are eliminated from total degrees of freedom by categorizing them as fixed degrees of freedom.
Thus we evaluate for Free Degrees of freedom
Free DoF=Total DoF-Fixed DoF
From this we calculate Global displacement vector as:
U(Free DoF)=F(Free DoF)/K(Free doF)



Conclusion:
The Topology Optimization method using finite element methods based on optimality criteria can be successfully implemented for both Structural and thermal problems.
The Sigmund-Bendsoe approach to divide the approach using 4 subparts as explained above can be extended to various cases as demonstrated.
The method can very well be extended to various structures problem like Simply Supported, Cantilever and Multi-load case by suitable modifications in the code.
Also the same method can handle various thermal conduction problems for various Boundary conditions. The fluid mechanic optimization problems for minimum resistance (viscous) paths can be also be explored by the same approach where the objective function needs to be modified.
The various future extensions multi-physics extensions to this technique are:
1. Thermo-structural problems (Structures+Thermal)
2. Fluid-structure interaction problems
3. 3D structural optimization
4. 3D thermal conductivity optimization
Various other techniques that can be compared along with OC criteria are:
Method of Moving average, Density based filtering
Based on the literature survey and sources referred, the proposed method is efficient than rest of the methods mentioned above.


Codes:
Visit the report Appendix for all the codes :)
