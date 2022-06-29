---
titlepage: true
toc: true
toc-own-page: true
title: "Service specification for the MCP Service Registry (MSR)"
author: [MCP Consortium]
date: "2022-06-29"
keywords: [maritime, technical, service, registry, MCP, MSR]
logo: "materials/mcplogo.png"
titlepage-text-color: "476E7D"
footer-center: "G-1128 MSR Service Specification"
code-block-font-size: \footnotesize
listings-disable-line-numbers: true
...

# Introduction

The International Maritime Organization (IMO) in its 'Strategy for the
development and  implementation of e‐Navigation' (MSC85/26, Annex 20) [1]
resolution, provides the following definition of e‐Navigation:

***E-Navigation, is the harmonised collection, integration, exchange,
presentation and analysis of maritime information on-board and ashore by
electronic means to enhance berth-to-berth navigation and related services, for
safety and security at sea and protection of the marine environment.***

In IMO resolution MSC.467(101) “Guidance on the Definition and Harmonization of
the Format and Structure of Maritime Services in the Context of e-Navigation”
[2], IMO defines Maritime Services and Technical Services in the context of
e-Navigation. In this resolution, the Maritime Services are on the highest 
level, describing a service in an entirely non-technical manner. One or more
Technical Services are associated with a Maritime Service, and these Technical
Services are the ones defining the actual information exchange needed to take
place in order to carry our a Maritime Service.

The Maritime Service Registry [3], or MSR for short, assumes the role of a
general  registry for Technical Services. It provides a reference point to the
most relevant information and the respective end-points of the registered
services and thus to improve the accessibility of available services in the
maritime domain.

The Technical Services in the resolution are defined on three levels following
the same structure as in IALA G-1128 [4] guideline. The MSR supervises all
service providers to describe their service in the format of G-1128.

## Purpose
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
the IALA G-1128 guideline. The main tasks of MSR are the registration of 
Technical Services by a service provider and the provision of a discovery 
mechanism for the registered services, so that any service consumer can identify
available services and gain access. 

The MSR registration is required to support all relevant e-Navigation services,
commercial and non-commercial, authorized and non-authorized, for free and
against payment. The MSR also needs to allow service consumers to discover
available services and enable the use of those services through defined 
end-point locations. It can therefore be seen as a sophisticated yellow pages 
phone book. A registry can be searched using a wide variety of different
criteria including the coverage area of interest.

## Intended readership
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

## Inputs from other sources
<!--
  This section lists previous work on the subject covered by this document.

  Special emphasis shall be put on what has been reused from other (already
  finished) projects. 
-->

The service management concept originally presented in the IALA G-1128
guideline has already bee considered and implemented by previous projects such
as EfficienSea2 [5] and Sea Traffic Management.

# Service identification

The purpose of this section is to provide a unique identification of the service
and describe where the service is in terms of the engineering lifecycle.

<!-- Table below shall be completed. -->

<!-- Spacing: | --- | --------- | -->
| Attribute    | Content                                                                                                                                                                                                             |
| --- | --------- |
| Name         | Maritime Service Registry (MSR)                                                                                                                                                                                     |
| ID           | urn:mrn:mcp:service:mcc:mcc:specification:msr                                                                                                                                                                       |
| Version      | 0.0.1                                                                                                                                                                                                               |
| Description  | A service registry acting as a reference point to provide information on the registered services and thus to improve the visibility and accessibility of available information and services in the maritime domain. |
| Keywords     | service, registry, discoverability, specification, G-1128, technical                                                                                                                                                |
| Architect(s) | MCC MSR WG                                                                                                                                                                                                          |
| Status       | Provisional                                                                                                                                                                                                         |

# Operational Context
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
the figure below.

![MSR Service Registration/Discoverability Concept](materials/msrcontext.drawio.png)

Another operational node to be taken into account is the MSR Instance Provider.
More specifically, multiple MSR Instances Providers can exist, each operating
an MSR instance independently of each other. This kind of decentralized
scenarios, demonstrates the need for a certain level of coordination, especially
in terms of service discoverability. This can be provided by a centralized or 
distributed ledger service, through which all interested MSRs can exchange
information on their current registrations. The specification of this ledger
operation however is outside the scope of this document. The participation of an
MSR is such a scheme and any implementation decisions are therefore left to the
MSR service developers/providers.

More detailed descriptions on the basic operational aspects can be found below.

#### Service Registration

An MSR Instance Provider is naturally only accountable towards its own users,
bounded by any Service Level Agreement (SLA) present. Hence, in regard to 
service registration, an MSR instance should be able to work independently.

Many services registered to an MSR might be *local*, i.e. will only be 
discoverable in that specific MSR instance. Some services however, might be
intended to be globally available, and should therefore be discoverable
across multiple MSR instances. When such a service is registered in an MSR, 
the registration will have to be propagated to the ledger mechanism mentioned
previously. Thus, the MSR instance provider needs to review whether to support
a centralized or distributed ledger operation.

Services registered in an MSR must follow the IALA guideline on the
specification of e-Navigation technical services (G-1128). In this guideline
services are described on three levels:

* Service specification
* Service technical design
* Service instance

The *Service Specification* is the highest level, giving a high level 
description and containing the data model of the service. This data model may be
a reference to an IHO product specification - or it could be defined as a
different bespoke data model. A service specification will have one or more
associated *Technical Designs*. Each technical design describes how the service
can be implemented using a specific technology.

Although these technologies in principle can be anything (even a phone number),
the *Maritime Connectivity Platform Consortium* (MCC) promotes the use of
web-services and services using the *Maritime Messaging Service* (MMS). For each
technical design there will be one or more service instances that provide the
required information, relying on a service provider. The most important
information is the endpoint of the service, but other significant information
includes a geographical coverage of the service. It is therefore mandated that
any MSR implementation must support at least the *Service Instance
Specification* of G-1128. Support in this context refers to the provision of a
G-1128 compliant service instance description in XML format. References to the
other two G-1128 specifications (i.e. service specification and technical
design) should also be provided, although it is acceptable that these are hosted
by third parties.

Optionally, MSR implementations may also support G-1128 non-compliant service
registrations. In those cases, the XML description of the service instance 
specification can be omitted, and only the mandatory fields of a registration
will be required from the service provider.

#### Service Discoverability

Service discoverability is intended to facilitate the dissemination of the 
e-Navigation service information. As such, the employed mechanism should follow
the most widely-used set of standards, which in the maritime domain related 
directly to the IEC 63173-2 ED1 standard [6], more widely known as SECOM. 

SECOM already defines a mechanism for service discovery and this should be 
employed by the MSR. Apart from the requirements set by SECOM however, the
following additional aspects need to be satisfied:

* Only organisations that are registered in a *Maritime Identity Registry* (MIR)
  instance (see details on the MCP "Vetting Procedure for MCP Instance
  Providers" [7]) are allowed to submit service descriptions (any level, i.e.
  service specifications, service designs, and service instances) to an MSR.
  i.e. a submitter needs to authenticate itself using MIR.
* MSR needs to be open for queries/searches without authentication.
* The registered endpoints of the service instances need to point to active 
  services that are in production (not test services). This is of course only
  the case if the MSR, itself is a production environment.
* Requirements on service provider authentication and service consumer
  authentication is entirely up to the service provider.

In terms of the discoverability mechanism, this must support at least a basic
query operation. A query is a just character string broken up into terms and 
operators. There are two types of terms: Single Terms and Phrases.

* A Single Term is a single word such as "test" or "hello".
* A Phrase is a group of words surrounded by double quotes such as "keyword1 
keyword 2".

Multiple terms can be combined together with Boolean operators (e.g. AND, OR) to
form a more complex query. A search can be performed either specify a field,
or use the default field. The field names and default field is implementation
specific. An MSR should support searching in any field by typing the field name
followed by a colon ":" and then the appropriate term. An example of a query,
assuming there are two terms included in it is the following:

\vspace*{-0.9cm}
```{.jql caption="MSR query format example"}
instanceId:"usr:mrn:mcp:msr:int:specification:test" AND version=0.0.1
```

If the *instanceId* is the default field, then field indicator is not required:

\vspace*{-0.9cm}
```{.jql caption="MSR query format example with default field"}
"usr:mrn:mcp:msr:int:specification:test" AND version=0.0.1
```

Wildcard searches should also be supported. 

* To perform a single character wildcard search use the "?" symbol.
* To perform a multiple character wildcard search use the "*" symbol.

#### MRN of Service Documents for Identification

Before registering a service, a service provider should be compliant with the
provisions of the MRN scheme [8] for the identification of service documents.
G-1128 clearly states MRN as a unique identifier scheme. A service provider
should follow the MRN scheme of the MIR Instance Provider (who operates a MIR)
that they belong. There is also the possibility of having more than one MRN of a
service document for the identification.

In MSR, the primary identification MRN needs to be aligned with the MCP MRN
scheme, defined in "MCC Identity Management and Security; Identity Management"
[9] as follows:

\vspace*{-0.9cm}
```{.markdown caption="MCP MRN Scheme Rules"}
<MCP-MRN> ::= "urn" ":" "mrn" ":" "mcp" ":" <MCP-TYPE> ":" <IPID> ":" <IPSS>
<MCP-TYPE> ::= "device" | "org" | "user" | "vessel" | "service" | "mir" | "msr" | "mms" |
<IPID> ::= <CountryCode> | (alphanum) 0*20(alphanum / "-") (alphanum)
<IPSS> ::= pchar *(pchar / "/")
```

For a service document, the MRN system is defined as follows:

\vspace*{-0.9cm}
```{.markdown caption="MSR Service Document MRN-IPSS Definition"}
<MSR-IPSS> ::= <ORG> ":" <G1128-TYPE> ":" <SERVICE-NAME>
<ORG> ::= pchar *(pchar / "/")
<G1128-TYPE> ::= "instance" | "specification" | "design"
```

The ```<ORG>``` section represents an organization ID assigned by MIR, 
```<G1128-TYPE>``` represents the type of the documentation, i.e. specification,
design, or instance, and ```<SERVICE-NAME>``` can be any specific string 
representing a unique identifier of a service.

More detailed description of the syntax is given in the referenced document.

Governance of MRN of service documents is the responsibility of an MSR provider, 
as well as the uniqueness of an MRN at the database level.

## Functional and non-functional requirements
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

### Functional Requirements

The table below lists applicable existing functional requirements for the MSR
service.

