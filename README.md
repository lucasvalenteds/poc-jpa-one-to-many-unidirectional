# POC: JPA One-to-Many Unidirectional

It demonstrates how to use JPA to implement one-to-many unidirectional relationship.

The goal is to be able to persist information about people, documents and links between them. Every person must have one
or none document registered, and we want to make the references consistent.

In this example we have the relationship implemented using a join table under the hood, unmapped in Java code.
The `Person` entity owns the relationship and contains the annotation `OneToMany` to define the relationship type
and `JoinTable` defining the two columns containing references to it and `Document` entity ID.

## How to run

| Description | Command          |
|:------------|:-----------------|
| Run tests   | `./gradlew test` |

## Preview

Entity Relationship Model:

```mermaid
classDiagram
direction LR

class Document {
    Long  id
    String  code
}

class Person {
    Long  id
    String  name
}

Person "0..1" --> "0..*" Document 
```

Database schema:

```mermaid
classDiagram
direction RL

class document {
   varchar document_code
   bigint document_id
}

class person {
   varchar person_name
   bigint person_id
}

class person_document {
   bigint person_id
   bigint document_id
}

person_document  -->  document : document_id
person_document  -->  person : person_id
```