<!-- Autor: Daniel Benjamin Perez Morales -->
<!-- GitHub: https://github.com/DanielPerezMoralesDev13 -->
<!-- Correo electrónico: danielperezdev@proton.me -->

# **Docker Compose App**

- **La opción `--file` en `docker compose` es equivalente a `-f`. Ambas permiten especificar el archivo de configuración de Docker Compose que se desea usar.**

**Ejemplo:**

```bash
docker compose --file mongo-services.yaml up;
```

- **o Simplemente:**

```bash
docker compose -f mongo-services.yaml up;
```

```bash
docker compose -fmongo-services.yaml up;
```

*![Docker Compose Mongo Express Depends MongoDB](/Images/Docker%20Compose%20Container%20Mongo%20Express%20Depends%20MongoDB.png "/Images/Docker%20Compose%20Container%20Mongo%20Express%20Depends%20MongoDB.png")*

## ***Red `bridge` dedicada***

> [!NOTE]
> *Docker Compose crea una red de tipo `bridge` de manera predeterminada para los contenedores definidos. Esta red permite que los contenedores puedan comunicarse entre sí, pero cada contenedor tendrá una dirección IP aislada dentro de esta red.*

- **Ejecutamos**

```bash
docker compose -fmongo-services.yaml up;
```

```bash
WARN[0000] /home/d4nitrix13/Escritorio/Repository/Docker Compose/Demo With Docker Compose/mongo-services.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
[+] Running 2/0
 ✔ Container demowithdockercompose-mongo-demo-1     Created                                                                      0.0s
 ✔ Container demowithdockercompose-mongo-express-1  Created                                                                      0.0s
Attaching to mongo-demo-1, mongo-express-1
mongo-express-1  | Waiting for mongo-demo:27017...
mongo-express-1  | /docker-entrypoint.sh: connect: Connection refused
mongo-express-1  | /docker-entrypoint.sh: line 15: /dev/tcp/mongo-demo/27017: Connection refused
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:39.532+00:00"},"s":"I",  "c":"CONTROL",  "id":23285,   "ctx":"main","msg":"Automatically disabling TLS 1.0, to force-enable TLS 1.0 specify --sslDisabledProtocols 'none'"}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:39.533+00:00"},"s":"I",  "c":"CONTROL",  "id":5945603, "ctx":"main","msg":"Multi threading initialized"}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:39.534+00:00"},"s":"I",  "c":"NETWORK",  "id":4648601, "ctx":"main","msg":"Implicit TCP FastOpen unavailable. If TCP FastOpen is required, set at least one of the related parameters","attr":{"relatedParameters":["tcpFastOpenServer","tcpFastOpenClient","tcpFastOpenQueueSize"]}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:39.537+00:00"},"s":"I",  "c":"NETWORK",  "id":4915701, "ctx":"main","msg":"Initialized wire specification","attr":{"spec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":25},"incomingInternalClient":{"minWireVersion":0,"maxWireVersion":25},"outgoing":{"minWireVersion":6,"maxWireVersion":25},"isInternalClient":true}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:39.539+00:00"},"s":"I",  "c":"TENANT_M", "id":7091600, "ctx":"main","msg":"Starting TenantMigrationAccessBlockerRegistry"}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:39.539+00:00"},"s":"I",  "c":"CONTROL",  "id":4615611, "ctx":"initandlisten","msg":"MongoDB starting","attr":{"pid":1,"port":27017,"dbPath":"/data/db","architecture":"64-bit","host":"d73dbd65efc9"}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:39.539+00:00"},"s":"I",  "c":"CONTROL",  "id":23403,   "ctx":"initandlisten","msg":"Build Info","attr":{"buildInfo":{"version":"8.0.4","gitVersion":"bc35ab4305d9920d9d0491c1c9ef9b72383d31f9","openSSLVersion":"OpenSSL 3.0.13 30 Jan 2024","modules":[],"allocator":"tcmalloc-google","environment":{"distmod":"ubuntu2404","distarch":"x86_64","target_arch":"x86_64"}}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:39.539+00:00"},"s":"I",  "c":"CONTROL",  "id":51765,   "ctx":"initandlisten","msg":"Operating System","attr":{"os":{"name":"Ubuntu","version":"24.04"}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:39.539+00:00"},"s":"I",  "c":"CONTROL",  "id":21951,   "ctx":"initandlisten","msg":"Options set by command line","attr":{"options":{"net":{"bindIp":"*"},"security":{"authorization":"enabled"}}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:39.543+00:00"},"s":"I",  "c":"STORAGE",  "id":22270,   "ctx":"initandlisten","msg":"Storage engine to use detected by data files","attr":{"dbpath":"/data/db","storageEngine":"wiredTiger"}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:39.543+00:00"},"s":"I",  "c":"STORAGE",  "id":22297,   "ctx":"initandlisten","msg":"Using the XFS filesystem is strongly recommended with the WiredTiger storage engine. See http://dochub.mongodb.org/core/prodnotes-filesystem","tags":["startupWarnings"]}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:39.543+00:00"},"s":"I",  "c":"STORAGE",  "id":22315,   "ctx":"initandlisten","msg":"Opening WiredTiger","attr":{"config":"create,cache_size=3413M,session_max=33000,eviction=(threads_min=4,threads_max=4),config_base=false,statistics=(fast),log=(enabled=true,remove=true,path=journal,compressor=snappy),builtin_extension_config=(zstd=(compression_level=6)),file_manager=(close_idle_time=600,close_scan_interval=10,close_handle_minimum=2000),statistics_log=(wait=0),json_output=(error,message),verbose=[recovery_progress:1,checkpoint_progress:1,compact_progress:1,backup:0,checkpoint:0,compact:0,evict:0,history_store:0,recovery:0,rts:0,salvage:0,tiered:0,timestamp:0,transaction:0,verify:0,log:0],prefetch=(available=true,default=false),"}}
mongo-express-1  | Sun Jan 12 02:54:40 UTC 2025 retrying to connect to mongo-demo:27017 (2/10)
mongo-express-1  | /docker-entrypoint.sh: connect: Connection refused
mongo-express-1  | /docker-entrypoint.sh: line 15: /dev/tcp/mongo-demo/27017: Connection refused
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:40.563+00:00"},"s":"I",  "c":"WTRECOV",  "id":22430,   "ctx":"initandlisten","msg":"WiredTiger message","attr":{"message":{"ts_sec":1736650480,"ts_usec":563944,"thread":"1:0x776cca03a680","session_name":"txn-recover","category":"WT_VERB_RECOVERY_PROGRESS","category_id":34,"verbose_level":"DEBUG_1","verbose_level_id":1,"msg":"Recovering log 2 through 3"}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:40.656+00:00"},"s":"I",  "c":"WTRECOV",  "id":22430,   "ctx":"initandlisten","msg":"WiredTiger message","attr":{"message":{"ts_sec":1736650480,"ts_usec":656345,"thread":"1:0x776cca03a680","session_name":"txn-recover","category":"WT_VERB_RECOVERY_PROGRESS","category_id":34,"verbose_level":"DEBUG_1","verbose_level_id":1,"msg":"Recovering log 3 through 3"}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:40.793+00:00"},"s":"I",  "c":"WTRECOV",  "id":22430,   "ctx":"initandlisten","msg":"WiredTiger message","attr":{"message":{"ts_sec":1736650480,"ts_usec":793811,"thread":"1:0x776cca03a680","session_name":"txn-recover","category":"WT_VERB_RECOVERY_PROGRESS","category_id":34,"verbose_level":"DEBUG_1","verbose_level_id":1,"msg":"Main recovery loop: starting at 2/11776 to 3/256"}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:40.929+00:00"},"s":"I",  "c":"WTRECOV",  "id":22430,   "ctx":"initandlisten","msg":"WiredTiger message","attr":{"message":{"ts_sec":1736650480,"ts_usec":929465,"thread":"1:0x776cca03a680","session_name":"txn-recover","category":"WT_VERB_RECOVERY_PROGRESS","category_id":34,"verbose_level":"DEBUG_1","verbose_level_id":1,"msg":"Recovering log 2 through 3"}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.021+00:00"},"s":"I",  "c":"WTRECOV",  "id":22430,   "ctx":"initandlisten","msg":"WiredTiger message","attr":{"message":{"ts_sec":1736650481,"ts_usec":21805,"thread":"1:0x776cca03a680","session_name":"txn-recover","category":"WT_VERB_RECOVERY_PROGRESS","category_id":34,"verbose_level":"DEBUG_1","verbose_level_id":1,"msg":"Recovering log 3 through 3"}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.092+00:00"},"s":"I",  "c":"WTRECOV",  "id":22430,   "ctx":"initandlisten","msg":"WiredTiger message","attr":{"message":{"ts_sec":1736650481,"ts_usec":92583,"thread":"1:0x776cca03a680","session_name":"txn-recover","category":"WT_VERB_RECOVERY_PROGRESS","category_id":34,"verbose_level":"DEBUG_1","verbose_level_id":1,"msg":"recovery log replay has successfully finished and ran for 529 milliseconds"}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.092+00:00"},"s":"I",  "c":"WTRECOV",  "id":22430,   "ctx":"initandlisten","msg":"WiredTiger message","attr":{"message":{"ts_sec":1736650481,"ts_usec":92692,"thread":"1:0x776cca03a680","session_name":"txn-recover","category":"WT_VERB_RECOVERY_PROGRESS","category_id":34,"verbose_level":"DEBUG_1","verbose_level_id":1,"msg":"Set global recovery timestamp: (0, 0)"}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.092+00:00"},"s":"I",  "c":"WTRECOV",  "id":22430,   "ctx":"initandlisten","msg":"WiredTiger message","attr":{"message":{"ts_sec":1736650481,"ts_usec":92733,"thread":"1:0x776cca03a680","session_name":"txn-recover","category":"WT_VERB_RECOVERY_PROGRESS","category_id":34,"verbose_level":"DEBUG_1","verbose_level_id":1,"msg":"Set global oldest timestamp: (0, 0)"}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.094+00:00"},"s":"I",  "c":"WTRECOV",  "id":22430,   "ctx":"initandlisten","msg":"WiredTiger message","attr":{"message":{"ts_sec":1736650481,"ts_usec":94832,"thread":"1:0x776cca03a680","session_name":"txn-recover","category":"WT_VERB_RECOVERY_PROGRESS","category_id":34,"verbose_level":"DEBUG_1","verbose_level_id":1,"msg":"recovery rollback to stable has successfully finished and ran for 2 milliseconds"}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.103+00:00"},"s":"I",  "c":"WTCHKPT",  "id":22430,   "ctx":"initandlisten","msg":"WiredTiger message","attr":{"message":{"ts_sec":1736650481,"ts_usec":103942,"thread":"1:0x776cca03a680","session_name":"WT_SESSION.checkpoint","category":"WT_VERB_CHECKPOINT_PROGRESS","category_id":7,"verbose_level":"DEBUG_1","verbose_level_id":1,"msg":"saving checkpoint snapshot min: 1, snapshot max: 1 snapshot count: 0, oldest timestamp: (0, 0) , meta checkpoint timestamp: (0, 0) base write gen: 30"}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.110+00:00"},"s":"I",  "c":"WTRECOV",  "id":22430,   "ctx":"initandlisten","msg":"WiredTiger message","attr":{"message":{"ts_sec":1736650481,"ts_usec":110372,"thread":"1:0x776cca03a680","session_name":"txn-recover","category":"WT_VERB_RECOVERY_PROGRESS","category_id":34,"verbose_level":"DEBUG_1","verbose_level_id":1,"msg":"recovery checkpoint has successfully finished and ran for 14 milliseconds"}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.110+00:00"},"s":"I",  "c":"WTRECOV",  "id":22430,   "ctx":"initandlisten","msg":"WiredTiger message","attr":{"message":{"ts_sec":1736650481,"ts_usec":110474,"thread":"1:0x776cca03a680","session_name":"txn-recover","category":"WT_VERB_RECOVERY_PROGRESS","category_id":34,"verbose_level":"DEBUG_1","verbose_level_id":1,"msg":"recovery was completed successfully and took 546ms, including 529ms for the log replay, 2ms for the rollback to stable, and 14ms for the checkpoint."}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.117+00:00"},"s":"I",  "c":"STORAGE",  "id":4795906, "ctx":"initandlisten","msg":"WiredTiger opened","attr":{"durationMillis":1574}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.117+00:00"},"s":"I",  "c":"RECOVERY", "id":23987,   "ctx":"initandlisten","msg":"WiredTiger recoveryTimestamp","attr":{"recoveryTimestamp":{"$timestamp":{"t":0,"i":0}}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.128+00:00"},"s":"W",  "c":"CONTROL",  "id":9068900, "ctx":"initandlisten","msg":"For customers running the current memory allocator, we suggest changing the contents of the following sysfsFile","attr":{"allocator":"tcmalloc-google","sysfsFile":"/sys/kernel/mm/transparent_hugepage/enabled","currentValue":"never","desiredValue":"always"},"tags":["startupWarnings"]}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.128+00:00"},"s":"W",  "c":"CONTROL",  "id":9068900, "ctx":"initandlisten","msg":"For customers running the current memory allocator, we suggest changing the contents of the following sysfsFile","attr":{"allocator":"tcmalloc-google","sysfsFile":"/sys/kernel/mm/transparent_hugepage/defrag","currentValue":"madvise","desiredValue":"defer+madvise"},"tags":["startupWarnings"]}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.128+00:00"},"s":"W",  "c":"CONTROL",  "id":8640302, "ctx":"initandlisten","msg":"We suggest setting the contents of sysfsFile to 0.","attr":{"sysfsFile":"/sys/kernel/mm/transparent_hugepage/khugepaged/max_ptes_none","currentValue":511},"tags":["startupWarnings"]}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.128+00:00"},"s":"W",  "c":"CONTROL",  "id":8718500, "ctx":"initandlisten","msg":"Your system has glibc support for rseq built in, which is not yet supported by tcmalloc-google and has critical performance implications. Please set the environment variable GLIBC_TUNABLES=glibc.pthread.rseq=0","tags":["startupWarnings"]}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.128+00:00"},"s":"W",  "c":"NETWORK",  "id":5123300, "ctx":"initandlisten","msg":"vm.max_map_count is too low","attr":{"currentValue":1048576,"recommendedMinimum":1677720,"maxConns":838860},"tags":["startupWarnings"]}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.128+00:00"},"s":"W",  "c":"CONTROL",  "id":8386700, "ctx":"initandlisten","msg":"We suggest setting swappiness to 0 or 1, as swapping can cause performance problems.","attr":{"sysfsFile":"/proc/sys/vm/swappiness","currentValue":60},"tags":["startupWarnings"]}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.134+00:00"},"s":"I",  "c":"NETWORK",  "id":4915702, "ctx":"initandlisten","msg":"Updated wire specification","attr":{"oldSpec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":25},"incomingInternalClient":{"minWireVersion":0,"maxWireVersion":25},"outgoing":{"minWireVersion":6,"maxWireVersion":25},"isInternalClient":true},"newSpec":{"incomingExternalClient":{"minWireVersion":0,"maxWireVersion":25},"incomingInternalClient":{"minWireVersion":25,"maxWireVersion":25},"outgoing":{"minWireVersion":25,"maxWireVersion":25},"isInternalClient":true}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.134+00:00"},"s":"I",  "c":"REPL",     "id":5853300, "ctx":"initandlisten","msg":"current featureCompatibilityVersion value","attr":{"featureCompatibilityVersion":"8.0","context":"startup"}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.135+00:00"},"s":"I",  "c":"STORAGE",  "id":5071100, "ctx":"initandlisten","msg":"Clearing temp directory"}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.138+00:00"},"s":"I",  "c":"CONTROL",  "id":6608200, "ctx":"initandlisten","msg":"Initializing cluster server parameters from disk"}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.138+00:00"},"s":"I",  "c":"CONTROL",  "id":20536,   "ctx":"initandlisten","msg":"Flow Control is enabled on this deployment"}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.139+00:00"},"s":"I",  "c":"FTDC",     "id":20625,   "ctx":"initandlisten","msg":"Initializing full-time diagnostic data capture","attr":{"dataDirectory":"/data/db/diagnostic.data"}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.143+00:00"},"s":"I",  "c":"REPL",     "id":6015317, "ctx":"initandlisten","msg":"Setting new configuration state","attr":{"newState":"ConfigReplicationDisabled","oldState":"ConfigPreStart"}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.143+00:00"},"s":"I",  "c":"STORAGE",  "id":22262,   "ctx":"initandlisten","msg":"Timestamp monitor starting"}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.144+00:00"},"s":"I",  "c":"STORAGE",  "id":7333401, "ctx":"initandlisten","msg":"Starting the DiskSpaceMonitor"}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.148+00:00"},"s":"I",  "c":"NETWORK",  "id":23015,   "ctx":"listener","msg":"Listening on","attr":{"address":"/tmp/mongodb-27017.sock"}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.148+00:00"},"s":"I",  "c":"NETWORK",  "id":23015,   "ctx":"listener","msg":"Listening on","attr":{"address":"0.0.0.0:27017"}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.148+00:00"},"s":"I",  "c":"NETWORK",  "id":23016,   "ctx":"listener","msg":"Waiting for connections","attr":{"port":27017,"ssl":"off"}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.149+00:00"},"s":"I",  "c":"CONTROL",  "id":8423403, "ctx":"initandlisten","msg":"mongod startup complete","attr":{"Summary of time elapsed":{"Startup from clean shutdown?":true,"Statistics":{"Set up periodic runner":"0 ms","Set up online certificate status protocol manager":"0 ms","Transport layer setup":"1 ms","Run initial syncer crash recovery":"0 ms","Create storage engine lock file in the data directory":"0 ms","Get metadata describing storage engine":"0 ms","Validate options in metadata against current startup options":"0 ms","Create storage engine":"1576 ms","Write current PID to file":"0 ms","Initialize FCV before rebuilding indexes":"5 ms","Drop abandoned idents and get back indexes that need to be rebuilt or builds that need to be restarted":"0 ms","Rebuild indexes for collections":"0 ms","Load cluster parameters from disk for a standalone":"1 ms","Build user and roles graph":"0 ms","Verify indexes for admin.system.users collection":"0 ms","Set up the background thread pool responsible for waiting for opTimes to be majority committed":"0 ms","Start up the replication coordinator":"0 ms","Ensure the change stream collections on startup contain consistent data":"0 ms","Write startup options to the audit log":"0 ms","Start transport layer":"1 ms","_initAndListen total elapsed time":"1609 ms"}}}}
mongo-express-1  | Sun Jan 12 02:54:41 UTC 2025 retrying to connect to mongo-demo:27017 (3/10)
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.442+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"172.18.0.2:36398","uuid":{"uuid":{"$uuid":"5c53f688-babd-48cf-b2b0-2b48868bc6f2"}},"connectionId":1,"connectionCount":1}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:41.443+00:00"},"s":"I",  "c":"NETWORK",  "id":22944,   "ctx":"conn1","msg":"Connection ended","attr":{"remote":"172.18.0.2:36398","uuid":{"uuid":{"$uuid":"5c53f688-babd-48cf-b2b0-2b48868bc6f2"}},"connectionId":1,"connectionCount":0}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:42.010+00:00"},"s":"W",  "c":"CONTROL",  "id":636300,  "ctx":"ftdc","msg":"Use of deprecated server parameter name","attr":{"deprecatedName":"internalQueryCacheSize","canonicalName":"internalQueryCacheMaxEntriesPerCollection"}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:42.010+00:00"},"s":"W",  "c":"CONTROL",  "id":636300,  "ctx":"ftdc","msg":"Use of deprecated server parameter name","attr":{"deprecatedName":"oplogSamplingLogIntervalSeconds","canonicalName":"collectionSamplingLogIntervalSeconds"}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:42.010+00:00"},"s":"W",  "c":"NETWORK",  "id":23803,   "ctx":"ftdc","msg":"Use of deprecated server parameter 'sslMode', please use 'tlsMode' instead."}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:42.010+00:00"},"s":"W",  "c":"CONTROL",  "id":636300,  "ctx":"ftdc","msg":"Use of deprecated server parameter name","attr":{"deprecatedName":"wiredTigerConcurrentReadTransactions","canonicalName":"storageEngineConcurrentReadTransactions"}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:42.010+00:00"},"s":"W",  "c":"CONTROL",  "id":636300,  "ctx":"ftdc","msg":"Use of deprecated server parameter name","attr":{"deprecatedName":"wiredTigerConcurrentWriteTransactions","canonicalName":"storageEngineConcurrentWriteTransactions"}}
mongo-express-1  | No custom config.js found, loading config.default.js
mongo-express-1  | Welcome to mongo-express 1.0.2
mongo-express-1  | ------------------------
mongo-express-1  |
mongo-express-1  |
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:43.399+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"172.18.0.2:41040","uuid":{"uuid":{"$uuid":"82f50c6f-ee3a-4bad-903a-4afefd122c8a"}},"connectionId":2,"connectionCount":1}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:43.416+00:00"},"s":"I",  "c":"NETWORK",  "id":51800,   "ctx":"conn2","msg":"client metadata","attr":{"remote":"172.18.0.2:41040","client":"conn2","negotiatedCompressors":[],"doc":{"driver":{"name":"nodejs","version":"4.13.0"},"os":{"type":"Linux","name":"linux","architecture":"x64","version":"6.8.0-51-generic"},"platform":"Node.js v18.20.3, LE (unified)|Node.js v18.20.3, LE (unified)"}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:43.433+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"172.18.0.2:41044","uuid":{"uuid":{"$uuid":"cbe9e57e-d87d-4432-afc3-a35314e49f45"}},"connectionId":3,"connectionCount":2}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:43.438+00:00"},"s":"I",  "c":"NETWORK",  "id":51800,   "ctx":"conn3","msg":"client metadata","attr":{"remote":"172.18.0.2:41044","client":"conn3","negotiatedCompressors":[],"doc":{"driver":{"name":"nodejs","version":"4.13.0"},"os":{"type":"Linux","name":"linux","architecture":"x64","version":"6.8.0-51-generic"},"platform":"Node.js v18.20.3, LE (unified)|Node.js v18.20.3, LE (unified)"}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:43.441+00:00"},"s":"I",  "c":"ACCESS",   "id":6788604, "ctx":"conn3","msg":"Auth metrics report","attr":{"metric":"acquireUser","micros":0}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:43.472+00:00"},"s":"I",  "c":"ACCESS",   "id":5286306, "ctx":"conn3","msg":"Successfully authenticated","attr":{"client":"172.18.0.2:41044","isSpeculative":true,"isClusterMember":false,"mechanism":"SCRAM-SHA-256","user":"admin","db":"admin","result":0,"metrics":{"conversation_duration":{"micros":31027,"summary":{"0":{"step":1,"step_total":2,"duration_micros":104},"1":{"step":2,"step_total":2,"duration_micros":34}}}},"extraInfo":{}}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:43.477+00:00"},"s":"I",  "c":"NETWORK",  "id":6788700, "ctx":"conn3","msg":"Received first command on ingress connection since session start or auth handshake","attr":{"elapsedMillis":4}}
mongo-express-1  | Mongo Express server listening at http://0.0.0.0:8081
mongo-express-1  | Server is open to allow connections from anyone (0.0.0.0)
mongo-express-1  | basicAuth credentials are "admin:pass", it is recommended you change this in your config.js!
mongo-express-1  | GET / 200 111.257 ms - 9259
mongo-express-1  | GET /public/css/bootstrap.min.css 304 10.393 ms - -
mongo-express-1  | GET /public/css/bootstrap-theme.min.css 304 6.107 ms - -
mongo-express-1  | GET /public/css/style.css 304 1.285 ms - -
mongo-express-1  | GET /public/vendor-93f5fc3ae20e0dfd68cb.min.js 304 3.128 ms - -
mongo-express-1  | GET /public/index-56afe067afbbbde795be.min.js 304 2.789 ms - -
mongo-express-1  | GET /public/img/mongo-express-logo.png 304 0.974 ms - -
mongo-express-1  | GET /public/img/gears.gif 304 1.171 ms - -
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:53.932+00:00"},"s":"I",  "c":"NETWORK",  "id":22943,   "ctx":"listener","msg":"Connection accepted","attr":{"remote":"172.18.0.2:34088","uuid":{"uuid":{"$uuid":"16d314bc-dbb3-449d-a17c-faace1f0419e"}},"connectionId":4,"connectionCount":3}}
mongo-demo-1     | {"t":{"$date":"2025-01-12T02:54:53.934+00:00"},"s":"I",  "c":"NETWORK",  "id":51800,   "ctx":"conn4","msg":"client metadata","attr":{"remote":"172.18.0.2:34088","client":"conn4","negotiatedCompressors":[],"doc":{"driver":{"name":"nodejs","version":"4.13.0"},"os":{"type":"Linux","name":"linux","architecture":"x64","version":"6.8.0-51-generic"},"platform":"Node.js v18.20.3, LE (unified)|Node.js v18.20.3, LE (unified)"}}}


Watch →  watch is not yet configured. Learn more: https://docs.docker.com/compose/file-watch/
```

