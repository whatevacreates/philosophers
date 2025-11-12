# 🧠 Philosophers  

### 🎯 Project Overview  
**Philosophers** is a classic concurrency exercise exploring **threads**, **synchronisation**, and **resource sharing**.  
The simulation models philosophers sitting around a table — alternating between **thinking**, **eating**, and **sleeping** — all competing for a limited number of forks.  

The challenge lies in designing a program that avoids **deadlocks**, **race conditions**, and **starvation**, while maintaining precise timing and clean thread management.  
It’s not just about making philosophers eat — it’s about mastering the art of balance between parallelism and control.

---

## ✅ My Approach  
I implemented a **thread-based simulation** where each philosopher operates independently but under synchronised constraints:

🔹 **Threads:** each philosopher runs as an individual thread.  
🔹 **Forks:** represented by mutexes (mutual exclusion locks).  
🔹 **Monitoring:** a watchdog thread detects death or completion.  
🔹 **Precision timing:** microsecond-level control via `gettimeofday()` for accuracy.  

🧭 I designed a **custom adaptive time-management algorithm** that dynamically adjusts internal delays between actions.  
This means if a philosopher is lagging or the system load changes, the timing adapts automatically — keeping the simulation fair, efficient, and rhythmically balanced.

---

## 🍀 Bonus: Algorithmic Time Adjustment  
To push the project further, I experimented with **dynamic delay adaptation**:  
- Track each philosopher’s waiting and eating times.  
- Adjust `sleep` and `eat` durations algorithmically to maintain synchrony.  
- Reduce starvation and jitter under high concurrency.  

The result: a smoother simulation with better resource distribution and a more “alive” system rhythm — an algorithmic choreography of thought and hunger.

---

## ⚙️ Usage  

```bash
make
./philo <number_of_philosophers> <time_to_die> <time_to_eat> <time_to_sleep> [number_of_times_each_philosopher_must_eat]

