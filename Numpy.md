# Numpy
NumPy is the fundamental package for scientific computing in Python. It is a Python library that provides a multidimensional array object, various derived objects (such as masked arrays and matrices), and an assortment of routines for fast operations on arrays, including mathematical, logical, shape manipulation, sorting, selecting, I/O, discrete Fourier transforms, basic linear algebra, basic statistical operations, random simulation and much more.

At the core of the NumPy package, is the _ndarray_ object. This encapsulates _n_-dimensional arrays of homogeneous data types, with many operations being performed in compiled code for performance. There are several important differences between NumPy arrays and the standard Python sequences:

- NumPy arrays have a fixed size at creation, unlike Python lists (which can grow dynamically). Changing the size of an _ndarray_ will create a new array and delete the original.
- The elements in a NumPy array are all required to be of the same data type, and thus will be the same size in memory. The exception: one can have arrays of (Python, including NumPy) objects, thereby allowing for arrays of different sized elements.
- NumPy arrays facilitate advanced mathematical and other types of operations on large numbers of data. Typically, such operations are executed more efficiently and with less code than is possible using Python’s built-in sequences.
- A growing plethora of scientific and mathematical Python-based packages are using NumPy arrays; though these typically support Python-sequence input, they convert such input to NumPy arrays prior to processing, and they often output NumPy arrays. In other words, in order to efficiently use much (perhaps even most) of today’s scientific/mathematical Python-based software, just knowing how to use Python’s built-in sequence types is insufficient - one also needs to know how to use NumPy arrays.

## Cheat sheet for Numpy
|Command|Description|Documentation|
|-|-|-|
|np.array(lst)|Takes a list and transforms it into a Numpy Array||
|np.genfromtxt(fname, delimiter, skip_header) | Used to [[Read a CSV using Python and Numpy\|read a csv file]]|[Link](https://numpy.org/doc/stable/reference/generated/numpy.genfromtxt.html)|
|@|Does matrix multiplication||
|np.dot(a, b)|Does the dot product of two arrays|[Link](https://numpy.org/doc/stable/reference/generated/numpy.dot.html)|
|np.concatenate((a, b, c, ...), axis)| Join a sequence of arrays along an existing axis.|[Link](https://numpy.org/doc/stable/reference/generated/numpy.concatenate.html)|
|np.reshape(arr, newshape)|Gives a new shape to an array without changing its data.|[Link](https://numpy.org/doc/stable/reference/generated/numpy.reshape.html)|
|np.savetxt(fname, X, fmt, header, comments)|Saves the information of a 1D or 2D array from **X** to **fname**|[Link](https://numpy.org/doc/stable/reference/generated/numpy.savetxt.html)|
|np.mean(arr)|Compute the arithmetic mean along the specified axis.|[Link](https://numpy.org/doc/stable/reference/generated/numpy.mean.html)|

You can find the complete documentation on [here.](https://numpy.org/doc/stable/reference/index.html)
