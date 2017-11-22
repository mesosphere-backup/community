#Introduction
The DC/OS overlay is a network control plane within DC/OS that allows
users to create virtual networks during install time. Once these
virtual networks have been created, schedulers in DC/OS can launch
Mesos and Docker containers on these virtual networks to get an
out-of-the box IP-per-container solution.

The DC/OS overlay builds on top of the CNI and CNM support that exists
in DC/OS. Using CNI and CNM, it builds a VxLAN-based overlay network
to allow Mesos and Docker containers to talk to each other over the
same virtual network. 

# Owners
[![](../../images/GitHub-Mark-32px.png)](https://github.com/asridharan) Avinash Sridharan<br>
[![](../../images/GitHub-Mark-32px.png)](https://github.com/jieyu) Jie Yu<br>
[![](../../images/GitHub-Mark-32px.png)](https://github.com/sargun) Sargun Dhilon<br>


# Design
You can view and comment on the design of the DC/OS overlay on the
[Google doc](https://goo.gl/49zAFr) or the [online
version](https://goo.gl/K8el10) of this
document.

# Components
The DC/OS overlay relies on various services and modules within the
DC/OS repo. Listing them here to capture their dependencies. More
details of how these components come together to create the DC/OS
overlay can be found in the design doc.

* **DC/OS overlay modules**: https://github.com/dcos/dcos-mesos-modules/tree/master/overlay
  These are the master and the agent modules used for subnet
  allocation for overlay networks. 

* **Navstar**: https://github.com/dcos/navstar
  This the overlay orchestrator. The navstar service runs on each
  agent. It is responsible for learning agent membership of the
  overlay, and the subnets allocated to each agent that is part of the
  overlay. It does so using a GOSSIP protocol. Once it learns the
  subnets in each agent that is part of the overlay it creates the
  VxLAN backend (VTEP devices) and installs the routes on the agent to
  create the overlay fabric on which Mesos and Docker containers can
  run.
  


