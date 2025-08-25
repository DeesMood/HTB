To assess the security of ML-based systems, it is essential to have a deep understanding of the underlying components and algorithms.

## What is Red Teaming?

Traditionally, when discussing security assessments of IT systems, the most common type of assessment is a `Penetration Test`. This type of assessment is typically a focused and time-bound exercise aimed at discovering and exploiting vulnerabilities in specific systems, applications, or network environments. Penetration testers follow a structured process, often using automated tools and manual testing techniques to identify security weaknesses within a defined scope. A penetration test aims to determine if vulnerabilities exist, whether they can be exploited, and to what extent. It is often carried out in isolated network segments or web application instances to avoid interference with regular users.

Commonly, there are two additional types of security assessment: `Red Team Assessments` and `Vulnerability Assessments`.

![](Pasted%20image%2020250825122212.png)

`Vulnerability assessments` are generally more automated assessments that focus on identifying, cataloging, and prioritizing known vulnerabilities within an organization's infrastructure.

The third type of assessment, and the one we will focus on throughout this module, is a `Red Team Assessment`. This describes an advanced, adversarial simulation where security experts, often called the `red team`, mimic real-world attackers' tactics, techniques, and procedures (TTPs) to test an organization's defenses. The red team's goal is to exploit technical vulnerabilities and challenge every aspect of security, including people and processes, by employing social engineering, phishing, and physical intrusions. Red team assessments focus on stealth and persistence, working to evade detection by the defensive `blue team` while seeking ways to achieve specific objectives, such as accessing sensitive data or critical systems. This exercise often spans weeks to months, providing an in-depth analysis of an organization's overall resilience against sophisticated threats.
## Red Teaming ML-based Systems

Unlike traditional systems, ML-based systems face unique vulnerabilities because they rely on large datasets, statistical inference, and complex model architectures. Thus, red team assessments are often the way to go when assessing the security of ML-based systems, as many advanced attack techniques require more time than a typical penetration test would last.


