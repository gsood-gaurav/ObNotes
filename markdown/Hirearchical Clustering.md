K-means works best when clusters are
- "round" or spherical
- equally sized
- equally dense
- most dense in the center of the sphere
- no contaminated by noise/outliers

Below fig shows K-means clustering with standardized vs non standardized data.
![[Pasted image 20230518112536.png]]
In Real data we may have
- clusters of arbitrary shape
- clusters of different sizes
- Clusters with different densities
- Some noise and maybe some outliers
![[Pasted image 20230518112447.png]]
Each of above point can be probelmatic for parametric algorithms such as K-means.

Gaussian Mixture can approximate any random distribution arbitrary well![[Pasted image 20230518114932.png]]
yhdbscan