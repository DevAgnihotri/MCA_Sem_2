# Functional Dependencies and Inference Rules

## What are Functional Dependencies?

A **functional dependency (FD)** is a relationship between two sets of attributes in a database relation. It describes how one set of attributes uniquely determines another set. In other words, if you know the value of one attribute (or a group of attributes), you can determine the value of another attribute (or group of attributes).

**Definition:**

- For a relation R, a functional dependency X → Y means that if two tuples (rows) have the same value for attributes X, they must also have the same value for attributes Y.
- X is called the **determinant**, and Y is the **dependent**.

**Example:**

- If StudentID → Name, then knowing the StudentID, you can uniquely determine the Name.

---

![Armstrong's Axioms](https://media.geeksforgeeks.org/wp-content/uploads/20250422123933036205/axioms.webp)

## Basic Inference Rules (Armstrong's Axioms)

To reason about functional dependencies, we use a set of rules called **Armstrong's Axioms**. These rules help us infer all possible FDs from a given set.

### 1. **Reflexivity Rule**

If Y is a subset of X, then X → Y.

### 2. **Augmentation Rule**

If X → Y, then XZ → YZ (for any set of attributes Z).

### 3. **Transitivity Rule**

If X → Y and Y → Z, then X → Z.

**Additional Derived Rules:**

- **Union:** If X → Y and X → Z, then X → YZ.
- **Decomposition:** If X → YZ, then X → Y and X → Z.
- **Pseudo-Transitivity:** If X → Y and YZ → W, then XZ → W.
- **Composition Rule** If X → Y and B → Z, then XB → YZ.

---

## Example Proof: AD → F

Given:

- R(A, B, C, D, E, F)
- FDs: A → BC, B → E, CD → EF

**To Prove:** AD → F

### Step-by-Step Solution

1. **List the FDs:**

   - A → BC
   - B → E
   - CD → EF

2. **Find the closure of AD (AD⁺):**

   - Start with AD = {A, D}

3. **Apply FDs to AD:**

   - A → BC: Since A is in AD, add B and C. Now we have {A, D, B, C}
   - B → E: B is now in the set, so add E. Now we have {A, D, B, C, E}
   - CD → EF: C and D are in the set, so add E and F. Now we have {A, D, B, C, E, F}

4. **Check if F is in AD⁺:**
   - Yes, F is in the closure.

**Conclusion:**

- Since F is in the closure of AD, **AD → F** holds.

---

## Summary Table

| Given FDs | Closure Steps for AD | Resulting Attributes |
| --------- | -------------------- | -------------------- |
| A → BC    | AD + BC              | A, D, B, C           |
| B → E     | + E                  | A, D, B, C, E        |
| CD → EF   | + F (and E again)    | A, D, B, C, E, F     |

**Therefore, AD → F is a valid functional dependency in R.**

---

## Normal Forms in Database Design (Normalization)

Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity. It involves dividing large tables into smaller ones and defining relationships between them. Normal forms are a series of guidelines to achieve this.

### 1. **First Normal Form (1NF)**

A relation is in **1NF** if:

- All attributes contain only atomic (indivisible) values.
- Each column contains values of a single type.
- Each row is unique, identified by a primary key.

**Example:**

| StudentID | Name  | Subjects         |
| --------- | ----- | ---------------- |
| 1         | Alice | Math, Science    |
| 2         | Bob   | English, History |

**Problem:** The `Subjects` column contains multiple values, violating 1NF.

**Solution (1NF):**

| StudentID | Name  | Subject |
| --------- | ----- | ------- |
| 1         | Alice | Math    |
| 1         | Alice | Science |
| 2         | Bob   | English |
| 2         | Bob   | History |

---

### 2. **Second Normal Form (2NF)**

A relation is in **2NF** if:

- It is in 1NF.
- If in a Realtion all Condidate keys are simple cand. keys
- All non-prime attributes are fully functionally dependent on the primary key (no partial dependency(NP depends on NP)).

**Example:**

| OrderID | ProductID | ProductName | Quantity |
| ------- | --------- | ----------- | -------- |
| 1       | 101       | Pen         | 10       |
| 1       | 102       | Notebook    | 5        |

**Problem:** `ProductName` depends only on `ProductID`, not the full composite key (`OrderID, ProductID`).

**Solution (2NF):**

**Orders Table:**

| OrderID | ProductID | Quantity |
| ------- | --------- | -------- |
| 1       | 101       | 10       |
| 1       | 102       | 5        |

**Products Table:**

| ProductID | ProductName |
| --------- | ----------- |
| 101       | Pen         |
| 102       | Notebook    |

---

### 3. **Third Normal Form (3NF)**

A relation is in **3NF** if:

- It is in 2NF.
- There are no transitive dependencies (non-prime attributes depend only on the primary key).
- A relation in which all attribute are key or prime attribute then in 3NF
- if a PA -> PA trans. is ignored, what's not allowed is NPA -> PA

**Example:**

| EmployeeID | DepartmentID | DepartmentName |
| ---------- | ------------ | -------------- |
| 1          | 10           | HR             |
| 2          | 20           | IT             |

**Problem:** `DepartmentName` depends on `DepartmentID`, not directly on `EmployeeID`.

**Solution (3NF):**

**Employees Table:**

| EmployeeID | DepartmentID |
| ---------- | ------------ |
| 1          | 10           |
| 2          | 20           |

**Departments Table:**

| DepartmentID | DepartmentName |
| ------------ | -------------- |
| 10           | HR             |
| 20           | IT             |

---

### 4. **Boyce-Codd Normal Form (BCNF)**

A relation is in **BCNF** if:

- It is in 3NF.
- Every determinant is a candidate key.

**Example:**

| StudentID | CourseID | Instructor |
| --------- | -------- | ---------- |
| 1         | C101     | Prof. A    |
| 2         | C102     | Prof. B    |

**Problem:** `Instructor` depends on `CourseID`, not `StudentID`.

**Solution (BCNF):**

**Enrollments Table:**

| StudentID | CourseID |
| --------- | -------- |
| 1         | C101     |
| 2         | C102     |

**Courses Table:**

| CourseID | Instructor |
| -------- | ---------- |
| C101     | Prof. A    |
| C102     | Prof. B    |

---

### Summary of Normal Forms

| Normal Form | Key Requirement                                                                 |
| ----------- | ------------------------------------------------------------------------------- |
| 1NF         | Atomic values in attributes, unique rows.                                       |
| 2NF         | No partial dependency (non-prime attributes depend on the whole primary key).   |
| 3NF         | No transitive dependency (non-prime attributes depend only on the primary key). |
| BCNF        | Every determinant is a candidate key.                                           |

By applying these normal forms, databases become more efficient, consistent, and easier to maintain.

## Multivalued Dependency (MVD)

A **multivalued dependency (MVD)** is a type of database constraint that occurs when one attribute in a relation uniquely determines a set of values for another attribute, independent of all other attributes. It represents a situation where two attributes are independent of each other but are both dependent on a third attribute.

### Definition:

For a relation `R`, a multivalued dependency `X ↠ Y` exists if, for every pair of tuples in `R` that agree on `X`, their values for `Y` can be swapped to produce new valid tuples, while keeping the rest of the attributes unchanged.

### Example:

Consider a relation `R(StudentID, Course, Hobby)`:

| StudentID | Course  | Hobby    |
| --------- | ------- | -------- |
| 1         | Math    | Painting |
| 1         | Science | Painting |
| 1         | Math    | Reading  |
| 1         | Science | Reading  |

Here:

- `StudentID ↠ Course`: A student can take multiple courses.
- `StudentID ↠ Hobby`: A student can have multiple hobbies.

The courses and hobbies are independent of each other but are both dependent on `StudentID`. This is a multivalued dependency.

### Properties of MVD:

1. If `X → Y`, then `X ↠ Y` (every functional dependency is also a multivalued dependency).
2. MVDs are used to identify relations that are not in **Fourth Normal Form (4NF)**.

### Resolving MVDs:

To eliminate multivalued dependencies and achieve 4NF, decompose the relation into smaller relations such that each relation contains only one multivalued dependency.

#### Decomposition Example:

Given the relation `R(StudentID, Course, Hobby)`:

1. Decompose into two relations:

- `R1(StudentID, Course)`
- `R2(StudentID, Hobby)`

2. The resulting relations are in 4NF, as they no longer have multivalued dependencies.

---

### Summary:

| Dependency Type        | Description                                                                  |
| ---------------------- | ---------------------------------------------------------------------------- |
| Functional Dependency  | One attribute uniquely determines another.                                   |
| Multivalued Dependency | One attribute determines a set of values for another, independent of others. |

By resolving MVDs, we ensure the database is free from redundancy and anomalies, improving its efficiency and consistency.

## Inclusion Dependence

**Inclusion Dependence** is a constraint in relational databases that ensures a relationship between two relations by requiring that certain values in one relation must also appear in another. It is often used to enforce referential integrity.

### Definition:

If we have two relations R and S, and attributes A in R and B in S, then an inclusion dependency R[A] ⊆ S[B] means that every value of A in R must also be a value of B in S.

### Example:

Consider the following relations:

**Students Table:**

| StudentID | Name  |
| --------- | ----- |
| 1         | Alice |
| 2         | Bob   |

**Enrollments Table:**

| StudentID | CourseID |
| --------- | -------- |
| 1         | C101     |
| 2         | C102     |

Here, the `StudentID` in the `Enrollments` table must match a `StudentID` in the `Students` table. This is an inclusion dependency that ensures referential integrity.

---

## Lossless Join Decomposition

A **lossless join decomposition** is a property of database decomposition that ensures no information is lost when a relation is decomposed into two or more smaller relations. This is crucial for maintaining the integrity of the original data.

### Definition:

A decomposition of a relation R into sub-relations R1 and R2 is **lossless** if the natural join of R1 and R2 results in the original relation R.

### Conditions for Lossless Join:

For a decomposition of R into R1 and R2 to be lossless, following conditions must hold:

- The common attributes (R1 ∩ R2) must be a superkey for R1 or R2.

### Example:

Consider the relation R(A, B, C) with the functional dependency A → B. Decompose R into:

- R1(A, B)
- R2(A, C)

The common attribute is A, which is a superkey for R1. Therefore, the decomposition is lossless.

#### Verification:

Original relation R:

| A   | B   | C   |
| --- | --- | --- |
| 1   | X   | Y   |
| 2   | W   | Z   |

Decomposed relations:

**R1:**

| A   | B   |
| --- | --- |
| 1   | X   |
| 2   | W   |

**R2:**

| A   | C   |
| --- | --- |
| 1   | Y   |
| 2   | Z   |

Natural join of R1 and R2:

| A   | B   | C   |
| --- | --- | --- |
| 1   | X   | Y   |
| 2   | W   | Z   |

The natural join restores the original relation, confirming a lossless decomposition.

---

### Importance of Lossless Join Decomposition:

1. **Data Integrity:** Ensures no data is lost during decomposition.
2. **Normalization:** Helps in achieving higher normal forms without redundancy.
3. **Query Accuracy:** Guarantees that queries on decomposed relations yield correct results.

By ensuring inclusion dependence and lossless join decomposition, databases maintain consistency, integrity, and efficiency.

---

Sure! Let's break it down simply:

---

### What is a **lossless decomposition**? (again)

- When you split a big table (relation) into smaller tables (relations), you want to be able to join them back **without losing any information**.
- If after joining the smaller tables, you get exactly the same data as the original table, the decomposition is called **lossless** or **lossless-join**.
- If some information is lost or extra rows appear after joining, the decomposition is **lossy**.

---

### Given:

- Relation $R(A, B, C, D, E, F)$

- Functional Dependencies (FDs):

  - $AB \to C$
  - $C \to A$
  - $D \to E$
  - $F \to A$
  - $E \to D$

- Decomposition:

  - $R_1 (A, C, D)$
  - $R_2 (B, C, D)$
  - $R_3 (E, F, D)$

---

### How to check if the decomposition is lossless?

- For lossless decomposition, **at least one of the intersections of decomposed relations should functionally determine one of those relations**.

- Check the intersections:

  - $R_1 \cap R_2 = \{ C, D \}$
  - $R_2 \cap R_3 = \{ D \}$
  - $R_1 \cap R_3 = \{ D \}$

- Check if the attributes in the intersection functionally determine either $R_1, R_2,$ or $R_3$ using the FDs.

---

### Step 1: Look at $R_1 \cap R_2 = \{ C, D \}$

- Does $C, D \to R_1$ or $R_2$?

- $R_1 = \{ A, C, D \}$

- We want to check if $CD \to A, C, D$ or at least $CD \to A$.

- Given $C \to A$, and $D \to E$ (not relevant here), so:

- From $C \to A$, $C$ alone determines $A$, so $CD \to A$ is true.

- Since $CD \to A$, and $A, C, D$ is $R_1$, so $CD \to R_1$.

---

### Step 2: Conclusion

- Since $R_1 \cap R_2 = \{ C, D \}$ and $CD \to R_1$, the decomposition is **lossless**.

---

### **Summary:**

- Lossless means: After splitting, you can join tables back without losing data.
- Check if intersection attributes determine one relation.
- Here, $C, D$ (intersection of $R_1$ and $R_2$) determines all of $R_1$.
- So, **the decomposition is lossless**.

---

## Partial Functional Dependency and Anomalies

### What is Partial Functional Dependency?

A **partial functional dependency** occurs in a relation when a non-prime attribute (an attribute that is not part of any candidate key) is functionally dependent on a part (proper subset) of a candidate key(i.e. Prime attribute), rather than the whole candidate key.

**Example:**
**Example:**

Consider a relation `R(A, B, C, D)` with the functional dependency `A → B`:

- Here, `B` is partially dependent on `A` because `A` is a part of the candidate key `(A, C)`.
- This partial dependency violates 2NF.

To resolve this, decompose `R` into two relations:

1. `R1(A, B)` where `A → B`
2. `R2(A, C, D)` where `(A, C)` is the candidate key.

This decomposition removes the partial dependency and ensures the relation is in 2NF.

Consider a relation `Student_Course (StudentID, CourseID, Instructor, CourseName)` where the candidate key is (StudentID, CourseID):

- `CourseName` depends only on `CourseID` (not on the full key).
- This is a partial dependency because `CourseName` is determined by part of the candidate key.

---

### Anomalies Due to Partial Dependency

When a relation has partial dependencies, it can lead to several types of anomalies:

#### 1. Insertion Anomaly

- **Problem:** You cannot insert information about a course unless a student is also enrolled in it.
- **Example:** If you want to add a new course to the database but no student has enrolled yet, you cannot insert the course name and instructor without a StudentID.

#### 2. Update Anomaly

- **Problem:** If you need to update information about a course (like the instructor), you must update it in every row where that course appears.
- **Example:** If the instructor for a course changes, you have to update the instructor's name for every student enrolled in that course. If you miss any row, the data becomes inconsistent.

#### 3. Deletion Anomaly

- **Problem:** Deleting a student's enrollment in a course might remove all information about the course itself.
- **Example:** If the last student enrolled in a course drops it and you delete that row, you also lose the course name and instructor information from the database.

---

### Technical Explanation

- **Partial dependency** violates the rules of Second Normal Form (2NF).
- To avoid these anomalies, relations should be decomposed so that non-prime attributes are fully functionally dependent on the whole candidate key (i.e., the relation should be in 2NF).

---

### Summary Table

| Anomaly Type      | Description                                                         | Example Scenario                                              |
| ----------------- | ------------------------------------------------------------------- | ------------------------------------------------------------- |
| Insertion Anomaly | Cannot insert course info without a student enrolled                | Can't add new course unless a student is enrolled             |
| Update Anomaly    | Must update course info in multiple rows; risk of inconsistency     | Instructor change must be updated for every student in course |
| Deletion Anomaly  | Deleting last student in a course removes all info about the course | Lose course info if last student drops the course             |

### What is Pseudo-Transitivity?

**Pseudo-transitivity** is a property of functional dependencies that allows us to infer new dependencies when combining existing ones. It is an extension of the transitivity rule.

#### Definition:

If we have the following functional dependencies:

1. `X → Y`
2. `YW → Z`

Then, by pseudo-transitivity, we can infer:

- `XW → Z`

#### Explanation:

- `X → Y` means that `X` determines `Y`.
- `YW → Z` means that the combination of `Y` and `W` determines `Z`.
- Therefore, if `X` determines `Y` and `YW` determines `Z`, then `XW` (combining `X` and `W`) determines `Z`.

#### Example:

Consider a relation `R(A, B, C, D)` with the following functional dependencies:

1. `A → B`
2. `BC → D`

Using pseudo-transitivity:

- From `A → B` and `BC → D`, we can infer `AC → D`.

#### Importance:

Pseudo-transitivity is useful for reasoning about functional dependencies and simplifying the process of finding closures or verifying normalization.

---

### Summary:

| Rule                | Description                             |
| ------------------- | --------------------------------------- |
| Transitivity        | If `X → Y` and `Y → Z`, then `X → Z`.   |
| Pseudo-Transitivity | If `X → Y` and `YW → Z`, then `XW → Z`. |

Pseudo-transitivity helps in deriving new functional dependencies, which is essential for database design and normalization.

### What is Transitive Functional Dependency?

A **transitive functional dependency** occurs when a non-prime attribute is functionally dependent on another non-prime attribute, which in turn is dependent on a candidate key. This creates an indirect dependency on the candidate key.

**Example:**

Consider a relation `R(A, B, C)` with the functional dependencies:

- `A → B`
- `B → C`

Here, `C` is transitively dependent on `A` through `B`. This violates the rules of Third Normal Form (3NF).

---

### Anomalies Due to Transitive Dependency

When a relation has transitive dependencies, it can lead to the following anomalies:

#### 1. Insertion Anomaly

- **Problem:** You cannot insert information about a dependent attribute(or can also be said as, an attribute) unless the related non-prime attribute is also known.
- **Example:** In the relation `R(A, B, C)`, you cannot insert a value for `C` unless a corresponding value for `B` is also provided.

#### 2. Update Anomaly

- **Problem:** Updating a value for a non-prime attribute may require multiple rows to be updated, leading to inconsistency.
- **Example:** If the value of `B` changes, you must update all rows where `B` determines `C`. Missing any row will result in inconsistent data.

#### 3. Deletion Anomaly

- **Problem:** Deleting a row may result in the loss of information about a dependent attribute.
- **Example:** If you delete a row containing a specific value of `B`, you may lose all information about the corresponding value of `C`.

---

### Resolving Transitive Dependency

To eliminate transitive dependencies, decompose the relation into smaller relations that satisfy 3NF. This ensures that non-prime attributes depend only on candidate keys.

**Example Decomposition:**

Given the relation `R(A, B, C)` with the dependencies `A → B` and `B → C`:

1. Decompose into two relations:

- `R1(A, B)` with `A → B`
- `R2(B, C)` with `B → C`

2. This eliminates the transitive dependency, as `C` now directly depends on `B` in `R2`.

---

### Summary Table

| Anomaly Type      | Description                                                             | Example Scenario                                      |
| ----------------- | ----------------------------------------------------------------------- | ----------------------------------------------------- |
| Insertion Anomaly | Cannot insert dependent attribute without related non-prime attribute   | Can't insert `C` without `B`                          |
| Update Anomaly    | Must update dependent attribute in multiple rows; risk of inconsistency | Changing `B` requires updating all rows where `B → C` |
| Deletion Anomaly  | Deleting a row may remove information about dependent attributes        | Deleting `B` may lose all info about `C`              |

By resolving transitive dependencies, the database becomes more consistent and easier to maintain.

---

## Dependency Preserving Decomposition

A decomposition of a relation is said to be **dependency preserving** if all the functional dependencies in the original relation can be enforced by simply enforcing the functional dependencies in the decomposed relations, without the need to compute a join of the relations.

### Why is Dependency Preservation Important?

Dependency preservation ensures that the constraints (functional dependencies) of the original relation are not lost during decomposition. This is crucial for maintaining the integrity of the data.

---

### How to Check Dependency Preservation?

To check if a decomposition is dependency preserving:

1. **Decompose the Relation:** Decompose the original relation into smaller relations based on the functional dependencies.
2. **Project FDs onto Decomposed Relations:** For each decomposed relation, find the functional dependencies that hold in that relation.
3. **Combine Projected FDs:** Take the union of all the functional dependencies from the decomposed relations.
4. **Compare with Original FDs:** Check if the closure of the combined functional dependencies is equal to the closure of the original functional dependencies. If they are equal, the decomposition is dependency preserving.

---

### Example

#### Given:

- Relation: `R(A, B, C, D)`
- Functional Dependencies (FDs):
  - `A → B`
  - `B → C`
  - `A → D`

#### Decomposition:

Decompose `R` into two relations:

1. `R1(A, B, D)`
2. `R2(B, C)`

#### Step 1: Project FDs onto Decomposed Relations

- For `R1(A, B, D)`:

  - `A → B` (from the original FDs)
  - `A → D` (from the original FDs)

- For `R2(B, C)`:
  - `B → C` (from the original FDs)

#### Step 2: Combine Projected FDs

Combine the FDs from `R1` and `R2`:

- `A → B`
- `A → D`
- `B → C`

#### Step 3: Compare with Original FDs

The closure of the combined FDs (`A → B`, `A → D`, `B → C`) is the same as the closure of the original FDs (`A → B`, `B → C`, `A → D`). Therefore, the decomposition is **dependency preserving**.

---

### Key Points:

- Dependency preservation ensures that all functional dependencies can be enforced without recombining the decomposed relations.
- A decomposition that is not dependency preserving may require additional joins to enforce the original constraints, which can be inefficient.

By ensuring dependency preservation, we maintain the integrity of the database while optimizing its structure.

# Question 1

## Checking 2NF for Relation R(P, Q, R, S, T)

### Given:

- Relation: `R(P, Q, R, S, T)`
- Functional Dependencies (FDs):
  - `PQ → R`
  - `S → T`

### Step 1: Identify Candidate Key(s)

To determine if the relation is in 2NF, we first identify the candidate key(s).

- From `PQ → R`, we know `PQ` determines `R`.
- From `S → T`, we know `S` determines `T`.
- To cover all attributes (`P, Q, R, S, T`), the candidate key is `{P, Q, S}`.

### Step 2: Check for Partial Dependencies

A relation is in 2NF if:

1. It is in 1NF.
2. There are no partial dependencies (i.e., no non-prime attribute is dependent on a proper subset of a candidate key).

#### Prime Attributes:

- Attributes that are part of any candidate key: `P, Q, S`.

#### Non-Prime Attributes:

- Attributes that are not part of any candidate key: `R, T`.

#### Check Dependencies:

- `PQ → R`: `R` is a non-prime attribute, and `PQ` is a proper subset of the candidate key `{P, Q, S}`. **This is a partial dependency.**
- `S → T`: `T` is a non-prime attribute, and `S` is a proper subset of the candidate key `{P, Q, S}`. **This is a partial dependency.**

### Conclusion:

The relation `R(P, Q, R, S, T)` is **not in 2NF** because it has partial dependencies.

---

### Step 3: Convert to 2NF

To convert the relation into 2NF, we remove the partial dependencies by decomposing the relation.

#### Decomposition:

1. Create a relation for each partial dependency:

   - For `PQ → R`: Create `R1(P, Q, R)`.
   - For `S → T`: Create `R2(S, T)`.

2. Create a relation for the remaining attributes:
   - `R3(P, Q, S)` (to ensure all candidate keys are preserved).

#### Final Relations:

- `R1(P, Q, R)` with FD: `PQ → R`
- `R2(S, T)` with FD: `S → T`
- `R3(P, Q, S)` (no FDs)

---

### Final 2NF Decomposition:

The decomposed relations are:

1. `R1(P, Q, R)`
2. `R2(S, T)`
3. `R3(P, Q, S)`

These relations are now in 2NF, as there are no partial dependencies.
