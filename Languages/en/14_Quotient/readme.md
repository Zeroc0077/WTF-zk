# WTF Tutorial 14: Normal Subgroups and Quotient Groups

In the previous tutorial, we discussed cosets, which are generated by the subgroup and the operation of elements, but not a group itself. However, when a subgroup satisfies certain properties, the cosets can form a group. Such a subgroup that satisfies these properties is called a normal subgroup, and the group formed by the cosets is called a quotient group. In this tutorial, we will dive deeper into them.

## 1. Normal Subgroups

A normal subgroup is a special type of subgroup in group theory, where the left cosets and right cosets are the same set.

Definition: Given a group G and its subgroup H, if for any g in G, gH = Hg (left coset equals right coset), then H is a normal subgroup of G, denoted as H ⊲ G.

This definition is sometimes written as gHg⁻¹ = H. The operation like aXa⁻¹ is also called conjugation, in other words, a normal subgroup is a subgroup that remains unchanged under conjugation. For any element h in the normal subgroup H and any g in G, ghg⁻¹ ∈ H holds.

Any group G has two trivial normal subgroups: {e} and G.

Most common subgroups in cryptography are essentially normal subgroups. For example, the additive group of integers Z, any subgroup of it, nZ = {..., -2n, -n, 0, n, 2n, ...}, is a normal subgroup. This is because for any integer k and nZ, the left cosets produced by addition are equal to the right cosets, k+nZ = nZ + k. Another example is the multiplicative group of integers modulo 5. Since multiplication is commutative, its left cosets are also equal to the right cosets, and any subgroup is a normal subgroup.

## 2. Quotient Groups

When a subgroup is a normal subgroup, the cosets it generates can form a group, which is called a quotient group.

Definition: Given a group (G, 🐔) and its normal subgroup H, the quotient group (G/H, 🐶) (read as G mod H). The set of the quotient group is formed by all the left cosets, G/H = {gH | g ∈ G}, and the operation 🐶 on the quotient group is defined between two cosets. For g₁, g₂ ∈ G, (g₁H) 🐶 (g₂H) = (g₁🐔g₂)H.

The quotient group is different from the groups we are familiar with. Each element is a left coset in the form of gH, not a number. You can think of the operation 🐶 as an operation between cosets, (g₁H) 🐶 (g₂H) = g₁Hg₂H. When the subgroup is a normal subgroup, the operation 🐶 is well-defined, and we have g₁Hg₂H = g₁(Hg₂)H = g₁g₂HH = g₁g₂H. For simplicity, we will omit the 🐶 operation and write it as (g₁H)(g₂H).

Next, let's check if the quotient group satisfies the four basic properties of a group:

1. Closure: According to the definition, for any g₁H, g₂H ∈ G/H, (g₁H)(g₂H) = (g₁g₂)H. Since g₁g₂ ∈ G, g₁g₂H ∈ G/H, closure holds.

2. Associativity: For any g₁H, g₂H, g₃H ∈ G/H, [(g₁H)(g₂H)](g₃H) = [(g₁g₂)H](g₃H) = (g₁g₂g₃)H, while (g₁H)[(g₂H)(g₃H)] = (g₁H)[(g₂g₃)H] = (g₁g₂g₃)H. Therefore, [(g₁H)(g₂H)](g₃H) = (g₁H)[(g₂H)(g₃H)], associativity holds.

3. Identity element: H is the identity element of G/H. Since the identity element of the group G is e, we have eH = H as a coset of H, so H ∈ G/H. For any gH ∈ G/H, gHH = gH, so H is the identity element of G/H.

4. Inverse element: For any gH ∈ G/H, the inverse element of gH is g⁻¹H. Because (gH)(g⁻¹H) = (gg⁻¹)H = H.

After verification, the quotient group satisfies the four basic properties of a group, so it is indeed a group. Now, let's look at the order (number of elements) of the quotient group. Since the quotient group is a group composed of cosets, its order is the number of left cosets. According to Lagrange's theorem:

|G/H| = [G:H] = [G]/[H]

We can see that the order of the quotient group is the quotient of the order of the parent group and the order of the subgroup, which is why it is called a "quotient group".

### 2.1 Examples

First, let's take the additive group of integers Z and the normal subgroup nZ as an example. The quotient group is Z/nZ.

- In the quotient group, the coset k + nZ represents all integers that are congruent to k modulo n. The order of this quotient group is n, and the elements are 0 + nZ, 1 + nZ, ..., (n-1) + nZ. The essence of this quotient group is the residue group modulo n.

- The operation in the quotient group is defined as (a + nZ) 🐶 (b + nZ) = (a+b) + nZ, still belonging to Z/nZ.

- Identity element: 0 + nZ.

- Inverse element: The inverse element of k + nZ is -k + nZ.

Next, let's take the multiplicative group of integers modulo 5, Z₅\*, and the normal subgroup H = {1,4} as an example.

- The quotient group is Z₅\*/H = {{1,4}, {2,3}}, of order 2 = 4/2.

- Since our example is a multiplicative group, the operation between quotient groups is also the modulo 5 multiplication between cosets.

- Identity element: {1,4}, because {1,4} 🐶 {1,4} = {1 × 1, 1 × 4, 4 × 1, 4 × 4} = {1,4}, while {1,4} 🐶 {2,3} = {2,3}.

- Inverse element: The inverse element of {1,4} is {1,4}, and the inverse element of {2,3} is {2,3}.

## 3. Quotient Groups and Congruence Relations

In the previous tutorial, we used cosets to extend the congruence relations of integers to groups, forming a special type of equivalence relation: For a group G and its subgroup H, if elements a and b belong to the same coset of H, we say a and b are congruent modulo H, denoted as a ≡ b (mod H). In the quotient group, this congruence relation is even more special:

1. Closure: Since the quotient group is a group formed by cosets of a normal subgroup, the operation is well-defined. For elements a, b, c, d in group G and the normal subgroup H, if a ≡ b (mod H) and c ≡ d (mod H), then ac ≡ bd (mod H).

2. Each element in the quotient group represents an equivalence class in the group: The quotient group G/H is a simplification of the group G. Each element in the quotient group is a coset and retains the operation of the group G. Through the congruence relation, each element in the quotient group represents an equivalence class in the group.

We will discuss the good properties of quotient groups when introducing homomorphisms and isomorphisms in the next tutorial.

## 4. Summary

In this tutorial, we introduced the two important concepts in group theory: normal subgroups and quotient groups. A normal subgroup is a special type of subgroup, where the left cosets and right cosets generated are the same, gH = Hg. Most common subgroups in cryptography satisfy this property. When a subgroup is a normal subgroup, the originally just a set of cosets can form a group, which is called a quotient group. You can think of the quotient group as a kind of residue group, which can help us better understand the structure of groups and can also be used to construct cryptographic algorithms, which we will continue to learn in the future.