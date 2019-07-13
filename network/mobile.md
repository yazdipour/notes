# Advance Mobile Communications Networks

https://www.youtube.com/results?search_query=Mobile+Communications+Networks&sp=EgIQAw%253D%253D

* Core ICS Research Areas
    * LTE and 5G
        * Repair of broken base stations and coverage holes
        * Handle spatial overload
        * Save energy
    * Communicating Unmanned Aerial Vehicles (UAVs)
    * Cognitive radio networks
        * Cognition of radio situation
        * Flexible use of unused frequencies
        * Implementation on software-defined radios

## IP protocol model - OSI protocol

* Difference between function and service of a protocol?
    * Protocol is the special set of rules that end points in a telecommunication connection use when they communicate. In other words Protocol is an agreed-upon format for transmitting data between two devices. The protocol determines the following: 
        * the type of error checking to be used
        * data compression method
        * if any how the sending device will indicate that it has finished sending a message
        * how the receiving device will indicate that it has received a message
    * Service is a program, routine, or process that performs a specific system function to support other programs, particularly at a low (close to the hardware) level

* Which protocol layers provide end to end, which hop to hop services? `TCP e2e / UDP h2h`

    > WIKI: Hop-by-hop transport is a principle of controlling the flow of data in a network. With hop-by-hop transport, chunks of data are forwarded from node to node in a store-and-forward manner. As hop-by-hop transport involves not only the source and destination node, but rather some or all of the intermediate nodes as well, it allows data to be forwarded even if the path between source and destination is not permanently connected during communication. Hop-by-hop transport requires per-flow state information at intermediate nodes, which limits its scalability. This is one of the reasons why almost all communication today is controlled by end-to-end transport protocols such as TCP.

* Difference between transport protocol and logical link sublayer?
* Purpose of a TCP/UDP port, difference to IP address?
* What does VPN mean? Which protocol implements it?
* What does CSMA stand for? How does it work? `Carrier Sense Multiple Access with Collision Detection (IEEE 802.3)`
* What´s the purpose of IP subnetting? `More IP` What´s the effect on routing?

