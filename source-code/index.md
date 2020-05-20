---
layout: page
title: Source-code overview
permalink: /source-code/
menuInclude: yes
menuLink: yes
menuTopTitle: Source
menuTopIndex: 4
menuSubTitle: Source-code overview
menuSubIndex: 1
---

The FOLIO platform consists of both server-side and client-side components, and
will grow to include library services that run on the platform as modules.
Some sample modules are located in
[folio-sample-modules](https://github.com/folio-org/folio-sample-modules).

Several repositories in the [folio-org GitHub
organization](https://github.com/folio-org) host the core project code.
Third-party modules may be hosted elsewhere.

NOTE: This overview page is undergoing some re-arrangement.
The new [Source-code map](/source-code/map/) will replace some sections.

A good starting point for understanding the FOLIO code is
[Okapi](https://github.com/folio-org/okapi) -- specifically the
[Okapi Guide and Reference](https://github.com/folio-org/okapi/blob/master/doc/guide.md), which
introduces the concepts and architecture of the FOLIO platform, and includes
installation instructions and examples.  Okapi is the central hub for
applications running on the FOLIO platform and enable access to other modules
in the architecture.

The FOLIO system is made up of the code in several GitHub repositories.
Each repository contains the code for a single well-defined element of the
system. These repositories fall into three categories:

- _server-side elements_ that provide services and the
  infrastructure that they run on;
- _client-side elements_ that provide a
  framework for using those services from a Web browser;
- and a few that fall into neither of these categories.

**PLEASE NOTE** that this is a technology preview following the [release early,
release often](https://en.wikipedia.org/wiki/Release_early,_release_often)
philosophy.  **We want your feedback** in the form of pull requests and filed
issues and general discussion via the
[collaboration tools](/community).

## Server-side

The key server-side element is Okapi itself: the FOLIO middleware component
that acts as a gateway for access to all modules, handling redundancy,
sessions, etc.  Individual modules are provided in their repositories, each
named `mod-`_name_ (note that these are mostly at the proof-of-concept stage).
Each back-end module has its documentation.

Some of these modules are built from specifications in
[RAML](https://raml.org/), the RESTful API Modeling Language: this process is
facilitated by the code in the `raml-module-builder` repository.

- [okapi](https://github.com/folio-org/okapi)
  -- Okapi API Gateway proxy/discovery/deployment service.

- [raml](https://github.com/folio-org/raml)
  -- Repository of RAML files, including JSON Schemas, traits and
  resource types centralized for re-usability.
  The [API reference](/reference/api/) documentation is also
  generated.
  This repository is the master location for the traits and resource
  types, while each module is the master for its own schemas, examples,
  and actual RAML files.
  It is included in other repositories via a git sub-module, usually called `raml-util`.

- [raml-module-builder](https://github.com/folio-org/raml-module-builder)
  -- Framework facilitating easy module creation based on RAML files.

- [mod-configuration](https://github.com/folio-org/mod-configuration)
  -- Configuration module based on the raml-module-builder and a set
  of RAML and JSON Schemas backed by a PostgreSQL asynchronous implementation.

- [mod-authtoken](https://github.com/folio-org/mod-authtoken)
  -- Filtering requests based on JWT tokens.

- [mod-login](https://github.com/folio-org/mod-login)
  -- Handles username/password login.

- [mod-login-saml](https://github.com/folio-org/mod-login-saml)
  -- Handles SAML login.

- [mod-password-validator](https://github.com/folio-org/mod-password-validator)
  -- Performs password validation and stores validation rules for specified tenant.

- [mod-permissions](https://github.com/folio-org/mod-permissions)
  -- Handles permissions and permissions/user associations.

- [mod-users](https://github.com/folio-org/mod-users)
  -- Provides user management.

- [mod-users-bl](https://github.com/folio-org/mod-users-bl)
  -- Business logic "join" module to provide simple access to all
  user-centric data.

- [mod-user-import](https://github.com/folio-org/mod-user-import)
  -- Importing new or already existing users into FOLIO.

- [mod-inventory](https://github.com/folio-org/mod-inventory)
  -- Provides basic physical item inventory management.

- [mod-inventory-storage](https://github.com/folio-org/mod-inventory-storage)
  -- Persistent storage to complement the inventory module.

- [mod-circulation](https://github.com/folio-org/mod-circulation)
  -- Circulation capabilities, including loan items from the inventory.

- [mod-circulation-storage](https://github.com/folio-org/mod-circulation-storage)
  -- Persistent storage to complement the circulation module.

- [mod-calendar](https://github.com/folio-org/mod-calendar)
  -- Provide calendar functionality.

- [mod-feesfines](https://github.com/folio-org/mod-feesfines)
  -- Provide central management for fees and fines.

- [mod-finc-config](https://github.com/folio-org/mod-finc-config)
  -- Knowledge base for amsl's finc-config module.

- [mod-datasets](https://github.com/folio-org/mod-datasets)
  -- Wrapper for running a Glint server as an Okapi module.

- [mod-graphql](https://github.com/folio-org/mod-graphql)
  -- Executing GraphQL queries.

- [mod-kb-ebsco-java](https://github.com/folio-org/mod-kb-ebsco-java)
  -- Broker communication with the EBSCO knowledge base.

- [mod-notes](https://github.com/folio-org/mod-notes)
  -- Notes on all types of objects.

- [mod-notify](https://github.com/folio-org/mod-notify)
  -- Notifications to the users.

- [mod-sender](https://github.com/folio-org/mod-sender)
  -- Intermediary for sending prepared messages through appropriate delivery channels.

- [mod-email](https://github.com/folio-org/mod-email)
  -- Provides functionality for sending notifications.

- [mod-event-config](https://github.com/folio-org/mod-event-config)
  -- Provides functionality for the notification events.

- [mod-pubsub](https://github.com/folio-org/mod-pubsub)
  -- Publisher-subscriber module to provide event-driven approach.

- [mod-codex-mux](https://github.com/folio-org/mod-codex-mux)
  -- Codex Multiplexer.

- [mod-codex-mock](https://github.com/folio-org/mod-codex-mock)
  -- Codex mock module - for testing and development.

- [mod-codex-ekb](https://github.com/folio-org/mod-codex-ekb)
  -- Codex wrapper for the EBSCO knowledge base.

- [mod-codex-inventory](https://github.com/folio-org/mod-codex-inventory)
  -- Codex wrapper for local inventory.

- [mod-courses](https://github.com/folio-org/mod-courses)
  -- CRUD storage module to support the Course Reserves functionality.

- [mod-marccat](https://github.com/folio-org/mod-marccat)
  -- Metadata management and cataloging (MARCcat).

- [mod-quick-marc](https://github.com/folio-org/mod-quick-marc)
  -- Backend for quickMARC editor.

- [acq-models](https://github.com/folio-org/acq-models)
  -- a Shared repository for the models of the various acquisition modules.

- [mod-finance](https://github.com/folio-org/mod-finance)
  -- Finance business logic.

- [mod-finance-storage](https://github.com/folio-org/mod-finance-storage)
  -- Persistent storage of finance-related data (i.e. funds, ledgers, transactions, etc.).

- [mod-invoice](https://github.com/folio-org/mod-invoice)
  -- Invoice business logic.

- [mod-invoice-storage](https://github.com/folio-org/mod-invoice-storage)
  -- Persistent storage of invoice data.

- [mod-orders](https://github.com/folio-org/mod-orders)
  -- Orders business logic.

- [mod-orders-storage](https://github.com/folio-org/mod-orders-storage)
  -- Persistent storage of order data.

- [mod-ncip](https://github.com/folio-org/mod-ncip)
  -- NISO Circulation Interchange Protocol (NCIP).

- [mod-receiving](https://github.com/folio-org/mod-receiving)
  -- Business logic for receiving and checking-in materials that have been ordered.

- [mod-patron](https://github.com/folio-org/mod-patron)
  -- Allow 3rd party discovery services to perform FOLIO patron actions via the discovery service's UI.

- [mod-patron-blocks](https://github.com/folio-org/mod-patron-blocks)
  -- Automated patron blocks.

- [mod-rtac](https://github.com/folio-org/mod-rtac)
  -- Real-Time Availability Check.
  Enable third-party discovery services to check for FOLIO inventory availability.

- [mod-tags](https://github.com/folio-org/mod-tags)
  -- Central list of tags that can be assigned to various objects.

- [mod-template-engine](https://github.com/folio-org/mod-template-engine)
  -- Stores templates and generates files by using them.

- [mod-custom-fields](https://github.com/folio-org/mod-custom-fields)
  -- Store and maintain custom fields.

- [mod-data-export](https://github.com/folio-org/mod-data-export)
  -- Export inventory instance records in binary MARC format.

- [mod-data-import](https://github.com/folio-org/mod-data-import)
  -- Data import.

- [mod-data-import-converter-storage](https://github.com/folio-org/mod-data-import-converter-storage)
  -- Data import converter storage.

- [mod-source-record-storage](https://github.com/folio-org/mod-source-record-storage)
  -- Persistent source record storage (SRS). Complements the data import module.

- [mod-source-record-manager](https://github.com/folio-org/mod-source-record-manager)
  -- Source record manager (SRM).

- [data-import-raml-storage](https://github.com/folio-org/data-import-raml-storage)
  -- Shared repository for the schemas of various data-import modules.

- [mod-organizations-storage](https://github.com/folio-org/mod-organizations-storage)
  -- Persistent storage of organizations data.

- [mod-agreements](https://github.com/folio-org/mod-agreements)
  -- Electronic resource management (ERM).

- [mod-erm-usage](https://github.com/folio-org/mod-erm-usage)
  -- Store ERM usage statistics and access data to these statistics.

- [mod-erm-usage-counter](https://github.com/folio-org/mod-erm-usage-counter)
  -- Library containing models and clients for COUNTER/SUSHI standard.

- [mod-erm-usage-harvester](https://github.com/folio-org/mod-erm-usage-harvester)
  -- Harvest ERM usage statistics.

- [mod-licenses](https://github.com/folio-org/mod-licenses)
  -- Upload, manage and analyze licenses.

- [mod-gobi](https://github.com/folio-org/mod-gobi)
  -- Allows GOBI® (Global Online Bibliographic Information) initiated orders to be fulfilled by FOLIO.

- [mod-oai-pmh](https://github.com/folio-org/mod-oai-pmh)
  -- Open Archives Initiative Protocol for Metadata Harvesting (OAI-PMH).

- [mod-workflow](https://github.com/folio-org/mod-workflow)
  -- Workflow proof-of-concept. With related modules:
  [mod-camunda](https://github.com/folio-org/mod-camunda),
  [spring-module-core](https://github.com/folio-org/spring-module-core),
  [mod-spring-sample](https://github.com/folio-org/mod-spring-sample).

- [mod-audit](https://github.com/folio-org/mod-audit)
  -- Manage audit data.

- [mod-audit-filter](https://github.com/folio-org/mod-audit-filter)
  -- Implements Okapi PRE and POST filters to capture audit data.

- [mod-aes](https://github.com/folio-org/mod-aes)
  -- Provide asynchronous event service (AES).

- [mod-data-loader](https://github.com/folio-org/mod-data-loader)
  -- RMB-based module used to load test data.
  Currently supports loading binary MARC records into the mod-inventory-storage instance table.

- [inventory-sample-data](https://github.com/folio-org/inventory-sample-data)
  -- Provides scripts for data preparation and deployment, e.g. MARC.

<a id="edge"></a>

- [edge-common](https://github.com/folio-org/edge-common)
  -- Common/Shared library for Edge APIs.

- [edge-ncip](https://github.com/folio-org/edge-ncip)
  -- Edge API for mod-ncip.

- [edge-oai-pmh](https://github.com/folio-org/edge-oai-pmh)
  -- Edge API for Metadata Harvesting.

- [edge-orders](https://github.com/folio-org/edge-orders)
  -- Edge API to interface with FOLIO for 3rd party ordering services and FOLIO.
  Initially GOBI.

- [edge-patron](https://github.com/folio-org/edge-patron)
  -- Edge API to interface with FOLIO for 3rd party discovery services to allow patrons to perform self-service actions.

- [edge-resolver](https://github.com/folio-org/edge-resolver)
  -- Edge API to bridge the gap between external reporting and analytics systems and FOLIO by allowing these systems to resolve FOLIO UUIDs, such as a FOLIO user id, thereby acquiring a richer set of data.

- [edge-rtac](https://github.com/folio-org/edge-rtac)
  -- Edge API for RTAC (Real-Time Availability Check).
  To interface with FOLIO for 3rd party discovery services to determine holdings availability.

- [edge-sip2](https://github.com/folio-org/edge-sip2)
  -- Edge API to bridge the gap between self-service circulation and patron services stations and FOLIO by allowing these systems to issue requests and receive responses in Standard Interchange Protocol v2 (SIP2).

## Client-side

Since Okapi represents all the FOLIO functionality as well-behaved web
services, UI code can, of course, be written using any toolkit. However,
we will provide Stripes, a toolkit optimized for accessing Okapi-based
services and wrapping UI functionality into convenient modules. We
envisage that most FOLIO UI work will be done in the context of
Stripes.

The stripes [documentation](https://github.com/folio-org/stripes/blob/master/README.md) is the starting point.
Each front-end module has its documentation.

Note that Stripes is still in the design phase, so although code
exists and can be run, the APIs are likely to change.

- [stripes](https://github.com/folio-org/stripes)
  -- The Stripes Framework.
  UI framework for building front-end FOLIO modules.
  Includes extensive documentation.

- [stripes-core](https://github.com/folio-org/stripes-core)
  -- The core of the Stripes/UI framework.

- [stripes-components](https://github.com/folio-org/stripes-components)
  -- A component library for Stripes.
  Includes documentation for each library, and guides to assist their development.

- [stripes-smart-components](https://github.com/folio-org/stripes-smart-components)
  -- A suite of smart components. Each communicates with an Okapi web-service to provide the facilities that it renders.

- [stripes-acq-components](https://github.com/folio-org/stripes-acq-components)
  -- Stripes components that are specific to use cases that arise in Acquisition-related modules.

- [stripes-data-transfer-components](https://github.com/folio-org/stripes-data-transfer-components)
  -- Stripes components that are specific to use cases that arise in ui-data-import and ui-data-export modules.

- [stripes-erm-components](https://github.com/folio-org/stripes-erm-components)
  -- Stripes components that are specific to use cases that arise in ERM-related modules.

- [stripes-util](https://github.com/folio-org/stripes-util)
  -- A library of utility functions to support Stripes modules.

- [stripes-connect](https://github.com/folio-org/stripes-connect)
  -- Manages the connection of UI components to back-end modules.

- [stripes-form](https://github.com/folio-org/stripes-form)
  -- A redux-form wrapper for Stripes.

- [stripes-final-form](https://github.com/folio-org/stripes-final-form)
  -- A Final Form Wrapper for Stripes.

- [stripes-logger](https://github.com/folio-org/stripes-logger)
  -- Simple category-based logging for Stripes.

- [stripes-cli](https://github.com/folio-org/stripes-cli)
  -- Command-line interface for creating, building, and testing Stripes UI modules.

- [ui-users](https://github.com/folio-org/ui-users)
  -- Stripes UI module: administrating users.

- [ui-inventory](https://github.com/folio-org/ui-inventory)
  -- Stripes UI module: administrating locally created instances, holdings records and items.

- [ui-requests](https://github.com/folio-org/ui-requests)
  -- Stripes UI module: making requests on items.

- [ui-calendar](https://github.com/folio-org/ui-calendar)
  -- Stripes UI module: institutional calendar functions.

- [ui-checkin](https://github.com/folio-org/ui-checkin)
  -- Stripes UI module: checking in items with simulated scans.

- [ui-checkout](https://github.com/folio-org/ui-checkout)
  -- Stripes UI module: checking out items with simulated scans.

- [ui-circulation](https://github.com/folio-org/ui-circulation)
  -- Stripes UI module: Circulation.

- [ui-datasets](https://github.com/folio-org/ui-datasets)
  -- Stripes UI module: FOLIO Datasets based on Glint.

- [ui-data-export](https://github.com/folio-org/ui-data-export)
  -- Stripes UI module: Managing data export.

- [ui-data-import](https://github.com/folio-org/ui-data-import)
  -- Stripes UI module: Managing batch data loader.

- [ui-courses](https://github.com/folio-org/ui-courses)
  -- Stripes UI module: Course reserves.

- [ui-marccat](https://github.com/folio-org/ui-marccat)
  -- Stripes UI module: searching, sorting, filtering, viewing, editing and creating BIB record.

- [ui-quick-marc](https://github.com/folio-org/ui-quick-marc)
  -- Stripes UI module: quickMARC editor.

- [ui-acquisition-units](https://github.com/folio-org/ui-acquisition-units)
  -- Stripes UI module: Management of Acquisition unit records.

- [ui-orders](https://github.com/folio-org/ui-orders)
  -- Stripes UI module: Orders.

- [ui-receiving](https://github.com/folio-org/ui-receiving)
  -- Stripes UI module: Receiving.

- [ui-eholdings](https://github.com/folio-org/ui-eholdings)
  -- Stripes UI module: E-holdings.

- [ui-agreements](https://github.com/folio-org/ui-agreements)
  -- Stripes UI module: Electronic resource management (ERM).

- [ui-erm-usage](https://github.com/folio-org/ui-erm-usage)
  -- Stripes UI module: Managing ERM usage statistics.

- [ui-ldp](https://github.com/folio-org/ui-ldp)
  -- Management Console for the Library Data Platform ([LDP](https://github.com/folio-org/ldp)).

- [ui-local-kb-admin](https://github.com/folio-org/ui-local-kb-admin)
  -- Stripes UI module: Manage the local KB for ERM.

- [ui-licenses](https://github.com/folio-org/ui-licenses)
  -- Stripes UI module: Upload, manage and analyze licenses.

- [ui-search](https://github.com/folio-org/ui-search)
  -- Stripes UI module: searching, sorting, filtering and viewing records from the FOLIO Codex, an aggregation of bibliographic metadata from multiple sources.

- [ui-tenant-settings](https://github.com/folio-org/ui-tenant-settings)
  -- Stripes UI module: managing tenant settings.

- [ui-myprofile](https://github.com/folio-org/ui-myprofile)
  -- Stripes UI module: managing user profile settings.

- [ui-notes](https://github.com/folio-org/ui-notes)
  -- Stripes UI module: notes helper.

- [ui-oai-pmh](https://github.com/folio-org/ui-oai-pmh)
  -- Stripes UI module: managing OAI PMH settings.

- [ui-tags](https://github.com/folio-org/ui-tags)
  -- Stripes UI module: managing tag settings.

- [ui-finance](https://github.com/folio-org/ui-finance)
  -- Stripes UI module: management of ledgers, funds, and budgets.

- [ui-invoice](https://github.com/folio-org/ui-invoice)
  -- Stripes UI module: management of invoices.

- [ui-finc-config](https://github.com/folio-org/ui-finc-config)
  -- Stripes UI module: amsl's finc-config.

- [ui-finc-select](https://github.com/folio-org/ui-finc-select)
  -- Stripes UI module: enable the selection of metadata sources and collections for the finc user community.

- [ui-servicepoints](https://github.com/folio-org/ui-servicepoints)
  -- Stripes UI module: Service Points handler.

- [ui-organizations](https://github.com/folio-org/ui-organizations)
  -- Stripes UI module: Organizations.

- [ui-audit](https://github.com/folio-org/ui-audit)
  -- Stripes UI module: Viewing audit trails.

<a id="ui-plugin"></a>

- [ui-plugin-create-item](https://github.com/folio-org/ui-plugin-create-item)
  -- Stripes UI plugin: Create item.

- [ui-plugin-find-contact](https://github.com/folio-org/ui-plugin-find-contact)
  -- Stripes UI plugin: Contact finder.

- [ui-plugin-find-agreement](https://github.com/folio-org/ui-plugin-find-agreement)
  -- Stripes UI plugin: ERM agreement finder.

- [ui-plugin-find-erm-usage-data-provider](https://github.com/folio-org/ui-plugin-find-erm-usage-data-provider)
  -- Stripes UI plugin: ERM usage data provider finder.

- [ui-plugin-find-finc-metadata-collection](https://github.com/folio-org/ui-plugin-find-finc-metadata-collection)
  -- Stripes UI plugin: finc metadata collection finder.

- [ui-plugin-find-finc-metadata-source](https://github.com/folio-org/ui-plugin-find-finc-metadata-source)
  -- Stripes UI plugin: finc metadata sources finder.

- [ui-plugin-find-import-profile](https://github.com/folio-org/ui-plugin-find-import-profile)
  -- Stripes UI plugin: Data Import profiles finder.

- [ui-plugin-find-instance](https://github.com/folio-org/ui-plugin-find-instance)
  -- Stripes UI plugin: Instance finder.

- [ui-plugin-find-interface](https://github.com/folio-org/ui-plugin-find-interface)
  -- Stripes UI plugin: Find an interface.

- [ui-plugin-find-license](https://github.com/folio-org/ui-plugin-find-license)
  -- Stripes UI plugin: License finder.
  UI Widget to lookup or create licenses.

- [ui-plugin-find-organization](https://github.com/folio-org/ui-plugin-find-organization)
  -- Stripes UI plugin: Organization finder.

- [ui-plugin-find-po-line](https://github.com/folio-org/ui-plugin-find-po-line)
  -- Stripes UI plugin: Display, filter and select PO lines.

- [ui-plugin-find-user](https://github.com/folio-org/ui-plugin-find-user)
  -- Stripes UI plugin: User finder.

- [ui-developer](https://github.com/folio-org/ui-developer)
  -- Stripes UI module: developer facilities,
  e.g. managing local developer settings.

- [eslint-config-stripes](https://github.com/folio-org/eslint-config-stripes)
  -- The shared eslint configuration for stripes applications and extensions.

- [platform-complete](https://github.com/folio-org/platform-complete)
  -- Stripes platform: Complete.

- [platform-core](https://github.com/folio-org/platform-core)
  -- Stripes platform: Core.

- [platform-erm](https://github.com/folio-org/platform-erm)
  -- Stripes platform: ERM.

- [folio-testing-platform](https://github.com/folio-org/folio-testing-platform)
  -- Stripes platform: Testing.

- [stripes-sample-platform](https://github.com/folio-org/stripes-sample-platform)
  -- Configuration for a sample platform and to run a local
  Stripes UI development server.

- [stripes-demo-platform](https://github.com/folio-org/stripes-demo-platform)
  -- Stripes platform for building the demo site.

- [stripes-testing](https://github.com/folio-org/stripes-testing)
  -- Toolkit for running tests against Stripes UI modules and platforms.

## Other projects

- [folio-sample-modules](https://github.com/folio-org/folio-sample-modules)
  -- Various sample modules, illustrating ways to structure a module for
  use with Okapi (e.g. `hello-vertx` and `simple-vertx` and `simple-perl`).

- [folio-ansible](https://github.com/folio-org/folio-ansible)
  -- Sample Ansible playbook and roles for FOLIO (and Vagrant).
  Get a FOLIO installation up and running quickly.
  Read the docs there, and follow to build the boxes.
  The currently built boxes are also available to download from
  [Vagrant Cloud](https://app.vagrantup.com/folio).

- [folio-install](https://github.com/folio-org/folio-install)
  -- Runbooks for FOLIO installation, including [step-by-step instructions for a single-server deployment](https://github.com/folio-org/folio-install/blob/master/runbooks/single-server).

- [folio-tools](https://github.com/folio-org/folio-tools)
  -- Various tools and support glue for FOLIO CI.

- [okapi-cli](https://github.com/folio-org/okapi-cli)
  -- Okapi command-line interface.

- [okapi.rb](https://github.com/thefrontside/okapi.rb)
  -- Ruby client to communicate with an Okapi cluster.

- [cql2pgjson-java](https://github.com/folio-org/raml-module-builder/tree/master/cql2pgjson)
  -- [CQL](/reference/glossary/#cql) (Contextual Query Language) to PostgreSQL JSON converter in Java.

- [Net-Z3950-FOLIO](https://github.com/folio-org/Net-Z3950-FOLIO)
  -- A Z39.50 server for FOLIO bibliographic data.

- [folio-graphiql](https://github.com/folio-org/folio-graphiql)
  -- Explore Okapi's GraphQL endpoint.

- [folio-di-support](https://github.com/folio-org/folio-di-support)
  -- Dependency Injection support for FOLIO backend modules.

- [folio-isbn-util](https://github.com/folio-org/folio-isbn-util)
  -- ISBN number converter utilities.

- [folio-liquibase-util](https://github.com/folio-org/folio-liquibase-util)
  -- Liquibase utilities.

- [folio-holdingsiq-client](https://github.com/folio-org/folio-holdingsiq-client)
  -- Client library to HoldingsIQ API.

- [folio-service-tools](https://github.com/folio-org/folio-service-tools)
  -- Library with general-purpose classes to help with FOLIO backend service development.

- [data-import-utils](https://github.com/folio-org/data-import-utils)
  -- Library with common utilities for data-import modules.

- [folio-perf-test](https://github.com/folio-org/folio-perf-test)
  -- Jenkins pipeline to test FOLIO performance.

- [perf-testing](https://github.com/folio-org/perf-testing)
  -- Tools and performance testing scripts (carrier-io).

- [folio-api-tests](https://github.com/folio-org/folio-api-tests)
  -- Postman collections for backend modules.

- [ldp](https://github.com/folio-org/ldp)
  -- Library Data Platform (LDP).

- [ldp-analytics](https://github.com/folio-org/ldp-analytics)
  -- Reports, queries and other data analysis code for the [LDP](https://github.com/folio-org/ldp).

- [ldp-realtime](https://github.com/folio-org/ldp-realtime)
  -- Real-time querying for the [LDP](https://github.com/folio-org/ldp).

- [ldp-erm-doc](https://github.com/folio-org/ldp-erm-doc)
  -- ERM reporting data dictionaries.

- [rfcs](https://github.com/folio-org/rfcs)
  -- RFCs for changes to the FOLIO platform.
  "Request for Comment" for "substantial" changes.
  Co-ordinated through the [FOLIO Technical Council](https://wiki.folio.org/display/TC/Technical+Council).

- [mod-rmb-template](https://github.com/folio-org/mod-rmb-template)
  -- A Maven archetype to commence a new RMB-based module.

- [ui-app-template](https://github.com/folio-org/ui-app-template)
  -- Stripes UI app module template.
  For use via [stripes-cli](https://github.com/folio-org/stripes-cli/blob/master/doc/user-guide.md#app-development) to commence a new UI module.

- [folio-org.github.io](https://github.com/folio-org/folio-org.github.io)
  -- The source for this dev.folio.org website.
