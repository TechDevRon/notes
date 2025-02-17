
CTI can also be used during engagement execution, emulating the adversary's behavioral characteristics, such as  

- C2 Traffic
    - User Agents
    - Ports, Protocols
    - Listener Profiles
- Malware and Tooling
    - IOCs
    - Behaviors

The second behavioral use of CTI is analyzing behavior and actions of an adversaries' malware and tools to develop your offensive tooling that emulates similar behaviors or has similar vital indicators.

An example of this could be an adversary using a custom dropper. The red team can emulate the dropper by,

- Identifying traffic
- Observing syscalls and API calls
- Identifying overall dropper behavior and objective
- Tampering with file signatures and IOCs