### **Problemas con los logs mezclados**

- **Si no se especifica un `container_name`, los logs de los contenedores se mezclarán, lo que puede dificultar el seguimiento y la depuración. Para evitarlo, se recomienda definir un `container_name` para cada contenedor, lo que facilita la identificación en los logs.**

### **Advertencia sobre la versión obsoleta**

**Advertencia en los logs:**

```bash
WARN[0000] /home/d4nitrix13/Escritorio/Repository/Docker Compose/Demo With Docker Compose/mongo-services.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
```

- *Para resolverla, se debe eliminar el atributo `version` del archivo `mongo-services.yaml`, ya que está **deprecated**.*

```yaml
# Autor: Daniel Benjamin Perez Morales
# GitHub: https://github.com/DanielPerezMoralesDev13
# Correo electrónico: danielperezdev@proton.me

services:
  mongo-demo:
    image: mongo:latest
    ports:
      - 27017:27017
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=supersecret
  mongo-express:
    image: mongo-express
    ports:
      - 8081:8081
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
      - ME_CONFIG_MONGODB_ADMINPASSWORD=supersecret
      - ME_CONFIG_MONGODB_SERVER=mongo-demo
      - ME_CONFIG_MONGODB_URL=mongodb://admin:supersecret@mongo-demo:27017/
      - ME_CONFIG_MONGODB_ENABLE_ADMIN=true
      - ME_CONFIG_OPTIONS_EDITORTHEME=material-darker
      - ME_CONFIG_REQUEST_SIZE=100kb
      - ME_CONFIG_SITE_BASEURL=/
      - ME_CONFIG_SITE_COOKIESECRET=cookiesecret
      - ME_CONFIG_SITE_SESSIONSECRET=sessionsecret
      - ME_CONFIG_SITE_SSL_ENABLED=false
      - ME_CONFIG_MONGODB_AUTH_USERNAME=admin
      - ME_CONFIG_MONGODB_AUTH_PASSWORD=pass
      - ME_CONFIG_MONGODB_PORT=27017
```

