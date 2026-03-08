INTRODUCTION..............................................................................................................................................4

-  a list of system-level security principles to be
considered in the design, development, and operation of an information system. 
- The 35 principles are grouped into the following 4 areas:


1. Security architecture and design
2. Security capability and intrinsic behaviors
3. Life cycle security
4. Approaches to trustworthy secure system development

* SECURITY ARCHITECTURE AND DESIGN  


-- CLEAR ABSTRACTIONS 

  * create a simple, well-defined interface / function, precisely defined.  
  * avoid 
    * - redundant unused interface, 
    * - info hiding, 
    * - semantic overloading of interfaces / parameters
    * - private variables (so they are not percieved by others.)
  
  * - * - * style guide ? ? for developers?
  * lead should be 'free' for the team. 

-- LEAST COMMON MECHANISM 
  * users should share a minial of mechanisms 
  * - no chance of user data getting mixed 
  * - sharing system state
  * - * - clearing the password?
  
-- MODULARITY AND LAYERING 
  - layering - relationships are clear
  - modularity - isolate functions by unit

-- PARTIALLY ORDERED DEPENDENCIES
  - beware of circular dependencies or keep them constrained
  - aim for top-down Approaches
  
--  EFFICIENTLY MEDIATED ACCESS 
 - prevent out of bound access from occuring
  
-- MINIMIZED SHARING 
- encapsulate / no gloabal variables showdow dom does this.  

--REDUCED COMPLEXITY
 -- keeping it simple makes it easier to debug


SECURE EVOLVABILITY - code with a sense of the future
2.9 F.1.9 TRUSTED COMPONENTs - use parts that are dependable

2.10 F.1.10 HIERARCHICAL TRUST - extends previous point
2.11 F.1.11 INVERSE MODIFICATION THRESHOLD - extends previous 
2.12 F.1.12 HIERARCHICAL PROTECTION - if you trust a part, ou shouldn't have to protect yourself from it. 
MINIMIZED SECURITY ELEMENTS - extends trust of parts 

2.14 F.1.14 LEAST PRIVILEGE - givv each part ofnly enough clearnace to do its task.
PREDICATE PERMISSION - many parties should sign off before giving consent
SELF-RELIANT TRUSTWORTHINESS - our trustworthiness hsouldnt' depend on another. 

SECURE DISTRIBUTED COMPOSITION whole should be as secure as its parts 
TRUSTED COMMUNICATION CHANNELS - restricted accessot communication changels for datat  tansmision.


3 F.2 SECURITY CAPABILITY AND INTRINSIC BEHAVIORS ............................................................13
3.1 F.2.1 CONTINUOUS PROTECTION -- all parts must have uninterupted protestionc
3.2 F.2.2 SECURE METADATA MANAGEMENT - metadata should be first class objects
3.3 F.2.3 SELF-ANALYSIS - a part should be able to assess its own state
3.4 F.2.4 ACCOUNTABILITY AND TRACEABILITY - should be able to trace source of an action
3.5 F.2.5 SECURE DEFAULTS - use restrictive defalts
3.6 F.2.6 SECURE FAILURE AND RECOVERY - system failure shouldn't lesad to security vilations
3.7 F.2.7 ECONOMIC SECURITY - security should n't cost more than what coudl be lost if a breach occurs.
3.8 F.2.8 PERFORMANCE SECURITY  - security mechanisms shouldn't degrade system over time unncesssearliy
3.9 F.2.9 HUMAN FACTORED SECURITY  - ui should be intuitive and userf riendly.
3.10 F.2.10 ACCEPTABLE SECURITY - ui shoudl convey sense that privacy assured

4 F.3 LIFE CYCLE SECURITY .....................................................................................................................20
4.1 F.3.1 REPEATABLE AND DOCUMENTED PROCEDURES  - documentation - enables process to repeat itself

4.2 F.3.2 PROCEDURAL RIGOR  - system lifecycle should be as rigousos as its intended trustworkthiness.  

4.3 F.3.3 SECURE SYSTEM MODIFICATION - a systems security should be upgradable. 
4.4 F.3.4 SUFFICIENT DOCUMENTATION ............................................................................................................21


5 F.4 APPROACHES TO TRUSTWORTHY SECURE SYSTEM DEVELOPMENT..............................22
5.1 F.4.1 REFERENCE MONITOR CONCEPT .........................................................................................................22
5.2 F.4.2 DEFENSE IN DEPTH..............................................................................................................................23
5.3 F.4.3 ISOLATION .................................................

SOLID

S
O
L
I
D