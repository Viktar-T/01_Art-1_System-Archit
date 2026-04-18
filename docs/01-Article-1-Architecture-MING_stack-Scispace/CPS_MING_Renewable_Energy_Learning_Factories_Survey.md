# Architectural Frameworks for Deploying Cyber-Physical Systems in Renewable Energy Learning Factories Using the MING Stack: A Comprehensive Survey

---

## Executive Summary

This survey examines architectural frameworks for deploying Cyber-Physical Systems (CPS) in renewable energy learning factories using the MING stack (MQTT, InfluxDB, Node-RED, Grafana). Drawing from 180 peer-reviewed publications, we analyze CPS layered architectures, the specific roles of each MING component, data acquisition strategies, communication protocols, time-series data management, workflow orchestration, visualization techniques, and existing framework benchmarks. The evidence demonstrates that MING-based architectures successfully implement the canonical four-layer CPS model (perception, network, middleware, application) in educational and industrial settings, with MQTT providing lightweight pub/sub messaging, Node-RED enabling edge protocol adaptation and orchestration, InfluxDB managing time-series persistence, and Grafana delivering real-time dashboards. However, significant challenges remain in standardization, interoperability with legacy industrial protocols, sensor reliability, scalability to large sensor networks, and digital twin consistency. We synthesize best practices for designing new learning factory CPS architectures, emphasizing on-premises deployment for pedagogical reproducibility, modular Node-RED flows for teaching, early retention policy design, fog-level sensor validation, and comprehensive benchmarking. This survey provides researchers and educators with a structured foundation for implementing robust, evolvable CPS architectures in renewable energy learning environments.

---

## Table of Contents