- *[Logs Mongo Services Version 2 Docker Compose](/Demo%20With%20Docker%20Compose/Version%202%20Mongo%20Services/Logs%20Mongo%20Services%20Version%202%20Docker%20Compose.md "/Demo%20With%20Docker%20Compose/Version%202%20Mongo%20Services/Logs%20Mongo%20Services%20Version%202%20Docker%20Compose.md")*

### **Error de conexión entre contenedores**

- **En los logs de `mongo-express`, vemos un error de conexión con el contenedor `mongo-demo`:**

```bash
mongo-express-1  | Waiting for mongo-demo:27017...
mongo-express-1  | /docker-entrypoint.sh: connect: Connection refused
mongo-express-1  | /docker-entrypoint.sh: line 15: /dev/tcp/mongo-demo/27017: Connection refused
```

- **Este error suele ocurrir cuando el contenedor de MongoDB (`mongo-demo`) no está disponible o no está completamente iniciado antes de que `mongo-express` intente conectarse.**

### **Solución para el error de conexión**

**Es posible que el contenedor `mongo-demo` aún esté iniciando cuando `mongo-express` intenta conectarse. Una forma de resolverlo es asegurarse de que `mongo-express` espere hasta que `mongo-demo` esté completamente listo. Esto puede lograrse mediante la configuración de dependencias en el archivo `docker-compose.yml` usando `depends_on` o configurando un retraso en el inicio de `mongo-express`.**

