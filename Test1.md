# FHIR DATA TYPES – INTERVIEW NOTES

FHIR data types are used to represent different kinds of information
inside FHIR resources.

There are 4 important categories:

1. Primitive Data Types
2. General-Purpose Data Types
3. Metadata Data Types
4. Special-Purpose Data Types


============================================================
1. PRIMITIVE DATA TYPES
============================================================

Primitive data types represent a basic / single value.

Examples:

- boolean       → true / false
- integer       → 25
- decimal       → 98.6
- string        → "Sameer"
- date          → "1996-05-02"
- dateTime      → "2026-09-26T10:30:00Z"
- time          → "10:30:00"
- instant       → Exact point in time
- id            → "Patient123"
- uri           → "http://example.com"
- url           → "https://example.com"
- canonical     → Canonical URL/reference
- code          → "male"
- base64Binary  → Base64 encoded binary data
- markdown      → Markdown text
- oid           → Object identifier
- uuid          → UUID
- positiveInt   → Positive integer
- unsignedInt   → Non-negative integer


Example:

{
  "resourceType": "Patient",
  "id": "P1001",
  "active": true,
  "gender": "male",
  "birthDate": "1996-05-02"
}

Here:

id          → id
active      → boolean
gender      → code
birthDate   → date


Interview Definition:

"Primitive data types represent basic values such as strings,
numbers, dates, Boolean values, codes and identifiers."


============================================================
2. GENERAL-PURPOSE DATA TYPES
============================================================

General-purpose data types are reusable complex data types.
They contain multiple related pieces of information.

Important examples:

- HumanName
- Address
- ContactPoint
- Identifier
- CodeableConcept
- Coding
- Quantity
- Period
- Range
- Ratio
- RatioRange
- Attachment
- Annotation
- Timing
- Money
- Distance
- Duration
- Count
- Age
- MoneyQuantity
- SimpleQuantity
- SampledData
- Signature


------------------------------------------------------------
HumanName
------------------------------------------------------------

Used to represent a person's name.

Example:

{
  "name": [
    {
      "family": "Shaik",
      "given": ["Sameer"]
    }
  ]
}

HumanName
    |
    |-- family → Shaik
    |
    |-- given  → Sameer


------------------------------------------------------------
Address
------------------------------------------------------------

Used to represent a person's address.

Example:

{
  "address": [
    {
      "line": ["Main Road"],
      "city": "Bengaluru",
      "state": "Karnataka",
      "postalCode": "560001"
    }
  ]
}


------------------------------------------------------------
ContactPoint
------------------------------------------------------------

Used for contact information such as phone or email.

Example:

{
  "telecom": [
    {
      "system": "phone",
      "value": "9876543210"
    }
  ]
}


------------------------------------------------------------
Identifier
------------------------------------------------------------

Used to identify a person or resource.

Example: MRN

{
  "identifier": [
    {
      "system": "http://hospital.example.org",
      "value": "MRN12345"
    }
  ]
}


------------------------------------------------------------
CodeableConcept
------------------------------------------------------------

Used to represent a clinical concept using one or more codes.

Example:

{
  "code": {
    "coding": [
      {
        "system": "http://snomed.info/sct",
        "code": "123456",
        "display": "Example condition"
      }
    ]
  }
}

Think:

CodeableConcept
       |
       ↓
Clinical Meaning
       |
       ↓
Coding
       |
       ↓
System + Code + Display


------------------------------------------------------------
Coding
------------------------------------------------------------

Represents a code from a particular coding system.

Example:

{
  "system": "http://snomed.info/sct",
  "code": "123456",
  "display": "Example condition"
}


------------------------------------------------------------
Quantity
------------------------------------------------------------

Represents a numerical value with a unit.

Example:

{
  "value": 98.6,
  "unit": "degF"
}

Meaning:

Temperature = 98.6 °F


============================================================
3. METADATA DATA TYPES
============================================================

Metadata types provide information about the content, author,
contributor, applicability, requirements, relationships and logic.

Important examples:

- ContactDetail
- Contributor
- DataRequirement
- RelatedArtifact
- TriggerDefinition
- ParameterDefinition
- Expression
- UsageContext


------------------------------------------------------------
ContactDetail
------------------------------------------------------------

