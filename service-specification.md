---
titlepage: true
toc-own-page: true
title: "Service specification for the MCP Service Registry (MSR)"
author: [MCP Consortium]
date: "2022-06-21"
keywords: [maritime, technical, service, registry, MCP, MSR]
logo: "materials/mcplogo.png"
titlepage-text-color: "476E7D"
footer-center: "G-1128 MSR Service Specification"
toc: true
toc-own-page: true
...

# Service specification for the MCP Service Registry (MSR)
<!-- Hey it is comment! This must be seen only at the source code editing.  -->

## Introduction

In IMO resolution MSC.467(101) “Guidance on the Definition and Harmonization of
the Format and Structure of Maritime Services in the Context of e-Navigation”,
IMO defines Maritime Services and Technical Services in the context of
e-Navigation. In this resolution, the Maritime Services are on the highest 
level, describing a service in an entirely non-technical manner. One or more
Technical Services are associated with a Maritime Service, and these Technical
Services are the ones defining the actual information exchange needed to take
place in order to carry our a Maritime Service.

The Maritime Service Registry, or MSR for short, assumes the role of a general 
registry for Technical Services. It provides a reference point to the most
relevant information and the respective end-points of the registered services 
and thus to improve the accessibility of available services in the maritime 
domain.

The Technical Services in the resolution are also defined on three levels
following the same structure as G-1128, where MSR supervises all service
providers to describe their service in the format of G-1128.

### Purpose
<!--
    This template shall support the service architects in creating a description
    of the services (put down in writing) at a high level of abstraction,
    following the guidelines given in [1].  The template provides for each 
    section descriptive instructions for the intended content.  Formally, such
    instructions are written in blue italic font – they shall be deleted when 
    writing the actual service specification document.  In addition, some parts
    of this template provide suggested text fragments that may be directly 
    re-used in the service specification document. Such proposed text fragments
    are given below.
    
    The purpose of the service specification document is to write down the 
    results of service identification and service design activities. The aim is
    to document the key aspects of a dedicated service at the logical level:
        * the operational and business context of the service;
          * requirements for the service (e.g. information exchange requirements);
          * involved nodes: which operational components provide/consume the service;
          * operational activities supported by the service;
          * relation of the service to other services:
        * the service description;
          * service interface definitions;
          * service interface operations;
          * service payload definition;
        * service provision and validation aspects.
    
    This service specification document describes just one dedicated service in 
    detail at logical level. In addition, there shall exist a service portfolio
    document, which presents all services of the maritime cloud that are 
    available (or are planned to become available) at a higher level.
    
    The purpose of this service specification document is to provide a holistic
    overview of one service and its building blocks at logical level.  It may be
    complemented by a model based description (e.g. UML model describing the
    service interfaces, operations and data structures).  The service 
    specification document describes a well-defined baseline of the service and
    clearly identifies the service version.  In this way, it supports the 
    configuration management process.
    
    The service specification document provides also the foundation material for
    the future standardisation process.
    
    Note that the service specification is intended to be technology-agnostic.
    The service specification document shall not describe the details of a
    specific service implementation. For that purpose, a service instance 
    description shall be provided, where the realisation of the service with a 
    dedicated technology shall be described.
    
    This section shall be replaced by a suitable description of the purpose. For
    instance:
-->

The MSR is an implementation of service management concept which was given from
the IALA G-1128 specification. The main tasks of MSR are the registration of 
Technical Services by a service provider and the provision of a discovery 
mechanism for the registered services, so that any service consumer can identify
available services and gain access. 

The MSR registration needs to be able to register all relevant e-Navigation 
services, commercial and non-commercial, authorized and non-authorized, for free
and against payment. The MSR also needs to allow service consumers to discover
available services and enable the use of those services through defined 
end-point locations. It can therefore be seen as a sophisticated yellow pages 
phone book. A registry can be searched using a wide variety of different
criteria including the coverage area of interest.

### Intended readership
<!--
  This service specification template is intended to be read by service 
  architects who shall produce service descriptions.

  This section shall describe the intended readers. e.g.:
-->

This service specification is primarily intended to be read by architects,
system engineers and developers in charge of developing and operating an 
instance of the MSR service.

Furthermore, this service specification is intended to be read by enterprise 
architects, service architects, information architects, system engineers and 
developers in pursuing architecting, design and development activities of 
other related e-Navigation services.

### Inputs from other sources
<!--
  This section lists previous work on the subject covered by this document.

  Special emphasis shall be put on what has been reused from other (already
  finished) projects. 
-->

The service management concept originally given from the IALA G-1128 
specification was given and implemented throughout previous projects such as
EfficienSea2 and Sea Traffic Management.

## Service identification

The purpose of this section is to provide a unique identification of the service
and describe where the service is in terms of the engineering lifecycle.

<!-- Table below shall be completed. -->

