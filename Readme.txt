Files modified and attached.

freelist.c
bufmgr.c


Here LRU is using only refcount variable and do not use usagecount which is used in clock sweep algorithm.

I have modified both functions StrategyGetBuffer and StrategyFreeBuffer in freelist.c file and in bufrmgr.c i have mofidied function UnpinBuffer here i am calling StrategyFreebuffer where ref count is 0 so that it gets added to LRU Queue.



In StrategyGetBuffer the buffer to evict is fetched from the freelist.

In Strategy Freebuffer, when the refcount reaches to 0, then it gets added to freelist at the tail. Then in the StrategyGetBuffer the buffer is fetched from the head of free list which is evicted in the least recently used manner.
