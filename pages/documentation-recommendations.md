---
layout: default
title: Recommendations
---

# Structuring Recommendations

This guide considers two aspects of structuring a clinical practice guideline recommendation:

1. The _definition_ of the recommendation, independent of any particular patient or setting in which it applies
2. The _instance_ of the recommendation, as applied to a particular patient at a specific time

## Recommendation Definitions

To support computable representation of a recommendation definition, this implementation guide describes the following components of a recommendation:

* **Personas**: Who are the participants in the recommendation and what roles do they play?
* **Settings**: Where do the activities in the recommendation occur?
* **Processes**: What are the common processes involved in delivering guideline-based care?

By establishing common patterns for these aspects of recommendations, specific guidelines can better share common aspects such as workflow insertion points.

### Personas

The personas identified in this implementation guide are defined based on the WHO recommendation for [Classifying health workers](https://www.who.int/hrh/statistics/Health_workers_classification.pdf). This recommendation uses codes from the [International Standard Classification for Occupations](http://www.ilo.org/public/english/bureau/stat/isco/index.htm) but defines several additional categories of workers. In addition, the codes in that recommendation are focused on health workers, so codes for patient and care partner personas need to be considered as well.

Where a code from the ISCO exists, it is used. Where a WHO recommended health worker category is used, a code is constructed beginning with a W. Where a code is introduced by this implementation guide, it is constructed beginning with a C.

### Settings

For settings, this implementation guide uses the [HL7 V3 ServiceDeliveryLocationRoleType](http://hl7.org/fhir/v3/ServiceDeliveryLocationRoleType/vs.html) value set, as it contains generally applicable, broadly standardized settings for use in the computable representation of guideline recommendations.

### Processes

The common processes identified in this implementation guide are based on surveys of guideline content, both in the examples used in this guide, as well as other guideline content from various clinical domains and guideline authors. The result is the definition of a _common pathway_ that is intended to be applicable in any guideline-based care content.

## Recommendation Instances

Across guideline-based care, there are many different types of recommendations that may be given, such as the recommendation to conduct a specific test, to prescribe a specific medication, recommendation for a particular procedure, and many others. In general though, these recommendations should provide at least:

* **Support**: A link back to the guideline, and ultimately the evidence, that supports the recommendation
* **Strength**: The _strength_ of the recommendation
* **Evidence Quality**: The _quality_ of the evidence supporting the recommendation

Within FHIR, a recommendation is typically represented using a [Request](http://hl7.org/fhir/request.html) patterned resource (such as ServiceRequest or MedicationRequest) with an [intent](http://hl7.org/fhir/codesystem-request-intent.html#request-intent-proposal) status. Note that some implementations may go further and use the `plan` or even `order` statuses of a request, depending on the capabilities of the systems involved.

This implementation guide defines profiles for each of the request resources to be used as recommendation instances:

* Appointment
* CommunicationRequest
* DeviceRequest
* ImmunizationRecommendation
* MedicationRequest
* NutritionOrder
* ServiceRequest

Specific guideline content will typically define derived profiles for recommendation instances establishing additional constraints.

# Using Terminology

Terminologies are a critical aspect of supporting interoperable computable content. This implementation guide defines profiles for the CodeSystem and ValueSet resources to identify key elements that must be supported.

## Code Systems

Standard and established code systems should be used whenever possible. Only in the case that existing code systems do not provide the necessary concepts should new code systems be defined. If required, code systems defined by content conforming to this IG SHALL use the [cpg-codesystem](StructureDefinition-cpg-codesystem.html) profile.

## Value Sets

This implementation guide defines three value set profiles, a base cpg-valueset profile that establishes key elements that must be supported for any value set content, and two derived profiles, cpg-computablevalueset and cpg-cachedvalueset, that define key elements that should be used to support computable value set content. Value sets defined by content conforming to this IG SHALL use at least the [cpg-valueset](StructureDefinition-cpg-valueset.html) profile, and may also use:

1. **Computable**: Value sets SHOULD be defined using computable (or _intensional_) definitions if supported by the code systems involved. Value sets defined in this way SHALL conform to the [cpg-computablevalueset](StructureDefinition-cpg-computablevalueset.html) profile.
2. **Cached**: For value sets that are defined computably, content conforming to this IG SHALL include a _cached_ (or _extensional_) version of the value set that lists the codes in the `compose` element of the value set, to ensure the content of the value set can be processed by systems that cannot process the computable version. Value sets defined in this way SHALL conform to the [cpg-cachedvalueset](StructureDefinition-cpg-cachedvalueset.html) profile.

# Inclusion/Exclusion Criteria

# Structuring Order Sets

# Applying to Patients in Context