```yaml
# Autor: Daniel Benjamin Perez Morales
# GitHub: https://github.com/DanielPerezMoralesDev13
# Correo electrónico: danielperezdev@proton.me

services:
  mongo-demo:
    image: mongo:latest
    ports:
      - 27017:27017
    environment:
      - MONGO_INITDB_ROOT_USERNAME=admin
      - MONGO_INITDB_ROOT_PASSWORD=supersecret
  mongo-express:
    depends_on:
      - mongo-demo
    image: mongo-express
    ports:
      - 8081:8081
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=admin
      - ME_CONFIG_MONGODB_ADMINPASSWORD=supersecret
      - ME_CONFIG_MONGODB_SERVER=mongo-demo
      - ME_CONFIG_MONGODB_URL=mongodb://admin:supersecret@mongo-demo:27017/
      - ME_CONFIG_MONGODB_ENABLE_ADMIN=true
      - ME_CONFIG_OPTIONS_EDITORTHEME=material-darker
      - ME_CONFIG_REQUEST_SIZE=100kb
      - ME_CONFIG_SITE_BASEURL=/
      - ME_CONFIG_SITE_COOKIESECRET=cookiesecret
      - ME_CONFIG_SITE_SESSIONSECRET=sessionsecret
      - ME_CONFIG_SITE_SSL_ENABLED=false
      - ME_CONFIG_MONGODB_AUTH_USERNAME=admin
      - ME_CONFIG_MONGODB_AUTH_PASSWORD=pass
      - ME_CONFIG_MONGODB_PORT=27017
```