Attribute     | Content
---           | ---
Name          | Maritime Service Registry (MSR)
ID            | urn:mrn:mcp:service:mcc:mcc:specification:msr
Version       | 0.0.1
Description   | A service registry acting as a reference point to provide information on the registered services and thus to improve the visibility and accessibility of available information and services in the maritime domain.
Keywords      | service, registry, discoverability, specification, G-1128, technical
Architect(s)  | MCC MSR WG
Status        | Provisional

## Operational Context
<!--
    The operational context description shall be based on the description of the
    operational model, consisting of a structure of operational nodes and
    operational activities.  If such an operational model exists, this section
    shall provide references to it.  If no such operational model exists, then 
    its main aspects shall be described in this section.
    
    Optionally, a simple high level use case, described in layman’s terms, could
    be provided as an introduction to this section.
    
    The operational context shall be a description of how the service supports
    interaction among operational nodes. This can be achieved in two different
    levels of granularity:
        1. A description of how the service supports the interaction between 
        operational nodes. This basically consists of an overview about which
        operational nodes shall provide the service and which operational nodes
        will consume the service.
        2. A more detailed description that indicates what operational 
        activities the service supports in a process model.
    
    Moreover, the operational context shall describe any requirement the service
    will fulfil or adhere to.  This refers to functional as well as 
    non-functional requirements at high level (business/regulatory requirements,
    system requirements, user requirements).  Especially, information exchange
    requirements are of much interest since the major objective of services is
    to support interaction between operational nodes.

    The source material for the operational context description should ideally
    be provided by operational users and is normally expressed in dedicated
    requirements documentation. Ensure that the applicable documents are defined
    in the References section.  If no requirements documents are available, then
    the basic requirements for the service shall be defined in the section D 3.1.
    
    Architectural elements applicable for this description are:
        * Service;
        * Nodes;
        * Operational activities;
        * Information exchange requirements.
-->

This section describes the context of the service from an operational 
perspective.

The main purpose of this section is to provide a description on how the MSR 
supports the interaction among the operational nodes. In this case, these are 
the ***service consumers*** and ***service providers*** that use the MSR. The
MSR acts as a trustworthy information provider to the service consumers, from 
which they can acquire a list of services that conform to a set of selection 
criteria. For service providers the MSR facilitates the dissemination of their 
service information and an access point where the relevant information is 
successfully registered. An example of this whole process can be seen in
the @fig:msrcontext.

