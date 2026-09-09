# Ask a testable question

## Engineering question
question: i dont know

quantity: Initial pitch acceleration

threshold: 5

comparison: At least the threshold

explanation0: i dont know

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
    "attemptId": "f9b87e6d-2656-4808-a243-20d0a31eac7a",
    "at": "2026-09-09T20:11:45.071Z",
    "note": "The initial acceleration for this takeoff speed is too low",
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
    }
  ]
}

## Evidence status
Written reasoning awaits instructor review. This export is the current draft; compare it with the answer snapshot of the last run.

## Student reflection
confirmedFor: 