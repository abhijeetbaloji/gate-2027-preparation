# ER Model — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

In a Chen-style ER diagram, which symbol denotes a weak entity set?

A. A diamond drawn with a double border
B. A rectangle drawn with a double border
C. An oval drawn with a double border
D. A rectangle drawn with a dashed border

---

## Q2 — MCQ

Every scooter is parked in exactly one bay, and each bay holds at most one scooter. Some bays are empty. There is no descriptive attribute on the relationship Parks. Which description of Parks is correct?

A. One-to-one, with total participation of Scooter and partial participation of Bay
B. One-to-many from Scooter to Bay, with total participation of Bay
C. Many-to-many, with total participation of both entity sets
D. One-to-one, with total participation of both entity sets

---

## Q3 — MCQ

Entity sets Bench and Lamp each have a single-attribute key and no multivalued attributes. Each lamp is fixed to at most one bench, and a bench may have many lamps. The relationship Fixes has no attributes of its own. What is the minimum number of relations in a standard reduction to the relational model?

A. 1
B. 2
C. 3
D. 4

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

Total participation of an entity set E in a relationship R means which of the following?

A. Every entity of E appears in at least one instance of R
B. Every entity of E appears in exactly one instance of R
C. R is necessarily an identifying relationship and E is weak
D. The relational mapping of R must be a separate table

---

## Q5 — MSQ

Which of the following statements are true? Select all that apply.

A. A partial key (discriminator) of a weak entity set is underlined with a dashed line
B. An identifying relationship is drawn as a diamond with a double border
C. In the standard mapping, an identifying relationship with no attributes of its own becomes its own relation
D. The primary key of the relation for a weak entity set includes the primary key of its owner

---

## Q6 — NAT

A schema has three entity sets and two relationships, and no multivalued attributes:

- Depot, with key Did
- Truck, with key Tid. Each truck is assigned to exactly one depot, and a depot may have many trucks. The relationship Assign has no attributes.
- Driver, with key Drid
- Drives, a many-to-many relationship between Driver and Truck, with a single attribute Shift

The minimum number of relations in a standard reduction is ______.

---

## Q7 — MCQ

A binary many-to-many relationship has two attributes of its own. In the standard reduction, that relationship becomes

A. a separate relation whose primary key is the combination of the keys of the two participating entity sets
B. two extra columns, one added to each of the two entity relations, and no new relation
C. a separate relation whose primary key is a fresh surrogate that replaces both entity keys
D. a multivalued attribute of each participating entity set

---

## Level 3 — Multi-Step

The next three questions use this ER description.

- Museum is a strong entity set with attributes Mid (key) and MName.
- Gallery is a weak entity set of Museum, with partial key GNo and attributes Floor and Area. The identifying relationship is Houses. Each gallery belongs to exactly one museum.
- Artist is a strong entity set with attributes Arid (key) and Name.
- Artifact is a strong entity set with attributes Aid (key), Title, and Year, and a multivalued attribute Material.
- Creates: each artifact is created by exactly one artist, and an artist may create many artifacts. Creates has no attributes.
- Displays: each artifact is shown in at most one gallery, and a gallery may show many artifacts. Displays has attribute Since. Some artifacts are in storage and are not shown.

## Q8 — MCQ

How many relations does a standard 1NF reduction of this description produce?

A. 3
B. 4
C. 5
D. 6

---

## Q9 — NAT

How many attributes does the relation that represents Gallery contain? ______

---

## Q10 — MSQ

Which statements about the reduction are true? Select all that apply.

A. The primary key of the Gallery relation is (Mid, GNo)
B. Houses is stored as a relation of its own
C. Material is stored in a separate relation, not as one column of Artifact
D. Since is a column of the Artifact relation

---

## Level 4 — Tricky / Trap-Based

## Q11 — MCQ

Which statement about an identifying relationship I between an owner entity set O and a weak entity set W is true?

A. O must have total participation in I, and W may have partial participation
B. W must have total participation in I, and O may have partial participation
C. Both O and W must have total participation in I
D. Neither O nor W is required to have total participation in I

---

## Q12 — MSQ

