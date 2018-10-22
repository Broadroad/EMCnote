# GenericKeyedObjectPool
- public class GenericKeyedObjectPool<K,V>
- extends BaseKeyedObjectPool<K,V>
- implements KeyedObjectPool<K,V>
it is a configurable KeyedObjectPool implemention. GenericKeyedObjectPool provide borrowObject/returnObject function which users can simply use it to get/put object from/to pool
you can see [detail](http://commons.apache.org/proper/commons-pool/api-1.6/org/apache/commons/pool/impl/GenericKeyedObjectPool.html).

## maxActive
maxActive controls the maximum number of objects (per key) that can allocated by the pool (checked out to client threads, or idle in the pool) at one time. When non-positive, there is no limit to the number of objects per key. When maxActive is reached, the keyed pool is said to be exhausted. The default setting for this parameter is 8.

## maxTotal
maxTotal sets a global limit on the number of objects that can be in circulation (active or idle) within the combined set of pools. When non-positive, there is no limit to the total number of objects in circulation. When maxTotal is exceeded, all keyed pools are exhausted. When maxTotal is set to a positive value and borrowObject is invoked when at the limit with no idle instances available, an attempt is made to create room by clearing the oldest 15% of the elements from the keyed pools. The default setting for this parameter is -1 (no limit).

## maxIdle+
maxIdle controls the maximum number of objects that can sit idle in the pool (per key) at any time. When negative, there is no limit to the number of objects that may be idle per key. The default setting for this parameter is 8.

## whenExhaustedAction
whenExhaustedAction specifies the behavior of the borrowObject method when a keyed pool is exhausted:
- When whenExhaustedAction is WHEN_EXHAUSTED_FAIL, borrowObject will throw a NoSuchElementException
- When whenExhaustedAction is WHEN_EXHAUSTED_GROW, borrowObject will create a new object and return it (essentially making maxActive meaningless.)
- When whenExhaustedAction is WHEN_EXHAUSTED_BLOCK, borrowObject will block (invoke wait until a new or idle object is available. If a positive maxWait value is supplied, the borrowObject will block for at most that many milliseconds, after which a NoSuchElementException will be thrown. If maxWait is non-positive, the borrowObject method will block indefinitely.

The default whenExhaustedAction setting is WHEN_EXHAUSTED_BLOCK.
When testOnBorrow is set, the pool will attempt to validate each object before it is returned from the borrowObject method. (Using the provided factory's validateObject method.) Objects that fail to validate will be dropped from the pool, and a different object will be borrowed. The default setting for this parameter is false.
When testOnReturn is set, the pool will attempt to validate each object before it is returned to the pool in the returnObject method. (Using the provided factory's validateObject method.) Objects that fail to validate will be dropped from the pool. The default setting for this parameter is false.

## Optional
You can use this optional feature to return object to if the object is idle to ensure minimum number of idle object.
