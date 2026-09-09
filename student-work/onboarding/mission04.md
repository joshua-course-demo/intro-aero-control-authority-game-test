# Separate trim, stability, and control

## Engineering question
A synthetic trainer condition is trimmed and statically restoring, but offers only 800 N m control capacity against a 1350 N m demand. Does it have sufficient initial pitch authority?

## Physics model
Trim indicator: net moment at the reference is zero. Stability indicator: restoring dCm/dalpha<0. Control indicator: margin=available-required.

## Inputs
Synthetic comparison: reference net moment=0 N m; dCm/dalpha=-0.6 per rad; available=800 N m; required=1350 N m. Indicators refer to their declared reference state.

## Outputs
output: Available minus required control moment

unit: N m

threshold: 0

control: Insufficient authority

explanation3: The available control moment is less than the required control moment

## Assumptions
Trim, stability, and control indicators answer different questions. The separate available-control increment is compared with the required-control increment.

## Validity
No dynamic stability or full-envelope control conclusion follows from these three static indicators.

## Predictions
Trim and restoring tendency can coexist with a negative control margin.

## Manual reference
Control margin=800−1350=−550 N m even though the other two indicators pass.

## Verification cases
At available=1350 N m the inclusive requirement is met exactly. At 800 it fails. A negative restoring slope cannot change that arithmetic.

## Feature requirements
Display three separate statuses; use a signed control margin with units and an inclusive zero threshold.

## Implementation
Sweep available control moment; compute available-required; compare with zero. Keep the trim and stability indicators unchanged.

## Decision
Withdraw the sufficient-control claim for this synthetic condition; trim and static stability alone are not proof of control.

## Recorded investigations
{
  "800": {
    "attemptId": "7eeadb12-daac-44f3-ad2a-5872696e9907",
    "at": "2026-09-09T21:20:48.241Z",
    "note": "this doesnt meet the requirement because the control margin is negative so this check fails",
    "evidence": "-550",
    "conclusion": "Insufficient authority",
    "readouts": [
      {
        "label": "Trim: reference net moment",
        "expression": "0",
        "unit": "N m",
        "value": 0
      },
      {
        "label": "Static restoring derivative",
        "expression": "-0.6",
        "unit": "per rad",
        "value": -0.6
      },
      {
        "label": "Available control moment",
        "expression": "available",
        "unit": "N m",
        "value": 800
      },
      {
        "label": "Required control moment",
        "expression": "required",
        "unit": "N m",
        "value": 1350
      },
      {
        "label": "Control margin",
        "expression": "available-required",
        "unit": "N m",
        "value": -550
      }
    ],
    "inputs": {
      "available": 800
    }
  },
  "1350": {
    "attemptId": "7eeadb12-daac-44f3-ad2a-5872696e9907",
    "at": "2026-09-09T21:21:49.258Z",
    "note": "This case has a control margin of 0 which means there is sufficient control authority",
    "evidence": "0",
    "conclusion": "Requirement met",
    "readouts": [
      {
        "label": "Trim: reference net moment",
        "expression": "0",
        "unit": "N m",
        "value": 0
      },
      {
        "label": "Static restoring derivative",
        "expression": "-0.6",
        "unit": "per rad",
        "value": -0.6
      },
      {
        "label": "Available control moment",
        "expression": "available",
        "unit": "N m",
        "value": 1350
      },
      {
        "label": "Required control moment",
        "expression": "required",
        "unit": "N m",
        "value": 1350
      },
      {
        "label": "Control margin",
        "expression": "available-required",
        "unit": "N m",
        "value": 0
      }
    ],
    "inputs": {
      "available": 1350
    }
  },
  "2000": {
    "attemptId": "7eeadb12-daac-44f3-ad2a-5872696e9907",
    "at": "2026-09-09T21:22:17.488Z",
    "note": "This case shows the control margin is met because 650 > 0",
    "evidence": "650",
    "conclusion": "Requirement met",
    "readouts": [
      {
        "label": "Trim: reference net moment",
        "expression": "0",
        "unit": "N m",
        "value": 0
      },
      {
        "label": "Static restoring derivative",
        "expression": "-0.6",
        "unit": "per rad",
        "value": -0.6
      },
      {
        "label": "Available control moment",
        "expression": "available",
        "unit": "N m",
        "value": 2000
      },
      {
        "label": "Required control moment",
        "expression": "required",
        "unit": "N m",
        "value": 1350
      },
      {
        "label": "Control margin",
        "expression": "available-required",
        "unit": "N m",
        "value": 650
      }
    ],
    "inputs": {
      "available": 2000
    }
  }
}

## Interpretation attempts
{
  "800": [
    {
      "correct": true,
      "feedback": "Your interpretation matches this comparison: Insufficient authority. Control margin: -550 N m. -550 ≥ 0 Written reasoning still awaits instructor review.",
      "attemptId": "7eeadb12-daac-44f3-ad2a-5872696e9907",
      "at": "2026-09-09T21:20:48.241Z",
      "conclusion": "Insufficient authority",
      "evidence": "-550",
      "note": "this doesnt meet the requirement because the control margin is negative so this check fails",
      "draftSnapshot": "{\"evidence\":\"-550\",\"conclusion\":\"Insufficient authority\",\"note\":\"this doesnt meet the requirement because the control margin is negative so this check fails\"}"
    }
  ],
  "1350": [
    {
      "correct": true,
      "feedback": "Your interpretation matches this comparison: Requirement met. Control margin: 0 N m. 0 ≥ 0 Written reasoning still awaits instructor review.",
      "attemptId": "7eeadb12-daac-44f3-ad2a-5872696e9907",
      "at": "2026-09-09T21:21:49.258Z",
      "conclusion": "Requirement met",
      "evidence": "0",
      "note": "This case has a control margin of 0 which means there is sufficient control authority",
      "draftSnapshot": "{\"evidence\":\"0\",\"conclusion\":\"Requirement met\",\"note\":\"This case has a control margin of 0 which means there is sufficient control authority\"}"
    }
  ],
  "2000": [
    {
      "correct": true,
      "feedback": "Your interpretation matches this comparison: Requirement met. Control margin: 650 N m. 650 ≥ 0 Written reasoning still awaits instructor review.",
      "attemptId": "7eeadb12-daac-44f3-ad2a-5872696e9907",
      "at": "2026-09-09T21:22:17.488Z",
      "conclusion": "Requirement met",
      "evidence": "650",
      "note": "This case shows the control margin is met because 650 > 0",
      "draftSnapshot": "{\"evidence\":\"650\",\"conclusion\":\"Requirement met\",\"note\":\"This case shows the control margin is met because 650 > 0\"}"
    }
  ]
}

## Evidence status
Written reasoning awaits instructor review. This export is the current draft; compare it with the answer snapshot of the last run.

## Student reflection
Question: Even when the control margin is positive, what additional information would you need to predict how quickly the aircraft reaches a new pitch angle?

Included: The cases compare starting moment balance, a static restoring derivative, and available versus required control moment.

Omitted: They do not simulate how pitch angle and pitch rate evolve after a control input.

confirmedFor: 7eeadb12-daac-44f3-ad2a-5872696e9907

observation: We require 1350 N-m of control capacity for this elevator. To meet this demand 

change: I did not change anything

result: supported

limit: the angular acceleration should be studied. Or perhaps it may also be useful to look at the dynamic stability