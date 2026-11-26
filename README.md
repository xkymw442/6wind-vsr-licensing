# 6WIND VSR: Which License Do You Need, What Hardware Does It Run On, and What Does It Cost?

6WIND VSR is a family of nine virtualized routing and security products, each enabled by its own license, and the base software is a long way from a fully loaded router. IPsec, CG-NAT, the fast-path firewall, DDoS protection and UPF all sit behind separate application licenses. 6WIND does not publish list prices on its own site, so every "6WIND VSR price" you see quoted comes from a reseller. The tiers at the store this article links to run from $5 for a seven-day trial to $4,500 one-time for an unlimited-throughput perpetual license.

Price is the easy part. Three gates decide whether VSR works on your hardware at all: the feature you need has to be licensed, the CPU and NIC have to be on 6WIND's support list, and the instance needs enough RAM. The details below come from the 3.8.12 documentation and the April 2026 appliance datasheet, which supersede the older 3.6 docs and 2023 datasheet still ranking in search results.

> **Short version:** match the license to the job, not to the biggest number on the price list. A branch or CPE role fits comfortably in the 10G tier. A CG-NAT or IPsec aggregation role should be sized from the session and tunnel counts you actually need. If you would rather buy a validated box with one support contract, the Dell-built appliance starts at the S size: 12 cores, 16GB, 4x10G and 4x25G ports. 👉 [Check the current 6WIND VSR license tiers and pricing](https://sixtynet.net/aff.php?aff=39)

## What each license tier actually includes

The storefront sells VSR by throughput cap, with tunnel and CG-NAT session allowances attached to each tier. Every tier is a one-time perpetual license with free upgrades, and a single license can be applied to either 6WIND VSR or 6WIND Virtual Accelerator.

| Tier | Max throughput | Included capacity | Price (one-time, USD) | Entry |
| --- | --- | --- | --- | --- |
| 7-day trial | 10G | 2,000 IPsec tunnels, 2M CG-NAT conntracks | $5 | [Start with the trial](https://sixtynet.net/aff.php?aff=39) |
| 10G | 10G | 2,000 IPsec tunnels, 2M CG-NAT conntracks | $100 | [See the 10G license](https://sixtynet.net/aff.php?aff=39) |
| 25G | 25G | 5,000 IPsec tunnels, 5M CG-NAT conntracks | $250 | [See the 25G license](https://sixtynet.net/aff.php?aff=39) |
| 40G | 40G | 10,000 IPsec tunnels, 10M CG-NAT conntracks | $400 | [See the 40G license](https://sixtynet.net/aff.php?aff=39) |
| 60G | 60G | 15,000 IPsec tunnels, 15M CG-NAT conntracks | $600 | [See the 60G license](https://sixtynet.net/aff.php?aff=39) |
| 100G | 100G | 30,000 IPsec tunnels, 30M CG-NAT conntracks | $1,000 | [See the 100G license](https://sixtynet.net/aff.php?aff=39) |
| Unlimited | Uncapped | Uncapped tunnels and conntracks | $4,500 | [See the unlimited license](https://sixtynet.net/aff.php?aff=39) |

The important detail in that table is that throughput is a licensed quantity. 6WIND's own datasheet describes performance in terms of cores: "multiple Gigabits of forwarding capabilities with a single CPU core" and, with linear scaling, "multiple hundreds of Gigabits on a single instance." The commercial tiers cap what you are entitled to run regardless of how many cores you throw at it. Adding 16 cores to a 10G license gives you a 10G router.

Prices are listed as "starting from" in USD, one-time, and they are reseller numbers rather than a 6WIND price list. Confirm them on the page before you build a budget around them. 👉 [Check current tier pricing before you size anything](https://sixtynet.net/aff.php?aff=39)

## The nine products, and why there is no single "VSR license"

The 3.8.12 documentation names nine products, and each one requires its own license to unlock the relevant features.

| Product | What it is for | Licensing note |
| --- | --- | --- |
| Virtual Border Router (vBR) | Border and peering role, full BGP tables, MPLS L3VPN, DMVPN | Own license |
| Virtual Provider Edge (vPE) | PE function, L3VPN, VXLAN EVPN | Own license |
| Virtual Security Gateway (vSecGW) | IPsec hub and VPN concentration, DMVPN with IPsec | Own license, IPsec application license needed |
| Virtual Carrier Grade NAT Router (vCGNAT) | NAT44, NAT64 with DNS64, port block allocation | Own license, CG-NAT application license needed |
| Virtual Broadband Network Gateway (vBNG) | Subscriber-aware BNG, multi-million session management | Own license |
| Virtual Firewall (vFW) | L3/L4 stateful filtering at fast-path speed | Own license, fast-path firewall license needed |
| Virtual Cell Site Router (vCSR) | RAN aggregation and backhaul from baseband units | Own license |
| Virtual CPE Router (vCPE) | uCPE routing, security and VPN on small on-site x86 boxes | Own license |
| Virtual UPF | 5G user plane, PFCP, PDR/FAR/QER/URR | Own license, UPF application license needed |

The older 3.6.25 documentation lists six of these. vBNG, vFW and vUPF were added between 3.6 and 3.8, so a comparison written against 3.6 is describing a smaller product line than the one you can buy now.

Underneath, the routing stack is not thin: BGP and BGP4+, OSPFv2/v3, IS-IS, RIP, SR-TE, PCEP, SRv6, PIM SM/SSM, MPLS LDP, BGP L3VPN, VXLAN EVPN, NHRP, cross-VRF, ECMP, PBR and BFD all appear in the base feature list. Management covers CLI, NETCONF/YANG, SNMP, sFlow, NetFlow/IPFIX, BMP, and streaming to Kafka, InfluxDB, Elasticsearch, Graphite or CloudWatch.

## Features that carry a separate application license

This is the part usually buried in a footnote. Beyond the product license, these capabilities need an application license of their own:

- **IPsec.** IKEv1/v2 with PSK or X509, MOBIKE, AES-CBC/GCM at 128/192/256, DH groups 1/2/5/14/31 (curve25519)/32 (curve448), ECDSA, RSA-PSS, EdDSA, tunnel/transport/BEET modes, static and dynamic SVTI.
- **CG-NAT.** NAT44 and NAT64 with DNS64, port block allocation, deterministic NAT, endpoint-independent and address-dependent mapping, ALGs for ICMP, FTP, TFTP, RTSP, PPTP, SIP and H323, plus hairpinning and paired IP pool management.
- **Fast Path Firewall.** Matches 5-tuples, DSCP, address groups and application names, with verdicts of accept, drop, track or reject and actions on TCP MSS and DSCP.
- **DDoS protection.** Traffic types ICMP, DNS, QUIC, UDP and TCP, rate limiters at global, per-source-IP and per-destination-IP granularity, trusted address lists.
- **PPPoE server and IPoE**, each licensed separately from the base IP services.
- **UPF**, with relay and gateway session modes, PDR/FAR/QER/URR and PFCP.
- **IKE/IPsec synchronization** for HA pairing, on top of the VRRP that comes with the base product.

If your design is "a router with a firewall bolted on the side," either budget the vFW and fast-path firewall licenses or terminate that traffic somewhere else. Same logic for a BNG design that assumes PPPoE server support is included: it is not.

## Hardware gates: CPU, NIC and RAM

This is where most failed proofs of concept come from. 6WIND maintains explicit support lists, and the components marked with an asterisk in the NIC list are the ones fully integrated into 6WIND's CI with broad functional and performance coverage.

**CPUs.** Intel Xeon E5-1600/2600/4600 v2, v3 and v4, Xeon E7-2800/4800 v2/v3 and E7-4800/8800 v4, Xeon Scalable across Skylake, Cascade Lake, Ice Lake and Sapphire Rapids, Atom C3000 (Denverton), Xeon D, Ampere Altra Server Snow, and AWS Graviton2. Note the ARM entries: this is not an x86-only product any more.

**NICs.** Intel 1G 82573, 82576, 82580, I210, I211, I350, I354 (igb); Intel 10G 82599\*, X520\*, X540, X550\* (ixgbe); X710\*, XL710\*, X722, XXV710\* (i40e); E810 25G\* and 100G\* (ice); Mellanox ConnectX-4/5/6 (mlx5); Broadcom NetXtreme E-Series 100G\* (bnxt). A card without the asterisk may still work, but nobody has run it through the regression suite, and that is where you discover a 100G adapter behaving badly with a particular driver build.

**RAM.** The minimum for bare metal or a VM is 2GB and 2 CPU cores, with default capabilities scaling automatically to available memory. The documented ceilings at 8GB are the numbers to plan against: 32 virtual routers, 1,000,000 routes, 200,000 next-hops, 10,300 neighbors, 4,096 PBR rules, 10,000 netfilter rules, 262,144 conntracks, 512 VXLAN interfaces, 100,000 IPsec tunnels, and for CG-NAT 4M conntracks, 4M NAT entries, 20K CPE users and 80K blocks. 6WIND adds a caveat worth repeating: "Some of these numbers (CG-NAT) are empirical. They may have to be tuned according to your use case."

**Containers.** For the CNF form factor the recommendation is at least 6GB of hugepages, 2GB of standard memory and 512MB of POSIX shared memory. The stated minimum is 1GB hugepages, 1GB standard memory and 64MB shared memory, plus at least 1GB of storage (8GB recommended for multiple images and logs). A CNF pod that looks like it has enough RAM but has no hugepages configured will not start properly, and that is a deployment-time surprise rather than a licensing one. 👉 [Compare license tiers against your target hardware](https://sixtynet.net/aff.php?aff=39)

Deployment targets cover bare metal, KVM, VMware, AWS and Azure with Virtio, VMXNET3, ENA, PCI passthrough or SR-IOV, plus Docker, Podman, Kubernetes, Red Hat OpenShift and VMware Telco Cloud Platform on the container side. Images ship as qcow2, ova or iso, with PXE and USB installation, cloud-init and Ansible provisioning, and update/rollback support.

## Do not size from the 3.6 documentation

Several 6WIND pages and third-party summaries still reflect the 3.6.25 documentation. The gaps matter if you are building a bill of materials:

- **Product line.** Six products in 3.6, nine in 3.8. No vBNG, vFW or vUPF in the older docs.
- **Routing.** SRv6 and PCEP are absent from 3.6.
- **Security.** No fast-path firewall and no DDoS protection in 3.6, only ACLs, uRPF, control plane protection and BGP Flowspec.
- **Capacity.** Next-hops doubled from 100,000 to 200,000 and neighbors from 5,000 to 10,300.
- **Container platforms.** 3.6 lists Docker and Kubernetes only; 3.8 adds OpenShift and VMware Telco Cloud Platform.
- **NIC list.** The 1G entry starts at 82575 in 3.6 and 82573 in 3.8, and the CI asterisks appear only in 3.8.

If a vendor or an internal wiki is quoting neighbor counts or a NIC list from an older document, the sizing is wrong in both directions: too small on scale, and possibly built around hardware that is no longer the tested baseline.

## The Dell-built appliance, and the 48-versus-64-core question

6WIND now sells a hardware appliance built with Dell Technologies and delivered through Dell and its authorized partners, positioned as a single point of procurement and support. It is a 1U PowerEdge R470XL or 2U PowerEdge R770, Intel Xeon 6 P-core, up to 256GB DDR5-6400 RDIMM ECC, Mellanox ConnectX-6 or 7 plus Intel I350 1G ports, dual hot-swappable SSDs in RAID 1, PCIe Gen5 and OCP 3.0 slots, redundant AC (100–240V) or DC (-48V) Titanium power supplies, NEBS Level 3 certified SKUs, and Dell Mission Critical 4-hour or next-business-day support.

| Size | Cores | Memory | Port density |
| --- | --- | --- | --- |
| Small (S) | 12 | 16GB | 4x10G, 4x25G |
| Medium (M) | 24 | 32GB | 8x10G, 8x25G |
| Medium (M') | 24 | 32GB | 2x100G |
| Large (L) | 32 | 64GB | 4x100G |
| Extra Large (XL) | 48 | 128GB | 6x100G, 8x100G |
| XX Large (XXL) | 64 | 256GB | 4x400G |

One inconsistency to be aware of: the same datasheet's key features section says "Intel Xeon 6 from 12 to 48 P-Core," while the configuration table lists 64 cores for the XXL size. Both statements appear in the April 2026 document. If you are ordering the top configuration, get the core count confirmed in the quote rather than assuming either number.

The appliance runs the full VSR use-case set, including vBNG, vCGNAT, vFW, vSecGW, dUPF and vBorder Router. The trade-off against software-only is straightforward: you pay for validated hardware and one support contract instead of reusing existing servers that may or may not be on the CPU and NIC lists.

## Choosing by role

- **Border routing and peering, full tables, MPLS L3VPN:** vBR.
- **Large-scale NAT44 or NAT64 with logging and port block allocation:** vCGNAT, and size from conntracks and CPE count rather than throughput.
- **IPsec aggregation, VPN concentration, DMVPN:** vSecGW, remembering that IPsec is a separately licensed application.
- **Subscriber management with millions of sessions:** vBNG.
- **5G user plane:** vUPF.
- **RAN backhaul from baseband units:** vCSR.
- **Small on-site boxes running routing plus security:** vCPE.
- **No appetite for hardware selection:** appliance S or M, which covers 12 to 24 cores with 10G and 25G ports.

If you only need a branch router with BGP and a few hundred tunnels, the 10G perpetual tier at $100 plus a supported 10G NIC does the job, and the unlimited tier is money you will never recover. The reverse is also true: a 25G license on a CG-NAT design that needs 20 million conntracks will hit the capacity ceiling long before the throughput ceiling.

## Before you ask for a quote

Two things decide whether the number you get back is usable.

First, write down the license list. Product license, plus which application licenses (IPsec, CG-NAT, fast-path firewall, DDoS, PPPoE server, IPoE, UPF, IKE/IPsec sync) attach to the design. A quote that covers only the product license will look cheaper and will not deliver the features you specified.

Second, check the server. CPU family and model, NIC model and whether it carries an asterisk in the 3.8.12 list, RAM per instance against the 8GB baseline table, and for containers whether hugepages are configured. 6WIND commercial terms are pay-as-you-grow, while the reseller tiers above are one-time perpetual with free upgrades, so confirm which model your quote follows before comparing it to anything else.

👉 [View the current 6WIND VSR license options](https://sixtynet.net/aff.php?aff=39)
