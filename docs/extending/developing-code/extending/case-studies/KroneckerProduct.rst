Adding Builtin Function ``KroneckerProduct``
=============================================

Find corresponding Sympy, SciPy, mpmath, or NumpPy function
-----------------------------------------------------------

Going to a `SymPy search page <https://docs.sympy.org/latest/search.html>`_ and looking for "Kronecker", we find this function and learn that it is also called a `"tensor product matrix" <https://docs.sympy.org/latest/modules/physics/quantum/tensorproduct.html>`_. Knowing alternate names can sometimes be helpful in finding the corresponding Wikipedia entry. For example, the mathics function ""EulerPhi" function is called "totient" in SymPy, and the Wikipedia name is "Euler's totient function".


``KroneckerProduct`` placement in Mathics
-----------------------------------------

To find where to put ``KroneckerProduct`` in Mathics, we look this up the  `WMA docs <https://reference.wolfram.com/language/ref/KroneckerProduct.html>`_  and then looking at the Related Guides dropdown menu we see:

* Matrix Operations
* Operations on Vectors

Inside running the Django application in the documentations section (on the right or click on the "?" if this doesn't appear), type in "Matrix", and we see there is no "Matrix Operations" section yet.

However if we type "Operations" we see "Operations on Vectors" is already there and it has a subsection called "Vector Space Operations". So let's use that.

A ``git grep 'Vector Space Operations'`` tells us that this is located in ``mathics/builtins/vectors/vector_space_operations.py``.

Armed with this we can start to write some code which is found in the following section:

.. toctree::
   :maxdepth: 1

   KroneckerProduct/basic-skeleton.rst
