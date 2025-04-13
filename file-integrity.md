
# Python: File Integrity Checker

**Objective**: Create a Python script to monitor files for unauthorized changes by comparing their hashes and alerting on modifications.

**Difficulty**: 7/9  
**Time**: 30 minutes

## Steps

1. **Setup**  
   - Import required libraries:  
     ```python
     import hashlib
     import os
     ```

2. **Hash File**  
   - Define a function to compute the SHA-256 hash of a file:  
     ```python
     def hash_file(file):
         return hashlib.sha256(open(file, 'rb').read()).hexdigest()
     ```

3. **Baseline**  
   - Create a dictionary of baseline hashes for monitored files:  
     ```python
     baseline = {f: hash_file(f) for f in ['file1.txt']}
     ```

4. **Check**  
   - Compare current file hashes against the baseline and alert on mismatches:  
     ```python
     for f in baseline:
         if hash_file(f) != baseline[f]:
             print(f"{f} modified!")
     ```

5. **Run**  
   - Test the script by modifying `file1.txt` and running the script to verify it detects the change.

## Solution

The script monitors specified files and alerts when changes are detected by comparing current SHA-256 hashes against baseline values.