![MSR Service Registration/Discoverability Concept](materials/mcpcontext.png) {#fig:msrcontext}

Another operational node to be taken into account is the MSR itself. More
specifically, multiple MSR instances that may exist independently of each other.
This kind of decentralized scenarios, result in the need for a certain level
of coordination, especially in terms of service discoverability. This can be
provided by a centralized/distributed ledger service, through which all 
interested MSRs can exchange information on their current registrations. The 
specification of this ledger operation however is outside the scope of this 
document. The participation of an MSR is such a scheme and any implementation 
decisions are therefore left to the MSR service providers.

More detailed descriptions on the basic operational aspects can be found below.

##### Service Registration

An MSR instance provider is naturally only accountable towards its own users, as
defined by any Service Level Agreements (SLAs) present. Hence, in regard to 
service registration, an MSR instance should be able to work independently.

Many services registered to an MSR might be local, i.e. will only be 
discoverable in that specific MSR instance. Some services however, might be
intended to be globally available, and should therefore be discoverable
across multiple MSR instances. When such a service is registered in an MSR, 
the registration will have to be propagated to the ledger mechanism mentioned
previously. Thus, the MSR instance provider needs to review whether to support
a centralized/distributed ledger operation.

##### Requirements on Service Registration

Services registered in an MSR must follow the IALA guideline on e-Navigation
technical services (G-1128). In this guideline services are described on three
levels:

* Service specification
* Service technical design
* Service instance

The service specification is the highest level, giving a high level description
and containing the data model of the service. This data model may be a reference
to an IHO product specification - or it could define a different data model. A
service specification will have one or more associated technical designs. Each
technical design describes how the service can be implemented using a specific
technology.

Although the technologies in principle can be anything (even a phone number),
the MCC promotes the use of web-services and services using the MMS. For each
technical design that will be one or more service instances that provides
information of concrete service providers. The most important information is the
endpoint of the service, but other significant information includes a 
geographical coverage of the service.

##### Service Discoverability

The following aspects need to be satisfied:
* Only organisations that are registered in a MIR instance (see details on
  “Vetting procedure for organisations joining MCP instances”; Document ID: MCP
  Gen 5) are allowed to submit service descriptions (any level, i.e. service
  specifications, service designs, and service instances) to a MSR. i.e. a
  submitter needs to authenticate itself using MIR.
* MSR needs to be open for queries/searches without authentication.
* Endpoints in Service Instances needs to point to active services that are in
  production (not test services). This is of course only the case if the MSR
  itself is a production environment.
* Requirements on service provider authentication and service consumer
  authentication is entirely up to the service provider.

##### MRN of Service Documents for Identification

At the time of registration of service, a service provider should be exposed to
the MRN scheme for the identification of service documents. The G1128 clearly
stated MRN as an unique identifier scheme. A service provider should follow the
MRN scheme of the MCP identity service provider (who operates a MIR) that they
belong. There is a possibility of having more than one MRN of a service document
for the identification.

In MSR, the primary identification MRN needs to be aligned with the MCP MRN
scheme, defined in “MCC Identity Management and Security Identity Management” as
follows:

```
<MCP-MRN> ::= "urn" ":" "mrn" ":" "mcp" ":" <MCP-TYPE> ":" <IPID> ":" <IPSS>
<MCP-TYPE> ::= "device" | "org" | "user" | "vessel" | "service" | "mir" | "mms" |
<IPID> ::= <CountryCode> | (alphanum) 0*20(alphanum / "-") (alphanum)
<IPSS> ::= pchar *(pchar / "/")
```

More detailed description of the syntax is given in the referenced document.

Here the MRN syntax of for a service document is given:

```
<MSR-IPSS> ::= <ORG> ":" <G1128-TYPE> ":" <SERVICE-NAME>
<ORG> ::= pchar *(pchar / "/")
<G1128-TYPE> ::= "instance" | "specification" | "design"
<SERVICE-NAME> ::= pchar *(pchar / "/")
```

where represents an organization ID assigned by, represents the type of the
documentation, i.e., specification, design, and instance, and can be any
specific string representing an unique identifier of a service. together with
represents the identity of the service provider, an organization or a company
registered to a specific MIR.

Governance of MRN of service documents is a responsibility of a MSR provider and
thus the uniqueness of a MRN at the database level.

### Functional and non-functional requirements

<!--
    This section lists all (functional and non-functional) requirements 
    applicable to the service being described. A tabular list of requirements 
    shall be added here.  If external requirements documents are available, 
    then the tables shall refer to these requirements, otherwise the 
    requirements shall be documented here.
    
    The service must be linked to at least one requirement.  At least one of 
    the following tables shall be presented in this section.  The first table 
    lists references to requirements available from external documents.  Make 
    sure you document the sources from where the requirements are coming from. 
    The second table lists new requirements defined for the first time in this 
    service specification document.
-->

#### Functional requirements
Requirement Id | Requirement Name | Requirement Text | References
--- | --- | --- | ---
MSR-FR001 | something | something | something
MSR-FR002 | something | something | something
MSR-FR003 | something | something | something

##### Requirement definitions - XYZ-FR001
Requirement Id | Requirement Name
--- | ---
Requirement Name |
Requirement Text |
Rationale |
Author |

##### Requirement definitions - XYZ-FR002
Requirement Id | Requirement Name
--- | ---
Requirement Name |
Requirement Text |
Rationale |
Author |

##### Requirement definitions - XYZ-FR003
Requirement Id | Requirement Name
--- | ---
Requirement Name |
Requirement Text |
Rationale |
Author |

#### Non-functional requirements
Requirement Id | Requirement Name | Requirement Text | References
--- | --- | --- | ---
MSR-NFR001 | something | something | something
MSR-NFR002 | something | something | something
MSR-NFR003 | something | something | something

##### Requirement definitions - XYZ-NFR001
Requirement Id | Requirement Name
--- | ---
Requirement Name |
Requirement Text |
Rationale |
Author |

##### Requirement definitions - XYZ-NFR002
Requirement Id | Requirement XYZ
--- | ---
Requirement Name |
Requirement Text |
Rationale |
Author |

##### Requirement definitions - XYZ-NFR003
Requirement Id | Requirement Name
--- | ---
Requirement Name |
Requirement Text |
Rationale |
Author |

### Other constraints

To be written

#### Relevant industrial standards
<!--
    List in this section the relevant industrial standards (if any) for the
    exchange of this type of data and or this type of service.  These may
    include, for example, OGC, WFS, WMS, etc.
-->

There are no such relevant industrial standards found.

#### Operational nodes
<!--
    If an operational model exists in external documents, then this section just
    shows the Service to Nodes mapping by providing three tables, as described
    below.

    If no external operational model exists, then the relevant operational nodes
    and their context shall be briefly described here before listing them in the
    tables of service providers and consumers.
-->

To be written

##### Operational nodes providing the MSR service

Operational Node    | Remarks
---                 | ---
something           | something

##### Operational nodes consuming the MSR service

Operational Node    | Remarks
---                 | ---
something           | something

#### Operational activities (Optional)
<!--
    Optional. If an operational model exists and provides sufficient details 
    about operational activities, then this section shall include a mapping of 
    the service to the relevant operational activities.
-->

To be written

##### Operational activities supported by the MSR service

Operational Node    | Remarks
---                 | ---
something           | something

To be written

## Service overview
<!--
    This section aims at providing an overview of the main elements of the
    service.  The elements in this view are all usually created by an UML
    modelling tool.

    Architectural elements applicable for this description are:
        * Service - the element representing the service in its entirety;
        * Service Interfaces - the mechanisms by which a service communicates. 
        Defined by allocating service operations to either the provider or the 
        consumer of the service;
        * Service Operations - describe the logical operations used to access 
        the service.
        * Service Operations Parameter Definitions - identify data structures 
        being exchanged via Service Operations.
    
    The above elements may be depicted in one or more diagrams.  Which and how
    many diagrams are needed depends on the chosen architecture description 
    framework and complexity of the service.
-->

This section aims at providing an overview of the main elements of the service.
The elements in this view are all usually created by an UML modelling tool.

### Service interfaces

<!--
    Describe the interfaces of the service including the selected Message 
    Exchange Pattern (MEP) by using an UML diagram5 that illustrates the service
    interfaces definitions and operations and in tabular form.
    
    It is also recommended to describe the considerations resulting in the 
    selection of a certain message exchange pattern.
    
    A service interface supports one or several service operations. Depending on
    the message exchange pattern, service operations are either to be 
    implemented by the service provider (e.g. in a Request/Response MEP, query 
    operations are provided by the service provider – the service consumer uses 
    them in order to submit query requests to the service provider), or by the 
    service consumer (e.g. in a Publish/Subscribe MEP, publication operations 
    are provided by the service consumer – the service provider uses them to 
    submit publications to the service consumer). This distinction shall be 
    clearly visualised in a service interface table (see example below): for
    each service interface, it shall be stated whether it is either provided or
    used by the Service. A service provides at least one service interface.

    An example diagram and corresponding table is given below.
-->

Describe the interfaces of the service including the selected Message Exchange 
Pattern (MEP) by using an UML diagram5 that illustrates the service interfaces
definitions and operations and in tabular form. It is also recommended to
describe the considerations resulting in the selection of a certain message
exchange pattern. A service interface supports one or several service
operations. Depending on the message exchange pattern, service operations are
either to be implemented by the service  provider (e.g. in a Request/Response
MEP, query operations are provided by the service provider – the service
consumer uses them in order to submit query requests to the service provider),
or by the service consumer (e.g. in a Publish/Subscribe MEP, publication
operations are provided by the service consumer – the service provider uses them
to submit publications to the service consumer). This distinction shall be
clearly visualised in a service interface table (see example below): for each
service interface, it shall be stated whether it is either provided or used by
the Service. A service provides at least one service interface. An example
diagram and corresponding table is given below.

## Service data model

<!--
    It is recommended to visualise the data structures by using UML diagrams.
    The full information model (logical data structure) shall be shown using
    diagram(s) and explanatory tables (see below).
-->

This section describes the information model, i.e., the logical data structures
to be exchanged between providers and consumers of the service.

Example of an UML diagram:

<!--
    It is mandatory to give a description of each entity item (class), its
    attributes and the associations between entity items after each diagram
    showing data items.
    
    If the service data model is related to an external data model (e.g. being a
    subset of a standard data model, e.g. based on an S-100 specification), then
    the service data model shall refer to it: each data item of the service data
    model shall be mapped to a data item defined in the external data model. 
    This mapping may be added in the same table that describes the data items
    and their attributes and associations.  The idea is: when reading the
    service specification (including the logical service data model), the
    payload structures shall become clear to the reader.  If the service re-uses
    structures of an external data model, then these structures can be referred
    to rather than replicated in the service specification.  The tabular
    presentation of the payload allows for providing references to an externally
    defined model.
    
    The table below is an example for describing a service data model including
    traces to an external model.
-->

#### Data Models

```json
      "XmlDto": {
        "required": [
          "content",
          "name"
        ],
        "type": "object",
        "properties": {
          "id": {
            "type": "integer",
            "format": "int64"
          },
          "name": {
            "type": "string"
          },
          "comment": {
            "type": "string"
          },
          "content": {
            "type": "string"
          },
          "contentContentType": {
            "type": "string"
          }
        }
      },
      "LedgerRequestDto": {
        "required": [
          "serviceInstanceId"
        ],
        "type": "object",
        "properties": {
          "id": {
            "type": "integer",
            "format": "int64"
          },
          "serviceInstanceId": {
            "type": "integer",
            "format": "int64"
          },
          "status": {
            "type": "string",
            "enum": [
              "INACTIVE",
              "CREATED",
              "VETTING",
              "VETTED",
              "REQUESTING",
              "SUCCEEDED",
              "FAILED",
              "REJECTED"
            ]
          },
          "reason": {
            "type": "string"
          },
          "createdAt": {
            "type": "string",
            "format": "date-time"
          },
          "lastUpdatedAt": {
            "type": "string",
            "format": "date-time"
          }
        }
      },
      "Coordinate": {
        "type": "object",
        "properties": {
          "x": {
            "type": "number",
            "format": "double"
          },
          "y": {
            "type": "number",
            "format": "double"
          },
          "z": {
            "type": "number",
            "format": "double"
          },
          "m": {
            "type": "number",
            "format": "double"
          },
          "coordinate": {
            "$ref": "#/components/schemas/Coordinate"
          }
        }
      },
      "CoordinateSequence": {
        "type": "object",
        "properties": {
          "dimension": {
            "type": "integer",
            "format": "int32"
          },
          "measures": {
            "type": "integer",
            "format": "int32"
          }
        }
      },
      "CoordinateSequenceFactory": {
        "type": "object"
      },
      "DocDto": {
        "required": [
          "filecontent",
          "mimetype",
          "name"
        ],
        "type": "object",
        "properties": {
          "id": {
            "type": "integer",
            "format": "int64"
          },
          "name": {
            "type": "string"
          },
          "comment": {
            "type": "string"
          },
          "mimetype": {
            "type": "string"
          },
          "filecontent": {
            "type": "array",
            "items": {
              "type": "string",
              "format": "byte"
            }
          },
          "filecontentContentType": {
            "type": "string"
          },
          "instanceId": {
            "type": "integer",
            "format": "int64"
          }
        }
      },
      "Envelope": {
        "type": "object",
        "properties": {
          "null": {
            "type": "boolean"
          },
          "width": {
            "type": "number",
            "format": "double"
          },
          "height": {
            "type": "number",
            "format": "double"
          },
          "area": {
            "type": "number",
            "format": "double"
          },
          "minX": {
            "type": "number",
            "format": "double"
          },
          "maxX": {
            "type": "number",
            "format": "double"
          },
          "minY": {
            "type": "number",
            "format": "double"
          },
          "maxY": {
            "type": "number",
            "format": "double"
          },
          "diameter": {
            "type": "number",
            "format": "double"
          }
        }
      },
      "Geometry": {
        "type": "object",
        "properties": {
          "envelope": {
            "$ref": "#/components/schemas/Geometry"
          },
          "factory": {
            "$ref": "#/components/schemas/GeometryFactory"
          },
          "userData": {
            "type": "object"
          },
          "length": {
            "type": "number",
            "format": "double"
          },
          "empty": {
            "type": "boolean"
          },
          "valid": {
            "type": "boolean"
          },
          "geometryType": {
            "type": "string"
          },
          "srid": {
            "type": "integer",
            "format": "int32"
          },
          "numGeometries": {
            "type": "integer",
            "format": "int32"
          },
          "coordinate": {
            "$ref": "#/components/schemas/Coordinate"
          },
          "coordinates": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Coordinate"
            }
          },
          "numPoints": {
            "type": "integer",
            "format": "int32"
          },
          "rectangle": {
            "type": "boolean"
          },
          "area": {
            "type": "number",
            "format": "double"
          },
          "centroid": {
            "$ref": "#/components/schemas/Point"
          },
          "interiorPoint": {
            "$ref": "#/components/schemas/Point"
          },
          "dimension": {
            "type": "integer",
            "format": "int32"
          },
          "boundary": {
            "$ref": "#/components/schemas/Geometry"
          },
          "envelopeInternal": {
            "$ref": "#/components/schemas/Envelope"
          },
          "simple": {
            "type": "boolean"
          },
          "boundaryDimension": {
            "type": "integer",
            "format": "int32"
          },
          "precisionModel": {
            "$ref": "#/components/schemas/PrecisionModel"
          }
        }
      },
      "GeometryFactory": {
        "type": "object",
        "properties": {
          "precisionModel": {
            "$ref": "#/components/schemas/PrecisionModel"
          },
          "coordinateSequenceFactory": {
            "$ref": "#/components/schemas/CoordinateSequenceFactory"
          },
          "srid": {
            "type": "integer",
            "format": "int32"
          }
        }
      },
      "InstanceDto": {
        "required": [
          "comment",
          "instanceId",
          "name",
          "status",
          "version"
        ],
        "type": "object",
        "properties": {
          "id": {
            "type": "integer",
            "format": "int64"
          },
          "name": {
            "type": "string"
          },
          "version": {
            "type": "string"
          },
          "publishedAt": {
            "type": "string",
            "format": "date-time"
          },
          "lastUpdatedAt": {
            "type": "string",
            "format": "date-time"
          },
          "comment": {
            "type": "string"
          },
          "geometry": {
            "$ref": "#/components/schemas/Geometry"
          },
          "geometryContentType": {
            "type": "string"
          },
          "instanceId": {
            "type": "string"
          },
          "keywords": {
            "type": "array",
            "items": {
              "type": "string"
            }
          },
          "status": {
            "type": "string",
            "enum": [
              "PROVISIONAL",
              "RELEASED",
              "DEPRECATED",
              "DELETED"
            ]
          },
          "organizationId": {
            "type": "string"
          },
          "unlocode": {
            "type": "array",
            "items": {
              "type": "string"
            }
          },
          "endpointUri": {
            "type": "string"
          },
          "endpointType": {
            "type": "string"
          },
          "mmsi": {
            "type": "string"
          },
          "imo": {
            "type": "string"
          },
          "serviceType": {
            "type": "array",
            "items": {
              "type": "string"
            }
          },
          "instanceAsXml": {
            "$ref": "#/components/schemas/XmlDto"
          },
          "instanceAsDoc": {
            "$ref": "#/components/schemas/DocDto"
          },
          "ledgerRequestId": {
            "type": "integer",
            "format": "int64"
          },
          "ledgerRequestStatus": {
            "type": "string",
            "enum": [
              "INACTIVE",
              "CREATED",
              "VETTING",
              "VETTED",
              "REQUESTING",
              "SUCCEEDED",
              "FAILED",
              "REJECTED"
            ]
          },
          "docIds": {
            "uniqueItems": true,
            "type": "array",
            "items": {
              "type": "integer",
              "format": "int64"
            }
          },
          "implementsServiceDesign": {
            "type": "string"
          },
          "implementsServiceDesignVersion": {
            "type": "string"
          }
        }
      },
      "Point": {
        "type": "object",
        "properties": {
          "envelope": {
            "$ref": "#/components/schemas/Geometry"
          },
          "factory": {
            "$ref": "#/components/schemas/GeometryFactory"
          },
          "userData": {
            "type": "object"
          },
          "coordinates": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Coordinate"
            }
          },
          "empty": {
            "type": "boolean"
          },
          "x": {
            "type": "number",
            "format": "double"
          },
          "y": {
            "type": "number",
            "format": "double"
          },
          "geometryType": {
            "type": "string"
          },
          "coordinate": {
            "$ref": "#/components/schemas/Coordinate"
          },
          "numPoints": {
            "type": "integer",
            "format": "int32"
          },
          "dimension": {
            "type": "integer",
            "format": "int32"
          },
          "boundary": {
            "$ref": "#/components/schemas/Geometry"
          },
          "simple": {
            "type": "boolean"
          },
          "boundaryDimension": {
            "type": "integer",
            "format": "int32"
          },
          "coordinateSequence": {
            "$ref": "#/components/schemas/CoordinateSequence"
          },
          "length": {
            "type": "number",
            "format": "double"
          },
          "valid": {
            "type": "boolean"
          },
          "srid": {
            "type": "integer",
            "format": "int32"
          },
          "numGeometries": {
            "type": "integer",
            "format": "int32"
          },
          "rectangle": {
            "type": "boolean"
          },
          "area": {
            "type": "number",
            "format": "double"
          },
          "centroid": {
            "$ref": "#/components/schemas/Point"
          },
          "interiorPoint": {
            "$ref": "#/components/schemas/Point"
          },
          "envelopeInternal": {
            "$ref": "#/components/schemas/Envelope"
          },
          "precisionModel": {
            "$ref": "#/components/schemas/PrecisionModel"
          }
        }
      },
      "PrecisionModel": {
        "type": "object",
        "properties": {
          "scale": {
            "type": "number",
            "format": "double"
          },
          "type": {
            "$ref": "#/components/schemas/Type"
          },
          "floating": {
            "type": "boolean"
          },
          "maximumSignificantDigits": {
            "type": "integer",
            "format": "int32"
          },
          "offsetX": {
            "type": "number",
            "format": "double"
          },
          "offsetY": {
            "type": "number",
            "format": "double"
          }
        }
      },
      "Type": {
        "type": "object"
      },
      "DtColumn": {
        "type": "object",
        "properties": {
          "data": {
            "type": "string"
          },
          "name": {
            "type": "string"
          },
          "searchable": {
            "type": "boolean"
          },
          "orderable": {
            "type": "boolean"
          },
          "search": {
            "$ref": "#/components/schemas/DtSearch"
          }
        }
      },
      "DtOrder": {
        "type": "object",
        "properties": {
          "column": {
            "type": "integer",
            "format": "int32"
          },
          "dir": {
            "type": "string",
            "enum": [
              "asc",
              "desc"
            ]
          }
        }
      },
      "DtPagingRequest": {
        "type": "object",
        "properties": {
          "start": {
            "type": "integer",
            "format": "int32"
          },
          "length": {
            "type": "integer",
            "format": "int32"
          },
          "draw": {
            "type": "integer",
            "format": "int32"
          },
          "order": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/DtOrder"
            }
          },
          "columns": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/DtColumn"
            }
          },
          "search": {
            "$ref": "#/components/schemas/DtSearch"
          },
          "springbootSort": {
            "$ref": "#/components/schemas/Sort"
          }
        }
      },
      "DtSearch": {
        "type": "object",
        "properties": {
          "value": {
            "type": "string"
          },
          "regexp": {
            "type": "string"
          }
        }
      },
      "Sort": {
        "type": "object",
        "properties": {
          "empty": {
            "type": "boolean"
          },
          "sorted": {
            "type": "boolean"
          },
          "unsorted": {
            "type": "boolean"
          }
        }
      },
      "DtPageInstanceDtDto": {
        "type": "object",
        "properties": {
          "data": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/InstanceDtDto"
            }
          },
          "recordsFiltered": {
            "type": "integer",
            "format": "int32"
          },
          "recordsTotal": {
            "type": "integer",
            "format": "int32"
          },
          "draw": {
            "type": "integer",
            "format": "int32"
          }
        }
      },
      "InstanceDtDto": {
        "required": [
          "comment",
          "instanceId",
          "name",
          "status",
          "version"
        ],
        "type": "object",
        "properties": {
          "id": {
            "type": "integer",
            "format": "int64"
          },
          "name": {
            "type": "string"
          },
          "version": {
            "type": "string"
          },
          "publishedAt": {
            "type": "string",
            "format": "date-time"
          },
          "lastUpdatedAt": {
            "type": "string",
            "format": "date-time"
          },
          "comment": {
            "type": "string"
          },
          "geometry": {
            "$ref": "#/components/schemas/Geometry"
          },
          "geometryContentType": {
            "type": "string"
          },
          "instanceId": {
            "type": "string"
          },
          "keywords": {
            "type": "array",
            "items": {
              "type": "string"
            }
          },
          "status": {
            "type": "string",
            "enum": [
              "PROVISIONAL",
              "RELEASED",
              "DEPRECATED",
              "DELETED"
            ]
          },
          "organizationId": {
            "type": "string"
          },
          "unlocode": {
            "type": "array",
            "items": {
              "type": "string"
            }
          },
          "endpointUri": {
            "type": "string"
          },
          "endpointType": {
            "type": "string"
          },
          "mmsi": {
            "type": "string"
          },
          "imo": {
            "type": "string"
          },
          "serviceType": {
            "type": "array",
            "items": {
              "type": "string"
            }
          },
          "instanceAsXml": {
            "$ref": "#/components/schemas/XmlDto"
          },
          "instanceAsDocId": {
            "type": "integer",
            "format": "int64"
          },
          "instanceAsDocName": {
            "type": "string"
          },
          "ledgerRequestId": {
            "type": "integer",
            "format": "int64"
          },
          "ledgerRequestStatus": {
            "type": "string",
            "enum": [
              "INACTIVE",
              "CREATED",
              "VETTING",
              "VETTED",
              "REQUESTING",
              "SUCCEEDED",
              "FAILED",
              "REJECTED"
            ]
          },
          "docIds": {
            "uniqueItems": true,
            "type": "array",
            "items": {
              "type": "integer",
              "format": "int64"
            }
          },
          "implementsServiceDesign": {
            "type": "string"
          },
          "implementsServiceDesignVersion": {
            "type": "string"
          }
        }
      },
      "DocDtDto": {
        "required": [
          "mimetype",
          "name"
        ],
        "type": "object",
        "properties": {
          "id": {
            "type": "integer",
            "format": "int64"
          },
          "name": {
            "type": "string"
          },
          "comment": {
            "type": "string"
          },
          "mimetype": {
            "type": "string"
          },
          "filecontentContentType": {
            "type": "string"
          },
          "instanceId": {
            "type": "integer",
            "format": "int64"
          }
        }
      },
      "DtPageDocDtDto": {
        "type": "object",
        "properties": {
          "data": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/DocDtDto"
            }
          },
          "recordsFiltered": {
            "type": "integer",
            "format": "int32"
          },
          "recordsTotal": {
            "type": "integer",
            "format": "int32"
          },
          "draw": {
            "type": "integer",
            "format": "int32"
          }
        }
      },
      "Pageable": {
        "type": "object",
        "properties": {
          "page": {
            "minimum": 0,
            "type": "integer",
            "format": "int32"
          },
          "size": {
            "minimum": 1,
            "type": "integer",
            "format": "int32"
          },
          "sort": {
            "type": "array",
            "items": {
              "type": "string"
            }
          }
        }
      }
```      

### Service internal data model (Optional)
<!--
    Optionally, this section may provide a description of the internal data
    model, as it seems appropriate to the service provider and/or the service
    consumer side.  Such description might be helpful for the better
    understanding as it provides additional information about the building of
    the service.  However, it should be considered just as an example – it is
    not an authoritative part of the service specification.
-->

To be written

## Service interface specifications

<!--
    The static interface description is vital since it describes how the 
    interfaces shall be constructed.

    Architectural elements applicable for this description are:
        * Service Interfaces;
        * Operations - function or procedures which enable programmatic 
        communication with a Service via a Service interface;
        * Parameters - constants or variables passed into or out of a Service 
        interface as part of the execution of an Operation.
        A Service may have one or more Service Interfaces.  Please describe 
        each in separate sections below.
-->

This section describes the details of each service interface. One sub-section
is provided for each Service Interface. The Service Interface specification 
covers only the static design description while the dynamic design (behaviour) 
is described in section D 5.

### Service interface <INTERFACE NAME>
<!--
    Please explain the purpose, message exchange pattern and architecture of 
    the Interface.

    A Service Interface supports one or several service operations.  Each 
    operation in the service interface shall be described in the following 
    sections.
-->

To be written

#### Operation <OPERATION NAME>
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

To be written

##### Operation functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

To be written

##### Operation parameters
<!--
    Describe the logical data structure of input and output parameters of the
    operation (payload) by using an explanatory table (see below) and
    optionally UML diagrams (which are usually sub-sets of the service data
    model described in previous section above).

    Figure 3 shows an example of a UML diagram (subset of the service data
    model, related to one operation).
-->

<!--
    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

To be written

## Service dynamic behaviour
<!--
    This section describes the interactive behaviour between service interfaces
    (interaction specification) and, if required, between different services
    (orchestration).  Architectural elements applicable for this description are:
        * Service Interaction Specifications;
        * Service State machines;
        * Service orchestration.
    Following types of views and UML diagrams can be used to describe the 
    dynamic behaviour:
        * Sequence diagrams;
        * Interaction diagrams;
        * State machine diagrams.
-->
A description should be given.

### Service interface <INTERFACE NAME>
<!--
    Include some information about the dynamic aspects of the service
    interface; each operation shall be exposed on at least one diagram.
    An example sequence diagram is shown in Figure 4.
-->

A description should be given.

### Service orchestration (Optional)
<!--
This section shall be provided, if the composition of the service and/or the relation to other services (e.g., which other services are used to provide this service; which other services are intended to use this service) is deemed relevant for the service specification.
An example sequence diagram is given below. This very simple example indicates that the AddressForPersionLookupService (i.e., the service that is being described in this Service Specification Document) acts as a consumer of a “notifyAddressChange” operation of another service, called “AddressForPersionService”. Note that the other service needs to be described by its own Service Specification Document; a reference to that document shall be added here).
-->
A description should be given.

