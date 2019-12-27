## Procedure of main function

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
        - Crystal case from poswan.in
    - Output
        - Rotation matrix
        - Translation matrix ( G-translation )
        - Number of symmetry
        - Number of P-translation (mannually set to 1 to "make code less and use type I")
        
    
3. Get rotation matrices of all symmetry opreations defined in symmop.dat file.
    - Input
        - Wannier.in
    - Output

4. 


        - atoms_cart = Amat * atoms_frac
