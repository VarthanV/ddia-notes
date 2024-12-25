# Timestamp ordering not sufficient

- Consider a system that needs to ensure that the a username uniquelty identifies a user account, if two user concurrently try to create an account with the same username one of the two should succeed and other should fail.

- The problem is total order emerges once we have collected all the operations from other nodes, for doing immediate decision we cannot rely on it.

- In order to implement something like uniqueness constraint total ordering is not sufficient.

- The idea for knowing when the total order is finalize is captured in the topic of **total order broadcast**.