<!-- Spacing: | --- | --- | ------ | --- | -->
| Requirement Id | Requirement Name                 | Requirement Text                                                 | References |
| --- | --- | ------ | --- |
| MSR-FR001      | Service Registration             | Allow the registrations of new service.                          | MCC MSR WG |
| MSR-FR002      | Service Registration Update      | Allow updates on an existing service instance registrations.     | MCC MSR WG |
| MSR-FR003      | Service Registration Cancelation | Allow the deletion of an existing service instance registration. | MCC MSR WG |
| MSR-FR004      | Service Discoverability          | Allow services to be discoverable as per SECOM.                  | MCC MSR WG |

The following tables define additional requirements for the MSR service.

<!-- Spacing: | --- | --------- | -->
| Requirement Id   | MSR-FR005                                                                               | 
| --- | --------- |
| Requirement Name | G-1128 Support                                                                          |
| Requirement Text | Support the registration of services following the G-1128 Service Instance XML schemas. |
| Rationale        | G-1128 standardizes the description of e-Navigation service instances.                  |
| Author           | GRAD                                                                                    |

<!-- Spacing: | --- | --------- | -->
| Requirement Id   | MSR-FR006                                                                     |
| --- | --------- |
| Requirement Name | Service Instance Documentation                                                |
| Requirement Text | Support multiple to documents to be attached to a service registration.       |
| Rationale        | Multiple documentation sources are frequently required to describe a service. |
| Author           | GRAD                                                                          |

#### Non-Functional Requirements

The table below lists applicable existing non-functional requirements for the
MSR service.

<!-- Spacing: | --- | --- | ------ | --- | -->
| Requirement Id | Requirement Name | Requirement Text                                                                                                     | References |
| --- | --- | ------ | --- |
| MSR-NFR001     | Authenticity    | The service consumers must be able to verify the authenticity of the received data.                                   | MCC MSR WG |
| MSR-NFR002     | Integrity       | It must be clear to both service providers and consumers whether changes have been made to the registered services.   | MCC MSR WG |
|  MSR-NFR003    | Availability    | The service must be available at least at a 99% availability rate.                                                    | MCC MSR WG |

The tables below define additional non-functional requirements for the MSR
service.

<!-- Spacing: | --- | --------- | -->
| Requirement Id   | MSR-NFR004                                                                                             |
| --- | --------- |
| Requirement Name | Performance                                                                                            |
| Requirement Text | The service must respond to a request in a timely fashion and not allow any request call to timeout.   | 
| Rationale        | Performance, especially in terms of service discoverability is crucial for a smooth service provision. |
|  Author          | GRAD                                                                                                   |

<!-- Spacing: | --- | --------- | -->
| Requirement Id   | MSR-NFR005                                                                                                                                                                       |
| --- | --------- |
| Requirement Name | Modularity                                                                                                                                                                       |
| Requirement Text | The services architecture must be constructed in such a way that individual functionality can be extended, modified or deleted, without changing the basic service architecture. |
| Rationale        | The MSR should be easily upgradable to ensure future operations.                                                                                                                 |
| Author           | GRAD                                                                                                                                                                             |

## Other constraints

Inter-compatibility with the other MCP components, namely the MIR and the MMS
should be ensured. In regard to different versions, the MSR should make clear
which MCP version it supports and if more than one.

### Relevant industrial standards
<!--
    List in this section the relevant industrial standards (if any) for the
    exchange of this type of data and or this type of service.  These may
    include, for example, OGC, WFS, WMS, etc.
-->

Apart from SECOM, there are no other relevant industrial standards found.

### Operational nodes
<!--
    If an operational model exists in external documents, then this section just
    shows the Service to Nodes mapping by providing three tables, as described
    below.

    If no external operational model exists, then the relevant operational nodes
    and their context shall be briefly described here before listing them in the
    tables of service providers and consumers.
-->

The following tables describe the operational nodes of the service.

#### Operational nodes providing the MSR service

<!-- Spacing: | --- | --------- | -->
| Operational Node      | Remarks                                                                                              | 
| --- | --------- |
| MCP Instance Provider | The notion of an MSR instance provider includes all entities able to make an MSR instance available. |

#### Operational nodes consuming the MSR service

<!-- Spacing: | --- | --------- | -->
| Operational Node  | Remarks                                                                                                                                  |
| --- | --------- |
| Service Provider  | The notion of a service provider includes all entities able to host and provide e-Navigation data services.                              |
| Service Consumer  | The notion of a service consumer includes all entities, human and non-human able to lookup and use the registered e-Navigation services. |

<!-- #### Operational activities (Optional) -->
<!--
    Optional. If an operational model exists and provides sufficient details 
    about operational activities, then this section shall include a mapping of 
    the service to the relevant operational activities.
-->

<!-- Spacing: | --- | --- | -->
<!--
| Operational Activity  | Remarks |
| --- | --- |
| TBD                   |         |
-->

# Service overview
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

## Service interfaces

<!--
    Describe the interfaces of the service including the selected Message 
    Exchange Pattern (MEP) by using an UML diagrams that illustrates the service
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

This section describes the interfaces of the service including the selected 
Message Exchange Pattern (MEP) by using UML diagrams that illustrate the 
service interfaces definitions and operations and in tabular form.

![MSR Interface Definition Diagram](materials/interfacedefinitions.drawio.png)

<!-- Spacing: | --- | --- | --- | -->
| Service Interface             | Role (from service provider point of view) | Service Operation                                                                                     | 
| --- | --- | --- |
| SearchServiceInterface        | Provided                                   | searchService                                                                                         |
| InstanceInterface             | Provided                                   | getInstance \newline createInstance \newline updateInstance \newline deleteInstance                   |
| InstanceStatusInterface       | Provided                                   | updateInstanceStatus                                                                                  |
| InstanceLedgerStatusInterface | Provided                                   | updateInstanceLedgerStatus                                                                            |
| XmlInterface                  | Provided                                   | getXmls \newline getXml \newline createXml \newline UpdateXml \newline deleteXml                      |
| XmlValidationInterface        | Provided                                   | validateXml                                                                                           |
| DocInterface                  | Provided                                   | getDocs \newline getDoc \newline createDoc \newline UpdateDoc \newline deleteDoc                      |
| LedgerRequestsInterface       | Provided                                   | getLedgerRequests \newline getLedgerRequest \newline createLedgerRequest \newline deleteLedgerRequest |
| LedgerRequestStatusInterface  | Provided                                   | updateLedgerRequestStatus                                                                             |

