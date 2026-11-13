# Database selection

Start with system requirements, not a preferred product. Capture data model, access patterns, read/write and batch/streaming workload, estimated records and storage, reads/writes per second, peak traffic, concurrent connections, growth, consistency, transaction guarantees, latency, durability, availability, RPO/RTO, operational capability, cost, and ecosystem fit.

Evaluate relational, document, key-value, wide-column, graph, time-series, search, and analytical systems only when their data model and workload justify consideration. For each serious candidate compare data model fit, transactions, consistency, scale, performance, availability, ecosystem, operations, total cost, and team expertise. Make assumptions visible and state trade-offs, risks, alternatives, migration implications, and operational requirements.

If an existing production database works, do not recommend migration merely because another product is theoretically stronger. Require a concrete business, performance, scalability, reliability, operational, or cost limitation, and account for migration risk.
