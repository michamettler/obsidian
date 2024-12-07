#machinelearning #sem5 

https://phonosync.github.io/mldm-notes/10_clustering.html

## Definition
**Clustering** is the task of grouping a set of objects in such a way that objects in the same group (called a cluster) are more similar (in some sense) to each other than to the objects in the other groups (clusters).

Given a set of $M$ data points $X=\{x^{(1)}, x^{(2)}, \ldots, x^{(M)}\}$, where each data point consists of n features $x^{(i)} = (x_{1}^{(i)}, \ldots, x_{N}^{(i)}) \in \mathbb{R}^{N}$, and a distance measure $d$, a **clustering** is a collection of subsets of $X$ referred to as _clusters_. The clusters are created with the goal that samples in the same cluster are similar, i.e. have a small distance according to the distance $d$.
![[Pasted image 20241207175337.png#invert]]
## Types

- **Hard clustering**: Each data point is assigned a unique cluster (belongs to one cluster);
- **Soft clustering**: Each data point m is assigned a probability pkm that it belongs to cluster $k$ fpr $k=1:K$
## Hard Clustering Methods
### K-Means
In practice, one will run K-Means clustering algorithm several times with different randomly selected initial centroids, and then choose the _best_ clustering that was obtained as quantified by the potential function.
#### Algorithm
**Input**:
- $X = \{x^{(1)}, \ldots, x^{(M)}\}$ set of $M$ data points
- The number of clusters $K$

**Output**:
- A set of $K$ centroids $\{c_1, \ldots, c_K\}$

**Algorithm**
Specify the number of clusters K Choose K initial centroids $c_1, \ldots, c_K$

REPEAT
- Compute closest centroid $c_k$ for each data point and “assign” data point to that centroid
- FOR EACH centroid $c_k$
    - $A_k$ = set of data points currently assigned to ck
    - $m_k = \frac{1}{|A_k|}\sum_{x^{(m)} \in A_k} x^{(m)}$(mean of all data points in $A_k$)
    - $c_k = m_k$
- END FOR
    
UNTIL stop-criterion is met
RETURN $c_1, \ldots, c_K$ as the centroids of the $K$ clusters

**Distance measure**
$$d(p,q)=\sqrt{\sum_{i = 1}^{N} (q_{i} - p_{i})^{2}}$$
![[Pasted image 20241207194011.png#invert]]
#### Selection of initial centroids
- - _Random points_
- The _Forgy method_ randomly chooses K observations from the dataset and uses these as the initial means;
- The _Random Partition_ method first randomly assigns a cluster to each observation and then proceeds to the update step, thus computing the initial mean to be the centroid of the cluster’s randomly assigned points
- K-means++
#### Stop-Criterion
- Stop when the centroids do not change anymore
- Stop when the coordinates of the centroids change only very little from one iteration to the next
- Stop when only very few data points are re-assigned to a different centroid in a new iteration.
- temibe-boxed (number of iterations or time)
#### Choosing the number of clusters K
The K-means clustering method requires that we specify the total number of clusters $K$.
In most cases unclear:
![[Pasted image 20241207195001.png#invert]]
##### The Elbow Method
n this method, we run K-Means with different values of $K$ and plot the value of the potential function $\Phi$ for each value of $K$ (when it starts to stagnate).
![[Pasted image 20241207195048.png#invert]]
##### The Silhouette Method
$$s_m=\frac{b_m-a_m}{max(b_m, a_m)}$$
Higher values of the Silhouette Score are indicative of better clustering of the target point, -1 in the wrong cluster.
![[Pasted image 20241207195333.png#invert]]
![[Pasted image 20241207195407.png#invert]]
The _Silhouette Method_ computes the average Silhouette score for the clustering results obtained by a target algorithm for range of different values of $K$ and selects the number of clusters $K$ corresponding to the highest average Silhouette score.
![[Pasted image 20241207195501.png#invert]]
Note that the Silhouette Method might not perform as expected for all data shapes (like here):
![[Pasted image 20241207195526.png#invert]]
### DBSCAN
_DBSCAN_ stands for _Density-based Spatial Clustering of Applications with Noise_.
he basic idea of DBSCAN is that clusters form dense regions in the data and are separated by relatively empty areas. Points within a dense region are called core points. DBSCAN identifies points in “densely populated” regions of the feature space in which many data points lie close together.

**Parameters:**
- _minPts_: The minimum number of points (a threshold) clustered together for a region to be considered dense
- $\epsilon$: A distance measure to define the neighborhood of any point.

Using these parameters, we can split up the input datapoints into three types of points depicted:
- _Core point_: has at least _minPts_ points within distance ϵ from itself (e.g. point A)
- _Border point_: has at least one core point within distance ϵ (e.g. point B, C)
- _Noise point_: a point that is neither a core nor a border point (e.g. point N).
![[Pasted image 20241207200228.png#invert]]
#### Algorithm
1. Select an unprocessed point P
2. If P is not a Core Point (i.e. there are less than _minPts_ points within range ϵ), then classify P as noise and go back to Step 1
3. Otherwise, if P is a core point, a new cluster is formed as follows:

- Assign all neighbors of P (i.e. all points within distance ϵ from P) to the new cluster
- Repeat previous assignment step for all newly-assigned neighbors that are core points

4. Go back to Step 1
5. Continue algorithm until all data points have been processed.

**The main advantages of DBSCAN is that we do not need to specify the number of clusters K in advance**.
## Distance Metrics
- The $L_1$ metric, known as the Manhattan distance defined as $d_1(p,q)=\sum_{i}|p_i-q_i|$ and illustrated here:
  ![[Pasted image 20241207200442.png#invert]]
  - The $L_{\inf}$ or the maximum metric defined as $d_{\inf}(p,q)=\max_{i}\{|p_i-q_i|\}$.
  - The Cosine similarity defined as $d_{cos}(p,q)=\frac{\sum_{i=1}^{N}p_iq_i}{\sqrt{\sum_{i=1}^{N}p_{i}^2}\sqrt{\sum_{i=1}^{N}q_{i}^2}}$, quantifies the similarity among two vectors by only accounting for the angle between them and ignoring their lengths.