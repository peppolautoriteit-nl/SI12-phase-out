# Introduction

*> Update July 1st 2022*
*SI-UBL 1.2 has been made optional by removing it as mandatory documenttype in the Peppol Authority Specific Requirements.*
*This document can still be used as reference for the reasons and process of phasing out the document type.*


In the Netherlands, Serviceprovider currently need to support three mandatory document types: SI-UBL 1.2, SI-UBL 2.0 (NLCIUS), and Peppol BIS 3.

Standaardisatieplatform e-factureren (STPE) and the Netherlands Peppol Authority (NPA) have taken the initiative to investigate what is necessary to phase out SI-UBL 1.2 as invoice document type. This would mean that sending and receiving Peppol serviceproviders no longer exchange SI-UBL 1.2 documents on the Peppol network.

# History

SI-UBL 1.2 is the third version of the Simplerinvoicing document format. It is a subset of the UBL Invoice format, and was created by the members of Simplerinvoicing for e-invoicing use in the Netherlands.

In 2018, after the publication of European Norm EN-16931, the STPE created a Core Invoice Usage Specification (CIUS) for EN-16931 for use in the Netherlands, called NLCIUS. To conform to EN-16931 and NLCIUS, SI-UBL was updated to SI-UBL 2.0. 

After this update, there was an attempt to phase out SI-UBL 1.2, but it turned out this wasn't possible at that time, due to a number of participants and service providers relying on features in SI-UBL 1.2 that were no longer supported in SI-UBL 2.0. These features were removed mostly due to restrictions in the European Norm.

The features that were blocking the phase out of SI-UBL 1.2 were:
1. Calculating VAT on invoice line level
2. Using G-Accounts
3. Rounding differences caused by using multiple decimals

# Why phase out SI-UBL 1.2

Interoperability is best served if there very few document formats to support, since each format requires both software and operational maintenance. While there can be valid reasons for having several different document formats, it should always be a goal to have as few as possible. Especially if there are newer versions of a format, the older ones should at some point be phased out.  

This requires that users replace their support for SI-UBL 1.2 with one of the other document formats we mentioned earlier: SI-UBL 2.0 or Peppol BIS 3. 
If users conclude that key scenario are not supported by other document formats, a fix or work around needs to be put in place.
This can take several forms:
- Add the missing functionality to the other format
- Work around limitations of the other formats
- Remove the business need for the functionality in the first place

# Current status

Since 2018 there have been changes to both of the newer document formats: SI-UBL 2.0 and Peppol BIS3. 
Other developments have been the creation/adoption of invoice extensions for SI-UBL 2.0 (notably G-rekening), changes in the European norm and the implementation of country specific rules for Peppol BIS3. Specifically, regarding the issues identified originally:
- A g-account extension has been specified and deployed
- A workaround exists for rounding issues in the form of an error tolerance in the validation rules
- A number of proposals, including potential solutions to the rounding issue and line-level VAT have been proposed as amendments to the European Norm

The amendments for the European Norm are still being finalized, but in the mean time, a number of other problems have surfaced. The following list shows the currently known issues for using SI-UBL 2.0 instead of SI-UBL 1.2, and a proposed solution (or workaround) for the issue. The original 3 issues have been included for completeness.

Issue                                       | Solution/workaround
------                                      |---------------
No line-level VAT                           | Proposed amendment of EN-16931
No support for g-account                    | Use g-account extension in SI-UBL 2.0
Rounding issues                             | Rounding tolerance in EN-16931 validation
Missing billing reference in credit notes   | See section 'Billing Reference'
Need credit notes without billing reference | See section 'Billing Reference'
No AccountingCostCode field                 | Use AccountingCost
No cost center accounting field             | Use AccountingCost
No validation of line-level calculation     | Use Peppol BIS 3, which does have line-level calculation validation
Mandatory KvK or OIN                        | Use Peppol BIS 3, NL rules will set where KvK or OIN is only mandatory if the optional LegalIdentifier is used.


## Billing Reference

For corrective invoices (InvoiceTypeCode 384), the use of a BillingReference is currently mandated. 
A corrective invoice always communicates a correction on top of an earlier invoice or creditnote and it therefor makes sense to mandate the BillingReference.

When it comes to CreditNotes there are two conflicting requirements regarding the use of BillingReference:
1. On the one hand, a group of serviceproviders and endusers state that there is a need for the billing reference to be always filled in Credit Notes
2. On the other hand, a group of serviceproviders and endusers state that there is a need for credit notes without a billing reference (Scenario P9 in NLCIUS)

One proposed solution was to create a warning for InvoiceTypeCode 381 (CreditNote) without a billing reference, but a warning does not enforce anything and thus does not solve the issue. Additionally, a valid scenario would then generate warnings, which is also not desirable.

Therefor the proposed solution is to mandate the BillingReference in documents with InvoiceTypeCode 381.
Scenario P9 (no BillingReference) could be solved with a general negative invoice (InvoiceTypeCode 380 with a negative invoice line and/or payable amount).
This solution is already implemented in the NL rules in Peppol BIS 3, so the future workaround could be to use Peppol BIS 3 for this scenario. 
It might be an additional rule for NLCIUS as well.

# Way forward

For each issue, the following things need to be considered by the STPE and NPA communities:

1. Does the solution or workaround actually solve the problem? (i.e. can the Service providers and End users actually use it instead of SI-UBL 1.2)
2. If so, is it known when the solution is deployed by users (if it hasn't already been)?
3. If not, is the problem large enough to warrant a solution (i.e. is it a problem only very few parties have, and does it completely block them from using e-invoicing, or could they in theory do without?)
4. If so, determine a new solution or workaround

If the STPE and NPA communities conclude that the key issues have been solved, the phase out process for SI-UBL 1.2 will start. 
At that point, NPA will update their requirements to deprecate SI-UBL 1.2 and it will be included in the NPA compliancy checks.
