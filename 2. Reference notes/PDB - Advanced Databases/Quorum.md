Quorum is a mechanism to ensure consistency and availability. It's a way to agree on a consensus among nodes about the current state of the dataset.

It's usually a majority vote that needs to agree and respond to a request for it to be successful.

If the quorum is not successful the request will fail.
## Write quorum
**W > N/2**
We need the majority to agree on a change. This will never lead to conflicts.

## Read quorum
**R > N - W** = R + W > N
We ask all nodes from read quorum and get the latest result (newest timestamp). This is enough because the write quorum agreed on the change.
