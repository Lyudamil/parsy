==================
Parsing primitives
==================

These are the lowest level building blocks for creating parsers.

.. module:: parsy

.. function:: string(expected_string)

   Returns a parser that expects the ``expected_string`` and produces
   that string value.

.. function:: regex(exp, flags=0)

   Returns a parser that expects the given ``exp``, and produces the
   matched string. ``exp`` can be a compiled regular expression, or a
   string which will be compiled with the given ``flags``.

.. function:: test(func, description)

   Returns a parser that tests a single character with the callable
   ``func``. If ``func`` returns ``True``, the parse succeeds, otherwise
   the parse fails with the description ``description``.

   .. code-block:: python

      >>> ascii = parsy_test(lambda c: ord(c) < 128,
                             "ascii character")
      >>> ascii.parse("A")
      'A'

.. function:: one_of(characters_or_strings):

   Accepts a string and returns a parser that matches and returns one character
   from the string.

   Alternatively, accepts a list of strings, and returns a parser that matches
   and returns one string from the list. The list is first sorted in descending
   length order, so that overlapping strings are handled as expected.

   .. code-block:: python

      >>> one_of("abc").parse("a")
      'a'

      >>> one_of(["y", "yes"]).parse("yes")
      'yes'

.. function:: success(val)

   Returns a parser that does not consume any of the stream, but
   produces ``val``.

.. function:: fail(expected)

   Returns a parser that always fails with the provided error message.

.. data:: whitespace

   A parser that matches and returns one or more whitespace characters

.. data:: letter

   A parser that matches and returns a single letter, as defined by
   ``str.isalpha``.

.. data:: digit

   A parser that matches and returns a single digit, as defined by
   ``str.isdigit``.
