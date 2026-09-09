# Choose the yaw-moment model

## Engineering question
For a separate twin-engine utility aircraft, can 8.6 kN m of usable opposing rudder/vertical-tail moment balance the yaw disturbance after losing 2.4 kN thrust at a 3.1 m lateral offset?

## Physics model
equation: deltaT*y

effector: Rudder / vertical tail

explanation1: The rudder must be able to at least supply a moment equal to or greater than the lost moment provided by the lost engine to keep the airplane from yawing

rudderEquation: -deltaT*y

## Inputs
Positive yaw turns the nose to the right, viewed from above. The right engine loses thrust; the left engine keeps pushing, creating a positive (nose-right) disturbance. deltaT is the positive thrust loss in N and y is the positive 3.1 m distance from the centreline. The rudder must create a negative (nose-left) moment to balance it. If the left engine fails instead, both moment signs reverse. Maximum usable opposing rudder capacity is 8600 N m.

## Outputs
Signed disturbance, required signed rudder moment, applied signed rudder moment, net yaw moment (all N m), and remaining capacity magnitude.

## Assumptions
Offset thrust creates yaw demand. Rudder primarily controls yaw but may couple to roll; ailerons primarily roll and can cause adverse yaw. Elevator primarily pitches. Flaps change lift/drag and pitching moment; spoilers change lift/drag and may roll; propulsion contributes forces and moments. These are dominant, not exclusive, responses.

## Validity
Static yaw balance only. No proof of engine-out controllability, bank limits, transient response, or minimum control speed.

## Predictions
Doubling lost thrust at fixed arm doubles yaw demand and reduces margin.

## Manual reference
Right-engine loss: disturbance +7440 N m; balancing rudder -7440 N m; net 0 N m. Capacity remaining: 8600-7440=1160 N m. Full -8600 N m would overcorrect to -1160 N m net.

## Verification cases
Zero loss → zero demand; 2400 N loss →7440 N m; 4800 N loss →14880 N m.

## Feature requirements
Plot yaw demand against lost thrust and compare with 8600 N m capacity; identify the yaw effector and the sign/magnitude convention.

## Implementation
Evaluate both student expressions. For illustration, apply only the opposing moment needed for balance, capped at -8600 N m. This ideal static command assumes immediate response; it is not an actuator or flight-control model.

## Decision
Retain only the nominal static yaw screen; investigate coupling, actuator limits, and uncertainty before an operational claim.

## Recorded investigations
{
  "0": {
    "attemptId": "f1322769-b414-4383-bce7-ede41a965402",
    "at": "2026-09-09T20:45:32.312Z",
    "note": "There is no disturbance in this case because there is no lost engine so the rudder does not need to be used",
    "evidence": "0",
    "conclusion": "Requirement met",
    "readouts": [
      {
        "label": "Your signed engine-out disturbance (positive = nose right)",
        "studentField": "equation",
        "unit": "N m",
        "value": 0
      },
      {
        "label": "Maximum opposing rudder capacity (magnitude, not command)",
        "expression": "available",
        "unit": "N m",
        "value": 8600
      },
      {
        "label": "Margin against your equation",
        "studentMargin": "equation",
        "capacity": "available",
        "unit": "N m",
        "value": 8600
      },
      {
        "label": "Your signed rudder moment needed for balance",
        "studentField": "rudderEquation",
        "unit": "N m",
        "value": 0
      },
      {
        "label": "Ideal applied rudder moment (negative = nose left; capacity limited)",
        "expression": "-0.0",
        "unit": "N m",
        "value": 0
      },
      {
        "label": "Net moment with ideal capacity-limited command",
        "expression": "student + (-0.0)",
        "unit": "N m",
        "value": 0
      }
    ],
    "inputs": {
      "deltaT": 0
    }
  },
  "2400": {
    "attemptId": "f1322769-b414-4383-bce7-ede41a965402",
    "at": "2026-09-09T20:47:34.126Z",
    "note": "The rudder is capable of supplying an opposing moment of 8600 N-m but the lost thrust case of 2400 N only requires a rudder balancing moment of 7440 N-m so the requirement is met. The rudder can balance this case",
    "evidence": "-7440",
    "conclusion": "Requirement met",
    "readouts": [
      {
        "label": "Your signed engine-out disturbance (positive = nose right)",
        "studentField": "equation",
        "unit": "N m",
        "value": 7440
      },
      {
        "label": "Maximum opposing rudder capacity (magnitude, not command)",
        "expression": "available",
        "unit": "N m",
        "value": 8600
      },
      {
        "label": "Margin against your equation",
        "studentMargin": "equation",
        "capacity": "available",
        "unit": "N m",
        "value": 1160
      },
      {
        "label": "Your signed rudder moment needed for balance",
        "studentField": "rudderEquation",
        "unit": "N m",
        "value": -7440
      },
      {
        "label": "Ideal applied rudder moment (negative = nose left; capacity limited)",
        "expression": "-7440.0",
        "unit": "N m",
        "value": -7440
      },
      {
        "label": "Net moment with ideal capacity-limited command",
        "expression": "student + (-7440.0)",
        "unit": "N m",
        "value": 0
      }
    ],
    "inputs": {
      "deltaT": 2400
    }
  },
  "4800": {
    "attemptId": "f1322769-b414-4383-bce7-ede41a965402",
    "at": "2026-09-09T20:49:07.058Z",
    "note": "This case requires a rudder moment of 14880 to balance the lost engine. However, the rudder is only capable of supplying a net moment of 8600 N-m. Therefore the rudder is insufficient for this case.",
    "evidence": "-14880",
    "conclusion": "Insufficient authority",
    "readouts": [
      {
        "label": "Your signed engine-out disturbance (positive = nose right)",
        "studentField": "equation",
        "unit": "N m",
        "value": 14880
      },
      {
        "label": "Maximum opposing rudder capacity (magnitude, not command)",
        "expression": "available",
        "unit": "N m",
        "value": 8600
      },
      {
        "label": "Margin against your equation",
        "studentMargin": "equation",
        "capacity": "available",
        "unit": "N m",
        "value": -6280
      },
      {
        "label": "Your signed rudder moment needed for balance",
        "studentField": "rudderEquation",
        "unit": "N m",
        "value": -14880
      },
      {
        "label": "Ideal applied rudder moment (negative = nose left; capacity limited)",
        "expression": "-8600",
        "unit": "N m",
        "value": -8600
      },
      {
        "label": "Net moment with ideal capacity-limited command",
        "expression": "student + (-8600)",
        "unit": "N m",
        "value": 6280
      }
    ],
    "inputs": {
      "deltaT": 4800
    }
  }
}

