# Redundancy of Data

## Backups

### Backing up software and having backup hardware is a large part of network availability

### It is important to be able to restore data:

#### 1) If a hard drive fails

#### 2) A disaster takes place

#### 3) Some type of software corruption

## Backup types:

### 1) Full backup

#### Archive Bit is reset

### 2) Incremental Backup

#### Backs up all files that have been modified since last backup

#### Archive Bit is reset

### 3) Differential Backup

#### Backs up all files that have been modified since last FULL backup

#### Archive Bit is NOT reset

### 4) Copy Backup 

#### Same as full backup, but Archive Bit is not reset

#### Use before upgrades, or system maintenance

## Backup Issues

### 1) Identify what needs to be backed up first

### 2) Media rotation scheme (Tower of Hanoi, Grandfather, father, son)

### 3) Backup schedule needs to be developed

### 4) If restoring a backup after a compromise, ensure that the backup material does not contain the same vulnerabilities that were exploited
