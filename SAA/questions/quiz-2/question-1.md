[![](https://img.shields.io/badge/<_Index-555555?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Index-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./question-2.md)

# Quiz 2 · Question 1 / 20

> Domain: **Secure**

A holding company manages 60 AWS accounts under AWS Organizations, grouped into OUs by business unit. Auditors require that, in every account within the "Regulated" OU, no principal — including users who hold the `AdministratorAccess` managed policy — can disable AWS CloudTrail, delete the central log bucket, or remove the account from the organization. The control must be enforced centrally and keep working for IAM roles created in the future. Which approach meets the requirement with the least ongoing effort?

- **A)** Attach an IAM permissions boundary that denies those actions to every role in each account
- **B)** Create a Service Control Policy denying those actions and attach it to the "Regulated" OU
- **C)** Add an explicit `Deny` in an IAM policy attached to every user and role in those accounts
- **D)** Enable AWS Config rules that automatically re-enable CloudTrail whenever it is turned off

*Anota tu respuesta y pásamela en el chat como `2.1: X`. Avanza con **Next >**.*

---
[![](https://img.shields.io/badge/<_Index-555555?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./question-2.md)
