# lab4
# HashTable
# hash
The provided function hash() accepts a key of type K and calculates the hash value for that key. It achieves this by utilizing the hashCode() method of the key object. The resulting hash code is then combined with the size of the hash table (M) using the modulo operation. This calculation determines the index in the hash table where the corresponding key-value pair will be stored.
```
   private int hash(K key) {
        return key.hashCode() % M;
    }
```
# put
Is used for inserting a key-value pair into a hash table. It begins by calculating the index for the key using a hash function. If the chain at that index is empty (null), it creates a new LinkedList to store multiple key-value pairs. Next, it iterates over the chain to check if the given key already exists. If the key is found, it updates the corresponding value. However, if the key is not found in the chain, it adds a new HashNode containing the provided key and value to the chain.
```
 public void put(K key, V value) {
        int index = hash(key);
        if (chain[index] == null) {
            chain[index] = new LinkedList<HashNode<K, V>>();
        }
        for (HashNode<K, V> node : chain[index]) {
            if (node.getKey().equals(key)) {
                node.setValue(value);
                return;
            }
        }
        chain[index].add(new HashNode<K, V>(key, value));
        size++;
    }
```
# get
Is used to retrieve the value associated with a given key from a hash table. It starts by calculating the index for the key using a hash function. Then, it iterates over the chain at that index to search for a matching key. If a match is found, the corresponding value is returned. If no match is found, it returns null to indicate that the key was not found in the hash table.
```
  public V get(K key) {
        int index = hash(key);
        if (chain[index] == null) return null;

        for (HashNode<K, V> node: chain[index]){
            if(node.getKey().equals(key)) return node.getValue();
        }
        return null;
    }
```
# remove
Is used to remove a key-value pair from a hash table. It begins by calculating the index for the given key using a hash function. Then, it iterates over the chain at that index to locate the key. If a match is found, the corresponding HashNode is removed from the chain, the size of the hash table is decremented, and the value is returned. However, if no match is found, it returns null to indicate that the key was not found in the hash table.
```
  public V remove(K key) {
        int index = hash(key);
        if (chain[index] == null) return null;

        for (HashNode<K, V> node: chain[index]){
            if(node.getKey().equals(key)) {
                chain[index].remove(node);
                size--;
                return node.getValue();
            }
        }
        size--;
        return null;
    }
```
# contains
Is used to check if a specific value exists within a hash table. It iterates over all the chains in the hash table and compares the value of each HashNode to the given value. If a match is found, it returns true to indicate that the value exists in the hash table. However, if no match is found after checking all the chains, it returns false to indicate that the value is not present in the hash table.
```
 public boolean contains(V value) {
        for(LinkedList<HashNode<K,V>> list: chain) {
            for(HashNode<K,V> node: list){
                if (node.getValue().equals(value)) return true;
            }
        }
        return false;
    }
```
# getKey

The provided function getKey() retrieves the key associated with a specific value in the hash table. It does so by iterating over the chains in the hash table and checking if any HashNode's value matches the given value. If a match is found, it returns the corresponding key using the getKey() method of the HashNode. If no match is found after checking all the chains, it returns null to indicate that the value was not found in the hash table.
```
  public K getKey(V value) {
        for(LinkedList<HashNode<K,V>> list: chain) {
            for(HashNode<K,V> node: list){
                if (node.getValue().equals(value)) return node.getKey();
            }
        }
        return null;
    }
```
