# Introduction

In the Netherlands, there are currently three mandatory document types: SI-UBL 1.2, SI-UBL 2.0 (NLCIUS), and Peppol BIS 3.

Standaardisatieplatform e-factureren (STPE) and the Netherlands Peppol Authority (NPA) have taken the initiative to investigate what is necessary to phase out SI-UBL 1.2 as invoice document type. This would mean that sending and receiving Peppol serviceproviders no longer exchange SI-UBL 1.2 documents on the Peppol network.


# History

SI-UBL 1.2 is the third version of the Simplerinvoicing document format. It is a subseet of the UBL Invoice format, and was created by the members of Simplerinvoicing for e-invoicing use in the Netherlands.

In 2018, after the publication of European Norm EN-16931, the STPE created a Core Invoice Usage specification for EN-16931 for use in the Netherlands, called NLCIUS. To conform to EN-16931 and NLCIUS, SI-UBL was updated to SI-UBL 2.0.

After this update, there was an attempt to phase out SI-UBL 1.2, but it turned out this wasn't possible at that time, due to a number of participants and service providers relying on features in SI-UBL 1.2 that were no longer present in SI-UBL 2.0. These were mostly due to restrictions in the European Norm.

The issues identified at time were:
1. Calculating VAT on invoice line level
2. Using G-Accounts
3. Rounding differences because of using multiple decimals

# Why phase out SI-UBL 1.2

Interoperability is best served if there are less different document formats to need to support: each format requires both software and operational maintenance. While there are valid use-cases for several different document formats, it should always be a goal to have as few as possible. Especially if there are newer versions of a format, thee older ones should at some point be phased out.

This does require that the necessity for SI-UBL 1.2 is removed. This can take several forms:
- Add the missing functionality to another format
- Work around limitations of the other formats
- Remove the scenario there the functionality is needed (e.g. work around the issue by using a different but functionally equivalent method)

# Current status

Many things have changed between 2018 and 2021. These changes include changes in SI-UBL 2.0, Peppol BIS3 and the European norm.
the creation/adoption of invoice extensions for SI-UBL 2.0, changes in the European norm and the implementation of country specific rules for Peppol BIS3.

Specifically, regarding the issues identified originally:
- A g-account extension has been specified and deployed
- A workaround exists for rounding issues in the form of an error tolerance in the validation rules
- A number of proposals, including potential solutions to the rounding issue and line-level VAT have been proposed as amendments to the European Norm

The amendments for the European Norm are still being finalized, so these may or may not solve the issue, but in the mean time, a number of other problems have surfaced.

The following list shows the currently known issues for using SI-UBL 2.0 instead of SI-UBL 1.2, and a workaround/proposed solution for the issue. The original 3 issues have been included for completeness.

Issue | Solution/workaround
------|---------------
No line-level VAT | Proposed amendment of EN-16931
No support for g-account | Use the g-account extension
Rounding issues | Rounding tolerance in EN-16931 validation
Missing billing reference in credit notes | See section 'Billing reference'
No AccountingCostCode field | Use AccountingCost OR update NLCIUS?
No cost center accounting field | Use AccountingCost
No validation of line-level calculation | If this is wanted, use Peppol BIS, which does have line-level calculation validation
Mandatory KvK or OIN | In Peppol BIS (with NL rules), KvK or OIN is only mandatory if the optional LegalIdentifier is used.



# Way forward

For each issue, the following things need to be considered:

1. Does the solution or workaround actually solve the problem? (i.e. can the Service providers and End users actually use it instead of SI-UBL 1.2)
2. If so, is it known when the solution is deployed (if it hasn't already been)?
3. If not, is the problem large enough to warrant a solution (i.e. is it a problem only very few parties have, and does it completely block them from using e-invoicing, or could they in theory do without?)
4. If so, determine a new solution or workaround

If for enough issues the answer to 1. and 2. is 'yes', and for the rest the answer to 3 is 'no', we can phase out SI-UBL 1.2. At that point, NPa will update their requirements to make 1.2 deprecated, and it will be included in their compliancy checks.
