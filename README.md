# AprilTagMatchingAlgorithm

Algorithm to best fit one array of IDs to another

```swift
/// Takes the generated markers for an edge and an array of sorted scanned markers by Y (or X depending on which edge). Tries to create the best match
/// between the two as output. Missing markers in scanned come out as -1 in final array. These are the missing markers if any,
/// - Parameters:
///   - generated: This is the genrated list of tagID's for an edge
///   - scanned: This is the scanneed list of tragID's for an edge ( may be smaller )
/// - Returns: a list of matched markers with -1 in gaps where markers didn't match
func compare(generated: [Int], scanned: [Int]) -> [Int] {
    
    var scannedArray = scanned // make copy of scanned array so we can mutate it
    var matchingArray = Array(repeating: -1, count: generated.count) // create output array pre-filled with -1s
    var index = 0
    
    for _ in matchingArray { // Start going through the matching array
        
        if scannedArray.isEmpty {
            break
        }
        if generated[index] == scannedArray[0] {
            matchingArray[index] = scannedArray[0]  // they match so put in matching array
            scannedArray.remove(at: 0)              // remove first Int from scanned array  as it is found
        }
        index += 1
    }
    
    return matchingArray
}

var generated = [1, 3, 4, 3, 2, 1, 2, 1, 3, 4]   // Expected
var scanned =   [1 ,3, 4,    2,    2, 1, 3]      // What we got
let output = compare(generated: generated, scanned: scanned)

# output [1, 3, 4, -1, 2, -1, 2, 1, 3, -1]
```
