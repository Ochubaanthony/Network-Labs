# OSPF Single-Area Lab (Cisco IOS)

A beginner-friendly, three-router OSPFv2 lab for Cisco Packet Tracer, GNS3, or EVE-NG.

## Objectives
- Build a routed triangle using three Cisco IOS routers.
- Configure IPv4 addressing and OSPF process 1 in area 0.
- Use router IDs and passive interfaces.
- Verify neighbor adjacencies, routes, and end-to-end reachability.
- Practice a basic OSPF troubleshooting workflow.

## Topology

```text
             10.0.12.0/30
       R1 ---------------- R2
        \                  /
         \                /
          \              /
           ---- R3 ------
             10.0.13.0/30
             10.0.23.0/30
```

Each router also has a loopback advertised into OSPF.

## Addressing plan

| Device | Interface | Address | Purpose |
|---|---|---|---|
| R1 | G0/0 | 10.0.12.1/30 | R1-R2 link |
| R2 | G0/0 | 10.0.12.2/30 | R1-R2 link |
| R1 | G0/1 | 10.0.13.1/30 | R1-R3 link |
| R3 | G0/0 | 10.0.13.2/30 | R1-R3 link |
| R2 | G0/1 | 10.0.23.1/30 | R2-R3 link |
| R3 | G0/1 | 10.0.23.2/30 | R2-R3 link |
| R1 | Lo0 | 1.1.1.1/32 | Router ID / test prefix |
| R2 | Lo0 | 2.2.2.2/32 | Router ID / test prefix |
| R3 | Lo0 | 3.3.3.3/32 | Router ID / test prefix |

> Interface names can differ by platform. Adapt them to your router model.

## Setup
1. Add three IOS routers and connect them in a triangle.
2. Configure interface addresses from the table.
3. Apply the matching configuration in `configs/`.
4. Ensure all physical interfaces are enabled with `no shutdown`.
5. Verify OSPF neighbors and learned routes.

## Verification

Run on each router:

```text
show ip interface brief
show ip ospf neighbor
show ip ospf interface brief
show ip route ospf
show ip protocols
show ip ospf database
```

Expected results:
- Each router forms two FULL adjacencies in this triangle.
- Each router learns the other routers' loopback /32 routes through OSPF.
- Pings between 1.1.1.1, 2.2.2.2, and 3.3.3.3 succeed.

Example tests:

```text
R1# ping 2.2.2.2
R1# ping 3.3.3.3
R2# ping 1.1.1.1
```

## Troubleshooting challenges
1. Shut down one transit interface. Observe neighbor state and route changes.
2. Configure a mismatched OSPF area on one end of a link. Identify and fix the issue.
3. Remove `no passive-interface` from one transit link. Observe adjacency behavior.
4. Change one side's subnet mask. Explain why the adjacency fails.
5. Restore the configuration and confirm two FULL neighbors per router.

Useful commands:
- `show ip ospf neighbor`
- `show ip ospf interface`
- `show ip interface brief`
- `show running-config | section router ospf`

## Notes
- This is an OSPFv2 single-area IPv4 exercise using area 0.
- Configurations use Cisco IOS-style syntax.
- Save verified configurations with `copy running-config startup-config`.
