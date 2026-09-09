# Ask a testable question

## Engineering question
question: Delivery smoke test — revised incomplete draft with spaces, second checkpoint.

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
{}

## Evidence status
Written reasoning awaits instructor review. This export is the current draft; compare it with the answer snapshot of the last run.

## Student reflection
confirmedFor: 