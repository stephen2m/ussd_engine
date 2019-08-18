==============
How ussd works
==============

Unstructured Supplementary Service Data (USSD) is a protocol used by GSM cellphones to
communicate with their service provider's computers.
USSD can be used for WAP browsing, prepaid callback service,
mobile money services, location-based content services,
menu-based information services, or even as part of configuring the phone on the network.

.. image:: ./img/how_ussd_works.jpg

From the diagram above, a request is sent from a mobile phone to a telecom network
such Vodafone.

The USSD Gateway (telecom) then sends the request to your USSD application
(i.e where we have the business logic to determine the menu to serve on receiving the incoming request.)

Your USSD application then responds to the request, and the USSD gateway displays your content to the user

Below is a another diagram to help understand the concept

.. image:: ./img/another_example_how_ussd_works.gif

================
Why USSD Airflow
================

Before I explain why we need USSD Airflow lets first look at one example of a use-case

Example Menu-Driven USSD Application
-------------------------------------
One could decide to develop a mobile-initiated “Balance Enquiry and
Top Up” application using USSD signaling, enabling a mobile user to
interact with an application via the user’s handset, in order to
view his/her current mobile account balance and top up as needed.

An example of such an application could be as follows:

#. A mobile user initiates the “Balance Enquiry and Top Up” service by dialing the USSD string defined by the
   service provider; for example, *123#.

#. The USSD application receives the service request from the user and responds by sending the user a menu of options.

#. The user responds by selecting a “current balance” option.

#. The USSD application sends back details of the mobile user’s current account balance and also gives the option to top up the balance.

#. The user selects to top up his/her account.

#. The application responds by asking how much credit to add?

#. The mobile user responds with the amount to add.

#. The USSD application responds by sending an updated balance and ends the session.

The figure below shows an example of the MAP/TCAP
message sequence required to realize the data transfers between
a mobile user’s handset and the USSD application to implement the
“Balance Enquiry and Top Up” service described above.

.. image:: ./img/example_of_menu_driven_ussd_application.png


Why ussd_airflow?
--------------------------
As you have seen in the previous section your USSD application is responsible for the content displayed.

Suppose you want to change the wording in one the USSD screens you are displaying
to the user, what is involved in most cases, or rather, all cases is that you
make a change in your code and deploy, and that's peanuts for most developers

The problem is once you start having many USSD screens and multiple USSD application
and many requirements of changing USSD screen.

The once simple task becomes overwhelming and would probably need you to think
of a way that non-developers would change the USSD content without a developer being involved.
This is where **ussd aiflow** comes in, providing an interface for users to change
USSD screens without code changes