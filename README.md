# yet_another_pprof_wrapper


```go
package main

import (
	yag "github.com/blackbass1988/yet_another_pprof_wrapper"
	"flag"
)

func main() {

	var (
		cpuProfile, heapProfile string
	)

	flag.StringVar(&cpuProfile, "cpuprofile", "", "Write the cpu heapProfile to `filename`")
	flag.StringVar(&heapProfile, "heapprofile", "", "enable heap profiling")
	flag.Parse()

	if cpuProfile != "" {
		go yag.ProfileCpu(cpuProfile)
	}

	if heapProfile != "" {
		go yag.ProfileMemory(heapProfile)
	}

	//do your stuff
}
```
