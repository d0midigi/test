# README

The Internet is composed of many independent networks (called autonomous systems) that must cooperate in order for packets to reach their destinations. This necessitates different protocols and algorithms for routing packets within autonomous systems (routers operated by the same entity) and between autonomous systems (where business agreements and policy affect routing).

This assignment focuses on intradomain routing algorithms used by routers within a single autonomous system (AS). The goal of intradomain routing is typically to forward packets along the shortest or lowest-cost path through the network.

Because routers must handle unexpected router or link failures, changing link costs (often depending on traffic volume), and connections from new routers and clients, distributed algorithms are used. In these distributed algorithms, routers start with only local state and must communicate to learn lowest-cost paths.

Nearly all intradomain routing algorithms used in real-world networks fall into one of two categories: distance-vector (DV) or link-state (LS). In this assignment you will implement distributed distance-vector and link-state routing algorithms in Python and test them with a provided network simulator.

## Background Reading

Begin by reading pages 240–258 in the textbook Computer Networks: A Systems Approach (5th edition) by Peterson & Davie. An excerpt of these pages is included in the `assignment2` directory with the filename `textbook_reading.pdf`. There is also a copy of the textbook in the Friend library.

The reading provides enough information to design both the distance-vector and link-state routing algorithms. Pay attention to the summary at the bottom of page 258:

"In distance-vector, each node talks only to its directly connected neighbors, but it tells them everything it has learned (i.e. distance to all nodes). In link-state, each node talks to all other nodes, but it tells them only what it knows for sure (i.e. only the state of its directly connected links)."

## Provided code

### Download and start the VM

Open your terminal and `cd` into the `<>/assignments` directory you downloaded in Assignment 1. Run:

* git pull to download the code for this assignment.
* vagrant reload --provision to install needed libraries and start the VM (no need to run `vagrant up` in addition).
* vagrant ssh and cd /vagrant to enter the virtual machine (just like Assignment 1).

The provided code is located at `/vagrant/assignments/assignment2` inside the VM.

### Familiarize yourself with the network simulator

* Each `.json` file in the `assignment2` directory specifies a different network simulation (varying numbers of routers, links, link costs). Some simulations include link additions and/or failures at pre-specified times.
* Run the simulator with a GUI: python visualize\_network.py 01\_small\_net.json
  * The default router implementation returns traffic back out the link on which it arrives. Your assignments will replace this behavior.
  * The visualization shows routers (red), clients (blue), link costs, and traceroute-like packets from clients that record the sequence of routers traversed. The most recent route to each client is printed in the top-right text box — a useful debugging aid.
  * Clicking a client hides all packets except those addressed to that client. Clicking again shows all packets.
  * Clicking a router prints a debug string in the lower-right box. You can set this string in your router implementation.
* Run without a GUI: python network.py 01\_small\_net.json
  * Runs faster; stops after a predetermined time and prints final routes taken by traceroute packets and whether they match known lowest-cost paths.

## Implementation instructions

You must complete the `DVrouter` and `LSrouter` classes in `DVrouter.py` and `LSrouter.py` to implement distance-vector and link-state routing algorithms, respectively.

* The simulator runs independent instances of your router classes in separate threads (one instance per router).
* The `DVrouter` and `LSrouter` files contain several unfinished methods marked with `TODO` (e.g. `handlePacket`, `debugString`). These override the `Router` superclass methods (in `router.py`) and are called by the simulator on corresponding events.
* The arguments to these methods provide all information needed to implement the algorithms. You may add fields or helper methods to these classes.

Important design notes (use the textbook reading to guide design):

* The assignment simplifies many real-world details. Focus on correct DV and LS behavior in the simulator.
* For DV, you must handle count-to-infinity. You may use small-infinity (e.g. 16), split horizon, or split horizon with poison reverse.
* For LS, implement reliable flooding of link-state updates conceptually: you will need sequence numbers for LSPs but you can assume single-hop sends are reliable (no retransmissions/acks required).
* Both protocols should send periodic routing packets at least once every heartbeatTime milliseconds. The constructor for each router receives heartbeatTime; `handleTime` will receive the current time in milliseconds for scheduling.

Allowed helper functions for packet serialization:

* `dumps()` and `loads()` are provided to stringify and parse packet `content` (they produce/consume JSON strings).
* Packet `content` must be a string (asserted when sending). Using `dumps()` is a recommended way to set `content`.

### Restrictions (must follow exactly)

Your solution must not require modification to any files other than `DVrouter.py` and `LSrouter.py`. The grading tests will use the unchanged versions of all other files.

When implementing your routers, you may not call functions, instantiate classes, or access variables defined in any other provided Python files, except for the following allowed interactions:

