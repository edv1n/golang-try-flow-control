# golang-try-flow-control
Golang proposal: nil detection and error handling with try keyword

## Example

```go

f1() (int, string, error) {}

func main() {
  a, s := try f1() else err { return err }
}

```

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
