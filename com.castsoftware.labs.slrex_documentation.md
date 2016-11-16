# _com.castsoftware.labs.slrex_ Description

This extension provides computation of the following new indicators
* the adjusted number of Critical Violations (anCV), an evolution of the Violation Index (VI), which puts more emphasis on Critical Violations while keeping swarming non-Critical Violations in check,
* the System-level Risk Exposure (SlRE), an evolution of the Propagated Risk Index (PRI), which is application-wide, and which measures both the amount and the "system-level situation" of quality issues
* the System-level Risk Exposure index (SlREi), an evolution of the Risk Propagation Factor (RPF), which is application-wide, and which measures "system-level situation" of quality issues

All these indicators are application-wide but can be applied (using SQL querying for now) to application subsets:
* transactions
* added and updated code
* modules
* technologies
* added and updated violations
* complex and highly complex code
* ...

# In what situation should you install this extension?

If you are interested in getting a preview of what these System-level indicators would be and are willing to share the results to help the CAST Research Labs validate them.

# Release notes

## 1.1.0
Starting with release 1.1.0 of the extension, these indicators are computed using quality rules which support the ASCRM, ASCSM, ASCPEM, ASCMM OMG standards.

## 1.2.0
Starting with release 1.2.0 of the extension, sample AAD tile configuration and static documentation is delivered within the extension.

## 1.3.0
Starting with release 1.3.0 of the extension, sample MS Excel 2013 spreadsheets are delivered within the extension.

## 1.4.0
Starting with release 1.4.0 of the extension, sample MS Excel 2013 spreadsheets are improved to have better UI controls and transaction mapping capabilities.

## 1.5.0
Starting with release 1.5.0 of the extension, computation of indicators for added and updated violations alone are delivered.

## 1.6.0
Starting with release 1.6.0 of the extension, pre-requisites are simplified so as to require only the Transaction extension part of AEP preview (i.e., com.castsoftware.labs.aep.transactions only, and not com.castsoftware.labs.aep.metrics), and ultimately let the Metrics part of AEP preview leverage some violation count indicators from the current extension.

## 1.7.0
Starting with 1.7.0 of the extension, huge RPF are supported and dependency to ASCTDM extension is removed.

## 2.0.0
Starting with 2.0.0 dependency to AEP transaction extension is removed.

# Technology support

All technologies configured to be analyzed by AIP are supported.

# Function Point, Quality and Sizing support

This extension is designed to bring new quality indicator aside existing ones.

# CAST AIP compatibility

This extension is compatible with:

* 8.1.x out-of-the-box \(AIP release used for the tests\)
* 8.0.x out-of-the-box \(there is no reason the extension would not work but it was not tested\)
* 7.x.x after changing the nuspec file \(there is no reason the extension would not work but it was not tested\)

# Supported DBMS servers

This extension is currently only supported on CAST databases installed on CAST Storage Server. All other supported RDBMS are not supported.

# Prerequisites

* An installation of any compatible release of CAST AIP \(see table above\)

# Bug Fix List

N\/A

# Download and installation instructions

