
Modified version of https://github.com/dgrijalva/lfu-go adding Pop functionality. 

Can be useful to use it for top counters like top N frequently used something.

Usage:

```go
import "github.com/basilboli/lfu-go"

// Make a new thing
c := lfu.New()

// Set some values
for i := 0; i < 10; i++ {
	c.Set("somekey" + i, myValue)
}

for i := 0; i < 5; i++ {
	c.Set("somekey" + i, myValue)
}

// Retrieve top N frequently used keys
	topN := 3
	values :=  c.Pop(topN)
	for value := range values {
		fmt.Println(value.Key, value.Freq)
	}
}

// Should print 
// somekey0, 2
// somekey1, 2
// somekey2, 2

```