Every firm has exactly one chairperson, and a person is chairperson of at most one firm. Some people chair no firm. The relationship Heads has attribute StartYear. Which statements are true? Select all that apply.

A. Heads can be merged into the Firm relation by storing the person's key and StartYear as columns that are not null
B. Total participation of Firm forces Heads to be a separate relation
C. Some persons need not appear in any instance of Heads
D. A one-to-one relationship must be stored as foreign keys in both entity relations

---

## Level 5 — Challenge

## Q13 — NAT

Reduce the following ER description to 1NF relations in the standard way. No attribute is multivalued except Phone.

- Hospital, key Hid, with attributes HName and multivalued Phone
- Ward, a weak entity set of Hospital, partial key WardNo, attributes Wing and Beds. Each ward belongs to exactly one hospital. The identifying relationship has no attributes of its own.
- Doctor, key Did, attributes DName and Rank
- Works, a many-to-many relationship between Doctor and Hospital, with attribute Since
- Patient, key Pid, attribute PName
- Admission, a weak entity set of Patient, partial key AdmNo, attributes AdmitDate and DischargeDate. Each admission belongs to exactly one patient.
- Attends: each admission has exactly one attending doctor, and a doctor may attend many admissions. Attends has no attributes of its own.

The minimum number of relations is ______.

---

## Q14 — MSQ

For the same hospital description, which statements are true? Select all that apply.

A. The primary key of the Admission relation is (Pid, AdmNo)
B. The attending doctor is represented by a foreign key in the Admission relation
C. Works can be represented by placing Hid in the Doctor relation without losing the ability to record a doctor who works at two hospitals
D. Because Phone is multivalued, a 1NF design stores phones in a separate relation

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | B |
| 2 | MCQ | A |
| 3 | MCQ | B |
| 4 | MCQ | A |
| 5 | MSQ | A, B, D |
| 6 | NAT | 4 |
| 7 | MCQ | A |
| 8 | MCQ | C |
| 9 | NAT | 4 |
| 10 | MSQ | A, C, D |
| 11 | MCQ | B |
| 12 | MSQ | A, C |
| 13 | NAT | 7 |
| 14 | MSQ | A, B, D |

## Detailed Solutions

### Q1

Answer: B

A weak entity set is a rectangle with a double border. A double diamond is the identifying relationship, not the weak entity set, so A is the symbol for a different construct. A double oval is sometimes used for a multivalued attribute, not for a weak entity set, so C fails. A dashed underline, not a dashed rectangle, marks the partial key, so D fails.

### Q2

Answer: A

"Exactly one bay per scooter" is total participation of Scooter and cardinality one toward Bay. "At most one scooter per bay" is cardinality one toward Scooter. "Some bays are empty" is partial participation of Bay. Together this is a one-to-one relationship with total participation only on the scooter side.

B reverses both the cardinality reading and which side participates totally. C invents a many-to-many relationship that the "at most one" conditions forbid. D would be right only if every bay contained a scooter.

### Q3

Answer: B

Fixes is many-to-one from Lamp to Bench: many lamps, at most one bench each. A many-to-one relationship with no attributes is a foreign key on the "many" side. Bench and Lamp are the only two relations; Lamp stores the bench key. No third relation is required.

A would collapse two independent entity sets into one. C is the count people get by mapping every relationship to its own table. D would fit a many-to-many relationship plus the two entity sets, which is not this cardinality.

### Q4

Answer: A

Total participation is a minimum of one: no entity of E is left out of R. It says nothing about the maximum. Exactly one participation needs total participation and a cardinality of one together, so B adds a restriction the term does not have. Total participation does not make an entity weak and does not make the relationship identifying, so C fails. A many-to-one relationship with total participation on the "many" side is still only a foreign key, so D fails.

### Q5

Answer: A, B, D

The partial key is a dashed underline, and the identifying relationship is a double diamond, so A and B are the standard notation. The weak entity's relation takes the owner's key as part of its own primary key, because the partial key is unique only inside one owner. That is D.

C is false. The identifying relationship is absorbed into the weak entity's relation. It does not become a table of its own when it has no extra attributes. Creating that extra table is a common over-count.

