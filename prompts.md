# Prompt Engineering
Sample prompts generated to extract the latent domain knowledge inherent in models like GPT-3.5.Turbo to align medical concepts for disjoint medical ontologies.

## GPT-Relation
Prompt designed to establish relationship between medical concepts in medical ontologies.
```
Given two input medical terminologies [E1] and [E2], determine their directed relationship between [E1] and [E2].
There exists four relationships: (i) parent-child, (ii) child-parent, (iii) equivalence, and (iv) no relation

Return then response output as a JSON

Example 1:
Input: [E1] malignant neoplasm of bronchus and lung
       [E2] malignant neoplasm of breast

Output: {
    'relation': 'no relation'
}

Example 2:
Input: [E1] cataract
       [E2] eye

Output: {
    'relation': 'child-parent'
}

Example 3:
Input: [E1] disease of the lungs
       [E2] lungs disease

Output: {
    'relation': 'equivalence'
}

Example 3:
Input: [E1] respiratory disease
       [E2] asthma

Output: {
    'relation': 'parent-child'
}


```

## GPT-MER
Prompt designed to extract medical terms from free-text medical documents.
```
Given an input medical document extract all relevant medical terms.

Return then response output as a JSON

Example 1:
Input: All respiratory related diagnoses

Output: {
    'response': ['respiratory']
}

Example 2:
Input: All eye related diagnoses including catract

Output: {
    'response': ['eye', 'cataract']
}

```

## GPT-UW
Prompt designed to establish the relationship between free-text UW exclusions and ICD codes
```
Given [i] underwriting exclusion [ii] list of ICD codes, the result 'response' is a boolean indicator to determine if any ICD code in [ii] is related to [i]
Return the result as a JSON with the following keys: response, reason.
reason should include description of ICD code and the association or lack of assoication between UW exclusion and ICD code

Example 1:
prompt: [i] Any complications of cataracts including loss of sight including any complications thereof	
        [ii] H26.9, T81.2

result: { 
    "response": "yes", "reason": H26.9 (Other Cataract, Unspecified), is related to cataract
}

Example 2:
prompt: [i] any treatment, whether diagnostic, medical, surgical or otherwise, relating to the ovarian cysts and/or its related complications
        [ii] H26, H21.8

result: { 
    "response": "no", "reason": Both H26 (Other cataract), and H21.8 (Other specified disorders of iris and ciliary body) are eye diseases and not related to ovarian cysts
}

```

## GPT-UW-Desc
Prompt designed to establish the relationship between free-text UW exclusions and ICD code descriptions
```
Given [i] underwriting exclusion [ii] list of ICD codes, the result 'response' is a boolean indicator to determine if any ICD code in [ii] is related to [i]
Return the result as a JSON with the following keys: response, reason.
reason should include description of ICD code and the association or lack of assoication between UW exclusion and ICD code

Example 1:
prompt: [i] Any complications of cataracts including loss of sight including any complications thereof	
        [ii] Unspecified cataract; Accidental puncture or laceration during a procedure, not elsewhere classified

result: { 
    "response": "yes", "reason": Unspecified cataract, is related to cataract
}

Example 2:
prompt: [i] any treatment, whether diagnostic, medical, surgical or otherwise, relating to the ovarian cysts and/or its related complications
        [ii] Other cataract; Other specified disorders of iris and ciliary body

result: { 
    "response": "no", "reason": Both Other cataract, and Other specified disorders of iris and ciliary body are eye diseases and not related to ovarian cysts
}

```
