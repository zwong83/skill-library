# Memcached Reference

Memcached is suited to simple, ephemeral key/value caching with a straightforward operational model. Treat entries as disposable: no durable source of truth, no general transactional workflow, and eviction or restart can remove data. Keep values bounded, choose TTL from freshness requirements, and protect the backing store from miss storms. Measure hit rate, evictions, memory, item size, connections, and latency.
