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