# DLR Statuses

(Delivery Report Status)

Unless otherwise specified, all of API endpoints will return the information that you request in the JSON data format.

Standard Response Format

Delivery Reports
Below is a description of each delivery report

| Status                 | Description                                                                                                                                                                                                                                                                          |     |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --- |
| DeliveredToTerminal    | Delivered to device                                                                                                                                                                                                                                                                  |
| AbsentSubscriber       | Subscriber has not been able to connect to the network for the last 24 hrs. In some cases (airtel) customers have to lock their phone to 3G only to be able to receive messages. This is an issue specific to them                                                                   |
|                        |
| Delivery Impossible    | Number has been ported to another telco or has temporarily been deactivated by SP. Or the number has been inactive for a long period of time. In some cases the telco has blocked delivery due to violation of policy. ie. Sending marketing message beyond 6PM and earlier than 7am |
| SenderName Blacklisted | The customer has explicitly blocked messages from the sender id. or opted out of receiving promotional messages                                                                                                                                                                      |
| Invalid Source Address | The sender ID does not exist on the telco                                                                                                                                                                                                                                            |
