Its security requirements help provide assurance that payment software is designed, developed, and mantained in a manner that <mark style="background: #FFB8EBA6;">protects payment transactions</mark> and data, minimizes vulnerabilities, and defends against attacks

# PCISSC

>[!INFO] What is?
>
>The PCI Security Standards Council (PCI SSC) is one of two standards that are part of the PCI Software Security Framework

^d952cc

## Versions

| Date | Version | Description                                                          |
| ---- | ------- | -------------------------------------------------------------------- |
| 2019 | 1.0     | Initial                                                              |
| 2021 | 1.1     | Support the Secure SLC Program expansion and the introduction of TSM |
| 2022 | 1.2     | Support the introduction of the WSM                                  |

- TSM => Terminal Software Module
- WSM => Web Software Module

## Concepts

>[!INFO] **Abstraction Layer**
>
>Process to hide implementation details from user
>Each layer can access the feature below it, but no layer can access layers above it

- Abstraction can improve code flexibility and maintenance, it can also pose problems to incident handling and forensics
- Entities should understand the complex hierarchies of abstraction layers, such as in many cloud-computing environments, and understand the different ways in which digital is lost due to abstraction layers.

>[!WARNING] Adversarial testing
>
>Methods or techniques used during a software evaluation to force the software to behave in unintended ways or to bypass **software security controls**

>[!INFO] Application Program Interface
>
>Series of communication protocols, subroutines and tools for building software that allows 2 applications to interact with each other

>[!HELP] Assessor
>
>Individuals and companies approved by PCI SSC to performance security assessments against PCI standards, including those standards associated with [[#^d952cc|SSF]]
>

>[!SUCCESS] Big number libraries
>
>Library functions that allow for the large numbers often used in cryptography to be processed and stored correctly (with needed levels of precision) in languages that may otherwise default to a less precise format.

>[!DANGER] [[CWE - Common Weakness Enumeration|Common Weakness Enumeration]]
>
>Category system for software weaknesses and vulnerabilities

>[!WARNING] Confidential data
>
>Form of sensitive data that explicitly requires protection from unauthorized disclosure

- CHD - Cardholder Data
- SAD - Sensitive Authentication Data
- Private cryptographic keys

>[!HELP] Control objective
>
>The high-level security that must be met

>[!DANGER] Critical assets
>
>Sensitive data, functions and resources. If those are exposed, misused, altered or disabled, could impair the software's ability to function properly or meet its security objectives

>[!SUCCESS] Data element
>
>Term used to represent a single piece of information or column

>[!IMPORTANT] EMVCo
>
>A global technical body owned by American Express, Discover, JCB, Mastercard, UnionPay, and Visa that facilitates the worldwide interoperability and acceptance of secure payment transactions by managing and envolving the EMV specifications and related testing processes

 >[!Entropy]
 >
 >Term used in cryptographic operations to represent the measure of the unpredictability of a random seed value.
 >
 >Measured in bits
 >Higher means less predictable
 >**Used to measure the security strength of cryptographic keys**

>[!EXAMPLE] Execution/Runtime Environment
>
>Hardware, networks, operating systems, databases, storage systems, and services required by the software to function as intended
>

>[!abstract] External communications
>
>Wireless, Local-area network, or a public domain protocol or a security protocol to transport data. 

This includes, but it is not limited to, bluetoooth, wi-fi, cellular, or Ethernet, and a serial P2P that is wireless or through a hub, switch, or other multiport device.

>[!help] Federal Information Processing Standard 
>
>A standard that provides four increasing, qualitative levels of security and is related to the Cryptographic Module Validation Program, which provides for vendors to submit products to a laboratory to validate cryptographic modules to the [[Federal Information Processing Standard|FIPS 140-2]]] standard and other cryptographic-based standards.

Products validated as conformation with it are accepted by the U.S. and Canadian federal agencies for the protection of sensitive information (United States) or designated information (Canada)







 
 






>

