Please see:  [Extension Link Installation](http://doc.castsoftware.com/display/DOCEXT/Extension+download+and+installation)

The installation steps are the following:

* download the extension through the CAST Extension Downloader using the https://extend.castsoftware.com:443/labs download server
* open Server Manager 8.x
* select the existing set of databases to update \/ install a new set of databases
* manage extensions of the existing set of database \/ follow the installation wizard up to the manage extension pane
* select _com.castsoftware.labs.slrex.2.0.0_
* run the update \/ the installation  
* open CAST Management Studio
* import the Assessment Model from the Dashboard Service processed in steps \#3 to \#6 above; this is a _Mandatory_ step to start computing the new indicator, one MUST import and use the Assessment Model from the Dashboard that was updated with the extension

# Packaging, delivering and analyzing your source code

Packaging, delivering and analyzing your source code is performed the same way as usual.

To get results:

* run a new snapshot 

# What results can you expect?

## Objects

N\/A

## Links

N\/A

## Quality rules

N\/A

## Technical Criteria

N\/A

## Business Criteria

N\/A

## Sizing indicators

List of new sizing indicators
| ID | Description |
--------------------
1000200|anCV
1000201|SlRE
1000202|SlREi
1000205|Security anCV
1000206|Security SlRE
1000207|Security SlREi
1000210|Efficiency anCV
1000211|Efficiency SlRE
1000212|Efficiency SlREi
1000215|Reliability anCV
1000216|Reliability SlRE
1000217|Reliability SlREi
1000220|Changeability anCV
1000221|Changeability SlRE
1000222|Changeability SlREi
1000225|Transferability anCV
1000226|Transferability SlRE
1000227|Transferability SlREi
1000230|ASCSM anCV
1000231|ASCSM SlRE
1000232|ASCSM SlREi
1000235|ASCPEM anCV
1000236|ASCPEM SlRE
1000237|ASCPEM SlREi
1000240|ASCRM anCV
1000241|ASCRM SlRE
1000242|ASCRM SlREi
1000245|ASCMM anCV
1000246|ASCMM SlRE
1000247|ASCMM SlREi

with:
* anCV = adjusted number of Critical Violations
* SlRE = System-level Risk Exposure
* SlREi = System-level Risk Exposure index
* ASCMM = Automated Source Code Maintainability Measure
* ASCPEM = Automated Source Code Performance Efficiency Measure
* ASCRM = Automated Source Code Reliability Measure
* ASCSM = Automated Source Code Security Measure
* ASCxM = all ASCMM, ASCPEM, ASCRM, and ASCSM

## How to read them

### nV, nCV, and anCV 
They are basically count of violations
* I.e., it's basically the number of violated rules per object
* In the case, of anCV, when the rule is not critical, it counts only as a share of a critical one; we always have nV >= anCV >= nCV

E.g.: 
anCV of 10 means 
* 10 critical rules violated by 1 object, 
* or 9 critical rules and 3 major rules violated by 1 object, 
* or 9 critical rules and 8 minor rules violated by 1 object, ...

### SlREf, and SlREi
They are basically a scaled down value of RPF

Bin number | Bin RPF max. | Bin RPF min. | Bin weight
-----------------------------------------------------
0 | - | - | 1
1 | 2 | 1 | 2
2 | 6 | 3 | 4
3 | 14 | 7 | 6
4 | 30 | 15 | 9
5 | 62 | 31 | 12
6 | 126 | 63 | 16
7 | 254 | 127 | 20
8 | 510 | 255 | 24
9 | 1,022 | 511 | 28
10 | 2,046 | 1,023 | 33
11 | 4,094 | 2,047 | 37
12 | 8,190 | 4,095 | 43
13 | 16,382 | 8,191 | 48
14 | 32,766 | 16,383 | 53
15 | 65,534 | 32,767 | 59
16 | 131,070 | 65,535 | 65
17 | 262,142 | 131,071 | 71
18 | 524,286 | 262,143 | 77
19 | 1,048,574 | 524,287 | 84
20 | 2,097,150 | 1,048,575 | 90
21 | 4,194,302 | 2,097,151 | 97
22 | 8,388,606 | 4,194,303 | 104
23 | 16,777,214 | 8,388,607 | 111
24 | 33,554,430 | 16,777,215 | 119
25 | 67,108,862 | 33,554,431 | 126
26 | 134,217,726 | 67,108,863 | 134
27 | 268,435,454 | 134,217,727 | 141
28 | 536,870,910 | 268,435,455 | 149
29 | 1,073,741,822 | 536,870,911 | 157
30 | 2,147,483,646 | 1,073,741,823 | 165
31 | 4,294,967,294 | 2,147,483,647 | 174

E.g.: 
An SlREf or SlREi of 9 means we are considering issues with 15 to 30 distinct call paths to it

### SlRE 
Theys are the product of the previous two.

Depending on the scope of objects and rule set, the value can greatly vary
E.g.: 1 Mo LOC software, ~ 60k Artifacts, ~ 2.5 kAFP can get 60k SlRE for a Health Factor
E.g.: 1 Transaction, ~ 10k Objects / ~ 5k Artifacts, 6 AFP can get 10k SlRE for a Health Factor
E.g.: 1 Transaction, 3 Objects / 1 Artifact, 7 AFP can get 60 SlRE for a Health Factor and 0 for another

## How to use them

### nV, nCV, anCV
* Can be used as alternatives to current count of [critical] violations
* The larger the worse: 
  * As for nCV, every single point counts; 
  * As for anCV, every single point counts as well as non-critical violations, left unchecked and spreading, create a critical situation
* Valid for any scope of objects and rule sets, even for an RPF range bin

### SlREi 
* The larger the worse
* Valid for any scope of objects and rule sets;
* Valid but not really valuable 
  * for an RPF range bin as it would be equal to SlREf by definition
  * for Transferability rule set as it would be always equal to 1 (so long as we use currentTransferability RPF definition)

### SlRE
* The larger the worse
* Valid for any scope of objects and rule sets

## Specifically about benchmarking and monitoring

Numbers can be compared despite differences in software size
* This is about Risk Exposure so 
  * greater exposure in a larger software leads to higher number, but this is not a strong correlation: a 3 Mo LOC software can have better SlREi than 80k LOC software
  * software being built can see its SlREi deteriorate because the integration of components increases the exposure
* RPF ranges that are considered to build the distributions and the weighting scheme are stable
  * In other words, the SlREf is the same in all softwares for the same RPF range

# Limitations

Handle the "Generic" Quality Area with care as it considers: 
* that the RPF is always based on the number of distinct call paths to the object carrying the issue(s). A rule-dependant configuration may be required in the future for more accurate modeling.
* that the severity is estimated based on current TC weight into the TQI BC, causing rules to have a generally higher severity than intended with Health Factors
