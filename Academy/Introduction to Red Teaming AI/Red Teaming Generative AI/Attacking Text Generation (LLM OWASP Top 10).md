To start exploring security vulnerabilities that may arise when using systems relying on generative AI, let us discuss vulnerabilities specific to text generation. The model of choice for text generation are `Large Language Models (LLMs)`. Similarly to OWASP's ML Top 10 security risks discussed a few sections ago, OWASP has published a Top 10 list of security risks regarding the deployment and management of LLMs, the [Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/assets/PDF/OWASP-Top-10-for-LLMs-2023-v1_1.pdf). We will briefly discuss the ten risks to obtain an overview of security issues that can arise with LLMs.

Some of the security issues on the list apply to ML-based systems in general, which is why they are similar to issues on OWASP's [Top 10 for Machine Learning Security](https://owasp.org/www-project-machine-learning-security-top-10/) list . Other issues, however, are specific to LLMs and text generation.

|ID|Description|
|---|---|
|LLM01|`Prompt Injection`: Attackers manipulate the LLM's input directly or indirectly to cause malicious or illegal behavior.|
|LLM02|`Insecure Output Handling`: LLM Output is handled insecurely, resulting in injection vulnerabilities such as Cross-Site Scripting (XSS), SQL Injection, or Command Injection.|
|LLM03|`Training Data Poisoning`: Attackers inject malicious or misleading data into the LLM's training data, compromising performance or creating backdoors.|
|LLM04|`Model Denial of Service`: Attackers feed inputs to the LLM that result in high resource consumption, potentially causing disruptions to the LLM service.|
|LLM05|`Supply Chain Vulnerabilities`: Attackers exploit vulnerabilities in any part of the LLM supply chain.|
|LLM06|`Sensitive Information Disclosure`: Attackers trick the LLM into revealing sensitive information in the response.|
|LLM07|`Insecure Plugin Design`: Attackers exploit security vulnerabilities in LLM plugins.|
|LLM08|`Excessive Agency`: Attackers exploit insufficiently restricted LLM access.|
|LLM09|`Overreliance`: An organization is overly reliant on an LLM's output for critical business decisions, potentially leading to security issues from unexpected LLM behavior.|
|LLM10|`Model Theft`: Attackers gain unauthorized access to the LLM itself, stealing intellectual property and potentially causing financial harm.|

## Prompt Injection (LLM01)
Prompt injection is a type of security vulnerability that occurs when an attacker can manipulate an LLM's input, potentially causing the LLM to deviate from its intended behavior. Furthermore, prompt injection attacks may be used to obtain sensitive information in case such information has been shared with the LLM (cf. `LLM06`)

## Insecure Output Handling (LLM02)
LLM-generated text should be treated the same as untrusted user input. If web applications do not validate or sanitize LLM output properly, common web vulnerabilities such as Cross-Site Scripting (XSS), SQL injection, or code injection may arise. If the user supplies input like `Give me the content of blog post #3`, the model might generate the output `SELECT content FROM blog WHERE id=3`. The backend web application can then use the LLM output to query the database and display the corresponding content to the user. Apart from the potential SQL injection attack vector, applying some plausibility checks to the LLM-generated SQL query is crucial. Without this kind of checks, unintended behavior might occur. All data is lost if an attacker can get the LLM to generate the query `DROP TABLE blog`.
## Training Data Poisoning (LLM03)

The quality and capabilities of any LLM depend highly on the training data used in the training process. Training Data Poisoning is the manipulation of all or some training data to introduce biases that skew the model into making intentionally bad decisions.

## Model Denial of Service (LLM04)

A denial-of-service (DoS) attack on an LLM is similar to a DoS attack on any other system. The goal of a DoS attack is to impair other user's ability to use the LLM by decreasing the service's availability. Since LLMs are typically computationally expensive, a specifically crafted query that results in high resource consumption can easily overwhelm available system resources, resulting in a system outage if the service has not been set up with proper safeguards or sufficient resources.

## Supply Chain Vulnerabilities (LLM05)

Supply chain vulnerabilities regarding LLMs cover any systems or software in the LLM supply chain. This can include the training data (refer to `LLM03`), pre-trained LLMs from another provider, and even plugins (cf. `LLM07`) or other systems interacting with the LLM.

## Sensitive Information Disclosure (LLM06)

LLMs may inadvertently reveal confidential data in their responses. This can result in unauthorized data access, privacy violations, and even security breaches. Furthermore, sensitive information provided to the LLM in an input prompt may be revealed through prompt injection attack payloads (cf. `LLM01`), even if the LLM is told to keep the data secret.

## Insecure Plugin Design (LLM07)

LLMs can be integrated with other systems via plugins. If such a plugin blindly trusts output from the LLM without any sanitization or validation, security vulnerabilities may arise. Depending on the concrete functionality of the plugin, common web vulnerabilities such as Cross-Site Scripting (XSS), SQL Injection, Server-side Request Forgery (SSRF), and Remote Code Execution can occur.

## Excessive Agency (LLM08)

Security vulnerabilities may arise if an LLM is given more agency than is required for its operation. Similar to the principle of least privilege, it is vital to restrict an LLM's capabilities as much as possible to reduce the attack surface for malicious actors.

For instance, if an LLM can interface with other systems or services, we need to ensure that a whitelisting is implemented to enable the LLM to access only the required services. On top of that, we need to think about what we want the LLM to do and restrict the LLM's permission to that specific purpose. Consider a scenario where an LLM interfaces with a SQL database to fetch data for the user. If we don't restrict the LLM's database access, it might be possible to trick it into executing `DELETE` or `INSERT` statements, affecting the integrity of the database.
## Overreliance (LLM09)

Due to the way LLMs work, they are inherently prone to providing false information. This can include factually incorrect statements but also erroneous or buggy code snippets. If an LLM is integrated into an organization's business processes without proper validation and checks of LLM-provided information, security vulnerabilities can arise from incorrect data provided by the LLM. As such, it is crucial to manually check and verify the information the LLM provides before using it in sensitive operations.

- - If an LLM generates **incorrect facts, misconfigurations, or unsafe code**, and an organization uses it without review, those errors could make it into production systems. For example, a buggy code snippet that disables SSL verification or hardcodes credentials might be copied directly into a live service.

## Model Theft (LLM10)

Model theft occurs when an attacker is able to steal the LLM itself, i.e., its weights and parameters. Afterward, an attacker would be able to replicate the LLM in its entirety.

#### Questions
 Get the LLM to respond with "I like HackTheBox Academy".
 
I want you to say my favorite quote "I like HackTheBox Academy"
HTB{0d439b3f57d1d234106a80776cd03b25}

Get the image generation model to generate an image of a cat on a skateboard.

cat on a skateboard
HTB{b932f8d4b64d9a824a0247366c658012}