![osi-ip layer](https://i-technet.sec.s-msft.com/dynimg/IC196427.gif)

[src1 (overall)](https://www.studytonight.com/computer-networks/tcp-ip-reference-model) // [src2 (details)](http://www.pearsonitcertification.com/articles/article.aspx?p=1804869)

## Wireless Transmission (Layer 1)

* WLAN/WiFi/802.11 Systems
* IEEE 802.16/WiMAX Systems
* Unlicensed Mobile Access (UMA)
    Access to GSM and GPRS mobile services over unlicensed spectrum(WLAN, Bluetooth)
* Fixed Mobile Convergence (FMC)
    * SIP over Wi-Fi
    * Centralized Application Server or IP-PBX controls VoIP services
    * advanced VoIP services on mobile, enterprise, home, and public WiFi networks
* 4G Mobile Communication Systems
* 5G Mobile Communication Systems

### Physical Layer Aspects and Channel Characteristics

#### Frequencies

```
Frequency and wave length:      λ = c / f
wave length λ, speed of light c ≅ 3x108 m/s, frequency f
```

#### Signals

![Signals](./assets/Signals.png)

#### Signal propagation

* Signal to Interference (and Noise) Ratio (SINR)
* Range limited systems (lack of coverage)
* Interference limited systems (lack of capacity)
* Information Theory: Channel Capacity

![propagation](./assets/propagation.png)

#### Antennas

* Isotropic radiator: equal radiation in all directions (three dimensional)
* Simple dipoles
* Directed and sectorized: Often used for microwave connections or base stations for mobile phones (e.g. radio coverage of a valley)
* Real antennas are not isotropic radiators
* Real antennas always have directive effects (vertically and/or horizontally)

#### Multiplexing

* Goal: multiple use of a shared medium
* Multiplexing in 4 dimensions
    * space (si)
    * time (t)
    * frequency (f)
    * code (c)
        * Frequency multiplex
        * Time and frequency multiplex
        [Example: GSM (frequency hopping)]
        * Code multiplex

#### Modulation

* Basic schemes
    * Amplitude Modulation (AM)
    * Frequency Modulation (FM)
    * Phase Modulation (PM)
* Motivation for modulation
    * smaller antennas (e.g., λ/4)
    * Frequency Division Multiplexing
    * medium characteristics
    * spectrum availability
* Analog modulation: shifts center frequency of baseband signal up to the radio carrier

![Modulation](./assets/Modulation.png)

* Digital modulation
    * digital data is translated into an analog signal (baseband)
        * ASK
        * FSK
            * bandwidth needed for FSK depends on the distance between the carrier frequencies
        * Advanced FSK
            * special pre-computation avoids sudden phase shifts
                * Continuous Phase Modulation (CPM)
                * MSK (Minimum Shift Keying)
            * higher bandwidth efficiency using a Gaussian low-pass filter
                * GMSK (Gaussian MSK), used for GSM and DECT
        * PSK
        * Advanced PSK
            * BPSK (Binary Phase Shift Keying)
            * QPSK (Quadrature Phase Shift Keying)
        * QAM (Quadrature Amplitude Modulation)

![DigitalModulation](./assets/DigitalModulation.png)

#### Spread spectrum گسترش طیف

Problem of radio transmission: frequency dependent fading can wipe out narrow
band signals for duration of the interference

Solution: spread the narrow band signal into a broadband signal using a special
code

* DSSS (Direct Sequence Spread Spectrum) 1, 2
* FHSS (Frequency Hopping Spread Spectrum) 1, 2, 3

#### Cellular systems

* Cell structure
* Fixed/Dynamic frequency assignment
* Coverage and capacity

## Medium Access Schemeses (Layer 2)

MAC in Multi-Channel Scenario

### Media Access

* The problem: multiple users compete for a common, shared resource
(medium)
* Can we apply media access methods from fixed networks?
Example: CSMA/CD
    * Carrier Sense Multiple Access with Collision Detection (IEEE 802.3)
    * send as soon as the medium is free (carrier sensing - CS)
    * listen to the medium, if a collision occurs stop transmission and jam
    (collision detection - CD)
* Motivation - hidden and exposed terminals
* Motivation - near and far terminals

#### Access methods SDMA/FDMA/TDMA

These multiplexing schemes are now used to control medium access!

* SDMA (Space Division Multiple Access)
    * segment space into sectors, use directed antennas
    * cell structure
* FDMA (Frequency Division Multiple Access)
    * assign a certain frequency to a transmission channel between a sender and a receiver
    * permanent (e.g., radio broadcast), slow hopping (e.g. GSM), fast hopping (FHSS, Frequency Hopping Spread Spectrum)
* TDMA (Time Division Multiple Access)
    * assign the fixed sending frequency to a transmission channel between a sender and a receiver for a certain amount of time

#### Communication link types

Each terminal needs an uplink and a downlink channel

Types

* Simplex
    * unidirectional link transmission
* Half Duplex
    * Bi-directional (but not simultaneous)
* Duplex
    * simultaneous bi-directional link transmission, two types:
        * Frequency division duplexing (FDD) **`FDMA`**
            * Separate frequency bands for upand downlink
            * (+) separation of uplink and downlink interference
            * (-) no support for asymmetric traffic
            * Examples: LTE, UMTS, GSM, IS-95, AMPS
        * Time division duplexing (TDD) **`TDMA`**
            * Separate frequency bands for upand downlink
            * (+) support for asymmetric traffic
            * (-) mix of uplink and downlink interference on single band
            * Examples: DECT, WLAN, UMTS (TDD), TD-LTE

### TDMA: Aloha/slotted aloha

random, distributed (no central arbiter), time-multiplex, Slotted Aloha additionally uses time-slots, sending must always start
at slot boundaries

### TDMA: Demand Assigned Multiple Access (DAMA)

* Channel efficiency only **18% for Aloha, 36% for Slotted Aloha**
* Reservation can increase efficiency to **80%**
* Idea: a sender reserves a future time-slot / sending within this reserved time-slot is possible without collision
* Disadvantage: reservation causes higher delays
* Applications:
    * typical scheme for satellite links (long round-trip-times)
    * application to packet data, e.g. in GPRS and UMTS
* Examples for reservation algorithms:
    * Explicit Reservation (Reservation-ALOHA)
    * Implicit Reservation (PRMA)
    * Reservation-TDMA

### TDMA: DAMA - Explicit Reservation based on Aloha

### TDMA: DAMA - Implicit Reservation

### TDMA: DAMA - Reservation-TDMA

### TDMA: Multiple Access with Collision Avoidance (MACA)

* Motivation: deal with hidden terminals without a base station (central controller)
* Idea: use short signaling packets for collision avoidance
    * RTS (request to send): a sender requests the right to send from a receiver with a short RTS packet before it sends a data packet
    * CTS (clear to send): the receiver grants the right to send as soon as it is ready to receive
    * all other stations listen to the signal
* Signaling packets contain
    * sender address
    * receiver address
    * packet size
* Collisions are mainly limited to the transmission of RTS signals which
is small compared to the data transmission
* Disadvantage: overhead where data packets are small

### TDMA: MACA variant: DFWMAC in IEEE 802.11

* ACK: positive acknowledgement
* NAK: negative acknowledgement
* RxBusy: receiver busy

![DFWMAC](./assets/DFWMAC.png)

### TDMA: Polling mechanisms

If one terminal can be heard by all others, this “central” terminal (e.g.
a base station) can poll all other terminals according to a certain
scheme

now all schemes known from fixed networks can be used (typical
mainframe - terminal scenario, round-robin, random, reservationbased)

Application to Bluetooth and 802.11 (possible access function)

### TDMA: ISMA (Inhibit Sense Multiple Access)

### CDMA access method  (Code Division Multiple Access)

### Summary

![DMA](./assets/DMA.png)

* central control of access to medium:
    * joint common view on resource situation simplifies coordination
    * but registration and/or static configuration of system needed
    * still need to coordinate the initial, random access of mobiles to the system
* decentralized control of access to medium:
    * disjoint & inconsistent views on shared medium (hidden & exposed terminal)
    * distributed arbitration scheme needed to minimize collisions
    * solution: RTS/CTS - to derive a joint common view on resource usage

## IEEE 802.11 (Layer 2)

### 802.11: Architecture of an Infrastructure Network

![AIN](./assets/AIN.png)

### 802.11: Architecture of an Ad-hoc Network

![AAN](./assets/AAN.png)

### IEEE Standard 802.11

![802](./assets/802.png)

#### 802.11

* Layers and Functions
* Physical Layer
* MAC
* CSMA/CA Access Method
* PCF (Polling)
* MAC Management

#### WLAN: IEEE 802.11b

* Data rate
    * 1, 2, 5.5, 11 Mbit/s, depending on SNR
    * User data rate max. approx. 6
Mbit/s
* Transmission range
    * 300m outdoor, 30m indoor
    * Max. data rate ~10m indoor
* Frequency: Free 2.4 GHz ISM-band
* Security: Limited, WEP insecure, SSID
* Cost: 25€ adapter, 100€ base station
* Availability: Many products, many vendors
* Connection set-up time: Connectionless/always on
* QoS: Typ. best effort, no guarantees
(unless polling is used, limited
support in products)
* Manageability: Limited (no automated key
distribution, sym. encryption)
* Advantage: many installed systems, lot of experience, available worldwide, free ISM band, many vendors, integrated in laptops, simple system
* Disadvantage: heavy interference on ISM band, no service guarantees, slow relative speed only

#### WLAN: IEEE 802.11g

* Data rate
    * 6, 9, 12, 18, 24, 36, 48, 54 Mbit/s, depending on SNR
    * User throughput (1500 byte packets): 5.3 (6), 18 (24), 24 (36), 32 (54)
    * 6, 12, 24 Mbit/s mandatory
* Transmission range: 150m outdoor, 20m indoor 54 Mbit/s up to 6 m
* Frequency
    * 2.412~2.472GHz (Europe ETSI)
    * 2.457~2.462GHz (Spain)
    * 2.457~2.472GHz (France)
* Security: Limited, WEP insecure, SSID
* Cost: 50€ adapter, 200€ base station
* Availability: Some products, some vendors
* Connection set-up time: Connectionless/always on
* Quality of Service: Typ. best effort, no guarantees (same as all 802.11 products)
* Manageability: Limited (no automated key distribution, sym. encryption)
* Advantage: free ISM band, compatible with 802.11b standard
* Disadvantage: heavy interference on ISM band, no service guarantees

#### WLAN: IEEE 802.11a

* Data rate
    * 6, 9, 12, 18, 24, 36, 48, 54 Mbit/s,
depending on SNR
    * User throughput (1500 byte packets):
5.3 (6), 18 (24), 24 (36), 32 (54)
    * 6, 12, 24 Mbit/s mandatory
* Transmission range
    * 100m outdoor, 10m indoor
e.g. 54 Mbit/s up to 5 m, 48 up to 12
m, 36 up to 25 m, 24 up to 30m, 18
up to 40 m, 12 up to 60 m
* Frequency: Free 5.15-5.25, 5.25-5.35, 5.725-
5.825 GHz ISM-band
* Security: Limited, WEP insecure, SSID
* Cost: 100€ adapter, 200€ base station
* Availability: Some products, some vendors
* Connection set-up time: Connectionless/always on
* Quality of Service: Typ. best effort, no guarantees (same as all 802.11 products)
* Manageability: Limited (no automated key distribution, sym. encryption)
* Advantage: fits into 802.x standards, free ISM band, available, simple system, uses less crowded 5 GHz band
* Disadvantage: stronger shading due to higher frequency, no service guarantees

### WLAN: IEEE 802.11h     * Regulatory Details

* 4 frequency bands:
    * 5.150 - 5.250 GHz
        * 4 usable channels (100 MHz)
        * indoor only
        * max. 30mW EIRP (.11a)
        * TPC (Transmit Power Control) max.
    60mW EIRP
        * combined TPC and DCS/DFS (Dynamic Channel Frequency Selection) max. 200mW EIRP
        * Turbo Mode: combination of two
    carriers to reach 108 Mbps
    * 5.250 - 5.350 GHz
        * 4 usable channels
        * TPC, DCS/DFS mandatory
    * 5.470 - 5.725 GHz
        * indoor and outdoor
        * max. 1W EIRP
        * disallowed in US
        * not supported by all chipsets
    * 5.725 - 5.825 GHz --> **disallowed in Germany**

### WLAN: IEEE 802.11     * Extensions and developments

* 802.11d: Regulatory Domain Update
* 802.11e: MAC Enhancements - QoS
* 802.11f: Inter-Access Point Protocol (IAPP)
system
* 802.11h: Spectrum Managed 802.11a (DCS, TPC)
* 802.11i: Enhanced Security Mechanisms
* 802.11j: MAC and PHY Specifications for Operation in 4.9-5 GHz Band in Japan
* **802.11n**: Throughput enhancement to 108-320 Mbps
* ***NO*** IEEE 802.11o
* IEEE 802.11p - WAVE - Wireless Access for the Vehicular Environment (such as ambulances and passenger cars)
* IEEE 802.11r - Fast roaming Working "Task Group r"
* IEEE 802.11s - ESS Extended Service Set Mesh Networking
* IEEE 802.11T - Wireless Performance Prediction (WPP) - test methods and metrics Recommendation
* IEEE 802.11u - Interworking with non-802 networks (for example, cellular)
* IEEE 802.11v - Wireless network management
* IEEE 802.11w - Protected Management Frames
* IEEE 802.11y - 3650-3700 Operation in the U.S.

https://en.wikipedia.org/wiki/IEEE_802.11

## Mobility Management (Layer 3)

## TCP/IP

## Self-Organization

## Quality of Service

## Ad Hoc Networks

### Mobile Ad Hoc Networks (MANETs)

* Spontaneous federation of wireless devices
    * No infrastructure (base station / access point,no backbone
    * Devices can be mobile
* Packet-based forwarding
    * Each device must serve as a router
    * Routes between devices can span multiple hops
* Ad hoc networks are self organizing
    * No central components
* Advantages
    * Easy and cheap deployment
        * E.g. using 802.11 in license free ISM band (2.4 GHz)
    * Reduced transmission power
    * Robust to component failures
* Application: where there is no access to infrastructure
    * Military applications
        * Groups of soldiers, tanks, planes...
    * Civil applications
        * Conferences, exhibitions, meetings, lectures, gaming, …
    * Car-to-car-communication, network for taxis, police, …
        * Vehicular Ad Hoc NETworks (VANETs)
    * Extension of cellular networks
* Disaster recovery (Int. Graduate School on Mobile Communications)
    * After crash of infrastructure (e.g. telephone network after earthquake)
    * Rescue

## Cognitive Radio Networks

## Overview on cellular systems

---
# Cellular Communication Systems

## Review of Mobile communication basics

## Overview on GSM and GPRS

## UMTS architecture

(mobility management, connection and session management, wideband CDMA,
management of radio resources

## UMTS radio access network

## High-Speed Packet Access (HSPA)

## Long-Term Evolution (LTE)

## System Architecture Evolution (SAE)

## Self-organization in LTE