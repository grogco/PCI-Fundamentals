# PCI-Fundamentals
My notes for PCI DSS 3.2 training (July 2023)  
<sub>_Please do not take this as an authoritative source for PCI DSS, these are just my notes._</sub>

![PCI Logo](Logo.png)

## Section 1 - Background
Payment cards are consistently one of the most highly stolen types of data. This is commonly seen done with credit card skimming devices, exploitation of outdated software, malware, or stolen credentials. According to the Verizon Data Breach Investigations Report of 2017, "“95% of breaches featuring the use of stolen credentials leveraged vendor remote access to hack into their customer’s POS [point-of-sales] environments".  

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
