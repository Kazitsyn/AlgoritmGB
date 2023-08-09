```Java
    class HashMapIterator implements Iterator<Entity>{
    private int bucketIndex = 0;
    private int nodeIndex = 0;
    private Bucket.Node nodeCurrent;
    private Entity entity;

    @Override
    public boolean hasNext() {
        for (int i = bucketIndex; i < buckets.length; i++){
            Bucket<K, V> bucket = buckets[i];
            if(bucket != null){
                Bucket.Node node = bucket.head;
                int index = 0;
                while (node != null){
                    if (index < nodeIndex){
                        index++;
                        node = node.next;
                        continue;
                    }
                    nodeCurrent = node;
                    return true;
                }
                nodeIndex = 0;
            }
            bucketIndex++;
        }
        return false;
    }

    @Override
    public Entity next() {
        entity = new Entity();
        entity.key = (K)nodeCurrent.value.key;
        entity.value = (V)nodeCurrent.value.value;
        nodeIndex++;
        return entity;
    }
}
```