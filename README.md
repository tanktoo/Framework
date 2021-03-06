# IoTCrawler Framework
IoTCrawler is a research project funded under the European Union's Horizon 2020 reserach and innovation program. The aim of the project is to develop a search engine for the Internet of Things (IoT), enabling search on it’s devices. IoTCrawler focuses on integration and interoperability across different platforms, dynamic and reconfigurable solutions for discovery and integration of data and services from legacy and new systems, adaptive, privacy-aware and secure algorithms and mechanisms for crawling, indexing, and search in distributed IoT systems. The project spans industry, universities and cities. It is comporised of multiple components:
## [Metadata Repository - Scorpio Broker](https://github.com/IoTCrawler/ScorpioBroker)
The core component of the architecture of IoTCrawler is what we call MetaData Repository, which can be seen as a Context Broker with the features of distributing information following both query-response and publication-subscription patters among the other components of the IoTCrawler architecture. This Context Broker must be capable of representing semantic, linked data and property graphs. These features has been included in NGSI-LD, a new standard which has been conducted under the ETSI ISG CIM initiative. For this reason, we have selected this technology for the instantiation of our MetaData Repository. 

Scorpio is an NGSI-LD compliant context broker developed by NEC Laboratories Europe and NEC Technologies India. This project is part of [FIWARE](https://www.fiware.org/). For more information check the FIWARE Catalogue entry for [Core Context](https://github.com/Fiware/catalogue/tree/master/core). We have selected this broker for the instantiation of our MetaData Repository because of their features related to the representation of distribution and federation scenarios.

## [Indexing](https://github.com/IoTCrawler/Indexing)
The Indexing component  provides a means for clients to search for IoT entities efficiently. It focuses on IoT streams and sensors, where queries can be based on sensor type and absolute or relative location. To initiate the process of indexing, a platform manager needs to register a metadata broker (MDR) with the Indexing component. In turn this will trigger the subscription to sensors and streams at the registered MDR. As metadata descriptions are updated at the MDR, the Indexing component will be notified, and will then index the sensors and streams based on location. For scalability, the Indexing component can be configured so that the persistence it relies on (MongoDB) can be sharded. With respect to other components in the framework, the Ranking component relies on Indexing for generating the ranking of search results.
## [Ranking](https://github.com/IoTCrawler/Ranking)
The Ranking component facilitates ranking mechanism for IoT resources. Ranking and resource selection rely on the registry built (and constantly updated) by crawling and indexing methods. The purpose of Ranking is to aid users and applications to not only find a set of resources relevant to their needs, but also to select the best or most appropriate one(s) from that set. There are multiple criterias for ranking IoT resources such as data type, proximity, latency, availability. The Ranking component supports application-dependent,multi-criteria ranking.
## [Orchestrator](https://github.com/IoTCrawler/Orchestrator)

## [Identity Manager - Keyrock](https://github.com/IoTCrawler/Keyrock)
Keyrock is the FIWARE component responsible for Identity Management. Using Keyrock (in conjunction with other security components such as PEP Proxy and Authzforce) enables you to add OAuth2-based authentication and authorization security to your services and applications.

## [Search Enabler](https://github.com/IoTCrawler/Search-Enabler)


## Authorization Enabler
The purpose of this enabler is twofold: on the one hand for a secure communication between the IoTCrawler components, and on the other, for controlling the access of the registered users to the resources stored in the IoTCrawler platform. It instantiates the Distributed Capability-Based Access Control (DCapBAC) technology by using both an XACML framework, and a Capability Manager. This latter is responsible for issuing authorisations tokens which must be present in each of the requests aimed at the MetaData Repository.

### [XACML PAP PDP](https://github.com/IoTCrawler/XACML_PAP_PDP)
This element corresponds to the implementation of the XACML framework. It comprises a Policy Administration Point (PAP) which is responsible for managing the authorisation policies, and a Policy Decision Point (PDP), responsible for issuing possitive/negativer verdicts whenever an authorisation request is received. 
The PAP presents a GUI for managing the XACML policies. They must be defined according to a triplet (subject, resource, action).

### [Capability Manager](https://github.com/IoTCrawler/Capability-Manager)
This component is the contact point for services and users that intend to access the resources stored in our IoTCrawler platform. It provides a REST API for receiving authorisation queries, which are tailored and forwarded to the XACML PDP for a verdict. When a positive verdict is received, the Capability manager issues an authorisation token called Capability Token which is a signed JSON document which contains all the required information for the authorisation, such as the resource to be accessed, the action to be performed, and also a time interval during the Capability Token is valid.

### [PEP-PROXY](https://github.com/IoTCrawler/PEP-Proxy)
Since the DCapBAC technology decouples the authorisation in two phases: one for issuing an authorisation token, and a second one when the authorisation token is validated, we need the figure of a Policy Enforcement Poing (PEP). This is the purpose of the PEP-Proxy. It is responsible for receiving the queries aimed at the MetaData Repository that must be accompanied by the corresponding Capability Token. The PEP-Proxy validates this token, and in case the evaluation is positive, it forwards the messages to the MetaData Repository, as well as the responses back to the requester.

### [Security Facade](https://github.com/IoTCrawler/Security-Facade)
This component has been designed as an endpoint for performing both authentication and authorisation operations in an transparent way for the requester. By receiving the corresponding request it interacts with both Identity Manager and Authorisation Enabler, and in case the requester owns the appropriate permissions for the request, it sends the authorsation token (Capability Token) back to the requester.

## [Pattern Extractor](https://github.com/IoTCrawler/Pattern-Extractor)
## [Semantic Enrichment](https://github.com/IoTCrawler/SemanticEnrichment)
