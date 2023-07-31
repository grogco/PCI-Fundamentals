# PCI-Fundamentals
My notes for PCI DSS 3.2 training (July 2023)  
<sub>_Please do not take this as an authoritative source for PCI DSS, these are just my notes._</sub>

![PCI Logo](Logo.png)

## Section 1 - Background
Payment cards are consistently one of the most highly stolen types of data. This theft is commonly done with credit card skimming devices, exploitation of outdated software, malware, or stolen credentials. According to the Verizon Data Breach Investigations Report of 2017, “95% of breaches featuring the use of stolen credentials leveraged vendor remote access to hack into their customer’s POS [point-of-sales] environments".  

Merchants that rely on credit card transactions are the primary targets of malicious actors looking for payment card data. It is the responsibility for merchants/organizations to have secure environments and prevent data theft.  

The Payment Card Industry Data Security Standard (PCI DSS) exists to help merchants prevent the theft of payment card data. It is a widely accepted set of policies and procedures intended to optimize the security of credit, debit, and cash card transactions and protect cardholders against misuse of their personal information.  

The body that provides oversight for PCI DSS is the PCI Security Standards Council. The council includes representatives from the 5 major payment card brands: Visa, American Express, MasterCard, Discover, and JCB. These card brands require PCI DSS compliance for merchants to use their payment card neworks.  

These are some resources that are provided by the council:
- PCI DSS, PA-DSS, P2PE, PTS, and Card Protection standards
- Rosters of QSAs, PA-QSAs, PCIPs, ASVs, validated payment applications, PTS Devices, and P2PE solutions
- Education programs
- Community meetings and FAQs  

Here are explanations for some of those standards listed above:  
### PCI DSS  
This covers security of all environments that store, process, or transmit account data. Its scope covers account data stored in payment applications and other sources.  

### PA-DSS  
This covers third-party payment applications to support PCI DSS compliance. This applies to things like POS devices, shopping carts in a web app, etc.. This standard covers how to validate off-the-shelf applications used in authorization and settlement. PA-DSS governs how these apps work so they can be compliant with PCI-DSS.  

### PCI P2PE  
This covers encryption, decryption, and key management requirements for point-to-point encryption solutions. It specifies requirements that must be in place from the POI (the Point Of Interaction, like when a card is swiped through the card reader) to the service provider's secure decryption environment. The council has a list of pre-approved P2PE solutions. Merchants may be able to reduce their PCI DSS scope when using a pre-approved solution.  

### PCI PTS  
This covers the protection of sensitive data at POI devices and hardware security modules, like cash registers, ATMs, fuel pumps/kiosks. The PTS program ensures terminals cannot be manipulated or attacked to allow the capture of Sensitive Authentication data, nor allow access to clear-text PINs or keys.  

### Card Production  
This covers the physical and logical security requirements for entities involved in card production and provisioning, which may include manufacturers, personalizers, pre-personalizers, chip embedders, data-preparation, and fulfillment.  

Here is an explanation of all the different entities involved in the payment card ecosystem:  

_**Issuer**_ banks give payment cards to **_Cardholders_**, who then make purchases from _**Merchants**_. The _**Merchants**_ then send the payment card data to their _**Acquirer**_ bank. The _**Acquirer**_ bank sends the payment card and transaction data over the _**Payment Brand Network**_ to the _**Issuer**_ bank. The _**Issuer**_ bank tells the _**Acquirer**_ bank that it approves or denies the transaction.

The Acquirer may also be referred to as the "Merchant Bank", "ISO", or "Payment Brand". Visa and MasterCard do not issue cards directly—their cards are always issued through another bank or entity—so they are never referred to as the Issuer.

During a process called **clearing** the processor provides complete reconcilation to the merchant's bank.
During a process called **settlement** the merchant bank pays the merchant for the carhdolder peurchase, and the cardholder's bank bills the cardholder.

A _**Service Provider**_ (SP) is a business that is not a payment brand, but controls or impacts the security of another entity's cardholder data. Some examples include transaction processors, Independent Sales Organizations (ISOs), managed firewall providers, IDS service providers, or hosting providers. SPs usually undergo their own PCI DSS assessments to demonstrate their compliance to their customers. Alternatively, a SP could have their services reviewed as part of their customers' PCI DSS assessments. _Note: Entities that only provide public network access, like a telecom company, are not considered SPs._ 


## Section 2 - Payment Card Brands and Their Compliance Programs  
Each of the 5 founding payment brands has their own PCI DSS compliance programs.
- American Express: [Data Security Operating Policy (DSOP)](https://www.americanexpress.com/content/dam/amex/us/merchant/new-data-security/DSOP_Oct2020_US_EN.pdf)
- Discover: [Discover Information Security Compliance (DISC)](https://www.discoverglobalnetwork.com/solutions/pci-compliance/discover-information-security-compliance/)
- JCB: [Data Security Program](https://www.global.jcb/en/products/security/data-security-program/index.html)
- MasterCard: [Site Data Protection (SDP)](https://www.mastercard.us/en-us/business/overview/safety-and-security/security-recommendations/site-data-protection-PCI.html)
- Visa Inc: [Cardholder Information Security Program (CISP)](https://usa.visa.com/partner-with-us/pci-dss-compliance-information.html)
- Visa Europe: [Account Information Security (AIS) Program](https://bm.visa.com/run-your-business/small-business/information-security/ais-program.html)
Payment brand compliance programs handle compliance tracking, enforcement, and any fees that may be incurred by noncompliance. Approval and posting of compliant entities and forensic investigation and response to data breaches are other responsibilities of the payment brands. It is important to note that the PCI SSC does not do investigations or response—this is all handled by the brands.

#### Merchant Levels
Every payment brand has different definitions for different *merchant levels*. Merchant levels range from 1-4 and are determined by the Acquirer based on annual number of transactions.  
Here is an overview of what the different merchant levels usually entail. Merchant level definitions for each payment brand are described in detail later:

|Merchants               | Level 1          | Level 2       | Levels 3 & 4                  |
|------------------------|:----------------:|:-------------:|:-----------------------------:|
| Assessment Type:       | Onsite Assessment|Self assessment|Determined by brand or acquirer|
| Reporting Requirements:| ROC & ASV scan   |SAQ & ASV scan |Determined by brand or acquirer|

|Service Providers       | Level 1          | Level 2       | Levels 3 & 4  |
|------------------------|:----------------:|:-------------:|:-------------:|
| Assessment Type:       | Onsite Assessment|Self assessment|Self assessment|
| Reporting Requirements:| ROC & ASV scan   |SAQ & ASV scan |SAQ & ASV scan |
_<sub>This is a summarized overview only - Merchants and Service Providers should consult with their acquirer or payment brand directly to understand each brand's validation criteria and reporting requirements.</sub>_
