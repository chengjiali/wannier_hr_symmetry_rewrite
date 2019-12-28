## Procedure of original code 

1. Read input files
    - Input
        - poscar.in
    - Output
        - A-matrix
        - Number of atoms in poscar.in
        - Atom_fraction vector for each atom

    - Input
        - wann.in
    - Output
        - Number of atoms in wann.in
        - Number of orbitals
        - Number of bands
        - Spinor or not?
        - Number of orbitals for each atom 
        - Index offset for each atom  
    
    - Input
        - locaxis.in
    - Output
        - Local axis of atoms in wannier projection
        - Read x and z axis, $y = x \times z$ (cross product)
        
        
2. Get symmetry with SPG Lib
    - Input
        - Crystal case (data from poswan.in)
    - Output
        - Rotation matrix
        - Translation matrix ( G-translation )
        - P-translation (didn't show how to compute in the given example)
        - Number of symmetry
        - Number of P-translation (mannually set to 1 to "make code less and use type I")
        
    
3. Get rotation matrices of all symmetry opreations defined in symmop.dat file.
    - Input
        - Data from wann.in
    - Output
        - R = rotation matrix
        - $R^{\prime} = Amat R Amat^{-1}$, global rotation matrix, in Cartesian coordinate
        - $Eular angle (\alpha, \beta, \gamma) = det(R^{\prime}) * R^{\prime}$
        - D-matrix, transform Euler angle (x, y, z) into 2x2 matrix with element of -1, 0, 1
        - Vector shift, $vec\_shift = R * atoms\_frac + gtrans + ptrans - atoms\_frac$
        - Rotation axis and rotation orbital
            - $RotAxis_{j} = axis[jatom]^{-1} * R^{\prime} * axis[jatom]$
            - $RotAxis_{i} = axis[iatom]^{T} * axis[jatom]$
            - $RotAxis = RotAxis_{i} * RotAxis_{j}$
        - Prot matrix
            - Spinor: $prot\_matrix = prot\_matrix \otimes Dmat$
            - Non-Spinor: 

4. Read wannier.dat
    - Saved as $H_{ij}$, two values for each cordinate (x, y, z)

Then do the following:

$H_{ij}^{\prime} = Prot_{i}^{\dagger} H_{ij} Prot_{j}$

$H_{ij} = (H_{ij}^{\prime} + H_{ij} )/2$

        - atoms_cart = Amat * atoms_frac
