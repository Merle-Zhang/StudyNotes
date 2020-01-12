# Logic and Proof





# Linear Algebra

### 1. Vectors and Dot Product

* #### Vector

  * **tuple**: ordered list

* #### Magnitude and Direction

  * **Scalars**: single real numbers
  * **Direction**
  * **Magnitude**: length
    * $ |y|^2 = y_1^2 + y_2^2 + ... + y_n^2 = \sum_{i=1}^n y_i^2 $
    * **Euclidean norm**
  * Two special vectors
    * **zero vector**: **O** $ = (0,0,0) $
    * **unit vectors**: e.g. $\vec w = (0.5, 0.5, -0.5, 0.5)$, $|\vec w| = \sqrt{0.5^2+0.5^2+0.5^2+0.5^2} = 1$
    * For any vector u, unit vector in the same direction as $\frac{\vec u}{|\vec u|}$

* #### Addition and Scalar Multiplication

  * $\vec y + \vec z = (y_1+z_1,y_2+z_2,...,y_n+z_n)$
  * $a\vec y=(ay_1,ay_2,...,ay_n)$
  * **Distance**: $d(\vec u,\vec v)=\sqrt{(u_1-v_1)^2+(u_2-v_2)^2+...+(u_n-v_n)^2}$
  * Triangular inequality: $|\vec{u}+\vec{v}|\leq|\vec{u}|+|\vec{v}|$

* #### The Dot Product

  * $\vec{u}.\vec{v}=(u_1v_2+u_2v_2+...+u_nv_n)$

  * $\vec{u}.\vec{v}=|\vec{u}||\vec{v}|cos\theta$

  * Equals to 1 or -1 when parallel, 0 when **orthogonal**
  * $\theta=arccos(\frac{\vec u.\vec v}{|\vec u||\vec v|})$

  * **Projection**
    * $\vec u.\vec v=arg min_a d(\vec v,a\vec u), |\vec u|=1$
    * $a\vec{u}$, where $a = \vec{u}\vec{v}$, is orthogonal to $(\vec{v}-a\vec{u})$
  * $|\vec{v}|^2=\vec{v}.\vec{v}$
  * $|\vec{u}.\vec{v}|\leq|\vec{u}||\vec{v}|$, **Cauchy-Schwarz inequality**
  * commutative and distributive

### 2. Vector Spaces, Span and Basis

* #### Linear Combinations

  * Set of vectors: $V=\{\vec{v_1},\vec{v_2},\dots,\vec{v_m}\}$,

    Linear Combination over $V$: $\vec{u}=a_1\vec{v_1}+a_2\vec{v_2}+\dots+a_m\vec{v}_m$

* #### Spanning vectors

  * Set of vectors: $s=\{\vec{s_1},\vec{s_2},\dots,\vec{s_m}\}$,

    Span: $Span(S)$: All linear combinations over S

* #### Vectors spaces and subspaces

  * Set of vectors $V$ is a vector space if there exists a set of vectors $S$ such that $V=Span(S)$

* #### (In)dependent vectors

  * Set $U=\{\vec{u_1},\vec{u_2},\dots,\vec{u_m}\}$is **linearly dependent**

    if $\sum_{j=1}^ma_j\vec{u}_j=0 $	$\Rightarrow$	$\vec{u_i}=\sum_{j=1\and j\neq i}^ma_j\vec{u_j}$	($a_1,a_2,\dots,a_m$not all zero)

    i.e. one vector can be written as linear combination of the others

    Otherwise the set is **linearly independent**

* #### Basis vectors and dimension

  * Linearly independent set: **basis set**
  * Number of vectors in basis: **dimension** of subspace
  * $a\vec{v_1}+b\vec{v_2}+c\vec{v_3}\neq0$ except when $a=b=c=0\Rightarrow$Linearly independent

* #### Coordinates and orthonormal bases

  * **Standard basis**: $\{(1,0,0),(0,1,0),(0,0,1)\}$

  * Assume vector represented by linear combination of basis set.

    **Weight** in linear combination → **coordinates** of the vector w.r.t the basis set

  * To get **weights** for given vector: Solve linear equations given by: $\vec{v}=\sum_{i=1}^{m}a_i\vec{b_i}$

  * **Orthonormal**: orthogonal and unit vectors:

    $\vec{v}=\sum_{i=1}^ma_i\vec{b_i}$, 	$\vec{b_i}.\vec{b_j}=0 \forall i\neq j$, 	$\vec{b_i}.\vec{b_i}=1\forall i$

  * **Coordinate** for vector: $a_i=\vec{v}.\vec{b_i}$

    Proof: $\vec{b_j}.\vec{v}=\vec{b_j}.\sum_{i=1}^ma_i\vec{b_i}=\sum_{i=1}^ma_i\vec{b_j}.\vec{b_i}=a_j=\vec{v}.\vec{b_j}$

  * For **orthogonal** basis:

    $\vec{v}=\sum_{i=1}^ma_i\vec{b_i}$, 	$\vec{b_i}.\vec{b_j}=0 \forall i\neq j$, 	$\vec{b_i}.\vec{b_i}=|\vec{b_i}|^2$

    $\Rightarrow$	 $a_i=\frac{\vec{v}.\vec{b_i}}{|\vec{b_i}|^2}=\frac{\vec{v}.\vec{b_i}}{\vec{b_i}.\vec{b_i}}$

  * **Gram-Schmidt orthogonalization**

* #### Projections onto subspaces

  * The vector projection of a vector $\vec{u}$ onto a subspace $V$ is the vector $\vec{u_v}$ such that $\vec{u_v}=argmin_{v\in V}|\vec{v}-\vec{u}|$

    i.e. the 'closest' vector to $\vec{u}$ that is within the subspace $V$

  * Coordinates for vector are scalar projections of vector onto basis vectors.