### Q6

Answer: 4

Assign is many-to-one from Truck to Depot and has no attributes, so Did becomes a non-null foreign key in Truck. That does not add a relation. Drives is many-to-many and has an attribute, so it is its own relation with key (Drid, Tid) and column Shift. The four relations are Depot, Truck, Driver, and Drives.

A fifth relation appears only if Assign is mistakenly mapped as if it were many-to-many.

### Q7

Answer: A

A many-to-many relationship cannot be a single foreign key on either side, so B loses pairs. The standard primary key is the pair of participating keys; the relationship attributes are ordinary columns of that relation. A surrogate may be added in a physical design, but it does not replace the two entity keys as the way the relationship is identified, so C is not the standard reduction. D confuses a relationship with a multivalued attribute.

### Q8

Answer: C

The relations are:

1. Museum(Mid, MName)
2. Gallery(Mid, GNo, Floor, Area), with primary key (Mid, GNo)
3. Artist(Arid, Name)
4. Artifact(Aid, Title, Year, Arid, Mid, GNo, Since)
5. ArtifactMaterial(Aid, Material)

Houses is identifying, so it is absorbed into Gallery. Creates is many-to-one toward Artist with total participation of Artifact, so Arid is a foreign key in Artifact. Displays is many-to-one toward Gallery, so (Mid, GNo) and Since sit in Artifact; they are nullable because participation of Artifact is partial. Material is multivalued, so it is the fifth relation. The total is 5.

A drops both the weak-entity key structure and the multivalued attribute. B forgets the separate material relation. D usually comes from also emitting a table for Houses or for Displays.

### Q9

Answer: 4

Gallery contains the owner key Mid, the partial key GNo, and the two descriptive attributes Floor and Area. Houses adds no column of its own. Since belongs to Displays, which is mapped into Artifact, not into Gallery.

### Q10

Answer: A, C, D

A is the weak-entity key rule: the owner's key plus the discriminator. C is required for 1NF, because one artifact can have several materials. D holds because Displays is many-to-one from Artifact to Gallery, so the relationship attribute rides on Artifact.

B is false. An identifying relationship is not a separate relation in the standard mapping.

### Q11

Answer: B

A weak entity cannot be identified without its owner, so every weak entity must participate in the identifying relationship. The owner need not. A museum, in the earlier example, could in principle have no gallery; the galleries that do exist still could not exist without a museum. The double line is drawn on the weak side.

A reverses the rule. C forces a restriction on the owner that the model does not require. D would leave a weak entity without an owner, so it would have no primary key.

### Q12

Answer: A, C

Heads is one-to-one. Total participation of Firm means every firm row can store exactly one person key and the start year, and those columns are not null. That is a standard merge into the total side, so A is true. Partial participation of Person means some people are not chairpersons, so C is true.

B treats total participation as a reason to create a table. It is a reason one can avoid nulls by merging into Firm, not a reason to add a relation. D is false because one foreign key is enough for a one-to-one relationship.

### Q13

Answer: 7

1. Hospital(Hid, HName)
2. HospitalPhone(Hid, Phone), because Phone is multivalued
3. Ward(Hid, WardNo, Wing, Beds)
4. Doctor(Did, DName, Rank)
5. Works(Did, Hid, Since), because Works is many-to-many
6. Patient(Pid, PName)
7. Admission(Pid, AdmNo, AdmitDate, DischargeDate, Did)

The identifying relationships of Ward and Admission add no tables. Attends is many-to-one from Admission to Doctor, and participation of Admission is total, so Did is a non-null foreign key in Admission.

The usual wrong counts are 6, if Phone is stored as a single column and 1NF is abandoned, and 8, if Attends or an identifying relationship is emitted as its own table.

### Q14

Answer: A, B, D

Admission is weak under Patient, so its key is the owner's key plus AdmNo. That is A. The attending doctor is a many-to-one relationship into Admission, so B is the foreign key from Q13. Phone cannot be a single atomic column if a hospital has several phones, so D is required for 1NF.

C is false. A single Hid column on Doctor stores at most one hospital per doctor and cannot represent the many-to-many relationship Works.
