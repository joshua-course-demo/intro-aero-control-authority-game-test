# Respect derivative units and usable travel

## Engineering question
Using Chapter 6 Worked Example A, does a requested dCm=-0.25 lie within the usable positive elevator travel?

## Physics model
deltaRad=demand/slope; deltaDeg=deltaRad*180/pi. Here slope is per radian; positive elevator deflection produces a negative pitching-moment increment.

## Inputs
slope: -1.05

demand: -0.25

usableLimit: 18

explanation2: The example requires a change in pitching moment coefficient of -0.25 up to an elevator deflection of 18 degrees. Over this range, the slope of the moment coefficient vs pitch angle is -1.05.

## Outputs
Required elevator deflection in rad and deg, travel residual in deg, and local-screen status.

## Assumptions
The local derivative is held fixed provisionally. The stated usable stop is a limit, not proof that the derivative applies throughout the travel.

## Validity
Local derivative/travel screen only. Actuator holding force, rate, nonlinear response and coupled limits remain unverified.

## Predictions
The required deflection should be positive and smaller than 18 degrees.

## Manual reference
(-0.25)/(-1.05)=0.238095 rad=13.6419 deg; residual=4.3581 deg.

## Verification cases
Retain the negative coefficient sign; use -1.05 per radian, not per degree; compare 13.6419 deg with the 18 deg usable limit.

## Feature requirements
Plot demand-derived deflection against coefficient demand and show the usable limit in degrees.

## Implementation
For each coefficient demand evaluate demand/slope*180/pi and compare with the supplied usableLimit. Do not substitute degrees into a per-radian derivative.

## Decision
Provisionally retain the local travel screen; request a coefficient-versus-deflection sweep and actuator data.

## Recorded investigations
{
  "-0.25": {
    "attemptId": "2cb1c93f-de66-4f1d-9925-99465f57879f",
    "at": "2026-09-09T21:05:28.972Z",
    "note": "13.6419 degrees is less than the maximum of 18 degrees so this check passes",
    "evidence": "0.2381",
    "conclusion": "Within positive travel",
    "readouts": [
      {
        "label": "Required deflection",
        "expression": "demand/slope",
        "unit": "rad",
        "value": 0.23809523809523808
      },
      {
        "label": "Required deflection",
        "expression": "demand/slope*180/pi",
        "unit": "deg",
        "value": 13.6418522650196
      },
      {
        "label": "Usable positive travel",
        "expression": "usableLimit",
        "unit": "deg",
        "value": 18
      },
      {
        "label": "Positive travel residual",
        "expression": "usableLimit-demand/slope*180/pi",
        "unit": "deg",
        "value": 4.358147734980401
      }
    ],
    "inputs": {
      "demand": -0.25
    }
  },
  "-0.35": {
    "attemptId": "2cb1c93f-de66-4f1d-9925-99465f57879f",
    "at": "2026-09-09T21:06:13.272Z",
    "note": "For this case, the required deflection of 19.0986 degrees is beyond the usable positive travel of 18 degrees so this check fails",
    "evidence": "0.3333",
    "conclusion": "Outside declared positive travel",
    "readouts": [
      {
        "label": "Required deflection",
        "expression": "demand/slope",
        "unit": "rad",
        "value": 0.3333333333333333
      },
      {
        "label": "Required deflection",
        "expression": "demand/slope*180/pi",
        "unit": "deg",
        "value": 19.098593171027442
      },
      {
        "label": "Usable positive travel",
        "expression": "usableLimit",
        "unit": "deg",
        "value": 18
      },
      {
        "label": "Positive travel residual",
        "expression": "usableLimit-demand/slope*180/pi",
        "unit": "deg",
        "value": -1.0985931710274421
      }
    ],
    "inputs": {
      "demand": -0.35
    }
  }
}

## Interpretation attempts
{
  "-0.25": [
    {
      "correct": false,
      "feedback": "Re-read “Required deflection”. Record its value in the labelled units (numbers within ±0.0001), then compare it with the criterion. Check the sign first, then compare the required positive deflection with the usable travel.",
      "attemptId": "2cb1c93f-de66-4f1d-9925-99465f57879f",
      "at": "2026-09-09T21:05:02.972Z",
      "conclusion": "Within positive travel",
      "evidence": "13.6419",
      "note": "13.6419 degrees is less than the maximum of 18 degrees so this check passes",
      "draftSnapshot": "{\"evidence\":\"13.6419\",\"conclusion\":\"Within positive travel\",\"note\":\"13.6419 degrees is less than the maximum of 18 degrees so this check passes\"}"
    },
    {
      "correct": true,
      "feedback": "Your interpretation matches this comparison: Within positive travel. Required deflection: 0.2381 rad. 13.6419 ≤ 18 Written reasoning still awaits instructor review.",
      "attemptId": "2cb1c93f-de66-4f1d-9925-99465f57879f",
      "at": "2026-09-09T21:05:28.972Z",
      "conclusion": "Within positive travel",
      "evidence": "0.2381",
      "note": "13.6419 degrees is less than the maximum of 18 degrees so this check passes",
      "draftSnapshot": "{\"evidence\":\"0.2381\",\"conclusion\":\"Within positive travel\",\"note\":\"13.6419 degrees is less than the maximum of 18 degrees so this check passes\"}"
    }
  ],
  "-0.35": [
    {
      "correct": true,
      "feedback": "Your interpretation matches this comparison: Outside declared positive travel. Required deflection: 0.3333 rad. 19.0986 ≤ 18 Written reasoning still awaits instructor review.",
      "attemptId": "2cb1c93f-de66-4f1d-9925-99465f57879f",
      "at": "2026-09-09T21:06:13.272Z",
      "conclusion": "Outside declared positive travel",
      "evidence": "0.3333",
      "note": "For this case, the required deflection of 19.0986 degrees is beyond the usable positive travel of 18 degrees so this check fails",
      "draftSnapshot": "{\"evidence\":\"0.3333\",\"conclusion\":\"Outside declared positive travel\",\"note\":\"For this case, the required deflection of 19.0986 degrees is beyond the usable positive travel of 18 degrees so this check fails\"}"
    }
  ]
}

## Evidence status
Written reasoning awaits instructor review. This export is the current draft; compare it with the answer snapshot of the last run.

## Student reflection
confirmedFor: 2cb1c93f-de66-4f1d-9925-99465f57879f

observation: The coefficient demand for the elevator lies somewhere between -0.25 and -0.35

change: I didnt change anything

limit: Whether this elevator is sufficient to actually control the airplane under a given set of conditions.

result: supported