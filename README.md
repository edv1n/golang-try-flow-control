# golang-try-flow-control
Golang proposal: nil detection and error handling with try keyword

## Example

```go

f1() (int, string, error) {}

func main() {
  a, s := try f1() with err { return err }
}

```

Problem: why try shall only check the last result, and return the non-last results? Also, the `with` syntax is special here.

```go

func main() {
  var v = byte(nil)
  
  try v {
    fmt.Println("v is nil")
  } else {
    fmt.Println("v is not nil")
  }
}

// result:
// v is nil
```

```go
func main() {
  try v := byte(nil); v {
    fmt.Println("v is nil")
  } else {
    fmt.Println("v is not nil")
  }
}

// result:
// v is nil
```

```go
f1() (int, string, error) {}

func main() {
  a, s, err := f1(); try err { return err }
}
```