* Use the `send` method inherited from the `Router` superclass: self.send(port, packet)
* Access the `addr` field of the `Router` superclass: self.addr
* Create new `Packet` objects and call any methods defined in `packet.py` EXCEPT for getRoute(), addToRoute(), and animateSend(). You may access and modify Packet fields except for `route`.

Violating these restrictions will cause serious grade penalties.

## Methods you must implement

Complete the following methods in both `DVrouter` and `LSrouter`:

* **init**(self, addr, heartbeatTime)
  * Constructor: `addr` is this router's address. Initialize fields (e.g. routing table, forwarding table). Ensure routing information is sent at least once every `heartbeatTime` milliseconds.
* handlePacket(self, port, packet)
  * Called whenever a packet arrives on `port`. Check whether the packet is a traceroute packet or a routing packet and handle appropriately. Use the Packet API in `packet.py`.
* handleNewLink(self, port, endpoint, cost)
  * Called when a new link is added on `port` to `endpoint` with link cost `cost`. Store these values for routing. To send packets along a link, call `self.send(port, packet)`.
* handleRemoveLink(self, port)
  * Called when a link on `port` is disconnected. Update data structures.
* handleTime(self, timeMillisecs)
  * Called regularly with the current time in milliseconds. Use this to trigger periodic routing messages (at least every `heartbeatTime` ms).
* debugString(self)
  * Returns a string useful for debugging (printed in GUI). This is not graded, but is helpful while developing.

### Packet creation and usage

* Create packets of kind ROUTING for routing information.
* Decide what to include in packet `content`. It must be a string. Use `dumps()`/`loads()` to serialize/deserialize Python objects into JSON strings.
* You can set/modify packet fields including `content`, `srcAddr`, `dstAddr`, `kind`, etc., except you must not touch `route`.

### Link reliability and ordering

* If a link between routers fails or is added, both endpoints will always receive the appropriate `handle` callback.
* Links have varying latencies; packets may arrive out of order relative to send times.

## Hints and simplifications

{% hint style="info" %}
* The textbook includes an example DV implementation in C (pp. 249–250). Use it as a guide.
* Page 248 discusses count-to-infinity; choose an approach (small infinity, split horizon, or poison reverse).
* For LS, sequence numbers for LSPs are required to prevent replaying stale information.
* Periodic sending of routing information is required for correctness and to detect silent failures.
{% endhint %}

## Running and Testing

* Use the provided network simulator JSON files (some include events like link failures/additions).
* Example JSONs: `05_pg242_net.json` and `03_pg244_net.json` correspond to textbook figures.
* Files without "events" are good for initial testing (no link changes).

Run with GUI:

* python visualize\_network.py \[networkSimulationFile.json] \[DV|LS]

Run without GUI:

* python network.py \[networkSimulationFile.json] \[DV|LS]

The second argument selects which router implementation to run: DV (DVrouter) or LS (LSrouter).

At the end of a non-GUI simulation the simulator prints routes and whether they match known lowest-cost routes. If they match, your implementation passes that test case.

A helper script is provided:

* test\_dv\_ls.sh runs all supplied networks with your implementations. You may need to chmod 744 test\_dv\_ls.sh to make it executable. You may pass an argument "LS" or "DV" to test only one implementation (e.g., test\_dv\_ls.sh DV).

You may see this benign error sometimes when threads stop at the end of simulation:

Unhandled exception in thread started by sys.excepthook is missing lost sys.stderr

You can ignore it.

## Submission and Grading

* Only one partner should submit `DVrouter.py` and `LSrouter.py` to the CS Dropbox: https://dropbox.cs.princeton.edu/COS461\_S2019/Assignment-2-Intradomain-Routing-Algorithms
  * Include both partners' names and netIDs in a comment at the top of both files.
* Submit a file `partners.txt` containing your netIDs (no aliases), one per line.

Grading:

* Your grade depends on whether your algorithms find lowest-cost paths (including after link failures/additions) and on adherence to the restrictions.
* The graders will verify that `DVrouter` implements a distance-vector algorithm and `LSrouter` implements a link-state algorithm.
* Start early and use Piazza or office hours if you have questions.

## Useful commands (examples)

* Run GUI simulation with DV implementation:
  * python visualize\_network.py 01\_small\_net.json DV
* Run simulation (no GUI) with LS implementation:
  * python network.py 01\_small\_net.json LS
* Run all tests:
  * chmod 744 test\_dv\_ls.sh
  * ./test\_dv\_ls.sh
  * or ./test\_dv\_ls.sh DV
  * or ./test\_dv\_ls.sh LS

***

If you want, paste your current `DVrouter.py` and/or `LSrouter.py` here and I can review for correctness, suggest fixes, or help implement specific parts (e.g., count-to-infinity handling, LSP sequence numbering, periodic messaging).
