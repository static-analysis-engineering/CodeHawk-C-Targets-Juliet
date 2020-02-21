# CodeHawk-C-Targets-Juliet
Juliet Test Suite v1.3 prepared for analysis by the CodeHawk-C Analyzer

### Origin
The Juliet Test Suite is a collection of test cases in C/C++ (we
only include the C test cases) developed by the NSA Center for Assured
Software, updated by NIST, and maintained by NIST as part of the
[SARD Test Suites](https://samate.nist.gov/SRD/testsuite.php).

We use
[version 1.3](https://www.nist.gov/publications/juliet-13-test-suite-changes-12),
which was released in October 2017 by NIST, and fixes a number of systematic
problems in the earlier versions.

### Organization
The test cases are organized in a similar way as the original Test
Suite except that the file hierarchy is extended by one level to
create separate directories for each functional variant that solely
contains the flow (controlflow/dataflow) variants for that
functional variant. Furthermore, C++ variants have been removed.

Each functional variant directory contains the following files:
- **[name]_src.tar.gz**, the original c source files
- **semantics_linux.tar.gz**: the semantic artifacts, the result
  of preprocessing and parsing the source files (on a linux
  platform) into XML files.
- **scorekey.json**: json file that identifies the type and locations
  of the vulnerabilities in each controlflow/dataflow variant.

These files provide all necessary information for the analysis; there
is no need for parsing; the analysis can be run either on macOS or on
linux.

### Access from the CodeHawk-C analyzer

Add the following line to your chc/util/ConfigLocal.py file (if not
present,copy from ConfigLocal.template):
```
    juliettargets_home = os.path.expanduser('~')
    config.targets = {
       "juliet": os.path.join(juliettargets_home,
	                            "CodeHawk-C-Targets-Juliet/targets/juliettestcases.json")
        }
```
(modify juliettargets_home to hold your local path to the CodeHawk-C-Targets-Juliet
repository). When registered in this way the scrips in CodeHawk-C/chc/cmdline/juliet
can be directly used as described
[here](https://github.com/kestreltechnology/CodeHawk-C/chc/cmdline/juliet/README.md).


### Scoring
Most tests have a scorekey.json file that contains a specification of
the primary proof obligations involved in the tested vulnerability. To
evaluate the analysis results against this score key:

```
> python chc_score_juliettest.py CWE121 CWE129_rand
```
This will create a report of the status of all listed proof
obligations in each file of the test and a summary for all tests in
the test case, e.g., for the above test case:
```
test              violations                    safe-controls
         V    S    D    U    O                S    D    X    U    O
--------------------------------------------------------------------------------
01       0    0    0    1    0       |        2    0    0    0    0
02       0    0    0    1    0       |        3    0    0    0    0
03       0    0    0    1    0       |        3    0    0    0    0
04       0    0    0    1    0       |        4    0    0    0    0
05       0    0    0    1    0       |        4    0    0    0    0
06       0    0    0    1    0       |        4    0    0    0    0
07       0    0    0    1    0       |        4    0    0    0    0
08       0    0    0    1    0       |        4    0    0    0    0
09       0    0    0    1    0       |        4    0    0    0    0
10       0    0    0    1    0       |        4    0    0    0    0
11       0    0    0    1    0       |        4    0    0    0    0
12       0    0    0    1    0       |        5    0    0    0    0
13       0    0    0    1    0       |        4    0    0    0    0
14       0    0    0    1    0       |        4    0    0    0    0
15       0    0    0    1    0       |        4    0    0    0    0
16       0    0    0    1    0       |        2    0    0    0    0
17       0    0    0    1    0       |        2    0    0    0    0
18       0    0    0    1    0       |        2    0    0    0    0
21       0    0    1    0    0       |        3    0    0    0    0
22       0    0    1    0    0       |        3    0    0    0    0
31       0    0    0    1    0       |        2    0    0    0    0
32       0    0    0    1    0       |        1    0    0    1    0
34       0    0    0    1    0       |        1    0    0    1    0
41       0    0    1    0    0       |        2    0    0    0    0
42       1    0    0    0    0       |        2    0    0    0    0
44       0    0    1    0    0       |        2    0    0    0    0
45       0    0    0    1    0       |        2    0    0    0    0
51       0    0    1    0    0       |        2    0    0    0    0
52       0    0    1    0    0       |        2    0    0    0    0
53       0    0    1    0    0       |        2    0    0    0    0
54       0    0    1    0    0       |        2    0    0    0    0
61       1    0    0    0    0       |        2    0    0    0    0
63       0    0    1    0    0       |        2    0    0    0    0
64       0    0    0    1    0       |        1    0    0    1    0
65       0    0    1    0    0       |        2    0    0    0    0
66       0    0    0    1    0       |        1    0    0    1    0
67       0    0    0    1    0       |        1    0    0    1    0
68       0    0    0    1    0       |        2    0    0    0    0
--------------------------------------------------------------------------------
total    2    0   10   26    0       |      100    0    0    5    0
```
where the column headers stand for the following
- (violations): V:violation, S:found-safe, D:delegated, U:unknown, O:other
- (safe-controls): S:safe, D:delegated, X:dead-code, U:unknown,
O:other

For the violations block,
something is wrong with the analyzer if a proof obligation for a violation is proven
safe (i.e., if any of the numbers in the S column under violations is
non-zero). Analysis is incomplete if a proof obligation for a
violation is deferred to the caller, but the caller does not identify
it as a violation (column D), or if the proof obligation is still open
(column U).

Similarly for the safe-controls block, something is wrong if a
violation is indicated (i.e., if any of the numbers in the O column is
non-zero).

### Dashboard

To see a summary of the results of all test cases:
```
> python chc_juliet_dashboard.py
```
or a summary for the results of a particular control flow/dataflow
variant, say 01, the baseline variant:
```
> python chc_juliet_dashboard_variant.py 01
```
which will show the results for all x01.c files in all test cases.

Each of these will show an overall summary for all test cases, e.g.,
```
                            violation      safe-control     total
--------------------------------------------------------------------------------
ppos                           4907           9176          14083
reported                       2428           6305           8733
percent reported               49.5           68.7           62.0
--------------------------------------------------------------------------------
```
which gives the percentage of all proof obligations related to vulnerabilities
that were reported, and the percentage of all proof obligations related to the
fixed vulnerabilities.

