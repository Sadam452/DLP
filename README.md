# Discrete Logarithm Problem Solver (Quasi-Polynomial Time)
**The code will be made available in due time**.

This project implements a quasi-polynomial time algorithm for solving the **Discrete Logarithm Problem (DLP)** in finite fields. The algorithm is divided into three key phases: **Polynomial Selection**, **Relation Collection**, and **Recursive Descent**. The field setup includes the base field $${F_q}$$, $$F_{q^2}$$, and $$F_{q^{2^k}}$$, where $${k = q-1}$$.

---

## Table of Contents
1. [Overview](#overview)
2. [Phases of the Algorithm](#phases-of-the-algorithm)
    - [Polynomial Selection](#1-polynomial-selection)
    - [Relation Collection](#2-relation-collection)
    - [Recursive Descent](#3-recursive-descent)
3. [Field Settings](#field-settings)
4. [Generators](#generators)
5. [Running the Code](#running-the-code)
6. [Variables to Modify](#variables-to-modify)
7. [Prerequisites](#prerequisites)
8. [Output Files](#output-files)

---

## Overview

The algorithm solves DLP in the following steps:

1. **Polynomial Selection**: Selects polynomials $${h_0}$$ and $${h_1}$$ such that $${h_1 \cdot X^q - h_0}$$ has an irreducible factor of degree $${k}$$.
2. **Relation Collection**: Constructs a relation matrix and computes discrete logarithms for the factor base.
3. **Recursive Descent**: Computes the discrete logarithm for arbitrary elements using the factor base logarithms.

---

## Phases of the Algorithm

### 1. Polynomial Selection

- **Goal**: Generate polynomials $${h_0}$$ and $${h_1}$$.
- **How it works**:
  - Run `PS120.magma` to generate polynomial pairs $${h_0}$$, $${h_1}$$, and $${m(x)}$$.
  - The file outputs the results in `h0_h1.txt` in the format:
    ```
    h0:value
    h1:value
    m(x):value
    ```

- **Customization**:
  - Adjust the `count` variable in `PS120.magma` to generate a desired number of $${h_0}$$-$${h_1}$$ pairs.

### 2. Relation Collection

- **Goal**: Build a relation matrix and calculate logarithms of factor base elements.
- **Steps**:
  1. Use the generated $${h_0}$$ and $${h_1}$$ as input.
  2. Compute the **factor base** and store it in `colPos.txt`.
  3. Generate the **relation matrix** and save it to `RelationMatrix.txt`.
  4. Solve the matrix to find logarithms of factor base elements, stored in files like `FactorBaseLog<i>.txt`.

- **Important**:
  - The solution may vary across multiple attempts. Select the solution where one entry in the factor base log equals `1`.
  - Use the corresponding entry in `colPos.txt` to determine the generator.

### 3. Recursive Descent

- **Goal**: Compute discrete logarithms for arbitrary elements using factor base logarithms.
- **Steps**:
  - Input the `FactorBaseLog<i>.txt` from the previous phase.
  - Set the variable `factor_base_log := [values from FactorBaseLog<i>.txt]`.
  - Use the generator $${\text{gen} := \text{value from colPos.txt}}$$ at the end of the program to verify the results.
  - Select any polynomial and compute its logarithm.

---

## Field Settings

The algorithm requires setting up fields:
1. **Base field $${F_q}$$**
2. **Field $${F_{q^2}}$$**
3. **Field $${F_{q^{2^k}}}$$, where \( k = q-1 \)**

---

## Generators

Generators are essential for each field:

- **For $${F_{q^{2^k}}}$$**:
  - Run `generator.magma` to compute generators.
  - Results are saved in `generators.txt`.

- **For other fields**:
  - Modify the field size in `generator.magma`:
    - $${F_q}$$: $${ q-1 }$$
    - $${F_{q^2}}$$: $${q^2-1}$$
    - $${F_{q^{2^k}}}$$: $${q^{2^k}-1}$$

---

## Running the Code

### Polynomial Selection
1. Execute `PS120.magma`:
   ```magma
   PS120.magma
   ```
2. Adjust `count` for the number of polynomial pairs.

### Relation Collection
1. Set $${ h_0}$$ and $${h_1}$$ values from `h0_h1.txt` in `RC120.magma`.
2. Execute `RC120.magma`:
   ```magma
   RC120.magma
   ```

### Recursive Descent
1. Input factor base log (`FactorBaseLog<i>.txt`) into the recursive descent phase:
   ```magma
   factor_base_log := [values from FactorBaseLog<i>.txt];
   ```
2. Set the generator at the end of the code for verification:
   ```magma
   gen := <generator from colPos.txt>;
   ```

---

## Variables to Modify

- **Polynomial Selection**:
  - Modify the `count` variable in `PS120.magma` to control the number of $${ h_0- h_1}$$ pairs generated.

- **Relation Collection**:
  - Set:
    ```magma
    h0 := <value from h0_h1.txt>;
    h1 := <value from h0_h1.txt>;
    g2 := <value m(x) from h0_h1.txt>;
    ```

- **Recursive Descent**:
  - Set:
    ```magma
    factor_base_log := [values from FactorBaseLog<i>.txt];
    gen := <value from colPos.txt>;
    ```

---

## Prerequisites

- **Software**: Magma Computational Algebra System.
- Ensure Magma is installed and configured.

---

## Output Files

1. **Polynomial Selection**:
   - `h0_h1.txt`: Contains generated polynomial pairs and irreducible factors.

2. **Relation Collection**:
   - `colPos.txt`: Stores the factor base.
   - `RelationMatrix.txt`: Contains the relation matrix.
   - `FactorBaseLog<i>.txt`: Logs of factor base elements.

3. **Generators**:
   - `generators.txt`: Stores generators for fields.

---

This project demonstrates an efficient, quasi-polynomial time approach for solving the Discrete Logarithm Problem in finite fields. If you have any issues or questions, please refer to the comments in the code or consult the documentation.
