# Modelling
## Questionnaires
* separate the questionnaires based on timing + reporting source
  * .fsh file layout will follow from that
* use groups to mark differences in categories
* enforce PROM best practice rendering guidelines, list so far:
  * make sure top of the questionnares has text for how a questionnaire shoud be filled out (sourced from original material PDF)
* questionnaires will include auto-scoring capabilities (pending ICHOM providing algorithms)
* BreastQ:
  * at baseline: ignore surgery type  (for example in breastq-masectomy), questions remain the same anyway
  * during follow-up: we need to be able to know the context of the patient that answers these questions. It is not an option to have the patient fill in the type of surgery they had, this should be filled in by a clinician. Therefore we need to be able to do some sort of prefill based on the CROMs. 
* answerOptions should still transmit the codes relevant for them, and not strings
* will model baseline, 6 mo, and up to 4 year follow-up for the May Connectathon
* will ignore neo-adjuvant and metastatic cases for now
* "Date by DD/MM/YYYY; Please enter "999" if date is unknown": put a checkbox in at the beginning to signal that the date is known, this should enable a date picker
* the receptor status (ER, PR and HER2) can be filled in at baseline, so we can ignore the inclusion criteria which requires the surgery type 
* the timing of the question about genetic mutation (linkID=MUTBC) can go from baseline + 1 year to baseline + 6 months. This change will leave us with 3 questionnaires for CROMs instead of 4.
* disutility of care is only timed at 6 months follow-up. We should limit the amount of questions about the treatment, this will be covered in the annual follow-up.

### Questionnaire pre-population
* need to strike a balance between reducing patient burden and patient safety
* OK to prefill is information already known in the healthcare information system, and say how old the information is:
  * MRN, last name, sex at birth, year birth
  * laterality of breast cancer and other clinical factors
* not OK is generally anything that can change within a few days: 
  * not body height, weight
  * not the 1st year's clinical response, but others are OK
  * patient-reported questions previously answered
  * comobirdities (these are also considered to be proms, so patients need to fill these in themselves)
* rule of thumb: if questions are event based, e.g. proms, prepopulation should not be applied. 

## Clinical data points
* this data will already be available in the health information system (HIT) as part of patient care
* aim is to extract it for purposes of analytics

## Terminology
* terminology will not be shared agross IGs, as there is little overlap between the initial [breast cancer](https://connect.ichom.org/patient-centered-outcome-measures/breast-cancer/) and [autism spectrum disorders](https://connect.ichom.org/patient-centered-outcome-measures/autism-spectrum-disorder/) sets that are proposed for the initial HL7 inclusion

# Tooling
* stay on top of errors and warnings: both SUSHI and publisher's QA report should always say 0 warnings and 0 errors
* keep IG publisher and sushi up to date - always use the latest version

# AnswerOptions versus ValueSet
* rule of thumb is: use ValueSets when the list of permitted answers consists of existing codes (e.g. gender) and/or when the list of permitted answers are repeatedly used in other questions. Otherwise, use answerOptions.
