Observer/observable:

public class Observable {
  ArrayList<Observer> observers;

  public Observable(){
    this.observers = new ArrayList<>();
  }

  public void registerObserver(Observer observer) {
    this.observers.add(observer);
  }

  public void unregisterObserver(Observer observer) {
    this.observers.remove(observer);
  }

  public void notifyObservers(String msg) {
    for (Observer observer : observers){
      observer.update(msg);
    }
  }
}

public class Observer {
  private String message;
  private int id;

  public Observer(int id) {
    this.id = id;
  }

  public String update(String message) {
    this.message = message;
    return String.format("%d: %s", id, message);
  }
}


Hashmap Example
//first part is class which represents node of a linked list
class Entry<K, V> {
    final K key;
    V value;
    Entry<K, V> next;

    public Entry(K key, V value, Entry<K, V> next) {
        this.key = key;
        this.value = value;
        this.next = next;
    }

    // getters, equals, hashCode and toString
}
//up to here

//inserting element
public class MyMap<K, V> {
    private Entry<K, V>[] buckets;
    private static final int INITIAL_CAPACITY = 1 << 4; // 16

    private int size = 0;

    public MyMap() {
        this(INITIAL_CAPACITY);
    }

    public MyMap(int capacity) {
        this.buckets = new Entry[capacity];
    }

    public void put(K key, V value) {
        Entry<K, V> entry = new Entry<>(key, value, null);

        int bucket = getHash(key) % getBucketSize();

        Entry<K, V> existing = buckets[bucket];
        if (existing == null) {
            buckets[bucket] = entry;
            size++;
        } else {
            // compare the keys see if key already exists
            while (existing.next != null) {
                if (existing.key.equals(key)) {
                    existing.value = value;
                    return;
                }
                existing = existing.next;
            }

            if (existing.key.equals(key)) {
                existing.value = value;
            } else {
                existing.next = entry;
                size++;
            }
        }
    }
    // . . .
}
//up to here

Retrieve from hashmap

public V get(K key) {
    Entry<K, V> bucket = buckets[getHash(key) % getBucketSize()];

    while (bucket != null) {
        if (bucket.key.equals(key)) {
            return bucket.value;
        }
        bucket = bucket.next;
    }
    return null;
}
//up to here
if testing

@Test
public void testMyMap() {
    MyMap<String, String> myMap = new MyMap<>();
    myMap.put("USA", "Washington DC");
    myMap.put("Nepal", "Kathmandu");
    myMap.put("India", "New Delhi");
    myMap.put("Australia", "Sydney");

    assertNotNull(myMap);
    assertEquals(4, myMap.size());
    assertEquals("Kathmandu", myMap.get("Nepal"));
    assertEquals("Sydney", myMap.get("Australia"));
}