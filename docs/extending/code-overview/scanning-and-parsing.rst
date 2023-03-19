Scanning and Parsing
====================

.. index:: tokeniser
.. index:: scanner

Scanner or Tokenizer
--------------------

We have split out the scanner into a separate `github repository
<https://pypi.org/project/Mathics-Scanner/>`_ which has its own `PyPI
package <https://pypi.org/project/Mathics-Scanner/>`_.

A little bit about the scanner...  There are two passes made in the
scanner, a "pre-scan" in found in `mathics_scanner.prescanner
<https://github.com/Mathics3/mathics-scanner/blob/master/mathics_scanner/prescanner.py>`_
which converts some WL-specific character codes to character or long
names and the `mathics_scanner.tokeniser
<https://github.com/Mathics3/mathics-scanner/blob/master/mathics_scanner/tokeniser.py>`_
which runs after that. The tokenizer breaks up a string into *tokens*,
classifications of a sequence of characters, which is then as the
atoms on which the parser pattern matches on.

.. index:: parsing
.. _parsing:

Parser
------

All parsing routines are located in `mathics.core.parser
<https://github.com/mathics/Mathics/tree/master/mathics/core/parser>`_. See
:ref:`Precedence-Climbing Parser` for parsing details.

However, here are the main points:

* The parser is recursive descent
* Because WL has a lot of operators an `Operator-precedence parser <https://en.wikipedia.org/wiki/Operator-precedence_parser#Precedence_climbing_method>`_ is used
* The result is an Full-form M-expression, which is a translation of the input string. See `Expressions as Trees <https://reference.wolfram.com/language/tutorial/Expressions.html#14609>`_.

To see a translation of the Full-Form *input* the flag ``--full-form`` can be given to the command-line utilities ``mathics`` or ``mathicsscript``.

Here is an example:

::

   $ mathics --full-form

   Mathics3 6.0.1
   ...
   Quit by pressing CONTROL-D

   In[1]:= 1 + 2 / 3
   System`Plus[1, System`Times[2, System`Power[3, -1]]]
   Out[1]= 5 / 3

Note that this is different from formatting the *output*:

::

   In[2]:= (x + 1) / 3
   System`Times[System`Plus[Global`x, 1], System`Power[3, -1]]
   Out[2]= (x + 1) / 3
   In[3]:= (x + 1) / 3 // FullForm
   System`FullForm[System`Times[System`Plus[Global`x, 1], System`Power[3, -1]]]
   Out[3]= Times[Rational[1, 3], Plus[1, x]]

Some things to notice:

* Parsing fully-qualifies names. So we have ``System`Times`` instead
  of ``Times``, even though the FullForm output shows the simple name.
* Parsing removes parenthesis used for grouping capturing this
  instead by the function nesting order

.. index:: parsing

Python Code for Parsing an String
---------------------------------

Inside Python, here is how you parse a string:

.. code-block:: python

   from mathics.core.parser import parse, SingleLineFeeder
   from mathics.core.definitions import Definitions

   definitions = Definitions(add_builtin=True)
   str_expression = "1 + 2 / 3"
   expr = parse(definitions, SingleLineFeeder(str_expression))
   print("type", type(expr))
   print("expr: ", expr)

Running the above produces:

::

   type <class 'mathics.core.expression.Expression'>
   expr:  System`Plus[1, System`Times[2, System`Power[3, -1]]]

The function ``SingleLineFeeder`` should be supplied by the front-end.
It reads input a line and a time and returns that back to the parser.
