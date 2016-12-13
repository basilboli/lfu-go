
Modified version of https://github.com/dgrijalva/lfu-go adding Pop functionality. 

Can be useful to use it for top counters like top N frequently used something.

Usage:

```go
import "github.com/basilboli/lfu-go"
import "fmt"

// Make a new thing
	c := lfu.New()

// Set some values
	for i := 0; i < 100; i++ {
		c.Set(fmt.Sprintf("somekey%d", i), "foobar")
	}

	for i := 0; i < 30; i++ {
		c.Set("somekey0", "foobar")
	}

	for i := 0; i < 20; i++ {
		c.Set("somekey1", "foobar")
	}
	for i := 0; i < 10; i++ {
		c.Set("somekey2", "foobar")
	}



// Retrieve top N frequently used keys
	topN := 3

	values :=  c.Pop(topN)

	for value := range values {
		fmt.Println(value.Key, value.Freq)
	}

// Should print :
// somekey0, 31
// somekey1, 21
// somekey2, 11

```