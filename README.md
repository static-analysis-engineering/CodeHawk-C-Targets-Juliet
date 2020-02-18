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



