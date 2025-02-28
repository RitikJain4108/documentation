# FTM

## Overview
Foundational Trust Module (FTM) is created using a secure microprocessor capable of performing all required biometric processing and secure storage of keys. The foundational device trust would satisfy the below requirements.

* The module has the ability to securely generate, store and process cryptographic keys.
* Generation of asymmetric keys and symmetric keys with TRNG.
* The module has the ability to protect keys from extraction.
* The module has to protect the keys from physical tampering, temperature, frequency and voltage related attacks.
* The module could withstand against Hardware cloning.
* The module could withstand probing attacks
* The module provides memory segregation for cryptographic operations and protection against buffer over flow attacks
* The module provides ability to withstand cryptographic side channel attacks like Differential Power analysis attacks, Timing attacks.
* CAVP validated implementation of the cryptographic algorithm.
* The module has the ability to perform a cryptographically validatable secure boot.
* The module has the ability to run trusted applications.

The foundational device trust derived from this module is used to enable trust-based computing for biometric capture. The foundational device trust module provides for a trusted execution environment based on the following:

* Secure Boot
    * Ability to cryptographically verify code before execution.
    * Ability to check for integrity violation of the module/device.
    * Halt upon failure.
    * Ability to securely upgrade and perform forward only upgrades, to thwart downgrade attacks.
    * SHA256 hash equivalent or above should be used for all hashing requirements
    * All root of trust is provisioned upon first boot or before.
    * All upgrades would be considered success only after the successful boot with proper hash and signature verification.
    * The boot should fail upon hash/signature failures and would never operate in a intermediary state.
    * Maximum of 10 failed attempts should lock the upgrade process and brick the device. However chip manufactures can decide to be less than 10.
* Secure application
    * Ability to run applications that are trusted.
    * Protect against downgrading of applications.
    * Isolated memory to support cryptographic operations.
    * All trust are anchored during the first boot and not modifiable.

## Certification
The FTM should have a at least one of the following certifications in each category to meet the given requirement.


##### Category: Cryptographic Algorithm Implementation
* CAVP (RSA, AES, SHA256, TRNG (DRBGVS), ECC)

{% hint style="info" %}
The supported algorithm and curves are listed [here](#cryptography)
{% endhint %}

##### Category: FTM Chip
(ONE of the following certifications)
* FIPS 140-2 L3 or above
* PCI PTS 5 or above (Pre-certified)
* PCI - PED 2.0 or above (Pre-Certified)
* One of following Common Criteria (CC) certification
	* https://www.commoncriteriaportal.org/files/ppfiles/pp0035a.pdf
	* https://www.commoncriteriaportal.org/files/ppfiles/pp0084a_pdf.pdf

##### System/Device Level Tamper (optional)
System/Device Level Tamper Responsiveness is recommended (not mandatory). In this case, FTM should be capable of showcasing Tamper Responsiveness (keys must be erased) against a tamper at the system/device level.

#### Threats to Protect
The FTM should protect against the following threats.

* Hardware cloning attacks - Ability to protect against attacks that could result in a duplicate with keys.
* Hardware Tamper attacks
    * Physical tamper - No way to physically tamper and obtain it secrets. 
    * Voltage & frequency related attacks - Should shield against voltage leaks and should prevent against low voltage. The FTM should always be in either of the state operational normally or inoperable. The FTM should never be operable when its input voltages are not met.
    * Temperature attacks on crypto block - Low or High the FTM is expected to operate or reach inoperable state. No state in between.
* Differential Power Analysis attack.
* Probing attacks - FTM should protect its surface area against any probe related attacks.
* Segregation of memory for execution of cryptographic operation (crypto block should be protected from buffer overflow type attacks).
* Vulnerability of the cryptographic algorithm implementation.
* Attacks against secure boot & secure upgrade.
* TEE/Secure processor OS attack.

#### Foundational Trust Module Identity
Upon an FTM provider approved by the MOSIP adopters, the FTM provider would submit a self signed public certificate to the adopter. Let us call this as the FTM root. The adopter would use this certificate to seed their device trust database. The FTM root and their key pairs should be generated and stored in FIPS 140-2 Level 3 or more compliant devices with no possible mechanism to extract the keys.  The foundational module upon its first boot is expected to generate a random asymmetric key pair and provide the public part of the key to obtain a valid certificate.  The FTM provider would validate to ensure that the chip is unique and would issue a certificate with the issuer set to FTM root.  The entire certificate issuance would be in a secured provisioning facility. Auditable upon notice by the adopters or its approved auditors.  The certificate issued to the module will have a defined validity period as per the MOSIP certificate policy document defined by the MOSIP adopters. This certificate and private key within the FTM chip is expected to be in it permanent memory.

{% hint style="info" %}
The validity for the chip certificate can not exceed 20 years from the date of manufacturing.
{% endhint %}

The FTM should have a at least one of the following certifications in each category to meet the given requirement.


### Secure Provisioning
Secure provisioning is applicable to both the FTM and the Device providers.

1. The devices and FTM should have a mechanism to protect against fraudulent attempts to create or replicate.
1. The device and FTM trust should be programmed in a secure facility which is certified by the respective MOSIP adopters.
1. Organization should have mechanism to segregate the FTM's and Devices built for MOSIP using cryptographically valid and repeatable process.
1. All debug options within the FTM or device should be disabled permanently
1. All key creations need for provisioning should happen automatically using FIPS 140-2 Level 3 or higher devices. No individual or a group or organization should have mechanism to influence this behavior.
1. Before the devices/FTM leaving the secure provisioning facility all the necessary trust should be established and should not be re-programmable.

{% hint style="info" %}
*As there are no adopter specific information being exchanged at the management server or at the FTM provisioning server, there are no mandates from MOSIP where these are located globally. However the adopter is recommended to have audit and contractual mechanisms to validate the compliance of these components at any point in time.*
{% endhint %}