*[Logs Mongo Services Version 3 Docker Compose](/Demo%20With%20Docker%20Compose/Version%203%20Mongo%20Services/Logs%20Mongo%20Services%20Version%203%20Docker%20Compose.md "/Demo%20With%20Docker%20Compose/Version%203%20Mongo%20Services/Logs%20Mongo%20Services%20Version%203%20Docker%20Compose.md")*

## **Comando para listar redes Docker personalizadas**

- **Para listar las redes de Docker creadas por `docker-compose` o personalizadas, utiliza el siguiente comando:**

```bash
docker network ls -f type=custom -f scope=local -f driver=bridge
```

```bash
docker network ls -ftype=custom -fscope=local -fdriver=bridge
```

```bash
docker network ls --filter type=custom --filter scope=local --filter driver=bridge
```

### **Salida esperada**

```bash
NETWORK ID     NAME                            DRIVER    SCOPE
8140ecfbde0e   demowithdockercompose_default   bridge    local
```

- **Este comando filtra las redes de tipo **custom**, con **scope local** y utilizando el **driver bridge**. El nombre de la red es generado por `docker-compose` y normalmente tiene el formato `<nombre_del_directorio>_default`.**

---

## **Comando para listar contenedores filtrados por diversos criterios**

- **Si deseas listar los contenedores que están corriendo en la red definida por `docker-compose`, y que están expuestos a ciertos puertos, puedes usar un comando como el siguiente:**

