# Log Reviews 

### Examination of system log files to detect security events or to verify the effectiveness of security controls

### Ensure that time is standardized across all networked devices.

### The Network Time Protocol (NTP) version 4, described in RFC 5905, is the industry standard for synchronizing computer clocks between networked devices

### By default, most log files are stored locally on the corresponding device.  The challenge with this approach is that it makes it more difficult to correlate events accross devices to a given incident

# Log Tampering Prevention

### Log files are often among the first artifacts that attackers will use to attempt to hide their actions.

## 5 steps to protect logs:

### 1) Remote logging: Putting the log files on a separate box will require the attackers to target that box too, which at the very least buys you some time to notice the intrusion

### 2) Simplex communication: Use one-way (or simplex) communications between reporting devices and the central log repository

### 3) Replication: By making multiple copies and keeping them in different locations, you make it harder for attackers to alter the log files

### 4) Write-once media: If one of the locations to which you back up your log files can be written to only once, you make it impossible for attackers to tamper with that copy of the data

### 5) Cryptographic hash chaining: To let you know if files changed
