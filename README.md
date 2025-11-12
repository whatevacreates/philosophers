Philosophers (42 Project)
🎯 Project Overview

The Philosophers project is a classic concurrency exercise designed to teach threading, synchronization, and resource-sharing. The scenario simulates a number of philosophers who sit around a table, alternate between thinking, eating, and sleeping, and must acquire two forks (shared resources) to eat. Without proper synchronization, issues like deadlock, starvation and race-conditions may occur. 
Medium
+3
fran byte | 42
+3
Medium
+3

In this implementation:

Each philosopher is represented by a thread (or process in the bonus part). 
GitHub
+1

Forks are mapped to mutexes (or semaphores for the bonus). 
GitHub
+1

The simulation terminates when either a philosopher dies (exceeds time_to_die without eating) or all have eaten a specified number of times (if provided). 
Medium
+1

✅ My Unique Time-Management Approach

I have added a custom algorithmic twist: I dynamically adjust the time delay of each philosopher’s cycle (think → eat → sleep) depending on runtime conditions. In other words, I monitor how long each philosopher has waited, track last-meal times, and then adaptively modify the sleep/eat delays so the system maintains fairness and avoids starvation more proactively. This time-adaptation means the system becomes more robust under edge loads, rather than relying on static fixed delays alone.

🧮 Usage

Build the project (assuming mandatory threads version):

make  


Run the simulation:

./philo <number_of_philosophers> <time_to_die_ms> <time_to_eat_ms> <time_to_sleep_ms> [number_of_times_each_philosopher_must_eat]  


For example:

./philo 5 800 200 200  


Or, with meal-limit:

./philo 5 800 200 200 7  

📂 Project Structure

philo.c — Program entry, argument parsing.

timing.c / timing.h — Time utilities, timestamp capture, adaptive delay logic.

philosopher.c / philosopher.h — Philosopher thread routines: picking forks, eating, sleeping, thinking.

forks.c / forks.h — Mutex/semaphore logic, fork acquisition/release.

monitor.c — Monitors philosopher lives (check time_to_die) and ends simulation when conditions are met.

Makefile — Build rules and optional flags (e.g., bonus version).

🧠 Key Concepts

Deadlock avoidance: My algorithm ensures that philosophers don’t all hold one fork and wait forever for a second. Solutions include ordering fork acquisition or limiting simultaneous eaters. 
Medium
+1

Starvation avoidance: By adaptively modifying delays based on wait times, I reduce variance in access and improve fairness.

Synchronization primitives: Use of pthread_mutex_t, pthread_create, pthread_join, and precise time calculations (gettimeofday or clock_gettime) for millisecond accuracy. 
Medium

Adaptive timing algorithm: On top of the standard delays (time_to_eat, time_to_sleep), I compute an adjusted delay if a philosopher has been waiting too long, or conversely shorten delay if others are idle—thus balancing the load dynamically.

🧪 Testing & Validation

Test scenarios include small philosopher counts (1, 2) and large counts (e.g., >100) to check for stability. 
fran byte | 42

Edge cases: invalid arguments (negative, zero), one philosopher (should die if cannot get two forks), high concurrency.

Use tools like Valgrind for memory leaks and thread-sanitizing tools for race conditions. 
GitHub

📋 Notes & Requirements

Input arguments must be positive integers in ms.

No global variables are allowed for shared state (per project rules). 
Medium

Precise timing is essential: the death message for a philosopher must print immediately when the condition triggers (not delayed). 
Medium

For bonus part (optional): use processes instead of threads, and semaphores instead of mutexes. 
GitHub

🧩 Why My Approach Stands Out

By implementing a dynamic delay algorithm I demonstrate a deeper understanding of concurrency beyond the minimum. Rather than static sleep/eat durations, I treat the simulation as adaptive: if the system is under pressure (many waiters), the algorithm shortens idle phases; if underutilised, intervals may lengthen to preserve resource fairness. This shows design thinking, not just implementation.
