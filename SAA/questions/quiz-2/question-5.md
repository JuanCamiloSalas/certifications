[![](https://img.shields.io/badge/<_Prev-555555?style=for-the-badge)](./question-4.md)
[![](https://img.shields.io/badge/Index-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./question-6.md)

# Quiz 2 · Question 5 / 20

> Domain: **Secure**

An EC2-hosted API sits behind a security group that allows inbound TCP 443 from `0.0.0.0/0`. An engineer then tightened the security group's outbound rules to deny all egress except TCP 443 to a single partner CIDR. A penetration tester reports that external clients can still complete HTTPS requests and receive responses. The team asks why responses still succeed even though there is no outbound rule allowing the clients' ephemeral ports. What is the correct explanation?

- **A)** Security groups are stateful, so response traffic for an allowed inbound connection is automatically permitted regardless of outbound rules
- **B)** The default outbound allow-all rule is still in effect and overrides the tightened rules
- **C)** Security groups are stateless, so a matching ephemeral-port outbound rule must already exist
- **D)** The subnet's network ACL is what permits the ephemeral response traffic

*Anota tu respuesta y pásamela en el chat como `2.5: X`. Avanza con **Next >**.*

---
[![](https://img.shields.io/badge/<_Prev-555555?style=for-the-badge)](./question-4.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./question-6.md)
