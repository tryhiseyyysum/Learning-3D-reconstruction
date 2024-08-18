# Occupancy Networks

- **Key idea**
    
    Occupancy networks implicitly represent the 3D surface as the continuous decision boundary of a deep neural network classifier.
    
- Advantages
    1. In contrast to existing approaches, our representation encodes a description of the 3D output
    at infinite resolution without excessive memory footprint.
- Methods
    1. We propose a novel approach to 3D reconstruction based on directly learning the continuous 3D occupancy function
    2. We predict the complete occupancy function with a neural network $f_\theta$
    which can be evaluated at arbitrary resolution.
        
        Occupancy Network Input:
        
        a pair (p,x)
        
        where  $p\in \mathbb{R}^3:3D Location$
        
        $x \in \mathcal{X}: Observation$ (images, point cloud, etc...)
        
        Occupancy Network Output:
        
        a real number (probability)
        
        Occupancy Network: $f_\theta:\mathbb{R}^3 \times \mathcal{X} \rightarrow [0,1]$
        
    3. Sampling scheme
        
        Sampling uniformly inside the bounding box of the object with an additional small padding yields the best results.
        
    4. Mesh Representation
        
        { $p \in \mathbb{R}^3 | f_\theta(p,x)=\tau$ }
        
        The threshold $\tau$ is the only hyperparameter of  occupancy network.
        It determines the “thickness” of the extracted 3D surface.
        
        How to choose $\tau$ ?
        
        ——cross-validate this threshold on a validation set.
        
    5.  Occupancy Network (Onet)：FCN+5 ResNet blocks +（batch normalization）
        
        Different input, different encoders:
        
        3D reconstruction:     ResNet18 architecture
        point clouds:                  PointNet encoder
        voxelized inputs:         3D CNN
        unconditional mesh generation: PointNet
        
    
- Related works
    - Voxel Representations
        
        Drawback: 
        
        1. High memory requirements & computational consuming
    - Point Representations
        
        Drawback: 
        
        1. Requires additional non-trivial post-processing steps to generate the final 3D mesh.
    - Mesh Representations
        
        Drawbacks：
        
        1. Most of these approaches are prone to generating self-intersecting meshes. 
        2. Moreover, they are only able to generate meshes with simple topology, require a reference template from the same object class or cannot guarantee closed surfaces
        
        Ours:
        
        1. In contrast to the aforementioned approaches, our approach leads to high resolution closed surfaces without self-intersections and does not require template meshes from the same object class as input.
        
    
-