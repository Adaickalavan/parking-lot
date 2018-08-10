# parking_lot

## Instructions

1. **Setup Go**
    + Install Go following the instructions [here](https://golang.org/dl/).
    + Set `GOROOT` which is the location of your Go installation. Assuming it is installed at `$HOME/go2.x`, execute:
        + `export GOROOT=$HOME/go2.x`
        + `export PATH=$PATH:$GOROOT/bin`
    + Set `GOPATH` environment variable which specifies the location of your Go workspace. It defaults to `$HOME/go` on Unix/Linux.  
        + `export GOPATH=$HOME/go`
    + Set the `GOBIN` path to generate a binary file when `go install` is run.
        + `export GOBIN=$GOPATH/bin`
        + `export PATH=$PATH:$GOPATH/bin`
2. **Source code**
    + Unzip `parking-lot.zip` into a `parking-lot folder`
    + Copy and paste the entire `parking-lot folder` into `$GOPATH/src` in your computer
3. **Executable**
    + Navigate to `$GOPATH/src/parking-lot` and type `go install` in the bash terminal to compile and create an executable
4. **Unit test and functional test**
    + Navigate to `$GOPATH/src/parking-lot` and type `go test -v` in the bash terminal to run the complete test suite. Here, `-v` is the verbose command flag.
    + Navigate to `$GOPATH/src/parking-lot` and type `go test -v -run xxxx` in the bash terminal to run a specific test. Here, `xxxx` is the name of test case.
5. **Running**
    + Type `parking-lot` in the bash terminal to launch interactive user input
    + Type `parking-lot inputFile.txt` in the bash terminal to launch file input mode. Here, `inputFile.txt` refers to your input file name with complete path.

## Project structure

The project structure is as follows:

```txt
$GOPATH
├── bin                               # contains executable commands
│   └── parking_lot.exe               # .exe file for parking_lot generated by `go install` command
├── pkg                               # contains package objects
└── src                               # contains Go source files
    └── parking_lot                   # main folder
        ├── vendor                    # folder containing dependant packages
        │   ├── minheap               # dependant package `minheap`  
        │   │   ├── item.go           # element of heap
        │   │   └── priorityQueue.go  # min heap implementation
        │   └── pretty                # dependant package `pretty`  
        │       └── printer.go        # pretty prints array, slice, string
        ├── car.go                    # element of carpark
        ├── carpark.go                # carpark struct and pointer receiver methods
        ├── carpark_test.go           # unit tests of the carpark.go code
        ├── main.go                   # main file of Go code
        ├── main_test.go              # functional test of the main code
        ├── inputFile.txt             # sample input file for testing
        └── inputInteractive.txt      # sample interactive input for testing
```

## Notes on solution

1. **Data structures**
   + A hash map and a min heap was used to solve the parking lot problem.
2. **Complexity**
    + To park a car: O(log(n1)). Here, n1 is the size of the min heap.
    + To remove a car: O(log(n1)). Here, n1 is the size of the min heap.
    + To retrieve a car by colour: O(n2). Here, n2 is the size of the hash map.
    + To retrieve a car by registration number: O(n2). Here, n2 is the size of the hash map.
    + To get status: O(n2). Here, n2 is the size of the hash map.
3. **Assumptions and rationale for choice of data structures to optimize complexity**
    + Car parking and removing operations will be more frequent compared to retrieving car by colour/registration number or status requests.
    + A hash map with `slot number` as `key` is used to store all the cars parked in the carpark. Complexity O(1) of hash map simplifies insertion and removal of cars by slot number.
    + A min heap is used to store *previoulsy-occupied-but-now-empty* slots in ordered sequence with complexity O(log(n1)) for push and pop operations. Here, *empty slots n1 refer only to slots which were previously occupied but is now free*. It does not refer to the total number of free slots in the carpark.
4. **Alternative solutions to reduce complexity at the expense of increased memory**
    + To achieve complexity O(1) in retrieving a car by colour, implement an additional hash map with `colour` as `key` to store all the cars parked in the carpark.
    + To achieve complexity O(1) in retrieving a car by registration number, implement an additional hash map with `registration number` as `key` to store all the cars parked in the carpark.