```bash
docker container ps --filter status=running --filter publish=27017 --filter expose=27017 --filter ancestor=mongo --filter publish=8081 --filter expose=8081 --filter ancestor=mongo-express --filter network=$(docker network ls --filter type=custom --filter scope=local --filter driver=bridge --quiet)
```

```bash
docker container ls --filter status=running --filter publish=27017 --filter expose=27017 --filter ancestor=mongo --filter publish=8081 --filter expose=8081 --filter ancestor=mongo-express --filter network=$(docker network ls --filter type=custom --filter scope=local --filter driver=bridge --quiet)
```

```bash
docker container list --filter status=running --filter publish=27017 --filter expose=27017 --filter ancestor=mongo --filter publish=8081 --filter expose=8081 --filter ancestor=mongo-express --filter network=$(docker network ls --filter type=custom --filter scope=local --filter driver=bridge --quiet)
```

```bash
docker ps -f status=running -f publish=27017 -f expose=27017 -f ancestor=mongo -f publish=8081 -f expose=8081 -f ancestor=mongo-express -f network=$(docker network ls -f type=custom -f scope=local -f driver=bridge -q)
```

```bash
docker ps -fstatus=running -fpublish=27017 -fexpose=27017 -fancestor=mongo -fpublish=8081 -fexpose=8081 -fancestor=mongo-express -fnetwork=$(docker network ls -qftype=custom -fscope=local -fdriver=bridge)
```

