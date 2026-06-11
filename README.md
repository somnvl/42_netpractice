*This project has been created as part of the 42 curriculum by somenvie.*

# NetPractice

## Description

NetPractice is an introductory networking project. The goal is to make a series of
small, non-functioning simulated networks work correctly by configuring their devices.

Across 10 progressive levels, each level presents a network diagram with one or more
goals (e.g. "host A must communicate with host B"). The network is broken: some IP
addresses, subnet masks, or routing entries are missing or wrong. The task is to edit
the unshaded fields until every goal reports `OK` and traffic flows correctly in both
directions.

The levels build up in difficulty, covering: assigning IP addresses within the same
network, choosing correct subnet masks, splitting an address space into separate
subnets, configuring default and static routes, connecting hosts through switches and
routers, and finally routing traffic to and from the Internet.

No code is written for this project; the deliverable is the exported configuration of
each solved level.

## Instructions

### Running the training interface

1. Download and extract the project files into a folder of your choice.
2. From inside that folder, run the launch script:

   ```sh
   ./run.sh
   ```

   This starts a local web server and opens the NetPractice interface in your browser.

3. If `run.sh` does not work, start the server manually and open the page yourself:

   ```sh
   python3 -m http.server 49242
   ```

   Then navigate to `http://localhost:49242` (you may use another port if needed).

4. On the welcome page, enter your intranet login (`somenvie`) before starting. This
   is required so the configuration and the evaluation are generated for your account.

### Solving and exporting

- Each level shows a network diagram and a list of goals at the top.
- Edit the unshaded fields (IP, mask, routes) until the network is correct.
- Use **Check again** to verify the configuration. The logs at the bottom of the page
  explain why a configuration fails (missing gateway, invalid IP, loop, no matching
  route, etc.).
- Once all goals report `OK`, a **Next level** button appears.
- Before moving on, click **Get my config** to export the configuration of the level.

### Submission

- Export one configuration file per level using **Get my config**.
- Place the **10 exported configuration files** (one per level) at the **root** of the
  Git repository, along with this `README.md`.
- During the defense, three random levels must be solved within a limited time, without
  external tools (a simple calculator such as `bc` is the only thing tolerated).

## Resources

### Networking concepts studied

- **TCP/IP addressing** — how IPv4 addresses identify a host on a network.
- **Subnet masks** — how a mask (e.g. `255.255.255.0`, or `/24` in CIDR notation)
  splits an address into a network part and a host part, and how block size is computed
  as `256 - mask` for the relevant octet.
- **Network and broadcast addresses** — the first and last addresses of a subnet are
  reserved and cannot be assigned to a host.
- **Default gateways** — the router interface a host uses to reach destinations outside
  its own network.
- **Static and default routes** — how a routing table maps a destination network
  (`0.0.0.0/0` for the default route, or a specific prefix) to a next-hop gateway, and
  how the most specific matching route is chosen.
- **Routers** — devices with multiple interfaces, each belonging to a different network,
  that forward packets between networks.
- **Switches** — devices that connect multiple hosts within the same network.
- **OSI layers** — the conceptual model situating IP addressing (network layer) and
  switching (data-link layer).
- **Private vs public address ranges** — private ranges (`10.0.0.0/8`,
  `172.16.0.0/12`, `192.168.0.0/16`) and the loopback range (`127.0.0.0/8`), and why
  private subnets are not routed over the Internet.

### References

- RFC 791 — Internet Protocol specification.
- RFC 1918 — Address Allocation for Private Internets.
- IBM / Cisco documentation on subnetting and CIDR notation.
- General TCP/IP and subnetting tutorials and subnet calculators (for learning only,
  not used during evaluation).

### Use of AI

AI was used as a learning aid. Specifically:

- To explain networking concepts (subnet masks, CIDR notation, block sizes, routing
  logic, gateways) interactively while working through the levels.
- To help interpret the simulator's logs (e.g. `loop detected`,
  `multiple interface match`, `destination does not match any route`) and translate them into the underlying configuration mistake.