## Service provisioning (Optional)
<!--
    This section shall describe the way services are planned to be provided and
    consumed.  It is labelled optional since one of the key aspects of
    service-orientation is to increase flexibility of the overall system by
    separating the definition of services from their implementation.  This
    means that a service can be provided in several different contexts that are
    not necessarily known at the time, when the service is designed.
-->

A service management concept with MSR is visualised as below. Both, service 
specifications as well as information about service instances can be published 
in a service registry. A service registry can be a collection of documents, or 
could be realised as a service itself that would have an Application 
Programming Interface (API) for automatic interfacing to the registry (lookup, 
updating, deleting etc.). This concept is implemented as MSR within MCP 
(formerly called the Maritime Cloud), see https://maritimeconnectivity.net/.

This section shall describe the way services are planned to be provided and
consumed. It is labelled optional since one of the key aspects of
service-orientation is to increase flexibility of the overall system by
separating the definition of services from their implementation. This means
that a service can be provided in several different contexts that are not
necessarily known at the time, when the service is designed.

## Definitions
<!--
    The definitions of terms used in this IALA Guideline can be found in the
    International Dictionary of Marine Aids to Navigation (IALA Dictionary) at
    http://www.iala-aism.org/wiki/dictionary and were checked as correct at the
    time of going to print.  Where conflict arises, the IALA Dictionary shall
    be considered as the authoritative source of definitions used in IALA
    documents.
-->

Most of terms in the context of MCP can be found in the terminology page of the
online documentation of MCP 
(https://docs.maritimeconnectivity.net/en/latest/terminology.html).

### Terminology
Persons producing the Technical Service are invited to add definitions to the
following list as appropriate.

Term    | Definition
---     | ---
MSR     | Maritime Service Registry
MIR     | Maritime Identity Registry
MRN     | Maritime Resource Name

### Terminology
Persons producing the Technical Service are invited to provide a list of
acronyms as appropriate.

Acronym | Meaning
---     | ---
MSR     | Maritime Service Registry
MIR     | Maritime Identity Registry
MRN     | Maritime Resource Name

## References
<!--
    This section shall include all references used when designing the service.
    Specifically, the applicable steering and requirements documents shall be
    listed.
-->

1. IALA Guideline - G1128 THE SPECIFICATION OF e-NAVIGATION TECHNICAL SERVICES
2. http://mrnregistry.org/
3. S-100 Universal Hydrographic Data Model, http://www.iho.int/iho_pubs/standard/S-100/S-100_Ed_2/S_100_V2.0.0_June-2015.pdf