Used to describe how to contact the person or organization
associated with the content.

Example:

{
  "name": "ABC Medical Organization",
  "telecom": [
    {
      "system": "email",
      "value": "contact@abcmedical.org"
    }
  ]
}

Remember:

ContactDetail → WHO CAN I CONTACT?


------------------------------------------------------------
Contributor
------------------------------------------------------------

Describes who contributed to creating or developing the content.

Example:

Clinical Guideline
       |
       ↓
Contributor
       |
       |-- Dr. Smith
       |
       |-- Dr. John
       |
       |-- ABC Medical Research Team

Remember:

Contributor → WHO CONTRIBUTED?


------------------------------------------------------------
RelatedArtifact
------------------------------------------------------------

Identifies another document, guideline, study or resource
related to the content.

Example:

Clinical Guideline
       |
       ↓
RelatedArtifact
       |
       ↓
WHO Clinical Guideline

Remember:

RelatedArtifact → WHAT IS THIS RELATED TO / BASED ON?


------------------------------------------------------------
UsageContext
------------------------------------------------------------

Describes where, for whom, or under what circumstances
the content applies.

Example:

Clinical Guideline
       |
       ↓
UsageContext
       |
       |-- Adult patients
       |-- Diabetes
       |-- Outpatient setting

Remember:

UsageContext → WHERE / FOR WHOM DOES IT APPLY?


------------------------------------------------------------
DataRequirement
------------------------------------------------------------

Describes what data is required for a clinical rule or
decision-support logic.

Example:

Clinical Guideline
       |
       ↓
DataRequirement
       |
       ↓
Patient's Blood Glucose Observation

Remember:

DataRequirement → WHAT DATA DO I NEED?


------------------------------------------------------------
TriggerDefinition
------------------------------------------------------------

Defines when a rule or clinical logic should be triggered.

Example:

Blood Glucose Result Available
             |
             ↓
     TriggerDefinition
             |
             ↓
      Run Clinical Rule

Remember:

TriggerDefinition → WHEN SHOULD IT RUN?


------------------------------------------------------------
ParameterDefinition
------------------------------------------------------------

Describes the parameters / input values required by
an operation or expression.

Example:

Clinical Rule
     |
     ↓
ParameterDefinition
     |
     |-- Patient Age
     |-- Blood Glucose
     |-- Medication

Remember:

ParameterDefinition → WHAT INPUT DOES IT NEED?


------------------------------------------------------------
Expression
------------------------------------------------------------

Represents computable logic or an expression.

Example:

Blood Glucose
      |
      ↓
  Expression
      |
      ↓
IF glucose > 200
      |
      ↓
Clinical Action

Remember:

Expression → WHAT LOGIC SHOULD BE EVALUATED?


============================================================
4. SPECIAL-PURPOSE DATA TYPES
============================================================

These data types are designed for specific FHIR purposes.

Important examples:

- Reference
- Meta
- Narrative
- Extension
- Dosage
- CodeableReference
- ProductShelfLife
- ElementDefinition
- MarketingStatus
- xhtml


------------------------------------------------------------
REFERENCE
------------------------------------------------------------

Reference is a SPECIAL-PURPOSE DATA TYPE.

It is used to establish a relationship / link between
FHIR resources.

Example:

Observation
     |
     | subject → Reference
     ↓
Patient


Example JSON:

{
  "resourceType": "Observation",
  "id": "OBS1001",
  "subject": {
    "reference": "Patient/P1001"
  }
}

Meaning:

"This Observation belongs to Patient P1001."

Interview Answer:

"Reference is a special-purpose data type in FHIR.
It is used to establish a relationship between FHIR resources.
For example, an Observation can reference a Patient using
the subject element."


------------------------------------------------------------
META
------------------------------------------------------------

Meta contains metadata about a FHIR resource.

Example:

{
  "meta": {
    "versionId": "2",
    "lastUpdated": "2026-09-26T10:30:00Z"
  }
}

Meta can contain information such as:

- Version
- Last Updated
- Security
- Profiles
- Tags

Remember:

Meta → INFORMATION ABOUT THE RESOURCE ITSELF


------------------------------------------------------------
NARRATIVE
------------------------------------------------------------

