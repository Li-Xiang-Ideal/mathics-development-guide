Introducing the Builtin Class
-----------------------------

.. index:: Builtin

Most of the time you'll probably need to pass information into the
Function you want to add. For this, use the ``Builtin`` class.  In WL
these things functions and variables defined this way are tagged as a
"Built-in Symbol".

The method that you should define in the Builtin class that should get
invoked needs to start off with the name ``apply``. (This is an
*evaluation* method and starting the name with ``eval`` would have
been the customary and correct thing to do. In the future we hope to
fix this.)

As before, this method has an ``evaluation`` parameter at the end.

Other parameters that are appropriate for the function can be
added. However those parameters must also be listed suffixed with an
underscore (``_``) in the Python method's docstring in a special way.

The docstring is used by Builtin's default *evaluate()* method when
trying to resolve what Python method to call. The docstring looks
pretty much the same as it would look if you were defining this in
WL.

For example, let's add a string parameter. In Mathics the function
might look like this:


.. code-block:: mathematica


  Hello[s_String] := Print["Hello, " <> s <> "!"]

The eavluation method, looks like this:

.. code-block:: python

  def apply(self, person: String, evaluation: Evaluation):
    "Hello[person_String]"
        return String(f"Hello, {person.value}!")

Here is the complete code:

.. code-block:: python

  from mathics.builtin.base import Builtin, String
  from mathics.core.evaluation import Evaluation

  class Hello(Builtin):
    def apply(self, person: String, evaluation: Evaluation) -> String:
      "Hello[person_String]"
          return String(f"Hello, {person.value}!")

The parameter *person* has type Mathics *String*. Therefore, to use
that for use in Python, we need to convert it to a Python value. This
is done with *person.value*. And the the return value
also needs to be a Mathics *String* so we need to convert the Python
string in Python back to a Mathics *String*.

Previously, since we weren't modifying the Mathics String, no
conversions to Python and from Python were needed.

See `Patterns
<https://reference.wolfram.com/language/tutorial/Patterns.html>`_ for
more information about how to specify expressions with patterns in
them that you might use in an *apply()* method docstring.
