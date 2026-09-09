# Ask a testable question

## Engineering question
question: At 20 m/s, can the trainer elevator overcome the opposing pitching moment and produce an initial nose-up angular acceleration of at least 0.12 rad/s²?

quantity: Initial pitch acceleration

threshold: 0.12

comparison: At least the threshold

explanation0: The specified minimum is 0.12 rad/s², including equality. I compare initial pitch acceleration with this requirement at the stated trainer condition. This question concerns initial elevator authority, not successful takeoff or aircraft safety.

scope: Initial pitch response at the stated condition

## Physics model
available = 0.5*rho*V^2*S*c*dCm; required=Iy*target-other; acceleration=(available+other)/Iy

## Inputs
900 kg trainer; rho=1.20 kg/m³; V=20 m/s; S=27.25 m²; c=4 m; usable dCm=0.153; Iy=5000 kg m²; other=-750 N m; target=0.12 rad/s². Nose-up moment is positive about the declared CG.

## Outputs
Available and required moment (N m), margin (N m), acceleration (rad/s²).

## Assumptions
Hold the supplied usable coefficient increment, loading, flap/power state, and local-flow assumption fixed during this first screen. Full available nose-up control moment is commanded. These assumptions require later review.

## Validity
This is a bounded teaching calculation. It does not establish aircraft safety, successful takeoff, or behavior outside the specified condition.

## Predictions
Increasing speed increases available moment quadratically.

## Manual reference
Available 4002.48 N m; required 1350 N m; margin 2652.48 N m; full-command acceleration 0.650496 rad/s².

## Verification cases
Test 20 and 10 m/s, include equality with the required acceleration.

## Feature requirements
Show controls with units, supplied and student results separately, a result trace, and a clear limitation.

## Implementation
For each speed, compute available moment, subtract the 1350 N m demand, and calculate (available-750)/5000. For the short replay only, pitch angle=0.5*initialAcceleration*time² from rest over 0.5 s. This extrapolation is not a ground-run simulation.

## Decision
The supplied baseline meets initial authority demand. No takeoff claim follows.

## Recorded investigations
{
  "10": {
    "attemptId": "13a10918-7e21-49d9-a16b-e75ac0681ff1",
    "at": "2026-09-09T20:31:57.517Z",
    "note": "At 10 m/s, the initial acceleration is 0.0501 rad/s², below the required 0.12 rad/s². The elevator produces a nose-up response but cannot meet the specified minimum. This model alone cannot assess takeoff safety.",
    "evidence": "0.0501",
    "conclusion": "Insufficient authority",
    "readouts": [
      {
        "label": "Available elevator capacity",
        "expression": "0.5*rho*V^2*S*c*dCm",
        "unit": "N m",
        "value": 1000.62
      },
      {
        "label": "Required elevator moment",
        "expression": "Iy*target-other",
        "unit": "N m",
        "value": 1350
      },
      {
        "label": "Pitch-authority margin",
        "expression": "0.5*rho*V^2*S*c*dCm-(Iy*target-other)",
        "unit": "N m",
        "value": -349.38
      },
      {
        "label": "Full-command initial acceleration",
        "expression": "(0.5*rho*V^2*S*c*dCm+other)/Iy",
        "unit": "rad/s²",
        "value": 0.050124
      },
      {
        "label": "Specified minimum initial acceleration",
        "expression": "target",
        "unit": "rad/s²",
        "value": 0.12
      }
    ],
    "inputs": {
      "V": 10
    }
  },
  "14": {
    "attemptId": "13a10918-7e21-49d9-a16b-e75ac0681ff1",
    "at": "2026-09-09T20:31:56.600Z",
    "note": "At 14 m/s, 0.2422 rad/s² still exceeds 0.12 rad/s². Lower speed reduces elevator capacity and the margin, but the initial response requirement is met. This does not establish a successful takeoff.",
    "evidence": "0.2422",
    "conclusion": "Requirement met",
    "readouts": [
      {
        "label": "Available elevator capacity",
        "expression": "0.5*rho*V^2*S*c*dCm",
        "unit": "N m",
        "value": 1961.2151999999999
      },
      {
        "label": "Required elevator moment",
        "expression": "Iy*target-other",
        "unit": "N m",
        "value": 1350
      },
      {
        "label": "Pitch-authority margin",
        "expression": "0.5*rho*V^2*S*c*dCm-(Iy*target-other)",
        "unit": "N m",
        "value": 611.2151999999999
      },
      {
        "label": "Full-command initial acceleration",
        "expression": "(0.5*rho*V^2*S*c*dCm+other)/Iy",
        "unit": "rad/s²",
        "value": 0.24224303999999997
      },
      {
        "label": "Specified minimum initial acceleration",
        "expression": "target",
        "unit": "rad/s²",
        "value": 0.12
      }
    ],
    "inputs": {
      "V": 14
    }
  },
  "20": {
    "attemptId": "13a10918-7e21-49d9-a16b-e75ac0681ff1",
    "at": "2026-09-09T20:31:40.352Z",
    "note": "At 20 m/s, 0.6505 rad/s² exceeds the specified 0.12 rad/s² minimum. Initial pitch authority is sufficient in this model, but the test does not model lift-off, runway distance or a complete takeoff.",
    "evidence": "0.6505",
    "conclusion": "Requirement met",
    "readouts": [
      {
        "label": "Available elevator capacity",
        "expression": "0.5*rho*V^2*S*c*dCm",
        "unit": "N m",
        "value": 4002.48
      },
      {
        "label": "Required elevator moment",
        "expression": "Iy*target-other",
        "unit": "N m",
        "value": 1350
      },
      {
        "label": "Pitch-authority margin",
        "expression": "0.5*rho*V^2*S*c*dCm-(Iy*target-other)",
        "unit": "N m",
        "value": 2652.48
      },
      {
        "label": "Full-command initial acceleration",
        "expression": "(0.5*rho*V^2*S*c*dCm+other)/Iy",
        "unit": "rad/s²",
        "value": 0.650496
      },
      {
        "label": "Specified minimum initial acceleration",
        "expression": "target",
        "unit": "rad/s²",
        "value": 0.12
      }
    ],
    "inputs": {
      "V": 20
    }
  }
}