A more detailed description on the implementation of the defined interfaces
can be found in the OpenAPI documentation (version 3.0.1) provided in the
[Annex A](#annex-a-openapi-documentation) and
[Annex B](#annex-b-secom-openapi-documentation) sections.

# Service Data Model
<!--
    It is recommended to visualise the data structures by using UML diagrams.
    The full information model (logical data structure) shall be shown using
    diagram(s) and explanatory tables (see below).

    Example of an UML diagram:

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

This section describes the information model, i.e., the logical data structures
to be exchanged between providers and consumers of the service.  As suggested by
the IALA G-1128 guideline, the data structure of the MSR implementation are 
visualised in the following UML digram.

![MSR UML Data Model Diagram](materials/umldiagram.png)

As demonstrated by the displayed diagram, there are four main data structures
employed by the MSR:

* The Instance Model
* The Xml Model
* The Doc Model
* The LedgerRequest Model

Each has its own unique purpose and should be used accordingly.

<!-- ### Service internal data model (Optional) -->
<!--
    Optionally, this section may provide a description of the internal data
    model, as it seems appropriate to the service provider and/or the service
    consumer side.  Such description might be helpful for the better
    understanding as it provides additional information about the building of
    the service.  However, it should be considered just as an example – it is
    not an authoritative part of the service specification.
-->

# Service Interface Specifications
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
is described in the [Service Dynamic Behaviour](#service-dynamic-behaviour)
section.

## Service Interface "SearchServiceInterface"
<!--
    Please explain the purpose, message exchange pattern and architecture of 
    the Interface.

    A Service Interface supports one or several service operations.  Each 
    operation in the service interface shall be described in the following 
    sections.
-->

The ***SearchServiceInterface*** interface is mandated by SECOM to allow service
consumers to use a SECOM-compliant Service Registry. Since the MSR
implementation aspires to be a fully SECOM-compliant service, it is mandatory
that this interface is implemented as required.

#### Operation "searchService"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The purpose of the interface's ***searchService*** operation is to allow service
consumers to query the MSR about registered instances of e-Navigation services
with specific properties, i.e. able to produce a compatible IALA S-100 [10] data 
product dataset. It is implemented following the REST methodology, using a POST
HTTP method. It receives a *SearhFilterObject* object, which contains all the
necessary parameters required to identify a set of matching registered services.
The MSR will respond with a list of matching service instances, encoded into
*SearchObjectResult* objects, in a paged response. The internal structure of
both the *SearhFilterObject* and *SearchObjectResult* objects is governed by the
SECOM standard.

##### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request with a valid *SearhFilterObject* payload, the service 
will first determine which of the applicable search filters are to be applied. 
This operation includes parsing the *freetext* field of the *SearhFilterObject* 
object, if it have been populated. This should be processed according to the
rules outlined in the [Service Discoverability](#service-discoverability) 
section. The parsing output should then be combined with the additional 
*SearhFilterObject* fields to generate the complete set of search filters to be
applied.

The applicable filters are then matched against the indexed database fields of
the registered services instances and the results are gathered and returned as
a paged response. Only the results of the page that has been selected by the
service consumer are returned. Navigation to other pages can be achieved by
repeating the same search query, with a difference page index parameter.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | ------ | --- | --- | --------- | -->
| Parameter (in)   | Encoding | Mult. | Description                                                         |
| ------ | --- | --- | --------- |
| SearhFilterObject | JSON    | 1     | The object contains information on the search filters to be applied |

<!-- Spacing: | ------ | --- | --- | --------- | -->
| Return Type (out)  | Encoding | Mult. | Description                                                                                  |
| ------ | --- | --- | --------- |
| SearchObjectResult | JSON     | 0..*  | A list of Instances, matching the requested criteria, encoded as per the SECOM documentation |

## Service Interface "InstanceInterface"
<!--
    Please explain the purpose, message exchange pattern and architecture of 
    the Interface.

    A Service Interface supports one or several service operations.  Each 
    operation in the service interface shall be described in the following 
    sections.
-->

The ***InstanceInterface*** interface allows service providers to interact with
the MSR in order to retrieve and manipulate the data on the registered service
instances. A service provider should be able to access information about all
registered service instances, but should only be allowed to modify/delete data
related to services it provides. MSR administrator users however, are allowed to
perform any data modifications.

The interface communicates using Instance objects, the structure of which is
described in the [Service Data Model](#service-data-model) section. Each
Instance object contains two additional fields, namely the *instanceAsXml* and
*instanceAsDoc*, that describe the IALA G-1128 service specification details in
XML and human-readable text formats using the Xml and Doc objects respectively.

### Operation "getInstances"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The purpose of the interface's ***getInstances*** operation is to enable service
providers to access a complete list of the registered service instances, without
calling the more specialised but also expensive (resource-wise) SearchService
interface. It is implemented following the REST methodology, using a GET HTTP 
method. It receives only a page number and a page size as input parameters.
The MSR will respond with a list of all Instance objects, in a paged response.
The internal structure of the Instance object is provided in more detail in the
[Service Data Model](#service-data-model) section.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to retrieve all registered service instances, the MSR
will access its database to retrieve and package the full list of Instance 
objects into a paged response. Only the results of the page that has been 
selected by the service consumers are returned. Navigation to other pages can
be achieved by repeating the same search query, with a difference page index
parameter.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter   | Encoding   | Mult | Description                                             |
| --- | --- | --- | --------- |
| page        | QueryParam | 0..1 | The number of the page the results to be returned       |
| pageSize    | QueryParam | 0..1 | The maximum size of each page that contains the results |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out) | Encoding | Mult.  | Description                                                                                          |
| --- | --- | --- | --------- |
| Page              | JSON     | 0..*   | A paged list of Instances, matching the requested criteria, structured as per the service data model |

### Operation "getInstance"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The purpose of the interface's ***getInstance*** operation is to enable service
providers to access the information of a single registered service instance. 
It is implemented following the REST methodology, using a GET HTTP method. It 
receives the ID of the Instance to be retrieved as an input argument. The MSR
will respond with the Instance object identified by the provided ID, if that is
found. The internal structure the Instance is provided in more detail in the 
[Service Data Model](#service-data-model) section.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to retrieve a specific registered service instance, the
MSR will access its database to locate, retrieve and package the Instance
object that matches the provided ID. If the ID is not located, for example
because it has  been selected by mistake, the service will make that clear in
the response generated.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter (in) | Encoding  | Mult. | Description                                             |
| --- | --- | --- | --------- |
| instanceId     | PathParam | 1     | The ID of the Instance object to be retrieved           |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out) | Encoding | Mult. | Description                                      |
| --- | --- | --- | --------- |
| Instance          | JSON     | 1     | The Instance object that matches the provided ID |

### Operation "createInstance"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The purpose of the interface's ***createInstance*** operation is to enable
service providers to create new entries of registered service instances. It is
implemented following the REST methodology, using a POST HTTP method. It
receives as an input a populated Instance object that contains all the mandatory
information. The MSR will  respond with a copy of the Instance object created,
including its assigned ID. The internal structure of the Instance object is
provided in more detail in the [Service Data Model](#service-data-model)
section.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to create a new registered service instance, the MSR
will access and validate the provided Instance fields, and depending on a
successful outcome, will persist the data in its database. If an error occurs
while persisting the provided Instance object, the service will make that clear
in the response generated.

It has to be noted at this point, that since the Instance objects are linked
with the Xml and Doc entries through the *instanceAsXml* and *instanceAsDoc*
fields, these should also be provided if necessary. The information from the XML
source provided by the Xml object, will be used to populate the respective
fields of the Instance object, overwriting any existing values. The Doc object
on the other hand, can be used to provide the human-readable text documentation.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter (in) | Encoding | Mult. | Description                                                           |
| --- | --- | --- | --------- |
| instance       | JSON     | 1     | The Instance object to be created with all mandatory fields populated |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out) | Encoding | Mult. | Description                                                     |
| --- | --- | --- | --------- |
| Instance          | JSON     | 1     | The Instance object that was created along with its assigned ID |


### Operation "updateInstance"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The purpose of the interface's ***updateInstance*** operation is to enable
service providers to update existing entries of registered service instances.
It is implemented following the REST methodology, using a PUT HTTP method. It
receives as an input a populated Instance object that contains all the mandatory
information. The MSR will respond with a copy of the Instance object updated.
The internal structure of the Instance object is provided in more detail in the
[Service Data Model](#service-data-model) section.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to update an existing registered service instance, the
MSR will access and validate the provided Instance fields, and depending on 
a successful outcome, will persist the data in its database. If an error occurs
while persisting the provided Instance object, the service will make that clear
in the response generated.

It has to be noted at this point that although the Instance objects are linked
with the Xml and Doc entries through the *instanceAsXml* and *instanceAsDoc*
fields, there is a clear distinction in how the service handles the two in an
update operation. The information from the XML source provided by the Xml
object, will be used to populate the respective fields of the Instance object,
overwriting any existing values, exactly as described in the
["createInstance"](#operation-createinstance) operation. In order to minimise
the amount of information exchange however, there is no need to re-upload the
Doc object of the Instance. It is sufficient to provide an empty Doc object
with just the ID field populated, so that the service can validate that there 
has not been change.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter (in) | Encoding | Mult. | Description                                                           |
| --- | --- | --- | --------- |
| instance       | JSON     | 1     | The Instance object to be updated with all mandatory fields populated |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out) | Encoding | Mult. | Description                          |
| --- | --- | --- | --------- |
| Instance          | JSON     | 1     | The Instance object that was updated |

### Operation "deleteInstance"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The purpose of the interface's ***deleteInstance*** operation is to enable
service providers to delete existing entries of registered service instances. It
is implemented following the REST methodology, using a DELETE HTTP method. It
receives as an input the ID of the registered Instance to be deleted. The MSR
will respond with the outcome of the deletion operation, if successful or not.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to delete an existing registered service instance, the
MSR will validate the respective entry indeed exists in its database. In that
case, the Instance record will be deleted and the service will send a response
to the original request. If an error occurs while deleting the identified
Instance object, the service will make that clear in the response generated.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter (in) | Encoding  | Mult. | Description                          |
| --- | --- | --- | --------- |
| instanceId     | PathParam | 1     | The ID of the Instance to be deleted |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out)     | Encoding | Mult. | Description                          |
| --- | --- | --- | --------- |
| result from operation | none     | 1     | The result of the deletion operation |

## Service Interface "InstanceStatusInterface"
<!--
    Please explain the purpose, message exchange pattern and architecture of 
    the Interface.

    A Service Interface supports one or several service operations.  Each 
    operation in the service interface shall be described in the following 
    sections.
-->

The ***InstanceStatusInterface*** interface allows service providers to 
manipulate the status of their registered service instances. The status value of
each instance is restricted to the options specified in the IALA G-1128 
guideline. As per the enumeration displayed in the UML diagram of the
[Service Data Model](#service-data-model) sectionm, these options are:

* PROVISIONAL
* RELEASED
* DEPRECATED
* DELETED

A service provider should only be able to alter information on the services
Instances it provides. MSR administrator users however, are allowed to perform
any data modifications.

### Operation "updateInstanceStatus"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The purpose of the interface's ***updateInstanceStatus*** operation is to allow
service providers to update the registration status of the service instances
they provide. It is implemented following the REST methodology, using a PUT HTTP 
method. It receives as input the ID of the Instance of which the status will be
updated, as well as the new applicable Instance status value. The MSR will
respond with the outcome of the update operation, if successful or not.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to update a service Instance registration status, the
MSR will access its database to validate that the Instance ID provided is indeed
valid. If that is the case, the status of the retrieved Instance entry will be
updated. The MSR will finally respond with the outcome of the update operation,
if successful or not.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter      | Encoding   | Mult | Description                                                              |
| --- | --- | --- | --------- |
| instanceId     | PathParam  | 1    | The ID of the Instance for which the registration status will be updated |
| instanceStatus | QueryParam | 1    | The new value for the registration status of the selected Instance       |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out)     | Encoding | Mult. | Description                               |
| --- | --- | --- | --------- |
| result from operation | none     | 1     | The result of the status update operation |

## Service Interface "InstanceLedgerStatusInterface" (Optional)
<!--
    Please explain the purpose, message exchange pattern and architecture of 
    the Interface.

    A Service Interface supports one or several service operations.  Each 
    operation in the service interface shall be described in the following 
    sections.
-->

The ***InstanceStatusInterface*** interface allows service providers to
manipulate the MSR global ledger status of their registered service Instances.
This is an optional interface meaning, it is only required if the MSR is connected
to an MSR global ledger service. This will make the registered services globally
available and discoverable through other MSR instances.

The status of each Instance is restricted to the options specified by the global
ledger service provider. As a guideline, the UML diagram in the 
[Service Data Model](#service-data-model) section provides the following
options:

* INACTIVE
* CREATED
* VETTING
* VETTED
* REQUESTING
* SUCCEEDED
* FAILED
* REJECTED

A service provider should be able to alter information only on the services
Instances it provides. MSR administrator users however, are allowed to perform
any data modifications.

### Operation "updateInstanceLedgerStatus"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The purpose of the interface's ***updateInstanceLedgerStatus*** operation is to
allow service providers to further register a provided service Instance to the
MSR global ledger, if that functionality is supported. The operation is 
implemented following the REST methodology, using a PUT HTTP method. It receives
as input the ID of the Instance of which the global registration status will be
updated, as well as the new applicable LedgerRequestStatus value. The MSR will
respond with the outcome of the update operation, if successful or not.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to update a service instance's global registration 
status, the MSR will access its database to validate that the Instance ID 
provided is indeed valid. If that is the case, the MSR will return a response
to the initial request and at the same time can initiate a request to the MSR
global ledger service to update the global registration status value, for the
specified service instamce. After a successful response from the ledger, the MSR
will update its own local copy of the Instance based on the received response. 

The process of contacting the MSR global ledger service described above, is
executed in an asynchronous manner, meaning the original request to the MSR will
be answered before the global ledger service is updated. Service providers can
only be informed on the final outcome, once this asynchronous process has been
completed.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter           | Encoding   | Mult | Description                                                                     |
| --- | --- | --- | --------- |
| instanceId          | PathParam  | 1    | The ID of the Instance for which the global registration status will be updated |
| ledgerRequestStatus | QueryParam | 1    | The new value for the global registration status of the selected Instance       |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out)     | Encoding | Mult. | Description                                                   |
| --- | --- | --- | --------- |
| result from operation | none     | 1     | The result of the global registration status update operation |

## Service Interface "XmlInterface"
<!--
    Please explain the purpose, message exchange pattern and architecture of 
    the Interface.

    A Service Interface supports one or several service operations.  Each 
    operation in the service interface shall be described in the following 
    sections.
-->

The ***XmlInterface*** interface allows service providers and consumers to
interact with the MSR in order to retrieve and manipulate the data on the
registered service instances' XML documents. A service provider should be able
to access information about all registered service Instances but should only be
allowed to alter/delete data related to the services it provides. Service
consumers on the other hand, should only be allowed access operations to XML
documents of the discovered Instances. MSR administrator users however, are
allowed to perform any data modifications.

### Operation "getXmls"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The purpose of the interface's ***getXmls*** operation is to enable service
providers to access a complete list of the registered service instances' XML
documents directly. It is implemented following the REST methodology, using a
GET HTTP method. It receives only a page number and page size as input
parameters. The MSR will respond with a list of all Xml objects, in a paged
response. The internal structure the Xml object is provided in more detail in
the [Service Data Model](#service-data-model) section.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to retrieve all available XML documents, the MSR will
access its database to retrieve and package the full list of Xml objects into a
paged response. Only the results of the page that has been selected by the
service consumers are returned. Navigation to other pages can be achieved by
repeating the same search query, with a difference page index parameter.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter   | Encoding   | Mult | Description                                             |
| --- | --- | --- | --------- |
| page        | QueryParam | 0..1 | The number of the page the results to be returned       |
| pageSize    | QueryParam | 0..1 | The maximum size of each page that contains the results |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out) | Encoding | Mult.  | Description                                                                                    |
| --- | --- | --- | --------- |
| Page              | JSON     | 0..*   | A paged list of Xml, matching the requested criteria, structured as per the service data model |

### Operation "getXml"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The purpose of the interface's ***getXml*** operation is to enable service
providers and consumers to access the information of a single XML document. It
is implemented following the REST methodology, using a GET HTTP method. It
receives the ID of the Xml to be retrieved as an input argument. The MSR will
respond with the Xml object identified by the provided ID, if that is found. The
internal structure of the Xml object is provided in more detail in the 
[Service Data Model](#service-data-model) section.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to retrieve a specific XML document, the MSR will
access its database to locate, retrieve and package the Xml object that matches
the provided ID. If the ID is not located, for example because it has been
selected by mistake, the service will make that clear in the response generated.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter (in) | Encoding  | Mult. | Description                              |
| --- | --- | --- | --------- |
| xmlId          | PathParam | 1     | The ID of the Xml object to be retrieved |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out)  | Encoding | Mult. | Description                                 |
| --- | --- | --- | --------- |
| Xml                | JSON     | 1     | The Xml object that matches the provided ID |

### Operation "createXml"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The XML documents of the registered services are normally uploaded to the MSR
as part of the [InstanceInterface createInstance](#operation-createinstance)
operation. Therefore, it is highly unlikely that the ***createXml*** operation
should ever be required by any service provider, while it should not be allowed
for any service consumer. The main purpose of the interface's ***createXml***
operation to allow the system administrators to correct issues related to the
registered instances' XML documents. It is implemented following the REST
methodology, using a POST HTTP method. It receives as an input a populated Xml
object that contains all the mandatory information, including the applicable
registered service Instance ID. The MSR will respond with a copy of the Xml
object created, including its assigned ID. The internal structure of the Xml
object is provided in more detail in the
[Service Data Model](#service-data-model) section.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to create a new Xml record, the MSR will access and
validate the provided Xml object fields, and depending on a successful outcome,
will persist the data in its database. If an error occurs while persisting the
provided Xml object, the service will make that clear in the response generated.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter (in) | Encoding | Mult. | Description                                                      |
| --- | --- | --- | --------- |
| xml            | JSON     | 1     | The Xml object to be created with all mandatory fields populated |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out) | Encoding | Mult. | Description                                                |
| --- | --- | --- | --------- |
| Xml               | JSON     | 1     | The Xml object that was created along with its assigned ID |


### Operation "updateXml"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The XML documents of the registered services are normally updated on the MSR
as part of the [InstanceInterface updateInstance](#operation-updateinstance)
operation. Therefore, it is highly unlikely that the ***updateXml*** operation
should ever be required by any service provider, while it should not be allowed
for any service consumer. The main purpose of the interface's ***updateXml***
operation to allow the system administrators to correct issues related to the
registered instances' XML documents. It is implemented following the REST
methodology, using a PUT HTTP method. It receives as an input a populated Xml
object that contains all the mandatory information. The MSR will respond with a
copy of the Xml object updated. The internal structure of the Xml object is
provided in more detail in the [Service Data Model](#service-data-model)
section.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to update an existing Xml record, the MSR will access
and validate the provided Xml object fields, and depending on a successful
outcome, will persist the data in its database. If an error occurs while
persisting the provided Xml object, the service will make that clear in the
response generated.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter (in) | Encoding | Mult. | Description                                                      |
| --- | --- | --- | --------- |
| xml            | JSON     | 1     | The Xml object to be updated with all mandatory fields populated |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out) | Encoding | Mult. | Description                     |
| --- | --- | --- | --------- |
| Xml               | JSON     | 1     | The Xml object that was updated |

### Operation "deleteXml"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The XML documents of the registered service are normally manipulated as part of
the [InstanceInterface createInstance](#operation-createinstance) and
[InstanceInterface updateInstance](#operation-updateInstance) operations.
Therefore, it is highly unlikely that the ***deleteXml*** operation should ever
be required by any service provider, while it should not be allowed for any
service consumer. The main purpose of the interface's ***deleteXml*** operation
to allow the system administrators to correct issues related to the registered
Instances XML documents. It is implemented following the REST methodology using
a DELETE HTTP method. It receives as an input the ID of the Xml object to be
deleted. The MSR will respond with the outcome of the deletion operation,
whether successful or not.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to delete an existing Xml record, the MSR will validate
the respective entry indeed exists in its database. If an error occurs while
deleting the identified Xml object, the service will make that clear in the
response generated.

#### Operation parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter (in) | Encoding  | Mult. | Description                     |
| --- | --- | --- | --------- |
| xmlId          | PathParam | 1     | The ID of the Xml to be deleted |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out)     | Encoding | Mult. | Description                          |
| --- | --- | --- | --------- |
| result from operation | none     | 1     | The result of the deletion operation |

## Service Interface "XmlValidationInterface"
<!--
    Please explain the purpose, message exchange pattern and architecture of 
    the Interface.

    A Service Interface supports one or several service operations.  Each 
    operation in the service interface shall be described in the following 
    sections.
-->

The ***XmlValidationInterface*** interface allows service providers to validate
whether the XML service Instance specifications to be uploaded to the MSR are
indeed valid. Since the compilation of a valid G-1128 specifications could be
seen as cumbersome task, this interface intends to alleviate some of the
complexities by automatically parsing the provided XML and reporting back any
errors detected.

### Operation "validateXml"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The purpose of the interface's ***validateXml*** operation is to allow
service providers to perform the actual validation task for their G-1128 XML
specifications.

Although only the G-1128 Instance Specification documentation is actually
mandatory for an MSR implementation, this interface can allow the verification
of all three levels of G-1128 specifications. These are modeled  by the
***G1128Schemas*** enumeration, found in the
[Service Data Model](#service-data-model) section.

* SERVICE
* DESIGN
* INSTANCE

The operation is implemented following the REST methodology, using a POST HTTP
method. It receives as an input the G1128Schemas type to be used for the
validation and the XML input to be validated.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to validate an XML input based on a G-1128 schema
specification, the MSR will access its database to retrieve the requested G-1128
schema. Afterwards it will attempt to parse the provided XML input using the
detected schema. The MSR will finally respond with the outcome of the parsing
operation, if successful or not. When the validation process is completed
successfully, the response will contain the unmarshalled XML object encoded
using JSON. If any errors have been detected, they will be described as clearly
as possible in the error response.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter | Encoding  | Mult | Description                                                           |
| --- | --- | --- | --------- |
| schema    | PathParam | 1    | The the ID of the G-1128 schema to be used for the validation         |
| xml       | XML       | 1    | The XML input to be validated against the G-1128 schema specification |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out) | Encoding | Mult. | Description                                                             |
| --- | --- | --- | --------- |
| Object            | JSON     | 1     | The umarshalled object generated after the successful parsing operation |

## Service Interface "DocInterface"
<!--
    Please explain the purpose, message exchange pattern and architecture of 
    the Interface.

    A Service Interface supports one or several service operations.  Each 
    operation in the service interface shall be described in the following 
    sections.
-->

The ***DocInterface*** interface allows service providers and consumers to
interact with the MSR in order to retrieve and manipulate the data on the
registered service instances' Doc documents. A service provider should be able
to access information about all registered service instances, but should only be
allowed to alter/delete data related to the services it provides. Service
consumers on the other hand, should only be allowed access operations to Doc
documents of the discovered Instances. MSR administrator users however, are
allowed to perform any data modifications.

### Operation "getDocs"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The purpose of the interface's ***getDocs*** operation is to enable service
providers to access a complete list of the registered service instances' Doc
documents directly. It is implemented following the REST methodology, using a
GET HTTP method. It receives only a page number and page size as input
parameters. The MSR will respond with a list of all Doc objects, in a paged
response. The internal structure of the Doc object is provided in more detail in
the [Service Data Model](#service-data-model) section.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to retrieve all available Doc documents, the MSR will
access its database to retrieve and package the full list of Doc objects into a
paged response. Only the results of the page that has been selected by the
service consumers are returned. Navigation to other pages can be achieved by
repeating the same search query, with a difference page index parameter.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter   | Encoding   | Mult | Description                                             |
| --- | --- | --- | --------- |
| page        | QueryParam | 0..1 | The number of the page the results to be returned       |
| pageSize    | QueryParam | 0..1 | The maximum size of each page that contains the results |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out) | Encoding | Mult.  | Description                                                                                            |
| --- | --- | --- | --------- |
| Page              | JSON     | 0..*   | A paged list of Doc objects, matching the requested criteria, structured as per the service data model |

### Operation "getDoc"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The purpose of the interface's ***getDoc*** operation is to enable service
providers and consumers to access the information of a single Doc document. It
is implemented following the REST methodology, using a GET HTTP method. It
receives the ID of the Doc to be retrieved as an input argument. The MSR will
respond with the Doc object identified by the provided ID, if that is found. The
internal structure of the Doc object is provided in more detail in the
[Service Data Model](#service-data-model) section.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to retrieve a specific Doc document, the MSR will
access its database to locate, retrieve and package the Doc object that matches 
the provided ID. If the ID is not located, for example because it has been 
selected by mistake, the service will make that clear in the response generated.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter (in) | Encoding  | Mult. | Description                              |
| --- | --- | --- | --------- |
| docId          | PathParam | 1     | The ID of the Doc object to be retrieved |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out) | Encoding | Mult. | Description                                 |
| --- | --- | --- | --------- |
| Doc               | JSON     | 1     | The Doc object that matches the provided ID |

### Operation "createDoc"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The relevant documents of a registered service are normally uploaded to the MSR
as part of the [InstanceInterface createInstance](#operation-createinstance)
operation. However, additional documents describing a service instance could
be required, resulting in a service Instance being associated with more than one
documents. The main purpose of the interface's ***createDoc*** operation is
to allow the service providers to upload these additional Doc documents at a
later stage, after a service has already been registered with the MSR. It is
implemented following the REST methodology, using a POST HTTP method. It receives
as an input a populated Doc object that contains all the mandatory information,
including the applicable registered service Instance ID. The MSR will respond
with a copy of the Doc object created, including its assigned ID. The internal
structure of the Doc object is provided in more detail in the
[Service Data Model](#service-data-model) section.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to create a new Doc record, the MSR will access and
validate the provided Doc object fields, and depending on a successful outcome,
will persist the data in its database. If an error occurs while persisting the 
provided Doc object, the service will make that clear in the response generated.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter (in) | Encoding | Mult. | Description                                                      |
| --- | --- | --- | --------- |
| doc            | JSON     | 1     | The Doc object to be created with all mandatory fields populated |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out)  | Encoding | Mult. | Description                                                |
| --- | --- | --- | --------- |
| Doc                | JSON     | 1     | The Doc object that was created along with its assigned ID |


### Operation "updateDoc"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The relevant documents of a registered service are normally updated on the MSR
as part of the [InstanceInterface updateInstance](#operation-updateinstance)
operation. However, additional documents describing a service Instance could
be required, resulting in a service Instance being associated with more than one
documents. The main purpose of the interface's ***updateDoc*** operation is
to allow the service providers to update the Doc documents of a service
Instance, after a service has already been registered with the MSR. It is
implemented following the REST methodology, using a PUT HTTP method. It receives
as an input a populated Doc object that contains all the mandatory information.
The MSR will respond with a copy of the Doc object updated. The internal
structure of the Doc object is provided in more detail in the
[Service Data Model](#service-data-model) section.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to update an existing Doc record, the MSR will access
and validate the provided Doc object fields, and depending on a successful
outcome, will persist the data in its database. If an error occurs while]
persisting the provided Doc object, the service will make that clear in the
response generated.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter (in) | Encoding | Mult. | Description                                                      |
| --- | --- | --- | --------- |
| doc            | JSON     | 1     | The Doc object to be updated with all mandatory fields populated |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out) | Encoding | Mult. | Description                     |
| --- | --- | --- | --------- |
| Doc               | JSON     | 1     | The Doc object that was updated |

### Operation "deleteDoc"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->


It has been mentioned previously, that additional documents describing a service
Instance could be required, resulting in a service Instance being associated
with more than one documents. The main purpose of the interface's 
***deleteDoc*** operation is to allow the service provider to remove documents
already uploaded for a registered service instance. It is implemented following
the REST methodology, using a DELETE HTTP method. It receives as an input the ID
of the Doc object to be deleted. The MSR will respond with the outcome of the
deletion operation, whether successful or not.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to delete an existing Doc record, the MSR will
validate the respective entry indeed exists in its database. If an error occurs
while deleting the identified Doc object, the service will make that clear
in the response generated.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter (in) | Encoding  | Mult. | Description                       |
| --- | --- | --- | --------- |
| docId            | PathParam | 1     | The ID of the Doc to be deleted |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out)     | Encoding | Mult. | Description                          |
| --- | --- | --- | --------- |
| result from operation | none     | 1     | The result of the deletion operation |

## Service Interface "LedgerRequestInterface" (Optional)
<!--
    Please explain the purpose, message exchange pattern and architecture of 
    the Interface.

    A Service Interface supports one or several service operations.  Each 
    operation in the service interface shall be described in the following 
    sections.
-->

The ***LedgerRequestInterface*** interface allows service providers to
interface with the MSR and access information on the registration requests made
to the global MSR ledger service, regarding their registered service instances.
A service provider should only be allowed to alter data related to the
services it provides. MSR administrator users however, are allowed to perform
any data modifications.

### Operation "getLedgerRequests"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The purpose of the interface's ***getLedgerRequests*** operation is to enable
service providers to access a complete list of the global MSR ledger service 
registration requests directly. It is implemented following the REST
methodology, using a GET HTTP method. It receives only a page number and page
size as input parameters. The MSR will respond with a list of all LedgerRequest
objects, in a paged response. The internal structure of the LedgerRequest object
is provided in more detail in the [Service Data Model](#service-data-model)
section.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to retrieve all available LedgerRequest records, the
MSR will access its database to retrieve and package the full list of
LedgerRequest objects into a paged response. Only the results of the page that
has been selected by the service consumers are returned. Navigation to other
pages can be achieved by repeating the same search query, with a difference page
index parameter.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter   | Encoding   | Mult | Description                                             |
| --- | --- | --- | --------- |
| page        | QueryParam | 0..1 | The number of the page the results to be returned       |
| pageSize    | QueryParam | 0..1 | The maximum size of each page that contains the results |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out)  | Encoding | Mult.  | Description                                                                                                      |
| --- | --- | --- | --------- |
| Page               | JSON     | 0..*   | A paged list of LedgerRequest objects, matching the requested criteria, structured as per the service data model |

### Operation "getLedgerRequest"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

The purpose of the interface's ***getLedgerRequest*** operation is to enable
service providers to access the information of a single getLedgerRequest entry.
It is implemented following the REST methodology, using a GET HTTP method. It
receives the ID of the LedgerRequest to be retrieved as an input argument. The
MSR will respond with the LedgerRequest object identified by the provided ID, if
that is found. The internal structure of the LedgerRequest object is provided in
more detail in the [Service Data Model](#service-data-model) section.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to retrieve a specific LedgerRequest entry, the MSR
will access its database to locate, retrieve and package the LedgerRequest
object that matches the provided ID. If the ID is not located, for example
because it has been selected by mistake, the service will make that clear in the
response generated.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter (in)  | Encoding  | Mult. | Description                              |
| --- | --- | --- | --------- |
| ledgerRequestId | PathParam | 1     | The ID of the LedgerRequest object to be retrieved |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out) | Encoding | Mult. | Description                                 |
| --- | --- | --- | --------- |
| LedgerRequest     | JSON     | 1     | The LedgerRequest object that matches the provided ID |

### Operation "createLedgerRequest"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

After a service Instance has been registered locally in an MSR, if the current
implementation supports a connection to a global MSR ledger service, the service
Instance can be made available to other supported MSRs. This is done by
sending a ledger request to the global MSR ledger service, usually through the
[InstanceInterface updateInstanceLedgerStatus](#operation-updateinstanceledgerstatus)
operation. Optionally, this operation can be initiated through the 
***createLedgerRequest*** operation. Note that this operation does *NOT*
contact the global MSR ledger service and will only create a local request entry
in the database. Only the ***InstanceInterface*** operation can then be used to 
update the global registration status. Therefore, it can be assumed that this
operation is primarily for administration purposes.

The operation is implemented following the REST methodology, using a POST HTTP
method. It receives as an input a populated LedgerRequest object that contains
all the mandatory information, including the applicable registered service
Instance ID. The MSR will respond with a copy of the LedgerRequest object
created, including its assigned ID. The internal structure of the LedgerRequest
object is provided in more detail in the
[Service Data Model](#service-data-model) section.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to create a new LedgerRequest record, the MSR will
access and validate the provided LedgerRequest object fields, and depending on a
successful outcome, will persist the data in its database. If an error occurs
while persisting the provided LedgerRequest object, the service will make that
clear in the response generated.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter (in) | Encoding | Mult. | Description                                                      |
| --- | --- | --- | --------- |
| LedgerRequest  | JSON     | 1     | The LedgerRequest object to be created with all mandatory fields populated |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out) | Encoding | Mult. | Description                                              |
| --- | --- | --- | --------- |
| LedgerRequest     | JSON     | 1     | LedgerRequest Doc object that was created along with its assigned ID |

### Operation "deleteLedgerRequest"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

Each service Instance, registered with an MSR, can only have at most one 
LedgerRequest entry associated with it. Therefore, if something goes wrong, it
might be required to delete this entry in order to create a new one. The 
***deleteLedgerRequest*** provides this functionality and is mainly used by
administrator users to correct this kind of issues. It is implemented following
the REST methodology, using a DELETE HTTP method. It receives as an input the ID
of the LedgerRequest object to be deleted. The MSR will respond with the outcome
of the deletion operation, whether successful or not.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to delete an existing LedgerRequest record, the MSR
will validate the respective entry indeed exists in its database. If an error
occurs while deleting the identified LedgerRequest object, the service will make
that clear in the response generated.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | --- | --- | --- | --------- | -->
| Parameter (in)  | Encoding  | Mult. | Description                               |
| --- | --- | --- | --------- |
| ledgerRequestId | PathParam | 1     | The ID of the LedgerRequest to be deleted |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out)     | Encoding | Mult. | Description                          |
| --- | --- | --- | --------- |
| result from operation | none     | 1     | The result of the deletion operation |

## Service Interface "LedgerRequestStatusInterface" (Optional)
<!--
    Please explain the purpose, message exchange pattern and architecture of 
    the Interface.

    A Service Interface supports one or several service operations.  Each 
    operation in the service interface shall be described in the following 
    sections.
-->

The ***LedgerRequestStatusInterface*** interface allows service providers to
communicate with the global MSR ledger service, if that is available, in order
to request an update on the global registration status of a registered service
instance. A Service provider should only be allowed to alter data related to the
services it provides. MSR administrator users however, are allowed to perform
any data modifications.

### Operation "updateLedgerRequestStatus"
<!--
    Give an overview of the operation: Include here a textual description of
    the operation functionality. In most situations this will be the same as
    the operation description taken from the UML modelling tool.
-->

After a service Instance has been registered locally in an MSR, if the current
implementation supports a connection to a global MSR ledger service, the service
Instance can be made available to other connected MSRs. This is done by sending
a ledger request to the global MSR ledger service, usually through the
[InstanceInterface updateInstanceLedgerStatus](#operation-updateinstanceledgerstatus)
operation. Alternatively, if a LedgerRequest entry has already been created and
its assigned ID is known, this operation can be performed through the
***updateLedgerRequestStatus*** operation.

This operation is implemented following the REST methodology, using a PUT HTTP
method. It receives as an input the ID of an already initialised LedgerRequest
object that provides all the mandatory information, including the applicable
registered service Instance ID. In addition, the new global registration status
value is required. The MSR will respond with the outcome of the update
operation, if successful or not.

#### Operation Functionality
<!--
    Describe the functionality of the operation, i.e. how does it produce the
    output from the input payload.
-->

Upon receiving a request to update a service instance's global registration
status for a specific LedgerRequest entry, the MSR will access its database to
validate that the LedgerRequest ID provided is indeed valid. If that is the
case, the MSR will return a response to the initial request and at the same time
can initiate a request to the MSR global ledger service to update the global
registration status value, for the specified service instance. After a
successful response from the ledger, the MSR will update its own local copy of
the Instance based on the received response.

As in the 
[InstanceInterface updateInstanceLedgerStatus](#operation-updateinstanceledgerstatus)
operation, the process of contacting the MSR global ledger service described
above, is executed in an asynchronous manner, meaning the original request to
the MSR will be answered before the global ledger service is updated. Service
providers will only be informed on the final outcome, once this asynchronous 
process has been completed.

#### Operation Parameters
<!--
    Describe the logical data structure of input and output parameters of the 
    operation (payload) by using an explanatory table (see below) and optionally
    UML diagrams (which are usually sub-sets of the service data model described
    in previous section above).

    Figure 9 shows an example of a UML diagram (subset of the service data 
    model, related to one operation).

    It is mandatory to provide a table with a clear description of each service
    operation parameter and the information about which data types defined in
    the service data mode are used by the service operation in its input and
    output parameters.

    Note: While the descriptions provided in the service data model shall 
    explain the data types in a neutral format, the descriptions provided here 
    shall explicitly explain the purpose of the parameters for the operation.
-->

<!-- Spacing: | ------ | --- | --- | ------------ | -->
| Parameter (in)      | Encoding   | Mult. | Description                                                                                               |
| ------ | --- | --- | ------------ |
| ledgerRequestId     | PathParam  | 1     | The ID of the ledger request to update the global regidstration status of the respective service Instance |
| ledgerRequestStatus | QueryParam | 1     | The global regidstration status requested by the global MSR ledger service request                        |

<!-- Spacing: | --- | --- | --- | --------- | -->
| Return Type (out)     | Encoding | Mult. | Description                          |
| --- | --- | --- | --------- |
| result from operation | none     | 1     | The result of the deletion operation |


# Service Dynamic Behaviour
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

This section describes the interactive behaviour between service interfaces
(interaction specification) and, if required, between different services
(orchestration).

## Service Interface "SearchServiceInterface"
<!--
    Include some information about the dynamic aspects of the service
    interface; each operation shall be exposed on at least one diagram.
    An example sequence diagram is shown in Figure 4.
-->

As described in the
[SearchService Interface](#service-interface-searchserviceinterface) section, the
MSR service discovery operation is performed through a simple REST call, using
the POST HTTP method. The service consumer can then receive a response,
containing all registered service Instances that match the provided criteria.

![MSR SearchService Interface Operation Sequence Diagram](materials/searchserviceintseqdiagram.drawio.png)

## Service Interface "InstanceInterface"
<!--
    Include some information about the dynamic aspects of the service
    interface; each operation shall be exposed on at least one diagram.
    An example sequence diagram is shown in Figure 4.
-->

As described in the
[Instance Interface](#service-interface-instanceinterface) section, the
MSR Instance manipulation operations are performed through simple REST calls.
The service providers can perform these operations and receive the respective
responses on the outcome of each.

![MSR Instance Interface Operation Sequence Diagram](materials/instanceintseqdiagram.drawio.png)

## Service Interface "InstanceStatusInterface"
<!--
    Include some information about the dynamic aspects of the service
    interface; each operation shall be exposed on at least one diagram.
    An example sequence diagram is shown in Figure 4.
-->

As described in the
[InstanceStatus Interface](#service-interface-instancestatusinterface) section,
the MSR Instance Status update operation is performed through a simple REST 
call, using a PUT HTTP method. The service providers can perform this operation
to update the local status of a registered service Instance (based on G-1128)
and receive the response on the outcome.

![MSR InstanceStatus Interface Operation Sequence Diagram](materials/instancestatusintseqdiagram.drawio.png)

## Service Interface "InstanceLedgerStatusInterface"
<!--
    Include some information about the dynamic aspects of the service
    interface; each operation shall be exposed on at least one diagram.
    An example sequence diagram is shown in Figure 4.
-->

As described in the
[InstanceLedgerStatus Interface](#service-interface-instanceledgerstatusinterface-optional)
section, the MSR Instance Ledger Status update operation is performed through a
simple REST call, using a PUT HTTP method. The service providers can perform
this operation to update the global MSR ledger registration status of a
registered service Instance and receive the response on the outcome. It has
already been noted that the actual global MSR ledger status update operatio
takes place asynchronously.

![MSR InstanceLedgerStatus Interface Operation Sequence Diagram](materials/instanceledgerstatusintseqdiagram.drawio.png)

## Service Interface "XmlInterface"
<!--
    Include some information about the dynamic aspects of the service
    interface; each operation shall be exposed on at least one diagram.
    An example sequence diagram is shown in Figure 4.
-->

As described in the
[Xml Interface](#service-interface-xmlinterface) section, the
MSR Xml manipulation operations are performed through simple REST calls. The
service providers can perform these operations and receive the respective
responses on the outcome of each. Note that service consumers are also allowed
to retrieve Xml document information through the getXml operation

![MSR Xml Interface Operations Sequence Diagram](materials/xmlintseqdiagram.drawio.png)

## Service Interface "XmlValidationInterface"
<!--
    Include some information about the dynamic aspects of the service
    interface; each operation shall be exposed on at least one diagram.
    An example sequence diagram is shown in Figure 4.
-->

As described in the
[XmlValidation Interface](#service-interface-xmlvalidationinterface) section,
the MSR Xml validation operation is performed through a simple REST call, using
a PUT HTTP method. The service providers can perform this operation to update
determine whether an XML input conforms to a specific G-1128 schema
specification and receive the response on the outcome.

![MSR XmlValidation Interface Operation Sequence Diagram](materials/xmlvalidationintseqdiagram.drawio.png)

## Service Interface "DocInterface"
<!--
    Include some information about the dynamic aspects of the service
    interface; each operation shall be exposed on at least one diagram.
    An example sequence diagram is shown in Figure 4.
-->

As described in the
[Doc Interface](#service-interface-docinterface) section, the
MSR Doc manipulation operations are performed through simple REST calls. The
service providers can perform these operations and receive the respective
responses on the outcome of each. Note that service consumers are also allowed
to retrieve Doc document information through the getDoc operation.

![MSR Doc Interface Operations Sequence Diagram](materials/docintseqdiagram.drawio.png)

## Service Interface "LedgerRequestInterface"
<!--
    Include some information about the dynamic aspects of the service
    interface; each operation shall be exposed on at least one diagram.
    An example sequence diagram is shown in Figure 4.
-->

As described in the
[LedgerRequest Interface](#service-interface-ledgerrequestinterface) section,
the MSR LedgerRequest manipulation operations are performed through simple REST
calls. The service providers can perform these operations and receive the
respective responses on the outcome of each. Note that service consumers are 
also allowed to retrieve Doc documents information through the getDoc operation.

![MSR LedgerRequest Interface Operations Sequence Diagram](materials/ledgerrequestintseqdiagram.drawio.png)

## Service Interface "LedgerRequestStatusInterface"
<!--
    Include some information about the dynamic aspects of the service
    interface; each operation shall be exposed on at least one diagram.
    An example sequence diagram is shown in Figure 4.
-->

As described in the
[LedgerRequestStatus Interface](#service-interface-ledgerrequeststatusinterface-optional)
section, the MSR Update LedgerRequest Status operation is performed through a
simple REST call, using a PUT HTTP method. The service providers can perform
this operation to update the global MSR ledger registration status of a
registered service Instance and receive the response on the outcome. It has
already been noted that the actual global MSR ledger status update operatio
takes place asynchronously.

![MSR LedgerRequestStatus Interface Operation Sequence Diagram](materials/ledgerrequeststatusintseqdiagram.drawio.png)


<!-- ## Service orchestration (Optional) -->
<!--
  This section shall be provided, if the composition of the service and/or the 
  relation to other services (e.g., which other services are used to provide this
  service; which other services are intended to use this service) is deemed 
  relevant for the service specification.

  An example sequence diagram is given below. This very simple example indicates
  that the AddressForPersionLookupService (i.e., the service that is being 
  described in this Service Specification Document) acts as a consumer of a 
  “notifyAddressChange” operation of another service, called 
  “AddressForPersionService”. Note that the other service needs to be described by
  its own Service Specification Document; a reference to that document shall be
  added here).
-->

# Service Provisioning
<!--
    This section shall describe the way services are planned to be provided and
    consumed. It is labelled optional since one of the key aspects of
    service-orientation is to increase flexibility of the overall system by
    separating the definition of services from their implementation. This
    means that a service can be provided in several different contexts that are
    not necessarily known at the time, when the service is designed.
-->

A service management concept using MSR can be described as follows. Both, 
service specifications, and information about the service Instances can be
published in a service registry. A service registry can be a collection of
documents, or could be realised as a service itself that would have an Application 
Programming Interface (API) for automatic interfacing to the registry (lookup, 
updating, deleting etc.). This concept is implemented as MSR within MCP 
(formerly called the Maritime Cloud), see
[https://maritimeconnectivity.net/](https://maritimeconnectivity.net/).

In the current implementation described in this document, the MSR has been 
implemented as an online web service, exposing an API using the REST
methodology over HTTP. The following HTTP methods are used for the various 
operations described in the
[Service Interface Specifications](#service-interface-specifications) section.

<!-- Spacing: | --- | ------------ | -->
| Method | Description                                                                                                               |
| --- | ------------ |
| GET    | Get a representation of the target resource’s state.                                                                      |
| POST   | Let the target resource process the representation enclosed in the request.                                               |  
| PUT    | Create or replace the state of the target resource with the state defined by the representation enclosed in the request.  | 
| DELETE | Delete the target resource’s state.                                                                                       |                                                                                 

The MSR uses a relational SQL database in order to store and retrieve the
involved service instances and relevant documentation. In addition, in order to
maximise its efficiency in terms of data querying an indexing operation is 
applied on the stored data, using well know indexing mechanisms, such as
ElasticSearch and Lucene.

# Definitions
<!--
    The definitions of terms used in this IALA Guideline can be found in the
    International Dictionary of Marine Aids to Navigation (IALA Dictionary) at
    http://www.iala-aism.org/wiki/dictionary and were checked as correct at the
    time of going to print.  Where conflict arises, the IALA Dictionary shall
    be considered as the authoritative source of definitions used in IALA
    documents.
-->

The definitions of terms used in this document can be found in the International
Dictionary of Marine Aids to Navigation (IALA Dictionary) [11]. Where conflict
arises, the IALA Dictionary shall be considered as the authoritative source of 
definitions used in IALA documents.

Most other terms in the context of MCP can be found in the terminology page of
the online documentation of MCP
(https://docs.maritimeconnectivity.net/en/latest/terminology.html).

## Terminology

Persons producing the Technical Service are invited to add definitions to the
following list as appropriate.

<!-- Spacing: | --- | --------- | -->
| Term                      | Definition                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| --- | --------- |
| Service Registry          | An application that acts as an access point where the relevant information about available maritime services can be found.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Service Provider          | Any entity that provides a maritime service to a certain customer group.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Service Consumer          | Any entity that has an interest in acquiring information from maritime services.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| External Data Model       | Describes the semantics of the ‘maritime world’ (or a significant part thereof) by defining data structures and their relations. This could be at logical level (e.g. in UML) or at physical level (e.g. in XSD schema definitions), as for example standard data models, or S-100 based data produce specifications.                                                                                                                                                                                                                                                                                                                                                                               |
| Message Exchange Pattern  | Describes the principles two different parts of a message passing system (in our case: the service provider and the service consumer) interact and communicate with each other. \newline Examples:  \newline In the Request/Response MEP, the service consumer sends a request to the service provider to obtain certain information; the service provider provides the requested information in a dedicated response. \newline In the Publish/Subscribe MEP, the service consumer establishes a subscription with the service provider to obtain certain information; the service provider publishes information (either in regular intervals or upon change) to all subscribed service consumers. |
| Service Discoverability   | The process of identifying availabily resources providing maritime information.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Instance                  | A single service resource being made available to service consumers, providing maritime information.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| Interface                 | A functional element of a maritime service, that allows a set of operations, accessing and/or altering maritime information.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Operation                 | An action on an interface of accessing or altering the available maritime information.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| Request                   | A formal user (service provider or consumer) request for maritime information new to be provided/altered.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| Response                  | A formal service reply on a request for maritime information new to be provided/altered.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |

# Acronyms

Persons producing the Technical Service are invited to provide a list of
acronyms as appropriate.

<!-- Spacing: | --- | --------- | -->
| Acronym | Mearning                                                                          |
| --- | --------- |
| API     | Application Programming Interface                                                 |
| IALA    | International Association of Marine Aids to Navigation and Lighthouse Authorities |
| IMO     | International Maritime Organization                                               |
| MCC     | Maritime Connectivity platform Consortium                                         |
| MCP     | Maritime Connectivity Platform                                                    |
| MIR     | Maritime Identity Registry                                                        |
| MMS     | Maritime Messaging Service                                                        |
| MRN     | Maritime Resource Name                                                            |
| MSR     | Maritime Service Registry                                                         |
| REST    | Representational State Transfer                                                   |
| SECOM   | Secure Communication (IEC 63173-2)                                                |
| SLA     | Service Level Agreement                                                           |
| SQL     | Structured Query Language                                                         |

# References
<!--
    This section shall include all references used when designing the service.
    Specifically, the applicable steering and requirements documents shall be
    listed.
-->

1. IMO Resolution MSC.85/26 'Strategy for the development and  implementation of e‐Navigation', Annex 20,
[https://wwwcdn.imo.org/localresources/en/OurWork/Safety/Documents/enavigation/MSC 85 - annex 20 - Strategy for the development and implementation of e-nav.pdf](https://wwwcdn.imo.org/localresources/en/OurWork/Safety/Documents/enavigation/MSC%2085%20-%20annex%2020%20-%20Strategy%20for%20the%20development%20and%20implementation%20of%20e-nav.pdf)
2. IMO Resolution MSC.467(101) - Guidance on the Definition and Harmonization of the Format and Structure of Maritime Services in the Context of e-Navigation,
[https://wwwcdn.imo.org/localresources/en/KnowledgeCentre/IndexofIMOResolutions/MSCResolutions/MSC.467%28101%29.pdf](https://wwwcdn.imo.org/localresources/en/KnowledgeCentre/IndexofIMOResolutions/MSCResolutions/MSC.467%28101%29.pdf)
3. Maritime Connectivity Platform, 
[https://maritimeconnectivity.net/](https://maritimeconnectivity.net/)
4. IALA Guideline - G1128 The Specification of e-Navigation Technical Services, 
[https://www.iala-aism.org/product/g1128-specification-e-navigation-technical-services/](https://www.iala-aism.org/product/g1128-specification-e-navigation-technical-services/)
5. EfficienSea2 Project, 
[https://efficiensea2.org/](https://efficiensea2.org/)
6. IEC 63173-2 - Maritime navigation and radiocommunication equipment and systems. Data interface Part 2. Secure exchange and communication of S-100 based products (SECOM)
7. MCP Gen5 Vetting Procedure for MCP Instance Providers,
[https://secureservercdn.net/160.153.138.143/qkh.3ac.myftpupload.com/wp-content/uploads/2022/06/MCP-Gen5-Vetting-procedure-for-MCP-instance-providers-v-1-1.pdf](https://secureservercdn.net/160.153.138.143/qkh.3ac.myftpupload.com/wp-content/uploads/2022/06/MCP-Gen5-Vetting-procedure-for-MCP-instance-providers-v-1-1.pdf)
8. IALA Maritime Resource Name (MRN) Registry, 
[https://www.iala-aism.org/technical/data-modelling/mrn/](https://www.iala-aism.org/technical/data-modelling/mrn/)
9. MCP IDsec2 MCC Identity Management and Security; Identity Management,
[https://maritimeconnectivity.github.io/maritimeconnectivity.net/docs/MCP%20IDsec2%20MCC%20Identity%20Management%20and%20Security;%20Identity%20Management.pdf](https://maritimeconnectivity.github.io/maritimeconnectivity.net/docs/MCP%20IDsec2%20MCC%20Identity%20Management%20and%20Security;%20Identity%20Management.pdf)
10. S-100 Universal Hydrographic Data Model, 
[https://iho-monaco.reisswolf.fit/content/7ad4b7fb-4bd8-4c51-920a-c972e5834df4](https://iho-monaco.reisswolf.fit/content/7ad4b7fb-4bd8-4c51-920a-c972e5834df4)
11. IALA International Dictionary of Marine Aids to Navigation, 
[http://www.iala-aism.org/wiki/dictionary](http://www.iala-aism.org/wiki/dictionary)

# Annex A: MSR OpenApi Documentation
```json
{
  "openapi": "3.0.1",
  "info": {
    "title": "Maritime Connectivity Platform Service Registry API",
    "description": "Maritime Connectivity Platform Service Registry, developed by the MCC MSR WG",
    "termsOfService": "null",
    "contact": {
      "name": "MCP Consortium",
      "url": "https://mcp.discourse.group/",
      "email": "Nikolaos.Vastardis@gla-rad.org"
    },
    "license": {
      "name": "Apache-2.0",
      "url": "http://www.apache.org/licenses/LICENSE-2.0"
    },
    "version": "0.1"
  },
  "servers": [
    {
      "url": "https://rnavlab.gla-rad.org/msr",
      "description": "Generated server url"
    }
  ],
  "paths": {
    "/api/xmls/{id}": {
      "get": {
        "tags": [
          "xml-controller"
        ],
        "operationId": "getXml",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/XmlDto"
                }
              }
            }
          }
        }
      },
      "put": {
        "tags": [
          "xml-controller"
        ],
        "operationId": "updateXml",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          }
        ],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/XmlDto"
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/XmlDto"
                }
              }
            }
          }
        }
      },
      "delete": {
        "tags": [
          "xml-controller"
        ],
        "operationId": "deleteXml",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK"
          }
        }
      }
    },
    "/api/ledgerrequests/{id}/status": {
      "put": {
        "tags": [
          "ledger-request-controller"
        ],
        "operationId": "updateRequestStatus",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          },
          {
            "name": "status",
            "in": "query",
            "required": true,
            "schema": {
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
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/LedgerRequestDto"
                }
              }
            }
          }
        }
      }
    },
    "/api/instances/{id}": {
      "get": {
        "tags": [
          "instance-controller"
        ],
        "operationId": "getInstance",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/InstanceDto"
                }
              }
            }
          }
        }
      },
      "put": {
        "tags": [
          "instance-controller"
        ],
        "operationId": "updateInstance",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          }
        ],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/InstanceDto"
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/InstanceDto"
                }
              }
            }
          }
        }
      },
      "delete": {
        "tags": [
          "instance-controller"
        ],
        "operationId": "deleteInstance",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK"
          }
        }
      }
    },
    "/api/instances/{id}/status": {
      "put": {
        "tags": [
          "instance-controller"
        ],
        "operationId": "updateInstanceStatus",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          },
          {
            "name": "status",
            "in": "query",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK"
          }
        }
      }
    },
    "/api/instances/{id}/ledger-status": {
      "put": {
        "tags": [
          "instance-controller"
        ],
        "operationId": "updateInstanceLedgerStatus",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          },
          {
            "name": "ledgerStatus",
            "in": "query",
            "required": true,
            "schema": {
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
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK"
          }
        }
      }
    },
    "/api/docs/{id}": {
      "get": {
        "tags": [
          "doc-controller"
        ],
        "operationId": "getDoc",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/DocDto"
                }
              }
            }
          }
        }
      },
      "put": {
        "tags": [
          "doc-controller"
        ],
        "operationId": "updateDoc",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          }
        ],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/DocDto"
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/DocDto"
                }
              }
            }
          }
        }
      },
      "delete": {
        "tags": [
          "doc-controller"
        ],
        "operationId": "deleteDoc",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK"
          }
        }
      }
    },
    "/api/xmls": {
      "get": {
        "tags": [
          "xml-controller"
        ],
        "operationId": "getAllXmls",
        "parameters": [
          {
            "name": "pageable",
            "in": "query",
            "required": true,
            "schema": {
              "$ref": "#/components/schemas/Pageable"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/XmlDto"
                  }
                }
              }
            }
          }
        }
      },
      "post": {
        "tags": [
          "xml-controller"
        ],
        "operationId": "createXml",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/XmlDto"
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/XmlDto"
                }
              }
            }
          }
        }
      }
    },
    "/api/xmls/validate/{schema}": {
      "post": {
        "tags": [
          "xml-controller"
        ],
        "operationId": "validateXmlWithG1128Schema",
        "parameters": [
          {
            "name": "schema",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "requestBody": {
          "content": {
            "application/xml": {
              "schema": {
                "type": "string"
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object"
                }
              }
            }
          }
        }
      }
    },
    "/api/ledgerrequests": {
      "get": {
        "tags": [
          "ledger-request-controller"
        ],
        "operationId": "getLedgerRequests",
        "parameters": [
          {
            "name": "pageable",
            "in": "query",
            "required": true,
            "schema": {
              "$ref": "#/components/schemas/Pageable"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/LedgerRequestDto"
                  }
                }
              }
            }
          }
        }
      },
      "post": {
        "tags": [
          "ledger-request-controller"
        ],
        "operationId": "createLedgerRequest",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/LedgerRequestDto"
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/LedgerRequestDto"
                }
              }
            }
          }
        }
      }
    },
    "/api/instances": {
      "get": {
        "tags": [
          "instance-controller"
        ],
        "operationId": "getInstances",
        "parameters": [
          {
            "name": "pageable",
            "in": "query",
            "required": true,
            "schema": {
              "$ref": "#/components/schemas/Pageable"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/InstanceDto"
                  }
                }
              }
            }
          }
        }
      },
      "post": {
        "tags": [
          "instance-controller"
        ],
        "operationId": "createInstance",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/InstanceDto"
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/InstanceDto"
                }
              }
            }
          }
        }
      }
    },
    "/api/docs": {
      "get": {
        "tags": [
          "doc-controller"
        ],
        "operationId": "getDocs",
        "parameters": [
          {
            "name": "pageable",
            "in": "query",
            "required": true,
            "schema": {
              "$ref": "#/components/schemas/Pageable"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/DocDto"
                  }
                }
              }
            }
          }
        }
      },
      "post": {
        "tags": [
          "doc-controller"
        ],
        "operationId": "createDoc",
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/DocDto"
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/DocDto"
                }
              }
            }
          }
        }
      }
    },
    "/api/xmls/schemas/{schema}": {
      "get": {
        "tags": [
          "xml-controller"
        ],
        "operationId": "getG1128Schema",
        "parameters": [
          {
            "name": "schema",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/xml": {
                "schema": {
                  "type": "string"
                }
              }
            }
          }
        }
      }
    },
    "/api/ledgerrequests/{id}": {
      "get": {
        "tags": [
          "ledger-request-controller"
        ],
        "operationId": "getLedgerRequest",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/LedgerRequestDto"
                }
              }
            }
          }
        }
      },
      "delete": {
        "tags": [
          "ledger-request-controller"
        ],
        "operationId": "deleteRequest",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "OK"
          }
        }
      }
    }
  },
  "components": {
    "schemas": {
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
          "width": {
            "type": "number",
            "format": "double"
          },
          "height": {
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
          "srid": {
            "type": "integer",
            "format": "int32"
          },
          "numPoints": {
            "type": "integer",
            "format": "int32"
          },
          "coordinates": {
            "type": "array",
            "items": {
              "$ref": "#/components/schemas/Coordinate"
            }
          },
          "geometryType": {
            "type": "string"
          },
          "simple": {
            "type": "boolean"
          },
          "area": {
            "type": "number",
            "format": "double"
          },
          "centroid": {
            "$ref": "#/components/schemas/Point"
          },
          "envelopeInternal": {
            "$ref": "#/components/schemas/Envelope"
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
          "rectangle": {
            "type": "boolean"
          },
          "numGeometries": {
            "type": "integer",
            "format": "int32"
          },
          "coordinate": {
            "$ref": "#/components/schemas/Coordinate"
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
          "dataProductType": {
            "type": "array",
            "items": {
              "type": "string",
              "enum": [
                "OTHER",
                "S57",
                "S101",
                "S102",
                "S104",
                "S111",
                "S122",
                "S123",
                "S124",
                "S125",
                "S126",
                "S127",
                "S128",
                "S129",
                "S131",
                "S210",
                "S211",
                "S212",
                "S401",
                "S402",
                "S411",
                "S412",
                "S413",
                "S414",
                "S421",
                "RTZ",
                "EPC"
              ]
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
          "coordinateSequence": {
            "$ref": "#/components/schemas/CoordinateSequence"
          },
          "numPoints": {
            "type": "integer",
            "format": "int32"
          },
          "geometryType": {
            "type": "string"
          },
          "simple": {
            "type": "boolean"
          },
          "dimension": {
            "type": "integer",
            "format": "int32"
          },
          "boundary": {
            "$ref": "#/components/schemas/Geometry"
          },
          "coordinate": {
            "$ref": "#/components/schemas/Coordinate"
          },
          "boundaryDimension": {
            "type": "integer",
            "format": "int32"
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
          "area": {
            "type": "number",
            "format": "double"
          },
          "centroid": {
            "$ref": "#/components/schemas/Point"
          },
          "envelopeInternal": {
            "$ref": "#/components/schemas/Envelope"
          },
          "interiorPoint": {
            "$ref": "#/components/schemas/Point"
          },
          "rectangle": {
            "type": "boolean"
          },
          "numGeometries": {
            "type": "integer",
            "format": "int32"
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
          "offsetX": {
            "type": "number",
            "format": "double"
          },
          "offsetY": {
            "type": "number",
            "format": "double"
          },
          "maximumSignificantDigits": {
            "type": "integer",
            "format": "int32"
          }
        }
      },
      "Type": {
        "type": "object"
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
    }
  }
}
```

# Annex B: SECOM OpenApi Documentation
```json
{
  "openapi": "3.0.1",
  "info": {
    "title": "MCP Service Registry (MSR) - SECOM Interfaces",
    "description": "Maritime Connectivity Platform Service Registry, developed by the MCC MSR WG",
    "termsOfService": "https://gla-rad.org/",
    "contact": {
      "email": "Nikolaos.Vastardis@gla-rad.org"
    },
    "license": {
      "name": "Apache 2.0",
      "url": "http://www.apache.org/licenses/LICENSE-2.0.html"
    },
    "version": "1.0"
  },
  "servers": [
    {
      "url": "http://rnavlab.gla-rad.org/msr/"
    },
    {
      "url": "http://palatia:8444"
    },
    {
      "url": "http://localhost:8444"
    }
  ],
  "paths": {
    "/api/secom/v1/searchService": {
      "post": {
        "tags": [
          "SECOM"
        ],
        "operationId": "search",
        "parameters": [
          {
            "name": "page",
            "in": "query",
            "schema": {
              "minimum": 0,
              "type": "integer",
              "format": "int32"
            }
          },
          {
            "name": "pageSize",
            "in": "query",
            "schema": {
              "minimum": 0,
              "type": "integer",
              "format": "int32"
            }
          }
        ],
        "requestBody": {
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/SearchFilterObject"
              }
            }
          }
        },
        "responses": {
          "default": {
            "description": "default response",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/SearchObjectResult"
                  }
                }
              }
            }
          }
        }
      }
    }
  },
  "components": {
    "schemas": {
      "SearchObjectResult": {
        "required": [
          "description",
          "endpointType",
          "endpointUri",
          "instanceId",
          "name",
          "organizationId",
          "status",
          "version"
        ],
        "type": "object",
        "properties": {
          "instanceId": {
            "pattern": "^urn:mrn:[a-z0-9][a-z0-9-]{0,31}:[a-z0-9()+,\\-.:=@;$_!*'%/?#]+$",
            "type": "string"
          },
          "version": {
            "type": "string"
          },
          "name": {
            "type": "string"
          },
          "status": {
            "type": "string"
          },
          "description": {
            "type": "string"
          },
          "dataProductType": {
            "type": "string",
            "enum": [
              "OTHER",
              "S57",
              "S101",
              "S102",
              "S104",
              "S111",
              "S122",
              "S123",
              "S124",
              "S125",
              "S126",
              "S127",
              "S128",
              "S129",
              "S131",
              "S210",
              "S211",
              "S212",
              "S401",
              "S402",
              "S411",
              "S412",
              "S413",
              "S414",
              "S421",
              "RTZ",
              "EPC"
            ]
          },
          "organizationId": {
            "type": "string"
          },
          "endpointUri": {
            "type": "string"
          },
          "endpointType": {
            "type": "string"
          },
          "keywords": {
            "type": "array",
            "items": {
              "type": "string"
            }
          },
          "unlocode": {
            "type": "array",
            "items": {
              "type": "string"
            }
          },
          "instanceAsXml": {
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
          "mmsi": {
            "type": "string"
          },
          "imo": {
            "type": "string"
          },
          "geometry": {
            "type": "object"
          }
        }
      },
      "SearchFilterObject": {
        "type": "object",
        "properties": {
          "query": {
            "$ref": "#/components/schemas/SearchParameters"
          },
          "geometry": {
            "type": "string"
          },
          "freetext": {
            "pattern": "^[a-zA-Z0-9 +_:\\-,.\\*\\?]*$",
            "type": "string"
          }
        }
      },
      "SearchParameters": {
        "type": "object",
        "properties": {
          "name": {
            "type": "string"
          },
          "status": {
            "type": "string"
          },
          "version": {
            "type": "string"
          },
          "keywords": {
            "type": "string"
          },
          "description": {
            "type": "string"
          },
          "dataProductType": {
            "type": "string",
            "enum": [
              "OTHER",
              "S57",
              "S101",
              "S102",
              "S104",
              "S111",
              "S122",
              "S123",
              "S124",
              "S125",
              "S126",
              "S127",
              "S128",
              "S129",
              "S131",
              "S210",
              "S211",
              "S212",
              "S401",
              "S402",
              "S411",
              "S412",
              "S413",
              "S414",
              "S421",
              "RTZ",
              "EPC"
            ]
          },
          "specificationId": {
            "pattern": "^urn:mrn:[a-z0-9][a-z0-9-]{0,31}:[a-z0-9()+,\\-.:=@;$_!*'%/?#]+$",
            "type": "string"
          },
          "designId": {
            "pattern": "^urn:mrn:[a-z0-9][a-z0-9-]{0,31}:[a-z0-9()+,\\-.:=@;$_!*'%/?#]+$",
            "type": "string"
          },
          "instanceId": {
            "pattern": "^urn:mrn:[a-z0-9][a-z0-9-]{0,31}:[a-z0-9()+,\\-.:=@;$_!*'%/?#]+$",
            "type": "string"
          },
          "mmsi": {
            "pattern": "^(MID\\d{6}|0MID\\d{5}|00MID\\{4})",
            "type": "string"
          },
          "imo": {
            "pattern": "^\\d{7}(?:\\d{2})?$",
            "type": "string"
          },
          "serviceType": {
            "type": "string"
          },
          "unlocode": {
            "pattern": "^[a-zA-Z]{2}[a-zA-Z2-9]{3}",
            "type": "string"
          },
          "endpointUri": {
            "type": "string",
            "format": "uri"
          },
          "page": {
            "minimum": 0,
            "type": "integer",
            "format": "int32"
          },
          "pageSize": {
            "minimum": 0,
            "type": "integer",
            "format": "int32"
          }
        }
      }
    }
  }
}
```