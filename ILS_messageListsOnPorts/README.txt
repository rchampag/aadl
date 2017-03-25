Modeling the Instrument Landing System (ILS) Receiver in AADL
=============================================================

This folder contains an AADL project created with OSATE 2.2.0. The purpose
of this AADL project is to determine if avionics systems using ARINC 429 data
buses can be modeled in AADL, in such a way that ARINC 429 interface informa-
tion can be captured in the AADL model, and the system's Interface Control 
Document (ICD) can then be automatically generated from the AADL model.

To establish the feasibility of our goal, we attempt to model an Instrument
Landing System (ILS) receiver, as per ARINC specification 710-10. We wish
to at least capture enough information in the model to be able to perform some
types of automatic validation. For example, when we interconnect two or more 
such systems, we wish to verify that an ARINC 429 output port on system A 
generates the messages expected by system B ARINC 429 input port at the other
end of the connection.

Dependencies and important note
===============================

The project has the following dependencies :

  - OSATE 2.2.0

This project uses a modified version of the OSATE ARINC429 property set. We
renamed this property set ARINC429_mod.aadl, and included it in the
project's AADL packages. This is not ideal, but appeared to us to be the simplest
solution to share it with others. We are likely to add properties as we model
more ARINC 429 messages. For now, the property set allows us to capture most
properties we need to model the messages relevant to the ILS receiver.

Integrating the ILS with other systems
======================================

Files required:

  - ARINC429_mod.aadl
  - ILS_04.aadl
  - ILS_control_panel.aadl
  - Integrated_system.aadl

In this attempt, we simply try to connect a second system to the ILS receiver.
We chose the simplest possible solution we saw, the ILS control panel, which
basically allows the pilot to specify the frequencies on which the ILS receiver
should tune itself. This results in an ARINC 429 message ("ILS frequency") sent
from the control panel's ARINC 429 output port to one of the ILS receiver's
ARINC 429 input ports. We intend to use this example to validate that messages
are modeled correctly and allow us to perform the validatSion we aim.

The Data components capturing message types are actually not needed in this
version. This attempt uses a solution proposed by Brian Larson, consisting in
specifying message "names" in a property containing a list of enumerations,
and then bind this property directly to data ports. As the data ports have no
classifiers, the type matching is "OK". Eventually, an analysis tool would
navigate the list of enumerations on both ends of each connection, and then
navigate the Data components based on the names in the lists of enumerations
bound to ports.

This solution works well for a small number of message types. However, it is
not clear what would be the right way to maintain a list (or lists) of message
types, if we were for example to model all possible ARINC 429 messages.

By Roger Champagne, P.Eng, Ph.D.
Ecole de technologie superieure, Montreal, Canada
+1-514-396-8825
roger dot champagne at etsmtl dot net
Updated 2017-Feb-24