#                 Parallel R (12.IX.2015)

Outline
-------

  0. Motivation and Overview.
  1. Snow
  2. Multicore
  3. Parallel

  4. More: R+Hadoop, RHIPE, Segue, doRedis, RevoConnectR, cloudNumbers.com
  5. Final comparison and conclusion

0. Motivation
-------------

  1. R is great -- many reasons (link to Alex Shlemov) and even speed can be corrected.
  2. R has limitations: single-threaded, memory bound. Solution -- parallel programming: first problem -- multiple CPUs, second -- multiple machines. 
  3. Overview: snow, multicore, parallel -- page 4.

1. snow [main word is cluster]
------------------------------
  
  1. Geneal usecase: you want to use a Linux Cluster (works on Linux, Mac OS X, Windows). Page 7.
     __Examples__: Monte Carlo simulation, bootstrapping, cross validation, ensemble machine learning algorithms. Page 7-8.
  2. Features: good support of parallel random number generation. Page 8.
               Different transport mechanisms between Master and Slaves. But you have to install additional packages for it. For socket you dont. Page 8.
               Input arguments should fit into memory. it is possible to arrange high-performance distributed file systems -- up to user to arrange. Page 8.  
  3. Structure of the library (??snow):
    * Low-level (cluster-level) functions: cluster* --- clusterApply, clusterApplyLB, clusterEvalQ, clusterCall, clusterSplit, etc.
    * High-level: par[L,S,A,R,C]apply --- Parallel versions of apply and related functions.
    * Start and Stop clusters: makeCluster, stopCluster.
    * Uniform RNG: L Ecuyer (pack: rlecuyer), SPRNG (pack: rsprng).
    * Timing. snow.time(expr). -- very useful.

  4. Creating Clusters: page 9-10.
  5. Initialize Clusters: ClusterEvalQ, ClusterCall + ClusterApply.
  6. __Example__: parallel K-means.
  7. Load Balance: clusterApplyLB vs clusterApply.
  8. High-level: ParApply (vs clusterApply).
  9. Main example: Random Number Generation.
  10. Maybe clusterSplit.

2. multicore [not maintained] [main word is fork]
-------------------------------------------------

  1. General usecase: R script on one machine (no Windows support (fork), no RNG support, but easier to use than snow). Restriction: do not use with R GUI.
  2. Highlevel function: mclapply() (with mc.cores). K-means example.
  3. No Load Balancing -- can be imitated (Page 42).
  4. pvec() -- similar to parVapply() in snow. parallel and collect.
  5. Problems with RNG. (page 46).
  6. (out of scope) There is also some low-level-api (page 47).

3. parallel [mainstream] [somewhat merge of snow and multicore]
---------------------------------------------------------------

  1. Built-in R since 2.14.0 (if you need MPI transport --- install rmpi), almost nothing to learn if you understand snow and multicore. internal RNG support.
  2. General usecases: anything above.
  3. It is possible to use on Posix-systems mclapply() from multicore. Also easy to use clusters (for instance, socket) -- parLapply() and clusterApplyLB() on multicore Windows and Linux clusters (page 52).
  4. detectCores(). (page 53). K-means on Posix-systems and on Windows.
  5. Creating clusters. Two transports: "PSOCK" and "FORK". (page 54).
  6. Parallel RNG: mc.reset.stream(). Page 55-7.
  7. Differences from multicore and snow. Page 57-58. 

4. Out of scope. MapReduce
--------------------------

  1. RHIPE, Segue, doRedis, RHadoop, cloudNumbers.com

5. Links
--------

  1. Parallel R
  2. Documentation of Parallel package.
  3. ??
