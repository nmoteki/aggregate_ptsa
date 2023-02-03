# aggregate_ptsa
Polydisperse tunable sequential aggregation (PTSA) method for generating a fractal-like aggregate of spheres

Algorithm reference: 
Singh and Tsotas 2022, https://doi.org/10.1016/j.ces.2021.117022  

The performance of the code written in Python numpy was optimized by the numba-jit. 
The syntax of the function "ptsa" for aggregate generation is defined as follows

    Np_final, xp, rp, V, Rve, Rg, eps_agg = ptsa(Np, mean_rp, rel_std_rp, Df, k, max_search_num, rng)
    
    ==== Input parameters ===
    Np: number of monomers
    mean_rp: mean of the normal distribution of the monomer radius
    rel_std_rp: relative standard deviation of the normal distrituion of the monomer radius 
    Df: fractal dimension
    k: fractal prefactor
    max_search_num: maximum number of iteration for searching a location of each monomer attached onto the surface of an aggregate 
    rng: random number generator constructed by the numpy.random.default_rng()

    === Output variables ===
    Np_final: number of monomers in the generated aggregate. If the aggregate generation failed, Np_final < Np.
    xp: (x,y,z) coordinate of the center of individual monomers relative to the centroid of the aggregate. 2D of shape= (Np,3).
    rp: radii of individual monomers. 1D array of size= Np.
    V: volume of the aggregate.
    Rve: volume-equivalent radius of the aggregate.
    Rg: gyration radius of aggregate.
    eps_agg: porosity of the aggregate calculated using the gyration method (cf. Singh PhD thesis, 2021).

Please see the JupyterNotebook file for an example of usage. N.Moteki tested only k=0.95, and Df= 2.35-2.95, Np=20-16000. 
The code execution might stack depending on the (k, Df)-pair due to the difficulty of finding an attachment condition following the scaling raw.
