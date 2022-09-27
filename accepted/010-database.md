# SQLite for Auraed

This feature will accomplish **data persistency after reboots/restarts/failure** because **auraed is a systems daemon built for humans who often make mistakes**.

### Outcomes

  - Allow **persistent records** to exist after a daemon crash, failure.
  - Allow **persistent records** to exist atomicaly after a gRPC request return. 
      - There will be a deliberate coupling between the gRPC server and the data layer/model.
  - Allow **encryption at rest** which can be unlocked using the `/etc/aurae/pki/server.key` (or a cryptographic hash) server key for the database.
  - Allow **joining** and **connecting** records and schemas. For example we should have a collection of `VirtualMachine` records, which need to be mapped to `NIC` records.
  - Allow **for a single database file** which can easily be backed up, recovered, and snapshotted for disaster recovery.
  - Alow **embedding** the database directly into the `auraed` daemon such that another server/client relationship does not need to be maintained, or such that auraed will scheduele the database directly.

### Goals

 - All **auraed** daemons will ship with this **database**.
 - All **auraed** daemons will have an upgrae/migration strategy of the data **in scope** for the entire project
 - All **aurae project** components will adhere to a version number that is indicitive of the data stored in this database and semver.
 - It will be impossible to recover a system without a key.
 - It will be impossible to access or mutate data without a key.

### Decisions

 - The project will use **SQLite** to serve as the most fundamental **storage layer**.
 - The project will encrypt the **SQLite** database according to the requirements above.
 - The project will reject any classes of database on a system other than a single "TEST" database which is managed by the source code.
    - There will be no concept of "dev" or "prod" data.
 - The project will attempt to couple the API definitions to the database schema.
 - The project will attempt to decouple an ORM on top of the core database.
 - The project will use **[SeaQL sea-orm](https://github.com/SeaQL/sea-orm)** for the ORM layer.

### Notes

 - The ORM layer is a low oriority decision, that if implemented correctly should be relatively trivial to change. 
 - The SQLite decision is a higher stakes decision, which is still relatively low-risk as it can be moved to another SQL compatible backend in the future.
 - The schema will need to be maintained in API alongside the protobuf definitions. Ideally we can come up with a way of cleanly mapping these without risk.

### Authors

 - [@kris-nova](https://github.com/kris-nova)
