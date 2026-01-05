###### \## DHCP Failure (APIPA Issue)



\### Symptom

\- PCs received 169.254.169.30 addresses

\- No default gateway



\### Root Cause

\- No OSPF adjacency with router

\- Missing DHCP relay on SVIs



\### Resolution

\- Fixed Layer 3 links

\- Added ip helper-address on VLAN interfaces on distribution switches



\### Lesson Learned

DHCP broadcasts do not cross routers without relay configuration.



