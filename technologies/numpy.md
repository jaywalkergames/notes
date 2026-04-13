# Overview
Python multi-dimensional array object with fast built-in methods
- fixed size at creation
- elements are same data type
- vectorized code is more concise and performant
### Use
`import numpy as np`
### Installation
`conda install -c conda-forge numpy`
# Best Practices
### Data Types
bool, int, uint, float, complex
### Views & Copies
```python
x = np.arange(9).reshape(3, 3)
y = x[1:3]  # creates a view
y = x[[1, 2]]  # advanced indexing creates a copy
```
# Technical
### Creation
```python
# from Python sequence
a1D = np.array([1, 2, 3, 4])
a2D = np.array([[1, 2], [3, 4]])
a3D = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])

# from built-in function
a_range = np.arange(10)
a_linspace = np.linspace(1., 4., 6)
m_identity = np.eye(3)
m_diagonal = np.diag([1, 2, 3])
m_vandermore = np.vander(np.linspace(0, 2, 5), 2)

# from creation functions
z23 = np.zeros((2, 3))
o232 = np.ones((2, 3, 2))

# from another ndarray
b = a[:2].copy()
```
### Indexing
```python
x = np.arange(10)

# single element index
x[2]

# slicing (start:stop:step)
x[1:7:2]
```
### Broadcasting
Operations can be performed on ndarrays if either,
- the dimensions are equal
- one has dimension of 1 (trailing dimensions must still align)
Resulting arrays will have the same number of dimensions as the larger array
### File IO
If no missing values
```python
np.loadtxt()
```
If missing values
```python
np.genfromtxt(
	"my.csv",
	comments="#",
	delimiter=",",
	usemask=True,
	skip_header=3,
	skip_footer=5
)
```
