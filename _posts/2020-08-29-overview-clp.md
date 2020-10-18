---
layout: post
title: Overview of Container Loading Problem
excerpt: "Staring guide for Container Loading Problem. It covers the basic theoretical concepts to kickstart with this problem."
categories: [Theory, Optimization, Reference]
tags: [CLP, Optimization, Concept]
share: true
comments: true
mathjax: false
---


---

The basic Container Loading Problem can be defined as the problem of placing a set of boxes into the container respecting the geometric constraints and physical world constraints.

## The Problem

The main problem can be either 1D, 2D, 3D or higher-dimensional. But here we will focus on the 3D containers and 3D Pallets.

### Container Loading Problem (CLP)

- **Homogeneous:** All boxes are of the same size
- **Weakly Heterogeneous:** Many identical boxes of the same dimension and some different boxes of a different dimension
- **Strongly Heterogeneous:** All boxes are of different sizes

### Pallet Loading Problem (PLP)

- **Manufacture’s PLP:** Occurs when there are homogeneous boxes to be efficiently placed onto the pallet
- **Distributer’s PLP:** Occurs when it is necessary to stack heterogeneous boxes onto the pallet

Now we breakdown CLP and PLP into multiple type as per their Input minimization and Output maximization.

## Input (value) minimization problem types are the following:

- **Single Stock-Size Cutting Stock Problem (SSSCSP)**
  
  Packing a weakly heterogeneous set of cargo into a minimum number of identical containers.

- **Multiple Stock-Size Cutting Stock Problem (MSSCSP)**
  
  Packing a weakly heterogeneous set of cargo into a weakly heterogeneous assortment of containers such that the value of the used containers is minimized.

- **Residual Cutting Stock Problem (RCSP)**
  
  Packing a weakly heterogeneous set of cargo into a strongly heterogeneous assortment of containers such that the value of the used containers is minimized.

- **Single Bin-Size Bin Packing Problem (SBSBPP)**
  
  Packing a strongly heterogeneous set of cargo into a minimum number of identical containers.

- **Multiple Bin-Size Bin Packing Problem (MBSBPP)**
  
  Packing a strongly heterogeneous set of cargo into a weakly heterogeneous assortment of containers such that the value of the used containers is minimized.

- **Residual Bin Packing Problem (RBPP)**
  
  Packing a strongly heterogeneous set of cargo into a strongly heterogeneous assortment of containers such that the value of the used containers is minimized.

- **Open Dimension Problem (ODP)**
  
  Packing a set of cargo into a single container with one or more variable dimensions such that the container volume is minimized.
  - Weakly Heterogeneous assortment of cargo (ODP/W)
  - Strongly Heterogeneous assortment of cargo (ODP/S)

## Output (value) maximization problem types can be distinguished

It is equivalent to the maximization of the container volume utilization if the value of the small items is proportional to their volume.

- **Identical Item Packing Problem (IIPP)**
  Loading a single container with a maximum number of identical small items.

- **Single Large Object Placement Problem (SLOPP)**
  Loading a single container with a selection from a weakly heterogeneous set of cargo such that the value of the loaded items is maximized.

- **Multiple Identical Large Object Placement Problem (MILOPP)**
  Loading a set of identical containers with a selection from a weakly heterogeneous set of cargo such that the value of the loaded items is maximized.

- **Multiple Heterogeneous Large Object Placement Problem (MHLOPP)**
  Loading a (weakly or strongly) heterogeneous set of containers with a selection from a weakly heterogeneous set of cargo such that the value of the loaded items is maximized.

- **Single Knapsack Problem (SKP)**
  Loading a single container with a selection from a strongly heterogeneous set of cargo such that the value of the loaded items is maximized.

- **Multiple Identical Knapsack Problem (MIKP)**
  Loading a set of identical containers with a selection from a strongly heterogeneous set of cargo such that the value of the loaded items is maximized.

- **Multiple Heterogeneous Knapsack Problem (MHKP)**
  Loading a set of (weakly or strongly) heterogeneous containers with a selection from a strongly heterogeneous set of cargo such that the value of the loaded items is maximized.

Next we will talk about some of the common and uncommon Constraints for the problem.

## The Constraints

### Basic Constraints

These constraints are common to all type of optimization problem regarding 3D Container Optimization.
1. Boxes may only be placed with their edges parallel to the walls of the container
2. All boxes must be placed within the container
3. Boxes may not intersect each other

Apart from these basic constraints, there is a multitude of practical considerations as well which are considered as well.

### Container- related constraints

- Weight limits
- Weight distribution constraints


### Item-related constraints

- Loading priorities
- Orientation constraints
  - Case 1: Only a single orientation is permitted for each box (type) in both vertical and horizontal direction, i.e. the boxes cannot be rotated
  - Case 2: Only a single vertical orientation is permitted for each box (type) while no restriction is given with respect to their horizontal direction
  - Case 3: There is no general restriction with respect to the orientation of the boxes in a vertical direction. However, up to two vertical orientations may be prohibited for each box (type). In the horizontal direction, the orientation is free, but – due to the limitation to orthogonal patterns – boxes can be rotated in steps of 90 degree
  - Case 4: There is no general restriction with respect to the orientation of the boxes in both vertical and horizontal direction. However, up to five orientations may be prohibited for each box (type). This case includes the largest variety of different orientation constraints
  - Case 5: There exists no constraint with respect to the orientation of the boxes, neither in vertical nor in the horizontal orientation. All boxes are free rotatable
- Stacking constraints
  Non-fragile boxes can only be placed on other non-fragile ones, but not on fragile ones, while fragile boxes can be put on non-fragile and other fragile ones
- Cargo-related constraints
  - Complete-shipment constraints
  - Allocation constraints
- Positioning constraints
- Load-related constraints
  - Stability constraints
  - Complexity constraints: Complex loading patterns, on one hand, may not be acceptable for manual container loading because such patterns cannot always be visualized in a way that they are understood properly by the loading personnel and their implementation may be too time consuming. More advanced mechanic and automatic packing/loading technologies, on the other hand, are not always suitable for complex cargo arrangements and may necessitate the involvement of additional, cost-intensive labour.

## References

- [Link 1](https://www.scielo.br/scielo.php?script=sci_arttext&pid=S0101-74382015000100001#:~:text=The%20basic%20Container%20Loading%20Problem%20can%20be%20defined%20as%20the,the%20dimensions%20of%20the%20container.)
- [Link 2](https://dialnet.unirioja.es/descarga/articulo/5403327.pdf)
- [Link 3](https://eprints.soton.ac.uk/364226/1/A%2520Comparative%2520Review%2520of%25203D%2520Container%2520Loading%2520Algorithms.pdf)
- [Link 4](https://www.sciencedirect.com/science/article/abs/pii/S037722171200937X?via%3Dihub)
  
