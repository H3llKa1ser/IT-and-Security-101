# Common Vulnerabilities Scoring System (CVSS)

### Consists of metrics such as:

#### 1) Attack Vector (AV)

 - Local (L): 0.395

 - Adjacent (A): 0.646

 - Network (N): 1

#### 2) Access Complexity (AC)

 - High (H): 0.350

 - Medium (M): 0.61

 - Low (L): 0.71

#### 3) Authentication (Au)

 - Multiple (M): 0.45

 - Single (S): 0.56

 - None (N): 0.704

#### 4) Confidentiality Impact (C)

 - None (N): 0

 - Partial (P): 0.275

 - Complete (C): 0.66

#### 5) Integrity Impact (I)

 - None (N): 0

 - Partial (P): 0.275

 - Complete (C): 0.66

#### 6) Availability Impact (A)

 - None (N): 0

 - Partial (P): 0.275

 - Complete (C): 0.66

## CVSS Base Score Formula

 - ((0.6 * Impact) + (0.4 * Exploitability) -1.5) + Impact Function

 - Impact = 10.41 * (1- (1- Confidentiality) * (1 - Integrity) * (1 - Availability))

 - Exploitability = 20 * Attack Vector * Access Complexity * Authentication

 - Impact Function = 0 if Impact is also 0, 1.176 otherwise

# CVSS v2.0 Ratings

## Severity -> Base Score Range

#### 1) Low -> 0.0-3.9

#### 2) Medium -> 4.0-6.9

#### 3) High -> 7.0-10.0

# CVSS v3.0 Ratings

## Severity -> Base Score Range

#### 1) None -> 0.0

#### 2) Low -> 0.1-3.9

#### 3) Medium -> 4.0-6.9

#### 4) High -> 7.0-8.9

#### 5) Critical -> 9.0-10.0