## Interpretation attempts
{
  "0": [
    {
      "correct": true,
      "feedback": "Your interpretation matches this comparison: Requirement met. Your signed rudder moment needed for balance: 0 N m. 8,600 ≥ 0 Written reasoning still awaits instructor review.",
      "attemptId": "f1322769-b414-4383-bce7-ede41a965402",
      "at": "2026-09-09T20:45:32.312Z",
      "conclusion": "Requirement met",
      "evidence": "0",
      "note": "There is no disturbance in this case because there is no lost engine so the rudder does not need to be used",
      "draftSnapshot": "{\"evidence\":\"0\",\"conclusion\":\"Requirement met\",\"note\":\"There is no disturbance in this case because there is no lost engine so the rudder does not need to be used\"}"
    }
  ],
  "2400": [
    {
      "correct": true,
      "feedback": "Your interpretation matches this comparison: Requirement met. Your signed rudder moment needed for balance: -7,440 N m. 8,600 ≥ 7,440 Written reasoning still awaits instructor review.",
      "attemptId": "f1322769-b414-4383-bce7-ede41a965402",
      "at": "2026-09-09T20:47:34.126Z",
      "conclusion": "Requirement met",
      "evidence": "-7440",
      "note": "The rudder is capable of supplying an opposing moment of 8600 N-m but the lost thrust case of 2400 N only requires a rudder balancing moment of 7440 N-m so the requirement is met. The rudder can balance this case",
      "draftSnapshot": "{\"evidence\":\"-7440\",\"conclusion\":\"Requirement met\",\"note\":\"The rudder is capable of supplying an opposing moment of 8600 N-m but the lost thrust case of 2400 N only requires a rudder balancing moment of 7440 N-m so the requirement is met. The rudder can balance this case\"}"
    }
  ],
  "4800": [
    {
      "correct": true,
      "feedback": "Your interpretation matches this comparison: Insufficient authority. Your signed rudder moment needed for balance: -14,880 N m. 8,600 ≥ 14,880 Written reasoning still awaits instructor review.",
      "attemptId": "f1322769-b414-4383-bce7-ede41a965402",
      "at": "2026-09-09T20:49:07.058Z",
      "conclusion": "Insufficient authority",
      "evidence": "-14880",
      "note": "This case requires a rudder moment of 14880 to balance the lost engine. However, the rudder is only capable of supplying a net moment of 8600 N-m. Therefore the rudder is insufficient for this case.",
      "draftSnapshot": "{\"evidence\":\"-14880\",\"conclusion\":\"Insufficient authority\",\"note\":\"This case requires a rudder moment of 14880 to balance the lost engine. However, the rudder is only capable of supplying a net moment of 8600 N-m. Therefore the rudder is insufficient for this case.\"}"
    }
  ]
}

## Evidence status
Written reasoning awaits instructor review. This export is the current draft; compare it with the answer snapshot of the last run.

## Student reflection
confirmedFor: f1322769-b414-4383-bce7-ede41a965402

change: I did not change anything

result: supported

observation: There is a maximum loss of thrust that can be overcome by this rudder. This is somewhere close to about 2700 N. If the lost thrust is greater than about 2700 N then the current rudder is insufficient to keep the airplane from yawing.

limit: I dont know