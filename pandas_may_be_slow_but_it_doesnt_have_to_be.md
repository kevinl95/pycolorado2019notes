# Pandas May Be Slow, but Pandas Doesn't Have to Be 9/7/19
## Andrew Vaccaro, Data engineer at Empiric Health
---

### Datatypes
Pandas uses datatypes slightly different from Python dtypes. It has multiple floats, ints, etc.
Runs ontop of numpy
By default it uses c-types float64, int64, etc.
Casting ints as uint8 instead can save you significant memory. Things like age, number of children, etc. '.astype()' method.
32 bit floats instead of 64 bits etc. for things where it is appropriate
Strings are very expensive. Regions and other categories that are limited you could map to integers to save memory. This saves a lot of memory. There is a .map method in Pandas.
.select_dtypes will let you filter to just columns of a given type.

### Categoricals
Automatically handle mapping from numbers to strings. No longer need to handle this map yourself. Can easily go back and forth.
.astype('category') for example gives you a category dtype that will map all the strings in 'category'
This comes with a great deal of memory savings. 80% in the talk!
Can still compare to Python strings- Pandas handles the mapping and conversion for you.

### When NOT to use Categoricals
- A bunch of unique values, like unique IDs. If you use categoricals on these, you now have a string AND an integer per row. You now have expanded your memory footprint.
- Dates: They do tend to duplicate, but the Pandas built-in datetime dtype is actually better.

### Looping
#### Multiplying a column
Worst thing you can do is loop over a column. Much faster to collect the columns as a list and then assign the list. Less memory shuffling. Also for doing the operation, the apply method is better than doing it yourself.
#### Iterating over rows
Use Panda's iterrows. Don't do this manually.
#### Vectorization
Using .values like in Numpy to access the underlying array is faster for numerical operations.

### Parallelization
#### Using Multiprocessing
Pro: In the stdlib. Using a processing pool, you can split your dataframe among the different threads, and then do an operation of the pool's results. Does not scale linearly with the number of threads- memory gets copied to each process. That is a downfall of multiprocessing and this is slow. Using Threading in the stdlib will take forever because they will share the memory though, so it is not a good alternative to processes. Concurrent_futures is newer, has some differences in the API to multiprocessing, but it is about the same.
#### Using Pandarallel
Abstracts this away. Excellent third party library for making working with processes with Pandas easy.