## Interpretation attempts
{
  "10": [
    {
      "correct": true,
      "feedback": "Your interpretation matches this comparison: Insufficient authority. Full-command initial acceleration: 0.0501 rad/s². 0.0501 ≥ 0.12 Written reasoning still awaits instructor review.",
      "attemptId": "f9b87e6d-2656-4808-a243-20d0a31eac7a",
      "at": "2026-09-09T20:11:45.071Z",
      "conclusion": "Insufficient authority",
      "evidence": "0.0501",
      "note": "The initial acceleration for this takeoff speed is too low",
      "draftSnapshot": "{\"evidence\":\"0.0501\",\"conclusion\":\"Insufficient authority\",\"note\":\"The initial acceleration for this takeoff speed is too low\"}"
    },
    {
      "correct": true,
      "feedback": "Your interpretation matches this comparison: Insufficient authority. Full-command initial acceleration: 0.0501 rad/s². 0.0501 ≥ 0.12 Written reasoning still awaits instructor review.",
      "attemptId": "13a10918-7e21-49d9-a16b-e75ac0681ff1",
      "at": "2026-09-09T20:31:57.517Z",
      "conclusion": "Insufficient authority",
      "evidence": "0.0501",
      "note": "At 10 m/s, the initial acceleration is 0.0501 rad/s², below the required 0.12 rad/s². The elevator produces a nose-up response but cannot meet the specified minimum. This model alone cannot assess takeoff safety.",
      "draftSnapshot": "{\"evidence\":\"0.0501\",\"conclusion\":\"Insufficient authority\",\"note\":\"At 10 m/s, the initial acceleration is 0.0501 rad/s², below the required 0.12 rad/s². The elevator produces a nose-up response but cannot meet the specified minimum. This model alone cannot assess takeoff safety.\"}"
    }
  ],
  "14": [
    {
      "correct": true,
      "feedback": "Your interpretation matches this comparison: Requirement met. Full-command initial acceleration: 0.2422 rad/s². 0.2422 ≥ 0.12 Written reasoning still awaits instructor review.",
      "attemptId": "13a10918-7e21-49d9-a16b-e75ac0681ff1",
      "at": "2026-09-09T20:31:56.600Z",
      "conclusion": "Requirement met",
      "evidence": "0.2422",
      "note": "At 14 m/s, 0.2422 rad/s² still exceeds 0.12 rad/s². Lower speed reduces elevator capacity and the margin, but the initial response requirement is met. This does not establish a successful takeoff.",
      "draftSnapshot": "{\"evidence\":\"0.2422\",\"conclusion\":\"Requirement met\",\"note\":\"At 14 m/s, 0.2422 rad/s² still exceeds 0.12 rad/s². Lower speed reduces elevator capacity and the margin, but the initial response requirement is met. This does not establish a successful takeoff.\"}"
    }
  ],
  "20": [
    {
      "correct": true,
      "feedback": "Your interpretation matches this comparison: Requirement met. Full-command initial acceleration: 0.6505 rad/s². 0.6505 ≥ 0.12 Written reasoning still awaits instructor review.",
      "attemptId": "13a10918-7e21-49d9-a16b-e75ac0681ff1",
      "at": "2026-09-09T20:31:40.352Z",
      "conclusion": "Requirement met",
      "evidence": "0.6505",
      "note": "At 20 m/s, 0.6505 rad/s² exceeds the specified 0.12 rad/s² minimum. Initial pitch authority is sufficient in this model, but the test does not model lift-off, runway distance or a complete takeoff.",
      "draftSnapshot": "{\"evidence\":\"0.6505\",\"conclusion\":\"Requirement met\",\"note\":\"At 20 m/s, 0.6505 rad/s² exceeds the specified 0.12 rad/s² minimum. Initial pitch authority is sufficient in this model, but the test does not model lift-off, runway distance or a complete takeoff.\"}"
    }
  ]
}

## Evidence status
Written reasoning awaits instructor review. This export is the current draft; compare it with the answer snapshot of the last run.

## Student reflection
confirmedFor: 13a10918-7e21-49d9-a16b-e75ac0681ff1

observation: The initial accelerations were 0.6505, 0.2422 and 0.0501 rad/s² at 20, 14 and 10 m/s respectively. The first two exceed the 0.12 rad/s² minimum; the 10 m/s case does not. Lower speed reduces available moment because the model scales capacity with speed squared.

change: I corrected the target from 5 to the specified 0.12 rad/s² and made the question about initial pitch response. I confirmed that the 20 m/s trainer meets this requirement, while sufficient authority at one speed does not imply sufficient authority at every speed.

limit: These tests do not determine takeoff distance, lift-off, longer-term pitch stability, crosswind control or flight safety. The short response assumes constant initial acceleration and omits changing aerodynamics, damping and actuator transients.

result: supported