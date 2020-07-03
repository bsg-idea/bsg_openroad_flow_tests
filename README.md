# BSG OpenROAD-Flow Tests

This repsoitory contains test cases for the designs checked into the
[OpenROAD-Flow](https://github.com/The-OpenROAD-Project/OpenROAD-Flow). These
test cases are designed to be run using Synopsys VCS. Directories in the
repository's root are the names of the design with sub-directories for each test case.

## How To Use

To run a test case, first enter the design directory and then enter the test case you
want to run. Inside the test case directory should be a Makefile which is used to run the
simulation. Before running the simulation, you will need to open the Makefile and set
a couple variables at the top of the Makefile. These variables are:

1. `LM_LICENSE_FILE` - Path to a valid license file / server for Synopsys VCS

2. `VCS` - Full path to Synopsys VCS binary (tested on version L-2016.06-SP2-15)

Once those variables have been set, save and close the makefile and then run:

```
$ make run
```

This will build and run the simulation, easy as that (hopefully)!
