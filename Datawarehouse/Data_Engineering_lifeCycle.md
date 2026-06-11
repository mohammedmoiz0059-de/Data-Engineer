
<img width="400" height="200" alt="image" src="https://github.com/user-attachments/assets/11f97edf-6404-46bf-b866-35512269245b" />
### Source
##### A source system is the origin of data in the data engineering lifecycle. Examples include:
    transactional databases
    IoT devices
    message queues
    web/mobile applications
#### Data engineers consume data from these systems but usually do not own them. They must understand:
how data is generated
data frequency and velocity
data formats and schema
limitations and reliability of the source

Communication with source-system owners is critical because application or schema changes can break downstream pipelines and analytics.

#### Common Source Systems
    ####Traditional Source Systems
        Application servers connected to relational databases (RDBMS)
        Modern systems often use microservices with separate databases
    #### Modern Source Systems
        IoT sensor networks
        event streams
        distributed applications
        
Key Engineering Considerations

When evaluating a source system, data engineers should understand:

#### Data Characteristics
What type of source is it?
What data does it generate?
How fast is data produced?
Is data temporary or stored long term?
#### Data Quality
Are there nulls or formatting issues?
How often do errors occur?
Can duplicate data appear?
Can late-arriving data occur?
#### Schema Management
What is the schema structure?
How are schema changes handled?
Will downstream systems be notified about changes?
#### Data Access and Performance
How frequently should data be pulled?
Will querying the source impact application performance?
#### Stateful Data Handling
For databases:
Is data provided as snapshots?
Or through Change Data Capture (CDC) events?

### Schema Concepts
Schema defines the organization and structure of data.
Two common schema approaches:
#### Fixed Schema
Enforced by relational databases
Application writes must follow strict structure
Example:
SQL databases
#### Schemaless
Schema defined during writes
More flexible
Example:
MongoDB
JSON events
message queues
Schemaless does NOT mean “no schema”; it means schema enforcement happens at the application layer.

### Major Challenge — Schema Evolution
Schemas change over time due to Agile development and evolving applications.
Challenges for data engineers:
new columns added
field formats changed
missing fields
renamed attributes

Data engineers must transform evolving raw source data into stable, analytics-ready datasets.
