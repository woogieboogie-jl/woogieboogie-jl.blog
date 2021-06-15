---
title: "Go Tour Excercises"
date: 2021-06-15T11:29:25+09:00
draft: true
---
> This post illustrates my personal answers for go-tour tutorial's sample excercises.
---




## Exercise 1. Loops and Functions

    As a way to play with functions and loops, let's implement a square root function: given a number x, we want to find the number z for which z² is most nearly x.

    Computers typically compute the square root of x using a loop. Starting with some guess z, we can adjust z based on how close z² is to x, producing a better guess:

    z -= (z*z - x) / (2*z)
    Repeating this adjustment makes the guess better and better until we reach an answer that is as close to the actual square root as can be.

    Implement this in the func Sqrt provided. A decent starting guess for z is 1, no matter what the input. To begin with, repeat the calculation 10 times and print each z along the way. See how close you get to the answer for various values of x (1, 2, 3, ...) and how quickly the guess improves.

    Hint: To declare and initialize a floating point value, give it floating point syntax or use a conversion:

    z := 1.0
    z := float64(1)
    Next, change the loop condition to stop once the value has stopped changing (or only changes by a very small amount). See if that's more or fewer than 10 iterations. Try other initial guesses for z, like x, or x/2. How close are your function's results to the math.Sqrt in the standard library?

    (Note: If you are interested in the details of the algorithm, the z² − x above is how far away z² is from where it needs to be (x), and the division by 2z is the derivative of z², to scale how much we adjust z by how quickly z² is changing. This general approach is called Newton's method. It works well for many functions but especially well for square root.)

#### Solution

```
package main

import (
	"fmt"
	"math"
)

func Sqrt(x float64) float64 {
	z := 1.0
	for math.Abs(z*z-x) > (1e-12) {
	z -= (z*z -x) / (2*z)
	}
	return z
}

func main() {
	fmt.Println(Sqrt(10))
}
```




<br />
<br />
<br />


## Exercise 2. Slices

    Implement Pic. It should return a slice of length dy, each element of which is a slice of dx 8-bit unsigned integers. When you run the program, it will display your picture, interpreting the integers as grayscale (well, bluescale) values.

    The choice of image is up to you. Interesting functions include (x+y)/2, x*y, and x^y.

    (You need to use a loop to allocate each []uint8 inside the [][]uint8.)

    (Use uint8(intValue) to convert between types.)


#### Solution
```
package main

import "code.google.com/p/go-tour/pic"

func Pic(dx, dy int) [][]uint8 {
    m := make([][]uint8, dy)
    for y := range m {
        m[y] = make([]uint8, dx)
        for x := range m[y] {
            m[y][x] = uint8((x*y) / 2)
        }
    }
    return m
}

func main() {
    pic.Show(pic)
}
```

<br />
<br />
<br />



## Excercise 3. Maps

    Implement WordCount. It should return a map of the counts of each “word” in the string s. The wc.Test function runs a test suite against the provided function and prints success or failure.

    You might find strings.Fields helpful.


#### Solution
```
package main

import (
	"code.google.com/p/go-tour/wc"
	"strings"
)

func WordCount(s string) map[string]int {
    m := make(map[string]int)
    p := strings.Fields(s)

    for _, v := range p {
        m[v]++
    }
    return m
}

func main() {
	wc.Test(WordCount)
```

<br />
<br />
<br />


## Excercise 4. Fibonacci closure

    Let's have some fun with functions.

    Implement a fibonacci function that returns a function (a closure) that returns successive fibonacci numbers (0, 1, 1, 2, 3, 5, ...).



#### Solution
```
package main

import "fmt"

func fibo() func() int {
    a, b := 0, 1
    return func() int {
        a, b = b, a+b
        return b
    }
}

func main() {
    f := fibo()
    for i := 0; i < 10; i++ {
        fmt.Printlin(f())
    }
}
```
<br />
<br />
<br />

## Excercise 5. Stringers

    Make the IPAddr type implement fmt.Stringer to print the address as a dotted quad.

    For instance, IPAddr{1, 2, 3, 4} should print as "1.2.3.4".


#### Solution



<br />
<br />
<br />

## Excercise 6. Errors

    Copy your Sqrt function from the earlier exercise and modify it to return an error value.

    Sqrt should return a non-nil error value when given a negative number, as it doesn't support complex numbers.

    Create a new type

    type ErrNegativeSqrt float64
    and make it an error by giving it a

    func (e ErrNegativeSqrt) Error() string
    method such that ErrNegativeSqrt(-2).Error() returns "cannot Sqrt negative number: -2".

    Note: A call to fmt.Sprint(e) inside the Error method will send the program into an infinite loop. You can avoid this by converting e first: fmt.Sprint(float64(e)). Why?

    Change your Sqrt function to return an ErrNegativeSqrt value when given a negative number.


#### Solution

<br />
<br />
<br />

## Excercise 7. Readers

    Implement a Reader type that emits an infinite stream of the ASCII character 'A'.

#### Solution


<br />
<br />
<br />


## Excercise 8. rot13Reader

    A common pattern is an io.Reader that wraps another io.Reader, modifying the stream in some way.

    For example, the gzip.NewReader function takes an io.Reader (a stream of compressed data) and returns a *gzip.Reader that also implements io.Reader (a stream of the decompressed data).

    Implement a rot13Reader that implements io.Reader and reads from an io.Reader, modifying the stream by applying the rot13 substitution cipher to all alphabetical characters.

    The rot13Reader type is provided for you. Make it an io.Reader by implementing its Read method.

#### Solution

<br />
<br />
<br />


## Excercise 9. Images

    Remember the picture generator you wrote earlier? Let's write another one, but this time it will return an implementation of image.Image instead of a slice of data.

    Define your own Image type, implement the necessary methods, and call pic.ShowImage.

    Bounds should return a image.Rectangle, like image.Rect(0, 0, w, h).

    ColorModel should return color.RGBAModel.

    At should return a color; the value v in the last picture generator corresponds to color.RGBA{v, v, 255, 255} in this one.

#### Solution

<br />
<br />
<br />

## Excercise 10. Equivalent Bianry Trees

    There can be many different binary trees with the same sequence of values stored in it. For example, here are two binary trees storing the sequence 1, 1, 2, 3, 5, 8, 13.
    

<div style="width: 60%; display: flex;, justify-items: center; margin: auto;">
<img src="/images/tree.png" alt="tree"/>
</div>



    A function to check whether two binary trees store the same sequence is quite complex in most languages. We'll use Go's concurrency and channels to write a simple solution.

    This example uses the tree package, which defines the type:

    type Tree struct {
        Left  *Tree
        Value int
        Right *Tree
    }

    1. Implement the Walk function.

    2. Test the Walk function.

    The function tree.New(k) constructs a randomly-structured (but always sorted) binary tree holding the values k, 2k, 3k, ..., 10k.

    Create a new channel ch and kick off the walker:

    go Walk(tree.New(1), ch)
    Then read and print 10 values from the channel. It should be the numbers 1, 2, 3, ..., 10.

    3. Implement the Same function using Walk to determine whether t1 and t2 store the same values.

    4. Test the Same function.

    Same(tree.New(1), tree.New(1)) should return true, and Same(tree.New(1), tree.New(2)) should return false.


The documentation for Tree can be found [here](https://tour.golang.org/concurrency/8)

<br />
<br />
<br />

## Excercise 11. Web Crawler
    In this exercise you'll use Go's concurrency features to parallelize a web crawler.  
    Modify the Crawl function to fetch URLs in parallel without fetching the same URL twice.  
    Hint: you can keep a cache of the URLs that have been fetched on a map, but maps alone are not safe for concurrent use!

#### Solution


<br />
<br />
