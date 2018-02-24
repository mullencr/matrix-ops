# matrix-ops
High Performance Computing: Multithreaded approach to blockwise matrix multiplication. Blocking was used to optimize use of caches.

***On cache usage:*** When processing data, CPU's will make use of caches, which read contiguous addresses in memory as blocks. When the CPU needs data, it will first look to see if that data is present in its caches, from the lowest to progressively higher levels. If the information cannot be found in any level of the cache, the next highest level of memory is searched (beyond level 3 caching, the CPU will read in data from RAM, completely replacing the current block of data). Reading from RAM in this way is much slower than reading from the cache, and adds the memory latency to the execution time for the script.

***On blocking:*** By assigning the independent threads (created using Open MP libraries) to process contiguous blocks of data, the number of cache-misses (and therefore lookups to the next highest level of memory, seen in cache-references) is reduced significantly, as the process doesn't have to jump around to random places in memory in order to retreive the next piece of data to be processed.

***The best demonstration of this can be found in [metrics/hw4_1000_perf.bash.e4032911](https://github.com/mullencr/matrix-ops/blob/master/metrics/hw4_1000_perf.bash.e4032911)*** Note the significantly increased cache-miss and cache-reference amount for the commands using a block size of 0 (no blocking, meaning dynamic assignment of thread processing). Next, note the significant reduction in runtime for each of the commands running a block size of 50. This shows the potential benefits when you effectively utlize the resources available to you in the computer's architecture (or the penalties if you fail to).
