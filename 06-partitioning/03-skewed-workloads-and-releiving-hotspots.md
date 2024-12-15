# Skewed Workloads and Relieving Hotspots

- Hashing a key to determine its partition can help reduce hotspots. It cannot be avoided entirely

- In extreme cases where read and write are all for the same key , we still end up requests being routed to same partition.

- For example a celebrity is there on social media and they post and update and fans interact with them in comments , the workload goes to the same partition even though we hashed it.

- It makes sense to append random number to a small number of hotkeys to relieve from skew and hotspots.