1. [Introduction](#1-introduction)
2. [Background and Theoretical Foundations](#2-background-and-theoretical-foundations)
   - 2.1 [Cyber-Physical Systems in Industry 4.0](#21-cyber-physical-systems-in-industry-40)
   - 2.2 [Learning Factories and Renewable Energy Education](#22-learning-factories-and-renewable-energy-education)
   - 2.3 [The MING Stack: Origins and Rationale](#23-the-ming-stack-origins-and-rationale)
3. [CPS Layered and Reference Architectures](#3-cps-layered-and-reference-architectures)
   - 3.1 [Four-Layer CPS Model](#31-four-layer-cps-model)
   - 3.2 [Digital Twin Architectures](#32-digital-twin-architectures)
   - 3.3 [Architectural Variants for Learning Factories](#33-architectural-variants-for-learning-factories)
4. [Role of MING Stack Components in CPS](#4-role-of-ming-stack-components-in-cps)
   - 4.1 [MQTT: Lightweight Messaging Fabric](#41-mqtt-lightweight-messaging-fabric)
   - 4.2 [Node-RED: Edge Orchestration and Protocol Adaptation](#42-node-red-edge-orchestration-and-protocol-adaptation)
   - 4.3 [InfluxDB: Time-Series Data Management](#43-influxdb-time-series-data-management)
   - 4.4 [Grafana: Visualization and Dashboarding](#44-grafana-visualization-and-dashboarding)
5. [Data Acquisition and Sensor Integration](#5-data-acquisition-and-sensor-integration)
   - 5.1 [Edge Gateway Mediation Strategies](#51-edge-gateway-mediation-strategies)
   - 5.2 [Virtual and Redundant Sensors](#52-virtual-and-redundant-sensors)
   - 5.3 [Sampling and Data Reduction Policies](#53-sampling-and-data-reduction-policies)
6. [Communication Protocols and Network Topologies](#6-communication-protocols-and-network-topologies)
   - 6.1 [MQTT as Backbone Protocol](#61-mqtt-as-backbone-protocol)
   - 6.2 [LPWAN Technologies for Wide Coverage](#62-lpwan-technologies-for-wide-coverage)
   - 6.3 [Hybrid and Multi-Protocol Topologies](#63-hybrid-and-multi-protocol-topologies)
   - 6.4 [Industrial Protocol Integration](#64-industrial-protocol-integration)
7. [Time-Series Data Management with InfluxDB](#7-time-series-data-management-with-influxdb)
   - 7.1 [Schema Design and Retention Policies](#71-schema-design-and-retention-policies)
   - 7.2 [Digital Twin Historical Data](#72-digital-twin-historical-data)
   - 7.3 [Query Patterns and Performance](#73-query-patterns-and-performance)
8. [Workflow Orchestration with Node-RED](#8-workflow-orchestration-with-node-red)
   - 8.1 [Flow-Based Programming for CPS](#81-flow-based-programming-for-cps)
   - 8.2 [Protocol Bridging and Data Transformation](#82-protocol-bridging-and-data-transformation)
   - 8.3 [Modularity for Pedagogical Applications](#83-modularity-for-pedagogical-applications)
9. [Visualization and Monitoring with Grafana](#9-visualization-and-monitoring-with-grafana)
   - 9.1 [Dashboard Design Patterns](#91-dashboard-design-patterns)
   - 9.2 [Real-Time and Historical Visualization](#92-real-time-and-historical-visualization)
   - 9.3 [Alerting and Interactive Demonstrations](#93-alerting-and-interactive-demonstrations)
10. [Benchmarking of Existing Frameworks](#10-benchmarking-of-existing-frameworks)
    - 10.1 [On-Premises MING Deployments](#101-on-premises-ming-deployments)
    - 10.2 [InfluxData-Based CPS Architectures](#102-influxdata-based-cps-architectures)
    - 10.3 [Digital Twin Pipeline Implementations](#103-digital-twin-pipeline-implementations)
    - 10.4 [Alternative and Hybrid Frameworks](#104-alternative-and-hybrid-frameworks)
11. [Challenges and Open Research Problems](#11-challenges-and-open-research-problems)
    - 11.1 [Standardization and Sustainable Design](#111-standardization-and-sustainable-design)
    - 11.2 [Interoperability and Legacy Systems](#112-interoperability-and-legacy-systems)
    - 11.3 [Sensor Reliability and Data Quality](#113-sensor-reliability-and-data-quality)
    - 11.4 [Scalability and Network Performance](#114-scalability-and-network-performance)
    - 11.5 [Digital Twin Consistency and Real-Time Constraints](#115-digital-twin-consistency-and-real-time-constraints)
12. [Best Practices for Designing Learning Factory CPS Architectures](#12-best-practices-for-designing-learning-factory-cps-architectures)
    - 12.1 [Architectural Design Principles](#121-architectural-design-principles)
    - 12.2 [Deployment and Hosting Strategies](#122-deployment-and-hosting-strategies)
    - 12.3 [Data Management and Quality Assurance](#123-data-management-and-quality-assurance)
    - 12.4 [Pedagogical Considerations](#124-pedagogical-considerations)
    - 12.5 [Performance Benchmarking and Instrumentation](#125-performance-benchmarking-and-instrumentation)
13. [Conclusion](#13-conclusion)
14. [References](#14-references)

---

## 1. Introduction

The convergence of renewable energy systems, Industry 4.0 technologies, and experiential learning methodologies has created unprecedented opportunities for educational institutions to develop learning factories that prepare students for the energy transition. Cyber-Physical Systems (CPS) serve as the technological backbone of these learning environments, integrating physical renewable energy assets—solar panels, wind turbines, battery storage systems, and smart inverters—with computational intelligence, real-time monitoring, and adaptive control. However, designing CPS architectures for learning factories presents unique challenges: systems must be pedagogically transparent, technically robust, cost-effective, reconfigurable for diverse experiments, and capable of operating independently of cloud infrastructure to ensure reproducibility in classroom settings.

The MING stack—comprising MQTT (Message Queuing Telemetry Transport), InfluxDB (time-series database), Node-RED (flow-based programming tool), and Grafana (visualization platform)—has emerged as a compelling open-source solution for CPS deployment in educational and industrial contexts. This technology stack offers vendor neutrality, modularity, and a balance between simplicity and capability that aligns well with learning factory requirements. MQTT provides lightweight, asynchronous messaging suitable for resource-constrained devices and heterogeneous sensor networks. Node-RED enables visual programming and protocol adaptation at the edge, making complex data flows accessible to students and researchers. InfluxDB specializes in time-series data storage with flexible retention policies, essential for managing high-frequency sensor data from renewable energy systems. Grafana delivers intuitive, real-time dashboards that support both operational monitoring and pedagogical demonstrations.

Despite growing adoption, the literature lacks a comprehensive synthesis of how MING-based architectures implement CPS principles in renewable energy learning factories. Existing surveys focus on either general CPS architectures, specific industrial applications, or individual MING components, but do not systematically address the integration challenges, design patterns, and best practices specific to educational renewable energy environments. This survey addresses that gap by analyzing 180 peer-reviewed publications to answer the following research questions:

1. How do MING stack components map to canonical CPS layered architectures?
2. What data acquisition and sensor integration strategies are effective in renewable energy learning factories?
3. Which communication protocols and network topologies best support MING-based CPS?
4. How should time-series data be managed in InfluxDB for educational and research use cases?
5. What workflow orchestration patterns in Node-RED facilitate both operational control and pedagogical activities?
6. What visualization and dashboard design principles in Grafana enhance learning outcomes?
7. How do existing MING-based frameworks perform in real-world deployments?
8. What are the primary technical challenges and open research problems?
9. What best practices should guide the design of new learning factory CPS architectures?

This survey is structured to provide both theoretical foundations and practical guidance. We begin with background on CPS, learning factories, and the MING stack, then systematically examine each architectural layer and component. We analyze benchmarks from existing implementations, identify persistent challenges, and synthesize evidence-based best practices. Our goal is to equip researchers, educators, and system architects with a comprehensive reference for designing, implementing, and evolving MING-based CPS architectures in renewable energy learning factories.

---

## 2. Background and Theoretical Foundations

### 2.1 Cyber-Physical Systems in Industry 4.0

Cyber-Physical Systems represent the integration of computation, networking, and physical processes, where embedded computers and networks monitor and control physical entities through feedback loops. In the Industry 4.0 paradigm, CPS enable smart manufacturing, intelligent energy systems, and autonomous operations by bridging the digital and physical worlds. Reference architectures such as ISA-95 and the 5C (Connection, Conversion, Cyber, Cognition, Configuration) model provide structured frameworks for organizing CPS components into hierarchical layers that separate concerns and enable modular design [1], [25].

The canonical CPS architecture typically comprises four layers: perception (sensors and actuators), network (communication infrastructure), middleware (data management and processing), and application (analytics, control, and user interfaces). This layered approach facilitates separation of concerns, technology substitution, and incremental evolution—properties particularly valuable in educational settings where systems must accommodate diverse experiments and evolving curricula [1], [12].

Digital twin concepts have become central to modern CPS architectures, providing virtual representations of physical assets that enable simulation, prediction, and optimization. A four-layer cognitive digital twin architecture—observation/actuation, data management, reasoning, and simulation—closely aligns with the canonical CPS model and has been successfully applied to renewable energy systems [8], [22]. The SLADTA (six-layer digital twin architecture) further emphasizes asynchronous, vendor-neutral data pipelines, making it particularly suitable for MQTT-based implementations [3].

### 2.2 Learning Factories and Renewable Energy Education

Learning factories are authentic, scaled production or energy systems designed for experiential education, combining real industrial equipment with pedagogical scaffolding. In renewable energy contexts, learning factories integrate solar photovoltaic arrays, wind turbines, battery energy storage systems, power electronics, and grid interconnection equipment to provide hands-on experience with energy generation, storage, conversion, and management [4], [19].

The educational value of learning factories lies in their ability to expose students to real-world complexity, variability, and failure modes while maintaining safety and pedagogical structure. Effective learning factory CPS architectures must therefore balance authenticity with accessibility, providing transparent data flows, reconfigurable experiments, and fail-safe operation. The conversion of traditional manufacturing labs into learning factories for Industry 4.0 education demonstrates the importance of modular, evolvable architectures that can accommodate new technologies and pedagogical approaches [19].

### 2.3 The MING Stack: Origins and Rationale

The MING stack emerged from the convergence of open-source IoT and time-series data management technologies. MQTT, originally developed by IBM for oil pipeline monitoring, provides a lightweight publish-subscribe protocol optimized for unreliable networks and resource-constrained devices. InfluxDB, purpose-built for time-series data, offers high write throughput, flexible retention policies, and SQL-like query capabilities. Node-RED, created at IBM Emerging Technology Services, enables flow-based visual programming for IoT applications. Grafana provides open-source visualization and dashboarding with native support for time-series databases.

The MING stack's appeal for learning factories stems from several factors: all components are open-source, reducing licensing costs and vendor lock-in; the stack supports on-premises deployment, ensuring independence from cloud services during teaching sessions; each component is modular and replaceable, facilitating technology evolution; and the visual, flow-based nature of Node-RED and Grafana makes system behavior transparent to students [1], [6].

---

## 3. CPS Layered and Reference Architectures

### 3.1 Four-Layer CPS Model

The four-layer CPS model provides a canonical framework for organizing system components according to their functional roles. This model has been widely adopted in Industry 4.0 implementations and serves as a foundation for MING-based architectures in renewable energy learning factories.

**Perception Layer:** The perception layer encompasses physical sensors, actuators, power meters, inverters, and local controllers that interface directly with renewable energy assets. In learning factory contexts, this layer includes current and voltage sensors on solar panels, anemometers and power meters on wind turbines, battery management systems, environmental sensors (irradiance, temperature, humidity), and grid interconnection monitoring equipment. The perception layer also includes virtual sensors—software components that derive measurements from multiple physical sensors or digital twin models [8], [12].

**Network Layer:** The network layer provides connectivity between perception devices and middleware services, spanning edge-to-fog-to-cloud topologies. This layer must accommodate diverse communication technologies: constrained links such as LoRaWAN and NB-IoT for battery-powered remote sensors, local Ethernet and Wi-Fi for high-bandwidth devices, and potentially cellular or satellite links for geographically distributed installations. The network layer implements protocol translation, message routing, and quality-of-service management [2], [3], [4].

**Middleware Layer:** The middleware layer provides data management, buffering, schema enforcement, retention policies, and query services. In MING architectures, this layer hosts MQTT brokers, Node-RED gateway instances, and InfluxDB databases. The middleware abstracts physical device heterogeneity, providing uniform interfaces to application services and implementing data quality assurance, aggregation, and archival functions [1], [5], [6].

**Application Layer:** The application layer delivers analytics, digital twin models, control services, dashboards, and user interfaces. In learning factories, this layer includes Grafana dashboards for real-time monitoring, Jupyter notebooks or similar tools for data analysis exercises, digital twin simulation environments, and control interfaces for experimental scenarios. The application layer also encompasses orchestration services that coordinate workflows across multiple system components [8], [9], [11].

### 3.2 Digital Twin Architectures

Digital twin architectures extend the basic CPS model by emphasizing bidirectional data flows and model-based reasoning. A four-layer cognitive digital twin architecture proposed for renewable energy CPS maps observation/actuation to the perception layer, data management to middleware, and reasoning/simulation to the application layer [8]. This architecture has been successfully implemented for energy cyber-physical systems, demonstrating high reconstruction accuracy for high-bandwidth digital twin use cases [8].

The SLADTA (six-layer digital twin architecture) provides a more granular decomposition: physical entity, data acquisition, data communication, data storage, data processing, and application. This architecture emphasizes asynchronous, vendor-neutral data pipelines and has been validated using MQTT as the transport layer for heliostat field digital twins [3]. The asynchronous nature of SLADTA aligns well with MQTT's publish-subscribe model, enabling loose coupling between data producers and consumers—a valuable property for learning factories where experimental configurations change frequently [3].

Recent work on semantic microservice frameworks for digital twins demonstrates how service-oriented architectures can be integrated with MING stacks to provide scalable, composable digital twin services. These frameworks use semantic descriptions to enable dynamic service discovery and composition, supporting complex workflows that combine data ingestion, model execution, and visualization [11].

### 3.3 Architectural Variants for Learning Factories

Learning factory CPS architectures exhibit several deployment variants, each with distinct trade-offs:

**On-Premises Architectures:** On-premises deployments host all MING components within the learning factory's local infrastructure, minimizing dependencies on external cloud services. This approach ensures system availability during teaching sessions, reduces latency for real-time control experiments, and addresses data sovereignty concerns. On-premises architectures have been successfully demonstrated for production data capture and visualization, with measured performance characteristics for write throughput and query latency [1], [6].

**Edge-Heavy Architectures:** Edge-heavy deployments place significant computational capability at or near sensors, using single-board computers or industrial edge gateways to run Node-RED instances, local MQTT brokers, and even lightweight InfluxDB instances. This approach supports fail-safe operation when network connectivity is unreliable and enables low-latency local control loops. Edge-heavy architectures are particularly valuable for distributed renewable energy installations where sensors may be geographically dispersed [10], [12].

**Hybrid Cloud Architectures:** Hybrid architectures combine on-premises components for real-time operation with cloud resources for computationally intensive analytics, long-term archival, and multi-site collaboration. In learning factory contexts, hybrid architectures enable local experiments to proceed independently while supporting research activities that require large-scale data analysis or sharing datasets across institutions [8], [9].

The choice among these variants depends on pedagogical requirements, available infrastructure, network reliability, and the balance between operational autonomy and analytical capability. Evidence suggests that on-premises or hybrid approaches are preferred for learning factories to ensure reproducible classroom experiences [1], [6].

---

## 4. Role of MING Stack Components in CPS

### 4.1 MQTT: Lightweight Messaging Fabric

MQTT serves as the messaging backbone in MING-based CPS architectures, providing lightweight publish-subscribe communication between perception devices, edge gateways, middleware services, and applications. MQTT's design prioritizes minimal protocol overhead, support for unreliable networks, and quality-of-service levels that balance reliability and performance—characteristics essential for renewable energy learning factories with heterogeneous devices and variable network conditions.

In CPS layered architectures, MQTT operates primarily at the network and lower middleware layers, transporting sensor data from edge gateways to central brokers and distributing commands from control services to actuators. The publish-subscribe model decouples data producers from consumers, enabling flexible system reconfiguration without modifying individual components—a valuable property for learning environments where experimental setups change frequently [1], [3].

MQTT has been successfully evaluated as the transport layer for digital twin data pipelines, including the SLADTA architecture applied to heliostat field monitoring. These implementations demonstrate MQTT's suitability for asynchronous, vendor-neutral data flows in complex CPS deployments [3]. The protocol's topic-based routing enables logical organization of sensor streams (e.g., `/site/building/floor/sensor_type/sensor_id`), facilitating both human comprehension and programmatic subscription patterns [1], [6].

Advanced MQTT deployments in learning factories may implement hierarchical broker topologies, where edge brokers aggregate local sensor data and bridge to central brokers, reducing network traffic and improving resilience. MQTT's support for retained messages and last-will-and-testament features enables status monitoring and automatic fault detection—capabilities useful for teaching reliability concepts [2], [4].

### 4.2 Node-RED: Edge Orchestration and Protocol Adaptation

Node-RED functions as a visual flow-based programming environment for orchestrating data flows, adapting protocols, and implementing edge logic in MING-based CPS architectures. Its role spans the network and middleware layers, serving as a bridge between heterogeneous perception devices and standardized middleware services.

In learning factory deployments, Node-RED typically runs on edge gateways or fog nodes, receiving data from sensors via diverse protocols (Modbus, OPC-UA, HTTP, serial) and publishing normalized messages to MQTT topics. This protocol adaptation capability is critical for integrating legacy industrial equipment commonly found in learning factories with modern IoT infrastructure [1], [6]. Node-RED's visual programming model makes data flow logic transparent and modifiable, supporting pedagogical objectives by allowing students to understand and modify system behavior without low-level programming [6].

Node-RED's extensive library of contributed nodes enables integration with virtually any sensor, actuator, or service. For renewable energy applications, nodes exist for Modbus RTU/TCP (common in power meters and inverters), OPC-UA (industrial automation standard), HTTP REST APIs (cloud services and web-based devices), and direct GPIO access (for single-board computers). This extensibility allows learning factories to incrementally add new equipment without architectural redesign [1], [10].

Beyond protocol adaptation, Node-RED supports inline data processing, including unit conversion, filtering, aggregation, and anomaly detection. These capabilities enable edge intelligence, reducing network traffic and enabling local decision-making. For learning factories, Node-RED flows can implement experimental scenarios, such as simulating sensor failures, injecting synthetic data, or triggering control actions based on threshold conditions [6], [11].

### 4.3 InfluxDB: Time-Series Data Management

InfluxDB serves as the primary time-series data store in MING architectures, occupying the middleware layer and providing persistent storage, retention management, and query services for sensor data streams. InfluxDB's design optimizes for high write throughput, efficient storage of timestamped data, and flexible query capabilities—requirements that align well with renewable energy monitoring applications generating continuous sensor streams.

InfluxDB's data model organizes measurements into series defined by measurement names, tag sets (indexed metadata), and field sets (actual values). This schema enables efficient queries across multiple dimensions (e.g., "all temperature sensors in Building A during the last week") while maintaining high write performance. For learning factories, this model supports both operational queries (current system state) and analytical queries (historical trends, comparative analysis) [5], [7].

Retention policies in InfluxDB enable automated data lifecycle management, a critical capability for learning factories that must balance high-resolution data for recent experiments with long-term archival for research. Continuous queries support automatic downsampling, where high-frequency raw data is aggregated into lower-resolution summaries for long-term storage. For example, per-second solar irradiance measurements might be retained at full resolution for one week, downsampled to one-minute averages for one year, and further aggregated to hourly averages for indefinite retention [5], [7].

InfluxDB integrations with digital twin frameworks demonstrate its role in maintaining historical state for virtual asset models. By combining InfluxDB time-series data with relational databases for metadata and configuration, systems can reconstruct equipment behavior for fault analysis, performance optimization, and predictive maintenance exercises [5], [7], [22].

### 4.4 Grafana: Visualization and Dashboarding

Grafana operates at the application layer, providing visualization, dashboarding, and alerting capabilities that transform raw time-series data into actionable insights and pedagogical demonstrations. Grafana's native integration with InfluxDB enables direct querying and visualization of sensor streams without intermediate data transformation.

In learning factory contexts, Grafana serves multiple roles: operational dashboards for system monitoring, analytical dashboards for data exploration, and pedagogical dashboards designed to illustrate specific concepts or experimental results. Role-based dashboard design enables different views for instructors (comprehensive system state), students (focused experimental data), and maintenance personnel (equipment health metrics) [1], [6], [7].

Grafana's panel types support diverse visualization needs: time-series graphs for trend analysis, gauges and stat panels for current values, heatmaps for correlation analysis, and tables for detailed data inspection. For renewable energy applications, common dashboard patterns include power generation vs. irradiance correlation, battery state-of-charge tracking, energy balance visualization (generation, consumption, storage), and efficiency metrics [4], [6], [7].

Grafana's alerting capabilities enable threshold-based notifications and can be integrated with teaching scenarios. For example, alerts can notify students when experimental conditions reach target states, or trigger automated responses in control experiments. Annotations support marking significant events on time-series graphs, enabling post-experiment analysis and discussion [1], [6].

---

## 5. Data Acquisition and Sensor Integration

### 5.1 Edge Gateway Mediation Strategies

Edge gateway mediation represents a fundamental strategy for integrating heterogeneous sensors into MING-based CPS architectures. Edge gateways—typically single-board computers, industrial PCs, or specialized IoT gateways—sit between perception devices and the central MING infrastructure, performing protocol adaptation, data normalization, local buffering, and preliminary processing.

The primary function of edge gateways is protocol adaptation: translating diverse sensor interfaces (Modbus RTU/TCP, OPC-UA, CAN bus, analog signals, serial protocols) into standardized MQTT messages. Node-RED is frequently deployed on edge gateways for this purpose, providing visual flow-based configuration that simplifies integration of new sensors and makes data flow logic transparent for educational purposes [1], [6]. This approach has been demonstrated in multi-machine production systems and low-cost motor monitoring applications, where Node-RED gateways collect data from heterogeneous sources and publish normalized topics to central MQTT brokers [1], [10].

Edge gateways also implement local buffering to handle network interruptions, ensuring data continuity when connectivity to central infrastructure is temporarily lost. This capability is particularly important for learning factories where network reliability may vary and where experiments should proceed uninterrupted. Store-and-forward mechanisms in Node-RED or lightweight local databases enable gateways to queue data during outages and synchronize when connectivity is restored [10], [12].

Data normalization at the edge includes unit conversion, timestamp standardization, and metadata enrichment. For example, a gateway might convert temperature readings from various sensors reporting in Celsius, Fahrenheit, or Kelvin into a standard unit, add location tags, and inject equipment identifiers. This normalization simplifies downstream processing and ensures consistency across heterogeneous sensor populations [1], [6].

### 5.2 Virtual and Redundant Sensors

Virtual sensors and sensor redundancy strategies enhance data quality and system reliability in learning factory CPS architectures. Virtual sensors are software components that derive measurements from multiple physical sensors, digital twin models, or analytical relationships, providing estimates when direct measurements are unavailable or unreliable.

Virtual sensor implementations at the edge or fog layer can mask sensor failures, reduce network traffic, and provide derived quantities not directly measurable. For example, a virtual power sensor might calculate instantaneous power from voltage and current measurements, or a virtual irradiance sensor might estimate solar radiation from weather forecasts and historical patterns when physical pyranometers fail. MQTT is commonly used to expose virtual sensors upstream, treating them as first-class data sources indistinguishable from physical sensors [12].

Sensor redundancy and ranking methods address data quality challenges in learning factories where sensors may experience drift, calibration errors, or intermittent failures. FOCUSeR (Fog Online Context-Aware Up-to-Date Sensor Ranking) represents a fog-level approach that continuously evaluates sensor reliability based on consistency with peer sensors, historical patterns, and contextual information. By ranking sensors and weighting their contributions, systems can maintain data quality even when individual sensors degrade [21].

The integration of virtual and redundant sensors with MING architectures typically involves edge or fog nodes running sensor fusion algorithms, publishing both raw sensor data and fused estimates to MQTT topics, and storing both streams in InfluxDB for comparative analysis. This approach supports pedagogical objectives by enabling students to observe sensor behavior, understand data quality issues, and experiment with fusion algorithms [12], [21].

### 5.3 Sampling and Data Reduction Policies

Sampling and data reduction policies at the edge optimize network utilization and storage costs while preserving information content necessary for learning and research activities. These policies must balance competing objectives: high-resolution data for detailed analysis, reduced network traffic for constrained links, and manageable storage requirements for long-term archival.

Adaptive sampling strategies adjust measurement frequency based on signal characteristics or system state. For example, solar irradiance might be sampled at high frequency during variable cloud conditions but reduced during clear-sky periods when values change slowly. Event-triggered sampling captures data when significant changes occur, reducing traffic during steady-state operation. These strategies can be implemented in Node-RED flows at edge gateways, with logic that evaluates signal derivatives or compares values against thresholds [10], [12].

Local aggregation at edge gateways reduces data volume while preserving statistical properties. Instead of transmitting every measurement, gateways can compute and transmit summary statistics (mean, min, max, standard deviation) over fixed time windows. For learning factories, this approach enables high-frequency local monitoring while reducing network and storage requirements for central infrastructure. InfluxDB's continuous query feature complements edge aggregation by providing additional downsampling at the database level [5], [10].

Compression and delta encoding techniques further reduce network traffic. MQTT's payload format is flexible, allowing binary encoding of sensor data rather than verbose JSON or XML. Delta encoding transmits only changes from previous values, significantly reducing bandwidth for slowly varying signals. These techniques are particularly valuable for battery-powered sensors or installations with limited network capacity [4], [10].

The design of sampling and reduction policies requires careful consideration of pedagogical and research requirements. Learning factories must retain sufficient detail for students to observe system dynamics and conduct meaningful experiments, while avoiding overwhelming storage and network infrastructure. Best practice involves configuring multiple retention tiers in InfluxDB: high-resolution recent data for active experiments, medium-resolution data for semester-long projects, and low-resolution long-term archives for multi-year research studies [5], [7].

---

## 6. Communication Protocols and Network Topologies

### 6.1 MQTT as Backbone Protocol

MQTT's role as the backbone communication protocol in MING-based CPS architectures stems from its lightweight design, publish-subscribe model, and quality-of-service options. MQTT's minimal protocol overhead (as low as 2 bytes per message) makes it suitable for resource-constrained devices and low-bandwidth networks common in distributed renewable energy installations.

The publish-subscribe model decouples message producers from consumers, enabling flexible system evolution. Sensors publish data to topics without knowledge of subscribers, and applications subscribe to topics of interest without direct connection to sensors. This loose coupling facilitates system reconfiguration—adding new sensors, modifying data flows, or introducing new applications—without disrupting existing components. For learning factories, this property supports rapid prototyping and experimental flexibility [1], [3].

MQTT's three quality-of-service levels provide trade-offs between reliability and performance: QoS 0 (at most once) for non-critical telemetry where occasional message loss is acceptable, QoS 1 (at least once) for important data where duplication is tolerable, and QoS 2 (exactly once) for critical commands where neither loss nor duplication is acceptable. Learning factory deployments typically use QoS 0 for high-frequency sensor data (where subsequent messages supersede previous values) and QoS 1 or 2 for control commands and configuration changes [1], [6].

MQTT's topic hierarchy enables logical organization and efficient filtering. A typical renewable energy learning factory might organize topics as `/site/building/system/device/measurement`, enabling subscriptions at any level of granularity. For example, an application monitoring all solar panels would subscribe to `/site/+/solar/#`, while a dashboard focused on a specific building would subscribe to `/site/building1/#`. This hierarchical structure also supports access control, where different user roles receive permissions for specific topic subtrees [1], [3].

### 6.2 LPWAN Technologies for Wide Coverage

Low-Power Wide-Area Network (LPWAN) technologies address the challenge of connecting distributed sensors across large geographic areas with minimal infrastructure and power requirements. LoRaWAN, NB-IoT, and Sigfox represent prominent LPWAN options, each with distinct characteristics relevant to renewable energy learning factories.

LoRaWAN integration with MQTT has been demonstrated through gateway architectures that bridge LoRaWAN radio networks to MQTT brokers. These implementations enable battery-powered sensors deployed across solar farms or wind installations to transmit data over multi-kilometer ranges while maintaining years of battery life. The MQTT2MULTICAST protocol extension optimizes MQTT for LoRaWAN by using UDP multicast for message distribution, reducing latency by approximately 90% and SDN controller traffic by 55% compared to standard MQTT over TCP [2].

LoRaWAN's star topology, where end devices communicate directly with gateways that forward messages to network servers, aligns well with learning factory deployments where sensors are distributed across a campus or facility. The network server can run MQTT clients that publish sensor data to central brokers, integrating LoRaWAN devices seamlessly into MING architectures. This approach has been validated in systems supporting tens of thousands of LoRaWAN gateways [2], [4].

The trade-offs of LPWAN technologies must be carefully considered for learning factory applications. LoRaWAN's low data rates (typically 0.3-50 kbps) and duty cycle restrictions limit message frequency, making it suitable for periodic monitoring (e.g., temperature, humidity, battery voltage) but not for high-frequency power measurements. Hybrid topologies that combine LPWAN for remote, low-frequency sensors with Wi-Fi or Ethernet for high-bandwidth devices provide balanced solutions [2], [4], [10].

### 6.3 Hybrid and Multi-Protocol Topologies

Hybrid network topologies combine multiple communication technologies to optimize coverage, bandwidth, latency, and cost across diverse sensor populations. Learning factory CPS architectures typically employ star topologies within buildings (sensors to local gateways) and hierarchical or mesh topologies for inter-building or campus-wide connectivity.

Within laboratory spaces, sensors connect to local gateways via Ethernet, Wi-Fi, or short-range wireless protocols (Zigbee, Bluetooth). These gateways aggregate data and publish to MQTT brokers over reliable, high-bandwidth links. This star topology minimizes latency for real-time monitoring and control experiments while simplifying network management [1], [6], [10].

For distributed installations—such as solar arrays across multiple rooftops or wind turbines at different campus locations—hierarchical topologies with edge brokers provide scalability and resilience. Edge brokers aggregate data from local sensors and bridge to central brokers, reducing traffic on backbone networks and enabling local operation during network partitions. MQTT's bridge functionality supports this topology, allowing edge brokers to selectively forward topics to central infrastructure [2], [6].

Fog computing architectures extend this hierarchy by placing computational resources at intermediate layers between edge and cloud. Fog nodes can run Node-RED for local orchestration, lightweight InfluxDB instances for short-term buffering, and edge analytics for real-time decision-making. This approach supports low-latency control loops and fail-safe operation while enabling cloud bursts for computationally intensive tasks [9], [10], [12].

### 6.4 Industrial Protocol Integration

Integration of industrial protocols—OPC-UA, Modbus RTU/TCP, CAN bus, PROFINET—represents a persistent challenge in learning factory CPS architectures, as renewable energy equipment often uses these protocols for monitoring and control. Node-RED serves as the primary integration tool, providing protocol adapter nodes that translate between industrial protocols and MQTT.

OPC-UA (Open Platform Communications Unified Architecture) is increasingly common in modern renewable energy equipment, providing standardized, secure, platform-independent communication. Node-RED's OPC-UA nodes enable browsing of OPC-UA server namespaces, subscribing to data changes, and invoking methods. For learning factories, OPC-UA integration enables access to inverter parameters, battery management system data, and grid interconnection status [12], [18].

Modbus, despite its age, remains ubiquitous in power meters, inverters, and industrial sensors. Node-RED's Modbus nodes support both RTU (serial) and TCP (Ethernet) variants, enabling polling of holding registers and coils. Learning factory implementations typically deploy Modbus-to-MQTT gateways that periodically poll Modbus devices and publish values to MQTT topics, abstracting Modbus's request-response model into MQTT's publish-subscribe paradigm [1], [6], [10].

CAN bus integration is relevant for battery management systems and electric vehicle charging infrastructure in learning factories. Node-RED nodes for CAN enable decoding of CAN frames and publishing extracted signals to MQTT. This integration exposes detailed battery cell voltages, temperatures, and state-of-charge information for educational analysis [12].

The adapter pattern—where Node-RED flows translate between industrial protocols and MQTT—provides a consistent integration approach. Each adapter flow subscribes to or polls industrial devices, normalizes data formats, adds metadata, and publishes to standardized MQTT topics. This pattern isolates protocol complexity at the edge, presenting a uniform MQTT interface to central infrastructure and applications [1], [6], [18].

---

## 7. Time-Series Data Management with InfluxDB

### 7.1 Schema Design and Retention Policies

InfluxDB's schema design revolves around measurements, tags, and fields, providing a flexible yet performant structure for time-series data. Measurements correspond to sensor types or data categories (e.g., `solar_power`, `battery_soc`, `temperature`), tags represent indexed metadata (e.g., `location`, `device_id`, `sensor_type`), and fields contain actual measured values (e.g., `power_watts`, `voltage`, `current`). This schema enables efficient queries across multiple dimensions while maintaining high write throughput.

For learning factory applications, schema design must balance query flexibility with write performance. A common pattern uses measurements to represent physical quantities or equipment types, tags for hierarchical location information and device identifiers, and fields for multiple related values. For example, a solar panel measurement might include tags for `building`, `array_id`, and `panel_id`, with fields for `voltage`, `current`, `power`, and `temperature`. This design enables queries like "average power from all panels in Building A" or "temperature distribution across Array 3" [5], [7].

Retention policies automate data lifecycle management, specifying how long data is retained at different resolutions. InfluxDB supports multiple retention policies per database, enabling tiered storage strategies. A typical learning factory configuration might include: a `realtime` policy retaining full-resolution data for 7 days (supporting active experiments), a `semester` policy retaining 1-minute aggregates for 6 months (supporting course projects), and a `research` policy retaining hourly aggregates indefinitely (supporting long-term studies) [5], [7].

Continuous queries implement automatic downsampling, periodically aggregating high-resolution data into lower-resolution summaries. For example, a continuous query might compute 1-minute averages from per-second measurements, or calculate daily energy totals from instantaneous power readings. These queries run automatically in the background, populating retention policies with aggregated data. For learning factories, continuous queries reduce storage requirements while preserving statistical properties necessary for analysis [5], [7].

### 7.2 Digital Twin Historical Data

InfluxDB's role in digital twin architectures extends beyond simple sensor data storage to maintaining comprehensive historical state for virtual asset models. Digital twins require not only current sensor values but also historical trajectories, event logs, and derived state variables to support simulation, prediction, and optimization.

Integration of InfluxDB with digital twin frameworks typically combines time-series data with relational databases for metadata and configuration. InfluxDB stores sensor measurements, calculated variables, and model outputs, while relational databases maintain equipment specifications, maintenance records, and configuration parameters. This hybrid approach balances InfluxDB's time-series performance with relational databases' structured data capabilities [5], [7], [22].

Digital twin implementations for compressor equipment and renewable energy systems demonstrate InfluxDB's capability to support real-time digital twin updates and historical reconstruction. These systems use MQTT or Telegraf agents to stream sensor data into InfluxDB, where it becomes immediately available for digital twin model updates and visualization in Grafana. Historical queries enable reconstruction of equipment behavior for fault analysis, performance optimization, and predictive maintenance exercises [5], [7].

For learning factories, digital twin historical data supports pedagogical objectives by enabling students to replay past experiments, compare actual vs. predicted behavior, and analyze system response to disturbances. InfluxDB's query language supports time-based joins, enabling correlation analysis between different sensor streams and identification of causal relationships [7], [8], [22].

### 7.3 Query Patterns and Performance

InfluxDB's query language (InfluxQL or Flux) provides SQL-like syntax for time-series data retrieval, aggregation, and transformation. Common query patterns in learning factory applications include: current value retrieval (most recent measurement), time-range queries (all data within a period), aggregation queries (average, sum, min, max over time windows), and correlation queries (relationships between multiple measurements).

Performance optimization for learning factory workloads involves several strategies. Indexing on tags enables efficient filtering by location, device, or sensor type, while fields remain unindexed to maintain write performance. Query performance benefits from limiting time ranges, using appropriate aggregation intervals, and leveraging continuous queries for pre-computed aggregates. For real-time dashboards, queries should target recent data (hours to days) rather than full historical ranges [5], [7].

Write performance in InfluxDB scales with batch size and write frequency. Learning factory implementations typically configure MQTT-to-InfluxDB bridges (using Telegraf or custom Node-RED flows) to batch sensor data, writing every few seconds rather than on every message. This batching reduces write overhead while maintaining acceptable latency for monitoring applications. Benchmarks from on-premises IIoT deployments demonstrate the importance of measuring write throughput and query latency during system design to ensure performance meets requirements [1], [5].

InfluxDB's support for multiple databases enables isolation of different projects or courses within a learning factory. Each course or research project can have dedicated databases with appropriate retention policies, preventing interference and simplifying data management. Database-level access control supports role-based security, ensuring students access only relevant data [5], [7].

---

## 8. Workflow Orchestration with Node-RED

### 8.1 Flow-Based Programming for CPS

Node-RED's flow-based programming paradigm provides an intuitive visual approach to orchestrating CPS workflows, making complex data flows and control logic accessible to students and researchers without extensive programming backgrounds. Flows consist of nodes (processing elements) connected by wires (data paths), with messages flowing between nodes in response to events or timers.

In learning factory CPS architectures, Node-RED flows implement diverse functions: sensor data acquisition and normalization, protocol translation, data transformation and enrichment, conditional routing, aggregation and filtering, external service integration, and control logic. The visual representation of these flows serves pedagogical purposes, enabling students to understand system behavior by inspecting flow diagrams rather than reading code [1], [6], [11].

Node-RED's event-driven execution model aligns well with CPS requirements. Flows react to incoming MQTT messages, HTTP requests, timer events, or file system changes, processing data and triggering downstream actions. This reactive model supports both continuous monitoring (processing sensor streams) and discrete event handling (responding to alarms or user commands). For learning factories, event-driven flows enable implementation of experimental scenarios, such as triggering data collection when specific conditions occur or simulating equipment failures at scheduled times [6], [11].

The modularity of Node-RED flows supports incremental system development and experimentation. Flows can be developed and tested independently, then integrated into larger systems. Subflows (reusable flow components) enable abstraction and code reuse, allowing common patterns (e.g., sensor data normalization, error handling) to be packaged and shared. For learning factories, this modularity enables instructors to provide template flows that students extend or modify for specific experiments [6], [11].

### 8.2 Protocol Bridging and Data Transformation

Node-RED's extensive node library enables protocol bridging between heterogeneous devices and services, a critical capability for learning factories integrating diverse equipment. Protocol adapter nodes translate between industrial protocols (Modbus, OPC-UA, CAN), IoT protocols (MQTT, CoAP, HTTP), and database interfaces (InfluxDB, SQL), presenting a unified data model to applications.

A typical protocol bridging flow reads data from industrial devices using protocol-specific input nodes, transforms the data into a standardized format (often JSON), enriches it with metadata (timestamps, location tags, units), and publishes it to MQTT topics or writes it directly to InfluxDB. This pattern abstracts protocol complexity, enabling applications to consume data without knowledge of underlying device interfaces [1], [6], [10].

Data transformation in Node-RED flows includes unit conversion, scaling, filtering, and derived value calculation. Function nodes enable custom JavaScript code for complex transformations, while built-in nodes handle common operations (JSON parsing, string manipulation, mathematical operations). For renewable energy applications, transformations might include converting power measurements to energy totals, calculating efficiency metrics, or normalizing irradiance measurements to standard test conditions [1], [6].

Error handling and data quality assurance are essential aspects of protocol bridging. Node-RED flows can implement validation logic, checking for out-of-range values, missing data, or communication errors. Invalid data can be logged, filtered, or replaced with default values, ensuring downstream applications receive clean data. For learning factories, explicit error handling in flows provides teaching opportunities about data quality and system reliability [6], [10].

### 8.3 Modularity for Pedagogical Applications

Node-RED's modularity and visual programming model make it particularly valuable for pedagogical applications in learning factories. Flows serve as executable documentation, illustrating system behavior in a format accessible to students with varying technical backgrounds. The ability to import and export flows as JSON files enables sharing of experimental setups, reproducibility of results, and version control of system configurations.

Pedagogical flow patterns include: sensor simulation flows that generate synthetic data for testing without physical equipment, data conditioning flows that demonstrate filtering, aggregation, and transformation techniques, control flows that implement feedback loops and setpoint tracking, and anomaly injection flows that simulate sensor failures or equipment malfunctions for troubleshooting exercises [6], [11].

Node-RED's dashboard nodes enable rapid development of custom user interfaces for experiments. Students can create control panels with buttons, sliders, and gauges, connecting them to MQTT topics or InfluxDB queries without web development expertise. This capability supports project-based learning, where students design and implement complete monitoring and control systems [6].

Integration with semantic microservice frameworks extends Node-RED's capabilities for complex digital twin workflows. Semantic descriptions enable dynamic service discovery and composition, allowing Node-RED flows to invoke machine learning models, simulation services, or optimization algorithms as needed. This integration supports advanced projects where students combine data acquisition, model execution, and visualization into end-to-end applications [11].

---

## 9. Visualization and Monitoring with Grafana

### 9.1 Dashboard Design Patterns

Grafana dashboard design for learning factory CPS architectures must balance operational monitoring requirements with pedagogical objectives. Effective dashboards provide clear, actionable information while illustrating system behavior and supporting experimental analysis. Several design patterns have emerged from practical deployments.

**Role-Based Dashboards:** Different user roles require different views of system data. Instructor dashboards provide comprehensive system state, including all sensors, equipment status, and system health metrics. Student dashboards focus on specific experiments, showing only relevant sensors and calculated variables. Maintenance dashboards emphasize equipment health, error rates, and performance metrics. Grafana's organization and permission features support this role-based approach, enabling multiple dashboards with appropriate access controls [1], [6], [7].

**Hierarchical Navigation:** Large learning factories with multiple buildings, systems, and equipment benefit from hierarchical dashboard organization. A top-level overview dashboard shows aggregate metrics and system status, with drill-down links to building-specific, system-specific, and equipment-specific dashboards. Grafana's dashboard links and variables enable this navigation pattern, allowing users to explore from high-level summaries to detailed sensor data [6], [7].

**Operational vs. Analytical Dashboards:** Operational dashboards emphasize current state and recent trends, using large gauges, stat panels, and short time ranges (minutes to hours). Analytical dashboards support data exploration with longer time ranges (days to months), multiple time-series graphs, and statistical panels. Learning factories typically provide both types, with operational dashboards for real-time monitoring during experiments and analytical dashboards for post-experiment analysis [1], [6], [7].

### 9.2 Real-Time and Historical Visualization

Grafana's native integration with InfluxDB enables seamless visualization of both real-time and historical data, supporting diverse learning factory use cases. Real-time visualization provides immediate feedback during experiments, while historical visualization enables comparative analysis and long-term trend identification.

**Real-Time Monitoring:** Real-time dashboards use short auto-refresh intervals (1-5 seconds) and recent time ranges (last 5-30 minutes) to display current system state. Time-series panels show recent trends, stat panels display current values, and gauge panels indicate status relative to thresholds. For renewable energy learning factories, real-time dashboards typically show power generation, consumption, battery state-of-charge, and environmental conditions [1], [4], [6], [7].

**Historical Analysis:** Historical dashboards use longer time ranges (hours to months) and support interactive time range selection. Multiple time-series panels enable comparison of different sensors or time periods. Heatmap panels visualize correlation patterns, and table panels provide detailed data inspection. For learning factories, historical dashboards support analysis of daily generation patterns, seasonal variations, equipment performance trends, and experimental results [6], [7].

**Correlation and Comparison:** Grafana's ability to overlay multiple time series on a single graph enables correlation analysis essential for renewable energy education. Students can visualize relationships between solar irradiance and power generation, temperature and efficiency, or wind speed and turbine output. Grafana's template variables enable rapid comparison across different equipment or time periods, supporting comparative experiments [4], [6], [7].

### 9.3 Alerting and Interactive Demonstrations

Grafana's alerting capabilities extend its role beyond passive visualization to active monitoring and event notification. Alerts evaluate query results against thresholds, triggering notifications via email, Slack, webhooks, or other channels. For learning factories, alerts support both operational monitoring and pedagogical scenarios.

**Threshold-Based Alerts:** Simple threshold alerts notify when sensor values exceed safe operating ranges, equipment fails, or experimental conditions reach target states. For example, alerts might trigger when battery state-of-charge falls below 20%, solar panel temperature exceeds 85°C, or grid voltage deviates from nominal values. These alerts teach students about system limits and safety considerations [1], [6].

**Experimental Scenario Alerts:** Alerts can be designed to support teaching scenarios, notifying students when experimental conditions are achieved or when specific events occur. For example, an alert might notify students when sufficient solar irradiance is available for a photovoltaic characterization experiment, or when battery charging reaches a target state-of-charge for efficiency testing [6].

**Annotations and Event Marking:** Grafana annotations enable marking significant events on time-series graphs, providing context for data interpretation. Annotations can be added manually (e.g., marking when equipment was adjusted) or automatically via API (e.g., marking control actions or experimental phases). For learning factories, annotations support post-experiment analysis by correlating sensor data with experimental actions [1], [6].

**Interactive Demonstrations:** Grafana's dashboard variables and panel links enable interactive demonstrations where students can select different equipment, time ranges, or experimental conditions and immediately see updated visualizations. This interactivity supports exploratory learning, allowing students to formulate and test hypotheses about system behavior [6], [7].

---

## 10. Benchmarking of Existing Frameworks

### 10.1 On-Premises MING Deployments

On-premises MING deployments represent a mature architectural pattern for learning factory CPS, emphasizing vendor neutrality, local control, and measured performance characteristics. The on-premises IIoT architecture for capturing, storing, and visualizing production data demonstrates this pattern, implementing Node-RED gateways, MQTT messaging, InfluxDB storage, and Grafana visualization entirely within local infrastructure [1].

This architecture addresses key learning factory requirements: independence from cloud services ensures system availability during teaching sessions, on-premises hosting addresses data sovereignty and security concerns, and measured performance characteristics (write throughput, query latency) inform capacity planning. The system uses Node-RED as locally available gateways that receive data from machines and forward it via MQTT to a central server, where InfluxDB stores the data and Grafana provides visualization and analysis [1].

Performance benchmarking of this deployment measured data writing and retrieval latency under various load conditions, demonstrating that on-premises MING stacks can support typical learning factory workloads (hundreds of sensors, second-scale sampling) with acceptable latency (sub-second write acknowledgment, near-instantaneous query response for recent data). These benchmarks provide valuable reference points for capacity planning in new learning factory deployments [1].

The emphasis on independent, exchangeable software components addresses vendor lock-in concerns, enabling technology evolution without wholesale system replacement. This modularity is particularly valuable for learning factories, where equipment and technologies evolve over academic cycles and where pedagogical objectives may require demonstrating alternative technologies [1].

### 10.2 InfluxData-Based CPS Architectures

InfluxData-based CPS architectures demonstrate tight integration between time-series data management and digital twin frameworks. The architecture for compressor equipment monitoring and control illustrates this pattern, using MQTT or Telegraf to feed sensor data into InfluxDB, where it supports both real-time monitoring and digital twin model updates [5].

This architecture combines InfluxDB for time-series storage with relational databases for metadata and configuration, providing a hybrid data management approach that balances time-series performance with structured data capabilities. The digital twin component uses historical data from InfluxDB to reconstruct equipment behavior, enabling predictive maintenance, performance optimization, and fault analysis [5], [7].

Grafana integration provides 3D visualization and real-time dashboards, demonstrating how MING components can be extended with domain-specific visualization tools. For learning factories, this integration supports immersive demonstrations where students can visualize equipment operation in 3D while monitoring sensor data in real-time [5], [7], [22].

The architecture's focus on industrial equipment monitoring translates well to renewable energy learning factories, where similar requirements exist for monitoring power electronics, battery systems, and grid interconnection equipment. The demonstrated integration patterns—MQTT for data ingestion, InfluxDB for storage, digital twin models for analysis, and Grafana for visualization—provide a template for learning factory implementations [5], [7].

### 10.3 Digital Twin Pipeline Implementations

Digital twin pipeline implementations using MQTT demonstrate the protocol's suitability for asynchronous, vendor-neutral data flows in complex CPS deployments. The SLADTA (six-layer digital twin architecture) implementation for heliostat field monitoring validates MQTT as the transport layer for digital twin data pipelines, emphasizing loose coupling between data producers and consumers [3].

This architecture decomposes digital twin functionality into six layers: physical entity, data acquisition, data communication, data storage, data processing, and application. MQTT operates at the data communication layer, providing asynchronous message transport between acquisition systems and storage/processing services. The asynchronous nature enables independent evolution of pipeline components, a valuable property for learning factories where experimental configurations change frequently [3].

Validation of the SLADTA architecture with heliostat field simulation demonstrates scalability to large sensor populations and complex physical systems. The architecture's emphasis on vendor neutrality and standard protocols aligns with learning factory requirements for technology independence and long-term evolvability [3].

IoT-based digital twin implementations for energy cyber-physical systems extend this pattern to cloud-enabled architectures, demonstrating high reconstruction accuracy for high-bandwidth digital twin use cases. These implementations show that MING-based architectures can support both on-premises and cloud deployments, enabling hybrid approaches where local infrastructure handles real-time operation and cloud resources support computationally intensive analytics [8].

### 10.4 Alternative and Hybrid Frameworks

Alternative and hybrid frameworks demonstrate the adaptability of MING components and their integration with complementary technologies. FIWARE-based monitoring systems for renewable energy illustrate how MING components can be combined with context broker middleware to provide dynamic data channel management and semantic interoperability [13].

The FIWARE architecture uses context brokers to manage entity relationships and data subscriptions, with MQTT and InfluxDB providing underlying transport and storage. This hybrid approach demonstrates how MING components can be integrated into larger middleware frameworks, potentially offering advantages for complex learning factories with diverse data sources and dynamic experimental configurations [13].

Semantic microservice frameworks for digital twins represent another hybrid approach, combining Node-RED orchestration with semantic service descriptions and dynamic service composition. These frameworks enable complex workflows that integrate data acquisition, machine learning model execution, simulation, and visualization, supporting advanced learning factory projects where students design end-to-end CPS applications [11].

Low-cost IoT systems for motor monitoring demonstrate MING stack applicability to resource-constrained deployments. Using single-board computers, open-source software, and minimal infrastructure, these systems achieve acceptable monitoring capabilities at costs suitable for educational budgets. This approach validates MING stacks for learning factories with limited resources, demonstrating that effective CPS architectures need not require expensive commercial platforms [10].

---

## 11. Challenges and Open Research Problems

### 11.1 Standardization and Sustainable Design

The lack of comprehensive guidelines for constructing sustainable and evolvable CPS architectures represents a fundamental challenge for learning factory deployments. A systematic mapping study identified this gap, noting that existing CPS architectures often lack explicit design principles for long-term sustainability, adaptability to changing requirements, and graceful evolution as technologies mature [28].

For learning factories, sustainability encompasses multiple dimensions: technical sustainability (ability to integrate new technologies without wholesale replacement), pedagogical sustainability (ability to adapt to evolving curricula and learning objectives), economic sustainability (manageable costs for acquisition, operation, and maintenance), and organizational sustainability (ability to transfer knowledge and maintain systems across personnel changes). Current MING-based architectures address some of these dimensions through modularity and open-source components, but lack systematic frameworks for evaluating and ensuring long-term sustainability [28].

Standardization challenges extend to data models, communication protocols, and integration patterns. While MQTT provides a standard transport protocol, topic naming conventions, message schemas, and metadata structures remain largely ad hoc, complicating system integration and data sharing. Efforts toward standardized data models for renewable energy systems (e.g., IEC 61850 for power systems, SunSpec for solar inverters) have not been systematically integrated with MING architectures, creating friction when interfacing with standards-compliant equipment [12], [18], [28].

The multidimensional complexity of CPS—spanning physical processes, computational systems, communication networks, and human interactions—challenges traditional design methodologies. Learning factories require design approaches that explicitly address this complexity, providing structured methods for requirements analysis, architecture selection, component integration, and system evolution. Current practice relies heavily on ad hoc design and incremental refinement, lacking systematic frameworks that could accelerate deployment and improve outcomes [28].

### 11.2 Interoperability and Legacy Systems

Interoperability challenges arise from the heterogeneity of industrial protocols, data formats, and equipment interfaces in learning factory environments. Renewable energy equipment uses diverse protocols—OPC-UA for modern industrial automation, Modbus for power meters and inverters, CAN bus for battery management systems, proprietary protocols for specific equipment—creating integration complexity that must be managed at the edge or middleware layers [12], [18].

Node-RED's protocol adapter pattern provides a practical solution, but requires manual configuration for each device type and protocol variant. The lack of automated device discovery and self-configuration capabilities means that adding new equipment to learning factories requires technical expertise and time-consuming integration work. This overhead limits the pace of equipment updates and creates barriers for instructors who wish to incorporate new technologies into curricula [1], [6], [18].

Legacy equipment presents particular challenges, as older renewable energy systems may lack digital interfaces entirely or provide only proprietary, poorly documented protocols. Retrofitting legacy equipment with IoT capabilities—using external sensors, protocol converters, or reverse-engineered interfaces—adds cost and complexity. For learning factories that inherit equipment from previous installations or donations, legacy integration can consume significant resources [12], [18].

Semantic interoperability—ensuring that data from different sources has consistent meaning and can be correctly interpreted—remains an open problem. Even when syntactic integration succeeds (data flows through the system), semantic mismatches (different units, reference frames, or definitions) can lead to incorrect analysis or control actions. Ontologies and semantic frameworks have been proposed to address this challenge, but practical integration with MING architectures remains limited [11], [18].

### 11.3 Sensor Reliability and Data Quality

Sensor reliability and data quality challenges directly impact learning factory effectiveness, as unreliable data undermines both operational monitoring and pedagogical objectives. Sensors in renewable energy environments experience harsh conditions—temperature extremes, humidity, vibration, electromagnetic interference—that accelerate degradation and cause intermittent failures [10], [12], [21].

Sensor drift, where measurements gradually deviate from true values due to aging or environmental exposure, is particularly insidious because it may go undetected for extended periods. Calibration procedures can address drift, but require reference standards, trained personnel, and equipment downtime—resources that may be limited in educational settings. Automated drift detection using peer sensor comparison or model-based validation represents an active research area, with fog-level sensor ranking methods showing promise [21].

Data quality assurance in MING architectures typically relies on threshold-based validation (rejecting out-of-range values) and simple statistical checks (detecting sudden jumps or frozen values). More sophisticated approaches—using machine learning for anomaly detection, sensor fusion for cross-validation, or digital twin models for plausibility checking—have been demonstrated in research contexts but are not yet standard practice in learning factory deployments [12], [21].

The trade-off between sensor cost and reliability presents particular challenges for learning factories with limited budgets. Low-cost sensors enable dense instrumentation and hands-on student projects, but may exhibit poor accuracy, high drift rates, and short lifespans. Balancing cost constraints with data quality requirements requires careful sensor selection, redundancy strategies, and data quality monitoring—considerations that must be explicitly addressed in learning factory design [10], [21].

### 11.4 Scalability and Network Performance

Scalability challenges emerge as learning factories grow in size, sensor density, and data rates. While MING architectures have been demonstrated at moderate scales (hundreds of sensors, second-scale sampling), scaling to thousands of sensors or sub-second sampling rates requires careful attention to network capacity, broker performance, database write throughput, and query optimization [1], [2], [5].

MQTT broker scalability depends on message rates, payload sizes, and subscriber counts. High-frequency sensor data from large installations can overwhelm single-broker deployments, requiring hierarchical broker topologies or broker clustering. The MQTT2MULTICAST optimization for LoRaWAN demonstrates one approach to scalability, reducing latency and network traffic through UDP multicast, but such optimizations require specialized infrastructure and expertise [2].

InfluxDB write performance scales with batch size and hardware resources, but learning factories must balance write throughput with query performance and storage costs. High-frequency data from large sensor populations can generate terabytes of data per year, requiring careful retention policy design and potentially tiered storage (fast SSDs for recent data, slower HDDs for archives). Quantitative scalability limits—specific thresholds for sensor counts, sampling rates, and data retention—are not well documented in the literature, requiring empirical benchmarking for specific deployments [1], [5].

Network bandwidth and latency constraints affect system responsiveness and data completeness. Learning factories with distributed installations may rely on campus networks with variable performance, potentially experiencing congestion during peak usage periods. LPWAN technologies address wide-area coverage but impose strict data rate limits, requiring careful message design and sampling rate selection. Hybrid topologies that combine high-bandwidth local networks with LPWAN for remote sensors provide balanced solutions but add architectural complexity [2], [4], [10].

### 11.5 Digital Twin Consistency and Real-Time Constraints

Digital twin consistency challenges arise from the need to maintain accurate virtual representations of physical assets despite heterogeneous update rates, network delays, and computational latencies. Renewable energy systems exhibit dynamics across multiple time scales—sub-second power fluctuations, minute-scale cloud transients, hourly load patterns, seasonal generation variations—requiring digital twins that can represent both fast and slow phenomena [8], [9], [15].

High-bandwidth digital twins that update at sub-second rates can achieve high reconstruction accuracy but require substantial network and computational resources. Low-bandwidth digital twins reduce resource requirements but may miss transient events or fast dynamics. The trade-off between update frequency and resource consumption must be carefully managed, potentially using adaptive update strategies that increase frequency during dynamic periods and reduce it during steady-state operation [8].

Synchronization challenges arise when digital twins integrate data from multiple sensors with different sampling rates and network delays. Timestamp alignment, interpolation, and extrapolation techniques are necessary to construct consistent state estimates, but these techniques introduce modeling assumptions that may not hold during abnormal conditions. For learning factories, digital twin consistency affects both operational reliability and pedagogical value, as students must be able to trust that virtual representations accurately reflect physical reality [8], [9], [15].

Real-time constraints in learning factory CPS architectures depend on application requirements. Monitoring and visualization applications typically tolerate latencies of seconds, while closed-loop control applications may require sub-second response times. MING architectures can support both regimes, but real-time control requires careful system design: edge-based control loops to minimize network latency, deterministic communication protocols, and real-time operating systems for critical functions. The balance between centralized intelligence (easier to program and maintain) and distributed control (lower latency, higher reliability) remains an active design trade-off [9], [15], [24].

---

## 12. Best Practices for Designing Learning Factory CPS Architectures

### 12.1 Architectural Design Principles

**Adopt Layered Reference Architectures:** Begin design with a clear layered reference architecture (perception, network, middleware, application) and explicitly map MING components to layers. This mapping provides conceptual clarity, facilitates communication among stakeholders, and guides technology selection. Document the architecture using standard notations (e.g., UML, SysML) to support long-term maintenance and knowledge transfer [1], [12], [25].

**Embrace Modularity and Loose Coupling:** Design systems with modular components connected through well-defined interfaces (MQTT topics, REST APIs, database schemas). Loose coupling enables independent evolution of components, simplifies testing and debugging, and supports pedagogical objectives by making system structure transparent. Use MQTT's publish-subscribe model to decouple data producers from consumers, enabling flexible system reconfiguration [1], [3], [6].

**Plan for Evolution:** Recognize that learning factory requirements evolve as curricula change, new technologies emerge, and equipment is added or replaced. Design architectures that accommodate evolution through: standardized interfaces that enable component substitution, version-controlled configuration (Node-RED flows, Grafana dashboards, InfluxDB schemas), and documentation that captures design rationale and integration patterns [6], [11], [28].

**Balance Simplicity and Capability:** Learning factories must balance technical capability with pedagogical accessibility. Avoid unnecessary complexity that obscures system behavior or creates maintenance burdens, but provide sufficient capability to support meaningful experiments and prepare students for industrial practice. The MING stack's visual programming (Node-RED) and intuitive dashboards (Grafana) exemplify this balance [1], [6].

### 12.2 Deployment and Hosting Strategies

**Prefer On-Premises or Hybrid Hosting:** Deploy core MING components (MQTT broker, Node-RED, InfluxDB, Grafana) on-premises to ensure system availability during teaching sessions, reduce latency for real-time experiments, and address data sovereignty concerns. Use cloud resources selectively for computationally intensive analytics, long-term archival, or multi-site collaboration, but ensure that local operation continues when cloud connectivity is unavailable [1], [6], [8].

**Implement Hierarchical Topologies:** For distributed installations, use hierarchical topologies with edge gateways, fog nodes, and central infrastructure. Edge gateways perform protocol adaptation and local buffering, fog nodes provide intermediate aggregation and edge analytics, and central infrastructure hosts primary databases and dashboards. This hierarchy improves scalability, resilience, and performance [2], [6], [9], [10].

**Containerize Services:** Deploy MING components as containers (Docker, Kubernetes) to simplify installation, enable rapid deployment of experimental configurations, and support reproducibility. Containerization also facilitates version control of complete system configurations, enabling rollback to known-good states and sharing of reference implementations [2], [11].

**Provide Redundancy for Critical Functions:** Implement redundancy for critical components (MQTT brokers, databases) to ensure system availability during equipment failures. Use MQTT broker clustering or active-standby configurations, database replication, and redundant network paths. For learning factories, redundancy also provides teaching opportunities about reliability engineering and fault tolerance [12], [21].

### 12.3 Data Management and Quality Assurance

**Design Retention Policies Early:** Define InfluxDB retention policies during initial system design, considering pedagogical requirements (high-resolution data for active experiments), research needs (long-term archives for multi-year studies), and storage constraints. Implement multiple retention tiers with automatic downsampling to balance data resolution with storage costs [5], [7].

**Implement Sensor Validation:** Deploy sensor validation at edge or fog layers to detect and mitigate data quality issues. Use threshold checks for out-of-range values, statistical methods for anomaly detection, peer sensor comparison for drift detection, and digital twin models for plausibility checking. Log validation results to support troubleshooting and teach students about data quality [12], [21].

**Use Virtual Sensors for Redundancy:** Implement virtual sensors that derive measurements from multiple physical sensors or models, providing estimates when direct measurements are unavailable. Expose virtual sensors through MQTT topics, treating them as first-class data sources. Virtual sensors improve system reliability and provide teaching opportunities about sensor fusion and estimation [12].

**Document Data Models:** Maintain clear documentation of MQTT topic hierarchies, InfluxDB measurement schemas, and data semantics (units, reference frames, sampling rates). Use consistent naming conventions and metadata standards to facilitate data interpretation and system integration. For learning factories, documented data models support student projects and enable data sharing across courses [1], [5], [6].

### 12.4 Pedagogical Considerations

**Provide Modular Teaching Flows:** Develop libraries of reusable Node-RED flows for common tasks (sensor data acquisition, protocol adaptation, data conditioning, control logic) that students can import, study, and modify. Modular flows reduce setup time for experiments, provide working examples of best practices, and enable students to focus on learning objectives rather than low-level implementation details [6], [11].

**Design Role-Based Dashboards:** Create Grafana dashboards tailored to different user roles (instructors, students, maintenance personnel) and learning objectives. Instructor dashboards provide comprehensive system visibility, student dashboards focus on specific experiments, and analytical dashboards support data exploration and project work. Use Grafana's organization and permission features to manage access [1], [6], [7].

**Enable Hands-On Experimentation:** Provide students with access to Node-RED and Grafana development environments where they can create and test flows and dashboards without affecting production systems. Use separate InfluxDB databases or retention policies for student projects to isolate experimental data from operational monitoring [6], [7].

**Support Reproducibility:** Maintain version-controlled repositories of Node-RED flows, Grafana dashboards, and system configurations to enable reproducibility of experiments and sharing of teaching materials. Use export/import features to distribute reference implementations and enable students to replicate experiments on personal or cloud-based MING instances [6].

### 12.5 Performance Benchmarking and Instrumentation

**Benchmark Early and Continuously:** Measure system performance (MQTT message rates, InfluxDB write throughput, query latency, network bandwidth utilization) during initial deployment and continuously during operation. Use benchmarks to validate that performance meets requirements, identify bottlenecks, and inform capacity planning for system expansion [1], [5].

**Instrument the System:** Deploy monitoring for MING infrastructure itself (broker message rates, database disk usage, query performance, container resource utilization) to detect performance degradation and capacity issues. Use Grafana dashboards to visualize infrastructure metrics alongside application data, providing holistic system visibility [1], [5], [6].

**Document Performance Characteristics:** Record and document measured performance characteristics (maximum sensor counts, sustainable message rates, query response times) to inform future design decisions and provide realistic expectations for system capabilities. Share performance data with the learning factory community to build collective knowledge about MING stack scalability [1], [5].

**Plan for Growth:** Design systems with headroom for growth in sensor counts, data rates, and user populations. Overprovisioning infrastructure (network bandwidth, database storage, computational resources) by 50-100% provides buffer for unexpected growth and experimental flexibility. Monitor utilization trends to anticipate when capacity expansion is needed [1], [5].

---

## 13. Conclusion

This comprehensive survey has examined architectural frameworks for deploying Cyber-Physical Systems in renewable energy learning factories using the MING stack (MQTT, InfluxDB, Node-RED, Grafana). Drawing from 180 peer-reviewed publications and structured insights, we have systematically analyzed CPS layered architectures, the specific roles of MING components, data acquisition strategies, communication protocols, time-series data management, workflow orchestration, visualization techniques, existing framework benchmarks, persistent challenges, and evidence-based best practices.

The evidence demonstrates that MING-based architectures successfully implement the canonical four-layer CPS model in educational and industrial settings. MQTT provides lightweight, asynchronous publish-subscribe messaging suitable for heterogeneous sensor networks and resource-constrained devices. Node-RED enables visual flow-based programming for edge protocol adaptation, data transformation, and workflow orchestration, making complex system behavior accessible to students and researchers. InfluxDB delivers high-performance time-series data storage with flexible retention policies essential for managing continuous sensor streams from renewable energy systems. Grafana provides intuitive, real-time dashboards that support both operational monitoring and pedagogical demonstrations.

Practical deployments validate the MING stack's effectiveness for learning factory applications. On-premises implementations demonstrate vendor neutrality, local control, and measured performance characteristics suitable for educational environments. Digital twin architectures using MQTT pipelines and InfluxDB storage show high reconstruction accuracy and support both real-time monitoring and historical analysis. Integration patterns for industrial protocols (OPC-UA, Modbus, CAN) through Node-RED adapters enable incorporation of diverse renewable energy equipment.

However, significant challenges remain. Standardization gaps create friction in system integration and data sharing, with ad hoc topic naming conventions and message schemas complicating interoperability. Legacy equipment integration requires manual protocol adaptation and reverse engineering. Sensor reliability and data quality issues demand sophisticated validation and redundancy strategies. Scalability to large sensor networks and high data rates requires careful architectural design and performance optimization. Digital twin consistency and real-time constraints present ongoing research challenges, particularly for systems spanning multiple time scales.

The synthesized best practices provide actionable guidance for designing new learning factory CPS architectures. Key recommendations include: adopting explicit layered reference architectures with clear MING component mapping, preferring on-premises or hybrid hosting to ensure pedagogical reproducibility, implementing hierarchical topologies for distributed installations, designing retention policies early to balance data resolution with storage costs, deploying sensor validation at edge or fog layers, providing modular Node-RED flows for teaching, creating role-based Grafana dashboards, and conducting early and continuous performance benchmarking.

Looking forward, several research directions merit attention. Standardization efforts should develop reference data models, topic naming conventions, and integration patterns for MING-based renewable energy CPS. Automated device discovery and self-configuration capabilities would reduce integration overhead and accelerate equipment updates. Advanced sensor validation techniques using machine learning and digital twin models could improve data quality assurance. Scalability studies should establish quantitative limits for sensor counts, sampling rates, and data retention under various hardware configurations. Digital twin consistency mechanisms for heterogeneous update rates and network delays require further investigation.

The MING stack represents a mature, capable, and pedagogically appropriate foundation for renewable energy learning factory CPS architectures. Its open-source nature, modularity, and balance between simplicity and capability align well with educational requirements. As renewable energy technologies evolve and learning factories expand, MING-based architectures provide a flexible, evolvable platform for preparing students and advancing research in sustainable energy systems. This survey provides researchers, educators, and system architects with a comprehensive reference for designing, implementing, and evolving these critical educational infrastructures.

---

## 14. References

[1] Hensler et al., "On Premises IIoT Architecture for Capturing, Storing and Visualizing Production Data," *Proc. IEEE Int. Conf. Electr. Electron. Eng.*, 2023, doi: 10.1109/iceee59925.2023.00039.

[2] Navarro-Ortiz et al., "A LoRaWAN Network Architecture with MQTT2MULTICAST," *Electronics*, vol. 11, no. 6, 2022, doi: 10.3390/electronics11060872.

[3] Human et al., "Digital Twin Data Pipeline Using MQTT in SLADTA," *Lecture Notes in Computer Science*, pp. 91-105, 2020, doi: 10.1007/978-3-030-69373-2_7.

[4] Silva et al., "Development of a Supervisory System Using Open-Source for a Power Micro-Grid Composed of a Photovoltaic (PV) Plant Connected to a Battery Energy Storage System and Loads," *Energies*, vol. 15, no. 22, 2022, doi: 10.3390/en15228324.

[5] Kychkin et al., "Architecture of Compressor Equipment Monitoring and Control Cyber-Physical System Based on Influxdata Platform," *Proc. IEEE Int. Conf. Ind. Eng. Appl. Manuf.*, 2019, doi: 10.1109/ICIEAM.2019.8742963.

[6] Hensler et al., "On Premises IIoT Architecture for Capturing, Storing and Visualizing Production Data," *Proc. IEEE Int. Conf. Electr. Electron. Eng.*, 2023, doi: 10.1109/iceee59925.2023.00039.

[7] Kychkin et al., "Architecture of Compressor Equipment Monitoring and Control Cyber-Physical System Based on Influxdata Platform," *Proc. IEEE Int. Conf. Ind. Eng. Appl. Manuf.*, 2019, doi: 10.1109/ICIEAM.2019.8742963.

[8] Saad et al., "IoT-Based Digital Twin for Energy Cyber-Physical Systems: Design and Implementation," *Energies*, vol. 13, no. 18, 2020, doi: 10.3390/EN13184762.

[9] Caiza et al., "Digital Twin to Control and Monitor an Industrial Cyber-Physical Environment Supported by Augmented Reality," *Applied Sciences*, vol. 13, no. 13, 2023, doi: 10.3390/app13137503.

[10] Magadán et al., "Low-Cost Industrial IoT System for Wireless Monitoring of Electric Motors Condition," *Mobile Networks and Applications*, 2022, doi: 10.1007/s11036-022-02017-2.

[11] Steindl et al., "Semantic Microservice Framework for Digital Twins," *Applied Sciences*, vol. 11, no. 12, 2021, doi: 10.3390/APP11125633.

[12] Peniak et al., "The Redundant Virtual Sensors via Edge Computing," *Proc. Int. Conf. Appl. Electron.*, 2021, doi: 10.23919/AE51540.2021.9542888.

[13] Velasquez et al., "Monitoring and Data Processing Architecture using the FIWARE Platform for a Renewable Energy Systems," *Proc. IEEE Annu. Comput. Commun. Workshop Conf.*, 2021, doi: 10.1109/CCWC51732.2021.9376026.

[14] Gutierrez et al., "Toward a conceptual framework for designing sustainable cyber-physical system architectures: A systematic mapping study," 2024, doi: 10.60692/0g218-3rv46.

[15] Balogh et al., "Digital Twins in Industry 5.0: Challenges in Modeling and Communication," *Proc. IEEE/IFIP Netw. Oper. Manag. Symp.*, 2023, doi: 10.1109/NOMS56928.2023.10154424.

[16] Costa et al., "FOCUSeR: A Fog Online Context-Aware Up-to-Date Sensor Ranking Method," *Journal of Sensor and Actuator Networks*, vol. 11, no. 2, 2022, doi: 10.3390/jsan11020025.

[17] Bochie et al., "LabSensing: Um Sistema de Sensoriamento para Laboratórios Científicos com Computação Inteligente nas Bordas," *Anais Estendidos do Simpósio Brasileiro de Redes de Computadores e Sistemas Distribuídos*, 2019, doi: 10.5753/SBRC_ESTENDIDO.2019.7793.

[18] Massaad-Massade, "Industry 4.0 Machine-to-Machine Communication Protocols and Architectures on the Shop Floor," *Springer Tracts in Additive Manufacturing*, 2023, doi: 10.1007/978-3-031-33890-8_19.

[19] Bies, "Conversion of a Manufacturing Lab as a Learning Factory to Educate Factories of the Future Concept," *Lecture Notes in Networks and Systems*, 2023, doi: 10.1007/978-3-031-28839-5_92.

[20] Arifianto et al., "Sistem Pemantauan dan Kontrol Energi Listrik Menggunakan Platform Node-RED, Influxdb dan Grafana melalui Jaringan WiFi dan Lora," *Jurnal fokus elektroda*, vol. 7, no. 1, 2022, doi: 10.33772/jfe.v7i1.23440.

[21] Costa et al., "FOCUSeR: A Fog Online Context-Aware Up-to-Date Sensor Ranking Method," *Journal of Sensor and Actuator Networks*, vol. 11, no. 2, 2022, doi: 10.3390/jsan11020025.

[22] Martínez-Ruedas et al., "A Cyber–Physical System Based on Digital Twin and 3D SCADA for Real-Time Monitoring of Olive Oil Mills," *Technologies*, vol. 12, no. 5, 2024, doi: 10.3390/technologies12050060.

[23] Kawa et al., "Integration of Machine Learning Solutions in the Building Automation System," *Energies*, vol. 16, no. 11, 2023, doi: 10.3390/en16114504.

[24] Balogh et al., "Digital Twins in Industry 5.0: Challenges in Modeling and Communication," *Proc. IEEE/IFIP Netw. Oper. Manag. Symp.*, 2023, doi: 10.1109/NOMS56928.2023.10154424.

[25] Jiang, "An improved cyber-physical systems architecture for Industry 4.0 smart factories," *Advances in Mechanical Engineering*, vol. 10, no. 6, 2018, doi: 10.1177/1687814018784192.

[26] Dani et al., "AI-Powered Predictive Energy Monitoring System Using Open-Source Tools: A Smart Building Case Study with Node-RED and InfluxDB," *Proc. IEEE Int. Conf. Software Testing*, 2025, doi: 10.1109/softt67007.2025.11213094.

[27] Promwungkwa et al., "Evaluation of the Long-Term Utilization of the Internet of Things in a Batch-Type Ceramics Kiln," *International Journal of Science and Business*, vol. 21, 2023, doi: 10.58970/ijsb.2172.

[28] Gutierrez et al., "Toward a conceptual framework for designing sustainable cyber-physical system architectures: A systematic mapping study," 2024, doi: 10.60692/0g218-3rv46.

[29] Rao et al., "A cyber-physical system approach for photovoltaic array monitoring and control," *Proc. Int. Conf. Inf. Intell. Syst. Appl.*, 2017, doi: 10.1109/IISA.2017.8316458.

[30] Kaestner et al., "Design of an efficient Communication Architecture for Cyber-Physical Production Systems," *Proc. IEEE Conf. Autom. Sci. Eng.*, 2018, doi: 10.1109/COASE.2018.8560563.