```bash
docker ps --filter status=running \
    --filter publish=27017 \
    --filter expose=27017 \
    --filter ancestor=mongo \
    --filter publish=8081 \
    --filter expose=8081 \
    --filter ancestor=mongo-express \
    --filter network=$(docker network ls --filter type=custom --filter scope=local --filter driver=bridge --quiet)
```

### ***Descripción de filtros utilizados:***

- **`status=running`:** *Filtra los contenedores que están actualmente en ejecución.*
- **`publish=27017`:** *Filtra los contenedores que tienen el puerto 27017 expuesto al host.*
- **`expose=27017`:** *Filtra los contenedores que exponen el puerto 27017 dentro de la red de Docker.*
- **`ancestor=mongo`:** *Filtra los contenedores que utilizan la imagen `mongo` como base.*
- **`publish=8081`:** *Filtra los contenedores que tienen el puerto 8081 expuesto al host.*
- **`expose=8081`:** *Filtra los contenedores que exponen el puerto 8081 dentro de la red de Docker.*
- **`ancestor=mongo-express`:** *Filtra los contenedores que utilizan la imagen `mongo-express` como base.*
- **`network=<name_network>`:** *Filtra los contenedores que están conectados a la red Docker especificada por su ID o nombre.*

### **Salida esperada:**

```bash
CONTAINER ID   IMAGE           COMMAND                  CREATED          STATUS          PORTS                                           NAMES
d73dbd65efc9   mongo:latest    "docker-entrypoint.s…"   22 minutes ago   Up 16 minutes   0.0.0.0:27017->27017/tcp, :::27017->27017/tcp   demowithdockercompose-mongo-demo-1
a0ea5cd9c7c1   mongo-express   "/sbin/tini -- /dock…"   22 minutes ago   Up 16 minutes   0.0.0.0:8081->8081/tcp, :::8081->8081/tcp       demowithdockercompose-mongo-express-1
```

---

### ***Explicación de la salida:***

- **`CONTAINER ID`:** *El identificador único del contenedor.*
- **`IMAGE`:** *La imagen de Docker que está siendo utilizada por el contenedor.*
- **`COMMAND`:** *El comando que está siendo ejecutado dentro del contenedor.*
- **`CREATED`:** *El tiempo desde que el contenedor fue creado.*
- **`STATUS`:** *El estado actual del contenedor.*
- **`PORTS`:** *Los puertos que están siendo mapeados entre el contenedor y el host.*
- **`NAMES`:** *El nombre del contenedor, generado por `docker-compose` según el formato `<name_network>-<name_service>-<número>`.*

> [!IMPORTANT]
> *Cuando usamos **Docker Compose** para ejecutar servicios, al presionar `Ctrl + C` en la terminal, estamos enviando una señal **SIGINT** (interrupción) al proceso principal del contenedor. Esto detiene los servicios de manera ordenada.*

```bash
[+] Stopping 2/2
 ✔ Container version1mongoservices-mongo-express-1  Stopped                                                                      0.2s
 ✔ Container version1mongoservices-mongo-demo-1     Stopped                                                                      0.3s
```

### *¿Qué es **SIGINT**?*

- **SIGINT** *(Signal Interrupt) es una señal enviada al proceso principal de una aplicación cuando el usuario solicita la interrupción de su ejecución. En este caso, `Ctrl + C` actúa como un atajo para enviar esta señal desde la terminal.*
- *Es una forma amigable de pedir al proceso que se detenga, lo que permite que los servicios realicen tareas de limpieza antes de terminar, como cerrar conexiones o liberar recursos.*

### *¿Qué hace Docker Compose al recibir **SIGINT**?*

1. **Propaga la señal:** *Docker Compose envía la señal **SIGINT** al proceso principal de cada contenedor administrado.*
2. **Finalización ordenada:**
   - *Los contenedores ejecutan sus **scripts de parada** definidos (si existen) o finalizan los procesos activos de manera limpia.*
   - *Docker espera un tiempo de gracia (por defecto 10 segundos) antes de forzar la detención con una señal más fuerte (**SIGKILL**) si el proceso no responde.*
3. **Registra la salida:** *La terminal muestra información sobre los contenedores detenidos.*

### ***Diferencias con otras señales***

