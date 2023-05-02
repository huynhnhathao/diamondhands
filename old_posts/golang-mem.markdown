<!-- ---

layout: post
title:  "Golang recipes"
date:   2022-05-14 13:05:18 +0700
categories: golang
--- -->

## Rules
- If no initial value is given to a variable, the Go compiler will assign it with a default zero value.
- The short assignment `:=` can not be used outside of a function.
- Only `const`, `var` work for global variables.
- 

## Facts
- The function `main()` run as a go routine, you don't want the main routine to finish before other go routines, because when main exits, other go routines will exit too.
- Go routines are initialized in random order and start running in random order.
- When you divide two integers, you get an integer result.
- A rune is an `int32` value, but you can not compare `int32` with a rune, go considers they are two different animals.
- You can convert a `[]byte` to a string using `string("hello")`, and vice versa. You can initialize a new byte slice with the desired string using `[]byte("This is a string represented as a byte slice")`
- A rune is defined inside a single quote string ``, when you print it out, you'll get its integer value representation with %c 
- `string` can be accessed as array, hence you can loop over a string using `for i, value := string("hello") {}`, Solidity does not allow string indexing, btw.
- To convert an `int` to a Unicode code point use `string(1)`, to convert that `int` to string as is, use `strconv.Itoa(1)`, which will give `"1"`. `string(100)` give a string `"d"` because the ASCII representation of `d` is 100.
- `map`'s keys don't have order, unlike Python dictionaries latest version. Go randomize key when iterating over a map, and that is intentional.
- `delete(mapName, key)` will delete a key-value pair in the map mapName.
- To tell whether a key in a map, `v, ok := myMap["key"]`, ok is a bool. Note that there is no panic error for non-existence key, you just received a zero value.
- If you received a `map`, you should check that the `map` is not `nil` before working with it. Because assign a key-value pair to a `nil` map will cause the program to crash.
- two structures with the same fields will not be considered identical in Go if their fields are not in the same order.
- The `new()` function can be used to initialize a struct or any data type (except channel and map) then zero it and return a pointer to that type.
- A variable of map type can receive a nil value. If you try to assign to a nil map, your program will crash
- Create a new structure:
    - using the new keyword: `myStruct := new(Student)` where Student is the name of the struct type, This way, myStruct receive a pointer to the newly created struct, and all the value of the created struct are allocated with fresh memory and zero out.
    - The second way is: `myStruct := Student{}`, that way you received a variable of type Student, not a pointer
    - The third way is `myStruct := &Student{}`, look like the above, but you want to get the pointer.
- Channels are unbuffered, receving and sending data to a channel are blocking instructions. `x := <- c` will blocks the execution and waits until x receive something, similar as `c <- 5`, which will wait until the receiver receive that value. It's because channels don't have buffering.
- We can use that as a way to achive synchronization
- We can also create buffered channels. Now the sending and receving instructions only block the execution if the buffer is full.

## Go concurrency
- If multiple go routines want to use a common resouce, we must make sure that  each goroutine has exclusive access (writing access, when goroutine is writting) to that resouce by using a mutex.
- defer stament is called even when panicing. If there is a panic between mutex.Lock() and mutex.Unlock(), the mutex will lock forever. So beter use defer mutex.Unlock()
- RWMutex gives you the ability to read lock and write lock a resource. To put it simply, multiple goroutines can read lock the same resource, but when one goroutine write lock that resource, no one can read that until the writelock unlocked. Write lock can not lock the resource if there are active readlocks, but when a writelock register, no one can start a readlock, they must wait the writelock to lock, mutate and unlock the resource before they can readlock it.
- The sync.Cond can help to communicate beween goroutines.
- To call to a function only one time between muliple goroutine, use `sync.Once`  
## Good practices
- Test whether a map point to nil before use it `if myMap == nil {...}`

