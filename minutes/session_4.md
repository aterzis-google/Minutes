## Minutes: Session 4 Sending Data Down for Network Management Benefits
* Date: 24th September
* Time: 16:15 - 17:30
* Chair: Dan Druta, ATT
* Minute Taker: Phil Roberts
* Panel:
  * Dirk Kutscher ZTH
  * Chunshan Xiong Huawei
  * Kevin Smith Vodafone

### Introduction (Dan Druta)
* What are the use cases?  What are the solutions applied?  Why are current solutions broken with e2e encryption?

### Dirk Kutscher
* Common theme was cooperative traffic management.  
* Previous attempts: UPCON
* Current proposal: throughput guidance solution architecture
* Two main concerns from Dirk's paper: meaningful capacity sharing; reacting correctly to wireless link layer conditions
* Traffic mgmt requirements: application independence (permission-less innovation), efficiency and effectiveness, generality, privacy-friendly
* CONEX principles: congestion marking/loss, TCP feedback, senders and receivers can see conditions along the route with some lessons learned: means to incentivize sender adaptivity, IP not designed for in-band management, security needs further thoughts
* SPUD
* Extensible and Efficient Traffic Mgmt:  allows for encrypted traffic, build on SPUD, design for flexibility, minimal info to overcome PII; re-think capacity sharing

### Chunshan Xiong
* Use Cases for Encrypted Traffic
 * For use cases we're missing priority in services.  Operator can eject things with less priority: emergency services trump everything; voice trumps data.
 * Middle boxes are used for service data flow for different content types.  Treatment is very different for the different types.
* Mobile network can manage different applications based on the resources available.
* 3GPP has defined PCC-QoS mechanism to support these applications
 * How Encryption Breaks all this:
  * no matched QoS for encrypted services
  * if there is a lack of radio resources, you may release the wrong services
  * during handover can't well adapt encrypted services
  * hard to detect different service data flow
  * middle box services can't work for the encrypted service

### Kevin Smith
* Why does it make sense for apps to send data to networks?  
 * Not sure that it does, but if so, just info about the flow (the bare minimum); test whether it works and brings a benefit, but also whether it is an improvement on heuristics
* Finally, a lot of mobile data traffic is sent by peering partners.

### Discussion

* __Ted Hardie:__ in the use cases, the critical use case was that in the presence of encryption you can't assign an SDF and couldn't match it to resources.  What is the minimum data you need, to be able to do this?
* __Dan Druta:__ trying to put as many shapes as possible in a fixed rectangle (analogy for what goes on in the radio network); all we really need to know is the shapes, not what is inside them
* __Ted Hardie:__ what are those shapes then?
* __Kevin Smith:__ even a flavor of latency vs. bandwidth - do you prefer one over the other?
* __Dirk Kutscher:__ depends on the incentive framework around it.
* __Joe Hildebrand:__ Ted's question reminds a lot of Jana's questions in the last panel.  The characterization bits in one direction may be similar to ones in the other direction.  And if we could think about the control loops based on inputs in this could help.
* __Dan Druta:__ direction matters
* __Mark Watson:__ there is an assumption that applications need to declare the QoS they need.  We've been talking about this for 20 years and it's never happened.  Let's just give up on that.  Start with 1 bit of information and see if we get anything out of that.
* __Jana Iyengar:__ low latency is not a property that only certain types of applications deserve (AQM mechanisms).  Then all the applications benefit from the low latency.  The problem them becomes one of network efficiency.  Want to encourage this strongly.  Does not require applications to indicate this.  None of these bits every get set.  We can solve these problems in the network without setting these bits.
* __Kevin Smith:__ how do AQM and the RRC interact effectively?  There is a gap where they are not aware of each other.
* __Jana Iyengar:__ would like to see work on this item.
* __Christian Huitema:__ if we look at the separate between application and network, we have relied on the application to share the bandwidths between themselves in a way that is fair.  This is not natural.  The network could handle this by making it so apps don't have to worry about other network users.
* __Joe Hildebrand:__ to model the kernel on my local box as a middlebox has helped me understand some of these things
* __Patrick McManus:__ this is a bad idea.  The dangers greatly outweigh the potential upside.  The notion of enabling traffic mgmt without dpi is very appealing.
* __Benoit Claus:__ the place we do this is in branch office.  We do dpi to optimize QoE in offices.
* __Jana Iyengar:__ try FQ_codel at home.
* __Chunsan Xiong:__ end users want their service, they don't know anything about QoS.  Business users want to just buy this.
* __Jari Aarko:__ not sure I agree with Patrick.  Not sure I don't.  Want to oppose the argument.  Today we have DPI and heuristics, next year app providers will try to confuse this.  Not sure that is true.
* __Diego Lopez:__ is important that this be done in an open way. 
* __NAME (Huawei):__ we need some conditions that the ASPs have some agreements with the network provider already
* __Dirk Kutscher:__ is it required to do this for a mobile network
* __Chunsan Xiong:__ this agreement is achieved by the user subscription
* __Dan Druta:__ QoS and resource usage are two different things.  If we have a relationship already, things are much easier.  The hard problem is dealing with best effort traffic.
* __Kevin Smith:__ NN is a consideration.
* __NAME:__ AQM and latency, not as true in mobile.  The capacity changes very so dynamically.  FQ-codel, if your throughput is stable, it's pretty amazing; even in my home though there are lots of changes.
* Spencer Dawkins:__ 20 or 30 people at IETF talking about problems with their kids playing games at home.  Do the "I pay the bills thing?"
* __Ted Hardie:__ if it's a 1 bit thing, encouraging people to release the one bit, so everyone does it.  If everyone tells you what tetris piece is coming down, then you get the herd minimality benefit.  RT critical or not may not be that helpful.  What's the simplest way to make sure that reaches the right place?  Is it the enodeB or something deeper.
* __Kevin Smith:__ will go back to the access specialists and find out where.
* __Chunsan Xiong:__ need some resource reservation to help with who calls you
* __Jana Iyengar:__ FQ-codel is not a Google product, being defined in IETF.  Should be built into equipment rather than requiring end users to use it.  Mobile folks should be looking at it seriously.
* __Mark Watson:__ previous comments against QoS classification was to say there is no value of info from the device to the network, the model is distracting us
* __Christian Huitema:__ ATM has died.  Because all that stuff became irrelevant once the best effort level of the I was good enough that all those apps worked anyway.