Narrative provides a human-readable representation
of a FHIR resource.

Example:

{
  "text": {
    "status": "generated",
    "div": "<div>Patient: Sameer</div>"
  }
}

Remember:

Narrative → HUMAN-READABLE CONTENT


------------------------------------------------------------
EXTENSION
------------------------------------------------------------

Extension allows additional information to be represented
when the standard FHIR resource does not have the required
element.

Concept:

Patient
   |
   ↓
Extension
   |
   ↓
Additional Information

Remember:

Extension → ADD ADDITIONAL INFORMATION


------------------------------------------------------------
DOSAGE
------------------------------------------------------------

Dosage describes how a medication should be taken
or administered.

Example:

{
  "dosageInstruction": [
    {
      "text": "Take 1 tablet twice daily"
    }
  ]
}

Dosage can describe:

- Dose
- Frequency
- Route
- Timing
- Instructions

Remember:

Dosage → HOW SHOULD THE MEDICATION BE TAKEN / ADMINISTERED?


============================================================
ELEMENT AND BACKBONEELEMENT
============================================================

Element
   |
   ↓
Base type for FHIR data structures

BackboneElement
   |
   ↓
Used for nested structures inside FHIR resources.

These are foundational types in FHIR and should not be
confused with simple types such as string, date or boolean.


============================================================
FINAL CLASSIFICATION
============================================================

FHIR DATA TYPES
|
|-- 1. Primitive
|      |
|      |-- string
|      |-- integer
|      |-- boolean
|      |-- decimal
|      |-- date
|      |-- dateTime
|      |-- time
|      |-- instant
|      |-- id
|      |-- uri
|      |-- url
|      |-- code
|      |-- etc.
|
|-- 2. General-Purpose
|      |
|      |-- HumanName
|      |-- Address
|      |-- ContactPoint
|      |-- Identifier
|      |-- CodeableConcept
|      |-- Coding
|      |-- Quantity
|      |-- Period
|      |-- Range
|      |-- Ratio
|      |-- Attachment
|      |-- etc.
|
|-- 3. Metadata
|      |
|      |-- ContactDetail
|      |-- Contributor
|      |-- DataRequirement
|      |-- RelatedArtifact
|      |-- TriggerDefinition
|      |-- ParameterDefinition
|      |-- Expression
|      |-- UsageContext
|
|-- 4. Special-Purpose
       |
       |-- Reference
       |-- Meta
       |-- Narrative
       |-- Extension
       |-- Dosage
       |-- CodeableReference
       |-- ProductShelfLife
       |-- etc.


============================================================
EASY WAY TO REMEMBER
============================================================

Primitive
    ↓
Basic value

General-Purpose
    ↓
Reusable structured information

Metadata
    ↓
Information ABOUT the content/context

Special-Purpose
    ↓
Specific FHIR functionality


============================================================
MOST IMPORTANT INTERVIEW QUESTIONS
============================================================

Q1: What is a Primitive Data Type?

Answer:
"Primitive data types represent basic values such as string,
integer, boolean, date, dateTime, code and id."


Q2: What is a General-Purpose Data Type?

Answer:
"General-purpose data types are reusable complex data types
such as HumanName, Address, Identifier, CodeableConcept,
Coding and Quantity."


Q3: What is a Reference?

Answer:
"Reference is a special-purpose data type used to establish
a relationship between two FHIR resources."


Q4: Give an example of Reference.

Answer:

Observation
     |
     | subject → Reference
     ↓
Patient


Q5: What is Metadata?

Answer:
"Metadata provides information about the content, contributor,
applicability, requirements, relationships or logic associated
with FHIR content."


============================================================
IMPORTANT MEMORY POINTS
============================================================

Primitive
    → Basic value

HumanName
    → Person's name

Address
    → Address information

ContactPoint
    → Phone / Email

Identifier
    → MRN / Other identifier

CodeableConcept
    → Clinical meaning

Coding
    → System + Code + Display

Quantity
    → Value + Unit

Metadata
    → Information ABOUT the content

Reference
    → CONNECTS / LINKS resources

Meta
    → Information ABOUT the FHIR resource

Narrative
    → Human-readable content

Extension
    → Additional information

Dosage
    → How medication is taken/administered
