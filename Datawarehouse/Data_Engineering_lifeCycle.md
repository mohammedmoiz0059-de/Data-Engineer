## SOURCE
    A source system is where data originally comes from in a data engineering pipeline. Examples include:
    application databases
    IoT devices
    message queues
    mobile and web applications
  #### A data engineer should understand:
    Data Characteristics
            What kind of system is it?
            How much data does it generate?
            How fast is data generated?
             Is the data stored permanently or deleted quickly?
    Data Quality
        Are there missing values or formatting issues?
        Can duplicate records occur?
        Does late-arriving data happen?
        How frequently do errors occur?
    Schema Handling
        What does the data structure look like?
        How are schema changes communicated?
        Will downstream systems break if the schema changes?
    Performance Concerns
        Can reading data affect source-system performance?
        How often should data be pulled?
    Stateful Systems
        For databases:
            Is data shared as full snapshots?
            Or through Change Data Capture (CDC) events?
#### Understanding Schemas
    A schema defines how data is organized.
    There are two common approaches:
        Fixed Schema : Structure is enforced strictly
            Common in relational databases
            Example:
            SQL databases
        Schemaless : Schema is defined while writing data
            More flexible
            Examples:
                MongoDB
                JSON event streams
                 message queues

        “Schemaless” does not mean there is no schema. It simply means the application controls the structure instead of the database enforcing it.

#### Schema Evolution : Schemas change over time as applications evolve.
    Common changes include:
        new columns added
        renamed fields
        changed formats
        removed attributes
        This creates challenges for data engineers because pipelines and analytics must continue working even when source data changes.
