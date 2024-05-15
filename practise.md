# Functions and file management
- Create a function which takes an integer 'n' and the function create 'n' empty files. You need to use loop and stacks.

# Functions and arrays
- Create a function and pass an array as an argument. You might have to do some research. The function should return the max value of the array.

# Implement Bubble sort - pseudocode
> Use atleast 5 random integers
```
procedure bubble_sort(array : list of sortable items, n : length of list)
    do
        swapped ← false
        i ← 1
        while i < n
            if array[i - 1] > array[i]
                swap array[i - 1] and array[i]
                swapped ← true
            end if
            i ← i + 1
        end while
        n ← n - 1
    while swapped
end procedure
```
