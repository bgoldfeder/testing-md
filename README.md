| Tribe Champion | API Call Name | Protocol | API Request                                | API Response                               | From Component | To Component | Implementation (does not exist, exists, steel) | 
|-----------|---------------|----------|--------------------------------------------|--------------------------------------------|----------------|--------------|---------------------------|
| 2 | Create Workspace | REST/rabbit | Submit workspace name and ViewPrint for subgraph creation over REST (POST) | Returns rabbit exchange info over REST.  Graph data then sent over Rabbit | UI/Wargaming (or any) | Glassworks | Exists |
| 2 | Collaborate (on) Workspace | REST/rabbit | Submit workspace to collaborate on over REST (POST) | Returns rabbit exchange info over REST.  Graph data then sent over Rabbit | UI/Wargaming (or any) | Glassworks | Exists |
| 2 | List Workspaces | REST | Submit request for list over REST (GET) | Returns list of workspaces over REST | UI/Wargaming (or any) | Glassworks | Exists |
| 2 | List Analytics | REST | Submit request for list over REST (GET) | Returns list of analytics (with name, parameters, types, default values) over REST | Planning/DSL/Ops (or any) | Glassworks | Partial |
| 2 | Run Analytic | REST/rabbit | Submit analytic name and parameters over REST (POST) | Returns analytic return values over REST.  Analytic may also (as a side-effect) annotate a graph/workspace, in which case those updates would be published over Rabbit | Planning/DSL/Ops (or any) | Glassworks | Exists |
| 2 | Run ViewPrint (i.e., extract one-time subgraph) | REST | Submit analytic name and parameters over REST (POST) | Returns graph in base64-encoded GraphML over REST | UI (but headed toward deprecation) | Glassworks | Exists, Slated for Deprecation |
| 2 | scan.* | Rabbit (topic) | Topic for publishing Shodan data to be ingested | n/a | gwm-ingest | Stream-catcher | Exists |
| 2 | bgp.* | Rabbit (topic) | Topic for publishing BGP routes to be ingested | n/a | gwm-ingest | Stream-catcher | Exists |
| 2 | traceroute.iplane | Rabbit (topic) | Topic for publishing iPlane traceroutes to be ingested | n/a | gwm-ingest | Stream-catcher | Exists |
| 2 | traceroute.caida | Rabbit (topic) | Topic for publishing CAIDA traceroutes to be ingested | n/a | gwm-ingest | Stream-catcher | Exists |
| 2 | graphedits | Rabbit (topic) | Topic for publishing GraphEdits to graph databases | n/a | Stream-catcher | Titan/BigData/Accumulo | Exists |
| 2 | changelog | Rabbit (topic) | Topic for publishing graph changes relevant to specific workspaces | n/a | Titan/BigData/Accumulo | Glassworks (workspaces) | Exists |
| 2 | archive | Flume | Publish history to archive and Solr | n/a | gwm-ingest | archive/Solr | Exists |
|  |  | REST/Q? | UI commands MSR to execute a mission |  | 7,8 |  | early prototype |
|  |  |  | Store annotations on existing GWM nodes/edges into GraphDB |  | 1,2,? |  | does not exist |
| 4 | Mission Specification API | AMQP | Client requests JSON Mission Specification, and descriptive paragraph (static for now) is returned. |  | 8 | Planning Server | In progress |
| 4 | Playbook API | AMQP | Client requests and receives JSON manifest of available Playbook plays. |  | 8 | Planning Server | In progress |
| 4 | Plan Editor API | AMQP | Client retrieves and saves complete block plans in Pinter-AST format from/to the Planning Server, and also handles requests for palettes of blocks available for inclusion in plan editor. |  | 8 | Planning Server | In progress |
| 4 | Mission Parametrization API | AMQP | Client retrieves JSON Mission Parametrization (MP), updates MP, and submits MP for execution. |  | 8 | Planning Server | In progress |
| 4 | Wargaming API | AMQP | Client requests a Wargaming analysis in JSON for a given MP, and receives streaming response. |  | 8 | Planning Server | In progress |
|  |  |  | Plan synthesis provides executable plan to MSR |  | 6,7 |  | does not exist |
| 5 | Obtain Score | REST call | Planning Server requests Wargaming analysis of a WG-targeted compilation of a plan. | Response is a plan score (JSON) | Planning Server | Wargaming | Stand up Sprint 2 |
| 5 | Obtain Wargaming view | REST call | Wargaming request to Glassworks for a view |  | Wargaming | Planning | Pending |
| 5 | Simulate Capabilities |  | Wargaming request to capabilities store |  | Wargaming | Capabilities | Does not exist |
| 7 | App Store | JSON-RPC (moving to AMQP) | Planning Server requests manifest of available capabilities for ultimate inclusion in client palettes. | App Store responds with list of capabilities, methodspecs, capability identifiers / URI's, etc... | Planning Server | App Store | Exists |
| 7 | Status Reporting | message stream over amqp | Executing mission script / MSR report status to the Operator UI | No response, just message streaming | Runtime | Operator Console UI | early prototype |
| 6 | Mission Plan to WG package compile | REST or command line call | UI client requests creation of wargaming package based on plan and parameter file input | Response is wargaming package ready for simulation (tar of several files) | Planning Server | 6 | on line |
| 6 | Mission Plan to Runtime package compile | REST or command line call | UI client requests creation of runtime package based on plan input | Response is runtime package ready for runtime use | Planning Server | 6 | on line |
