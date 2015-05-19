# Introduction #

CaM (Command and Monitor) Interface is created to be a remote drone interface for user willing to connect a drone.

# Details #

Principle function of the interface:

**Client-Drone connection**

- a client lunch the "CaM Interface" on any PC with internet access.
- login procedure (mode=5)
- three lists of accessible Drones is presented after the login procedure
  1. Drones you reserved for connection       (mode=11)
  1. Drones you are owner or administrator of (mode=6)
  1. Drones you are a groupe member of        (mode=7)
- after you select one Drone in any list, you choose the interface mode
  1. Enduser CaM (drone connection)
  1. Interbase CaM (make any serial USB drones internet accessible)

**Enduser CaM**
- after choosing the interface mode, the CAM proceed following
  1. gets the IP address and port of the drone (mode=1 and mode=2)
  1. click on "Connect" to confirm you are ready for drone connection
- Drone accept the connection
- Drone wait 2 sec for username and password to confirm the access is permitted
- Drone ask server via the same login procedure (mode=5)
- if the Drone is reserved, Drone ask server the start and finish timestamps of reservation
-