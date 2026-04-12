A) Write a JAVA program to demonstrate a Message Queue using the Producer–Consumer model
import java.util.*;
class MessageQueue {
Queue<Integer> q = new LinkedList<Integer>();
int max = 5;
synchronized void produce(int x) {
while (q.size() == max) {
try { System.out.println("Queue Full -> Producer Waiting"); wait(); } catch (Exception e) {}
}
q.add(x);
System.out.println("Producer Produced: " + x);
notifyAll();
}
synchronized void consume() {
while (q.isEmpty()) {
try { System.out.println("Queue Empty -> Consumer Waiting"); wait(); } catch (Exception e) {}
}
System.out.println("Consumer Consumed: " + q.poll());
notifyAll();
}
}
public class ProducerConsumerDemo {
public static void main(String[] args) {
MessageQueue mq = new MessageQueue();
new Thread(() -> {
for (int i = 1; i <= 10; i++) mq.produce(i);
}).start();
new Thread(() -> {
for (int i = 1; i <= 10; i++) mq.consume();
}).start();
}
}
B) Write a Java program to detect deadlock in a distributed system with a single resource model.
import java.util.*;
public class DeadlockDetection {
Map<Integer, List<Integer>> g = new HashMap<>();
void add(int u, int v) {
if (!g.containsKey(u)) g.put(u, new ArrayList<Integer>());
if (!g.containsKey(v)) g.put(v, new ArrayList<Integer>());
g.get(u).add(v);
}
int dfs(int u, Set<Integer> vis, Set<Integer> st, List<Integer> path) {
if (st.contains(u)) {
int i = path.indexOf(u);
System.out.print("Deadlock Cycle: ");
for (int j = i; j < path.size(); j++)
System.out.print("P" + path.get(j) + " -> ");
System.out.println("P" + u);
return 1;
}
if (vis.contains(u)) return 0;
vis.add(u);
st.add(u);
path.add(u);
List<Integer> list = g.get(u);
for (int i = 0; i < list.size(); i++)
if (dfs(list.get(i), vis, st, path) == 1)
return 1;
st.remove(u);
path.remove(path.size() - 1);
return 0;
}
int detect() {
Set<Integer> vis = new HashSet<Integer>();
Set<Integer> st = new HashSet<Integer>();
List<Integer> path = new ArrayList<Integer>();
for (Integer u : g.keySet())
if (dfs(u, vis, st, path) == 1)
return 1;
return 0;
}
public static void main(String[] args) {
DeadlockDetection d = new DeadlockDetection();
d.add(1, 2);
d.add(2, 3);
d.add(3, 1);
if (d.detect() == 1)
System.out.println("Deadlock Detected");
else
System.out.println("No Deadlock");
}
}
