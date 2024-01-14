- Basically Available
	- The system is always available (as a unit)
- Soft-state
	- The state of the system may change over time (even without input). After write we might still read old data.
- Eventually consistent
	- System will be consistent at some point in the future
	- But might not be at all times

BASE focuses on databases that are in the "AP" category according to CAP.

[[_PDB Reference]]
[[CAP]]