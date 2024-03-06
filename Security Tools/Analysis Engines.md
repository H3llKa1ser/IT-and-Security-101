# Analysis Engines

## Signature Based (Pattern Matching)

### Most netwrok attacks have distinct "signatures: that is data that is passed between attacker and victim. A signature based NIDS has a database of known attack signatures, and compares network traffic against this database.

## Concerns for Signature Based Systems

### 1) Pay for a signature subscription from vendor

### 2) Keep signatures updated

### 3) Does not protect against 0day attacks!

## Anomaly Based (Profile Matching)

### Anomaly based systems, look for changes in "normal" behavior. To do this generally you let an anomaly based system learn what normal behavior is over a few days or weeks, creating a baseline.

### The anomaly base dsystem will then look for traffic types and volume that is outside of the normal behavior.