- **SIGTERM:** *Similar a **SIGINT**, se usa al ejecutar `docker-compose down` o detener contenedores individualmente con `docker stop`. También permite una finalización ordenada.*
- **SIGKILL:** *Esta señal no permite la limpieza. Mata el proceso inmediatamente. Se usa como último recurso.*

### ***Resumen***

- **`Ctrl + C` envía SIGINT:** *Detiene los contenedores de forma controlada.*
- **Proceso principal de cada contenedor:** *Debe gestionar la señal para liberar recursos correctamente.*
- *Es el método recomendado cuando estás trabajando en desarrollo o necesitas detener servicios temporalmente.*

- *Si necesitas apagar todo el stack de manera más completa (incluyendo eliminación de redes y volúmenes), usa el comando `docker-compose down`.*

### **Problema: MongoDB no está listo cuando mongo-express intenta conectarse `depends_on`**

*[Foro Depends On](https://stackoverflow.com/questions/71060072/docker-compose-depends-on-with-condition-invalid-type-should-be-an-array "https://stackoverflow.com/questions/71060072/docker-compose-depends-on-with-condition-invalid-type-should-be-an-array")*

- *Mongo-express podría estar intentando conectarse a MongoDB antes de que el servicio `mongo-demo` esté completamente disponible. Aunque hayas configurado la dependencia en el archivo YAML con `depends_on`, esto solo garantiza que Docker intente iniciar el contenedor `mongo-demo` antes de `mongo-express`, pero **no espera a que MongoDB esté realmente listo para aceptar conexiones**.*

- **Docker Compose asegura que el contenedor de `mongo-demo` inicie primero, pero no verifica si MongoDB está en funcionamiento o si está completamente listo para aceptar conexiones. Esto puede llevar a que `mongo-express` falle al intentar conectarse, ya que MongoDB aún no está escuchando en el puerto.**

### ***Solución: Mecanismo de espera en `mongo-express`***

*[Logs Mongo Services Version 3](/Demo%20With%20Docker%20Compose/Version%203%20Mongo%20Services/Logs%20Mongo%20Services%20Version%203%20Docker%20Compose.md "/Demo%20With%20Docker%20Compose/Version%203%20Mongo%20Services/Logs%20Mongo%20Services%20Version%203%20Docker%20Compose.md")*

- *Para asegurarte de que MongoDB esté completamente disponible antes de que `mongo-express` intente conectarse, puedes agregar un **mecanismo de espera**. Esto se puede lograr de varias maneras:*

1. **Usar `nc` para esperar a que MongoDB esté listo**:

   - **Puedes añadir un bucle `until` en el `entrypoint` de `mongo-express` para verificar continuamente si el puerto de MongoDB (`27017`) está abierto y accesible.**

   **Ejemplo de configuración en exec form:**

   ```yaml
   entrypoint:
     - /bin/sh
     - -c
     - |
       until nc -zv mongo-demo 27017; do
         echo "Waiting For Mongo";
         sleep 1;
       done;
       exec /sbin/tini -- /docker-entrypoint.sh
   ```

   - *En este caso, el contenedor `mongo-express` esperará hasta que el puerto `27017` en el servicio `mongo-demo` esté accesible, lo que indica que MongoDB está listo. Una vez que se establezca la conexión, se ejecutará el comando principal del contenedor (`/docker-entrypoint.sh`).*

2. **Alternativas:** *También puedes usar herramientas como **wait-for-it** o **dockerize**, que están diseñadas específicamente para este tipo de casos. Estas herramientas permiten que un contenedor espere a que otro servicio esté disponible antes de continuar con su ejecución.*

> [!TIP]
> *El símbolo **`|`** en un archivo YAML (y en general en muchos lenguajes y configuraciones) se utiliza para indicar que el valor de una clave será un **bloque de texto multilínea**. Cuando se usa en YAML, permite escribir texto que se extiende a varias líneas y se conserva la indentación en el resultado final.*

### **¿Cómo funciona?**

- **Cuando se usa `|` en YAML, el contenido que sigue en las líneas posteriores se considera parte de un bloque de texto y las nuevas líneas se preservan tal como están, incluyendo saltos de línea. La principal diferencia entre `|` y otros símbolos es que `|` **mantiene los saltos de línea**, mientras que el símbolo `>` (usado en lugar de `|`) **combina las líneas en una sola línea**.**

### **Ejemplo con `|`:**

```yaml
entrypoint:
  - /bin/sh
  - -c
  - |
    until nc -zv mongo-demo 27017; do
      echo "Waiting For Mongo";
      sleep 1;
    done;
    exec /sbin/tini -- /docker-entrypoint.sh
```

- **Aquí, el contenido después de `|` se interpreta como un bloque de texto, y las líneas de código en el `entrypoint` se mantienen con saltos de línea y formato original.**

- **¿Qué ocurre con las nuevas líneas?**

- **En el ejemplo anterior, el texto tiene saltos de línea donde corresponde:**

- *Las líneas dentro del bloque `|` se conservan con saltos de línea, por lo que el comando `until nc -zv mongo-demo 27017` y el comando `exec /sbin/tini -- /docker-entrypoint.sh` aparecerán en líneas separadas en el contenedor.*
  
**Resumen:**

- **`|`** *conserva los saltos de línea y mantiene la indentación tal cual.*
- *Se usa para declarar bloques de texto donde se necesita preservar la estructura de las líneas (por ejemplo, en comandos complejos o scripts).*

- *Si usaras `>` en lugar de `|`, las líneas se concatenarían y el resultado final sería una sola línea.*
