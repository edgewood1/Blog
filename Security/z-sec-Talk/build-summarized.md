1. initialize
  - if only one instance is running, create a encrypted log file and give self debug privileges
2. monitor build processes
  - is MsBuild.exe running? if so, spawn a thread to determin if orion software is being built, and if so, higjack build operation and inject sunburst.
  - sunspot modifies target code before it is read by compiler
  - runs checks to quit (when injection thread completes, it exists, thus proces not killed)
3. extract from the process memory
   - malware extracts command-line arguments for each MsBuild.exe process from memory
   - this is parsed to extract arguments. sunspot seeks directory path to orion software.  
   - When SUNSPOT finds the Orion solution file path in a running MsBuild.exe process, it replaces a source code file in the solution directory, with a malicious variant to inject SUNBURST while Orion is being built.
4. sunburst source code
   - The source code of SUNBURST was likely sanitized before being included in SUNSPOT. The use of generic variable names, pre-obfuscated strings, and the lack of developer comments or disabled code is similar to what could be obtained after decompiling a backdoored Orion binary
____ read... 


5. 
7. How Sunspot works
 
 
- SUNSPOT masquerades as a legitimate Windows Binary, and writes its logs in a fake VMWare log file.
- SUNSPOT monitors running processes looking for instances of MsBuild.exe.
- sunspot is persisted in a scheduled task set to execute after the ost has booted.
- sunspot configuration encrypted and contains replacement source code (sunburst?), vs solution filename, and targeted source code file paths relative to solution directory.
- The replacement of source code is done only if the MD5 checksums of both the original source code file and backdoored replacement source code match hardcoded values.



 

"The design of SUNSPOT suggests StellarParticle developers invested a lot of effort to ensure the code was properly inserted and remained undetected, and prioritized operational security to avoid revealing their presence in the build environment to SolarWinds developers," CrowdStrike found.