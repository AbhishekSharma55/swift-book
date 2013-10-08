.. docnote:: Subjects to be covered in this section

    * Declaration syntax
    * Multiple variable declarations and initializations on one line
    * Naming conventions
    * Integer types
    * Floating point types
    * Bool
    * Void
    * No suffixes for integers / floats
    * Lack of promotion and truncation
    * Lazy initialization
    * A brief mention of characters and strings
    * Tuples
    * Enums
    * Enum element patterns
    * Enums for groups of constants
    * Enums with raw values (inc. getting / setting raw values)
    * Enum default / unknown values?
    * Enums with multiple identical values?
    * Enum delayed identifier resolution
    * Typealiases
    * Type inference
    * Type casting through type initializers
    * Arrays
    * Optional types
    * Pattern binding
    * Literals
    * Immutability
    * (Don't redeclare objects within a REPL session)
    * C primitive types

Basic Types
===========

Declaring Variables
-------------------

Creating and naming variables in Swift takes the following form:

.. testcode:: declaringVariables

    (swift) var a = 1
    // a : Int = 1
	
This declaration says “Define a variable called ``a``, and give it an initial value of ``1``”.

Variable definitions can include a specific *type*, to be explicit about the kind of variable you want to create:

.. testcode:: declaringVariables

    (swift) var b : Int = 2
    // b : Int = 2

This asks Swift to create a new variable called ``b`` to store whole numbers (shown here as ``Int``), and to give ``b`` an initial value of ``2``. The colon in the declaration means ‘of type’, so we can read this as “define a variable called ``b``, which is of type ``Int``, and set it to equal ``2``”.

You can use pretty much :term:`any character` you like in a variable name:

.. glossary::

    any character
        Variable names can't start with a number, but they can contain numbers elsewhere in their name. They also can't contain mathematical symbols, arrows, line and box drawing characters, or private-use or invalid Unicode code points.

.. testcode:: declaringVariables

    (swift) var π = 3.14159
    // π : Double = 3.14159
    (swift) var 你好 = "你好世界"
    // 你好 : String = "你好世界"
    (swift) var 🐶🐮 = "dogcow"
    // 🐶🐮 : String = "dogcow"
    
Once you've declared a variable, you can't redeclare it again with the same name, but you can set the existing variable to another value of the same type:

.. testcode:: declaringVariables

    (swift) var tattooText = "Eric 💘 Janine"
    // tattooText : String = "Eric 💘 Janine"
    (swift) tattooText = "Eric 💘 Margaret"
    (swift) println(tattooText)
    >>> Eric 💘 Margaret

Numbers
-------

Swift supports two fundamental types of number: :term:`integers`, and :term:`floating-point numbers`. Swift provides both types of number in :term:`signed and unsigned` forms up to 128 bits in size. These basic numeric types follow a similar naming convention to C, in that an 8-bit unsigned integer is a ``UInt8``, and a signed 64-bit floating-point number is a ``Float64``. Like all types in Swift, these basic numeric types have capitalized names. (See the :doc:`ReferenceManual` for a complete list of numeric types.)

.. glossary::

    integers
        An integer is a whole number with no fractional component (such as ``42``, ``0`` and ``-23``).

    floating-point numbers
        A floating-point number (also known as a float) is a number with a fractional component (such as ``3.14159``, ``0.1`` or ``-273.15``).

    signed and unsigned
        Signed values can be positive or negative. Unsigned values can only be positive.

In most cases, there's no need to pick a specific size of integer or floating-point number to use in your code. Swift provides three standard number types:

* ``Int``, which is the same as ``Int64``, and should be used for general integer values
* ``Float``, which is the same as ``Float32``, and should be used for normal floating-point values
* ``Double``, which is the same as ``Float64``, and should be used when floating-point values need to be very large or particularly precise

Unless you need to work with a :term:`specific size` of integer or floating-point number, you should always use ``Int``, ``Float`` or ``Double`` for code consistency and interoperability.

.. glossary::

    specific size
        Certain tasks may require you to be more specific about the type of number that you need. You might use a ``Float16`` to read 16-bit audio samples, or a ``UInt8`` when working with raw 8-bit byte data, for example.

Strong typing and type inference
--------------------------------

Swift is a :term:`strongly-typed language`. Strong typing enables Swift to perform type checks when it compiles your code, which helps to avoid accidental errors when working with different value types. However, this doesn't mean that you always have to provide an explicit type definition. If you don't specify the type of value you need, Swift will use :term:`type inference` to work out the appropriate type to use.

.. glossary::

    strongly-typed language
        Strongly-typed languages require you to be clear about the types of values and objects your code can work with. If some part of your code expects a string, for example, strong typing means that you can't accidentally pass it an integer by mistake.

    type inference
        Type inference is the ability for a compiler to automatically deduce the type of a particular expression at compile-time (rather than at run-time). The Swift compiler can often infer the type of a variable without the need for explicit type definitions, just by examining the values you provide.

For example: if you assign the value ``42`` to a variable, without saying what type it is:

.. testcode:: typeInference

    (swift) var meaningOfLife = 42
    // meaningOfLife : Int = 42

…Swift will deduce that you want the variable to be an ``Int``, because you have initialized it with an integer value.

Likewise, if you don't specify a type for a floating-point number:

.. testcode:: typeInference

    (swift) var pi = 3.14159
    // pi : Double = 3.14159

…Swift assumes that you want to create a ``Double`` from the value of ``3.14159``. (Swift always chooses ``Double`` rather than ``Float`` when inferring the type of floating-point numbers.)

Number literals
---------------

:term:`Number literals` can be expressed in several different ways:

* Integer literals can be decimal (with no prefix), :term:`binary` (with a ``0b`` prefix), :term:`octal` (``0o``), or :term:`hexadecimal` (``0x``)
* Floating-point literals can be decimal (no prefix) or hexadecimal (``0x``), and can have an optional :term:`exponent` (indicated by an upper- or lower-case ``e`` for decimal floats, and upper- or lower-case ``p`` for hexadecimal floats).

.. glossary::

    number literals
        Number literals are fixed-value numbers included directly in your source code, such as ``42`` or ``3.14159``.

    binary
        Binary numbers are counted with two (rather than ten) basic units. They only ever contain the numbers ``0`` and ``1``. In binary notation, ``1`` is ``0b1``, and ``2`` is ``0b10``.

    octal
        Octal numbers are counted with eight (rather than ten) basic values. They only ever contain the numbers ``0`` to ``7``. In octal notation, ``7`` is ``0o7``, and ``8`` is ``0o10``.

    hexadecimal
        Hexadecimal numbers are counted with 16 (rather than ten) basic values. They contain the numbers ``0`` to ``9``, plus the letters ``A`` through ``F`` (to represent base units with values of ``10`` through ``15``). In hexadecimal notation, ``9`` is ``0x9``, ``10`` is ``0xA``, ``15`` is ``0xF``, and ``16`` is ``0x10``.

    exponent
        Floating-point values with an exponent are of the form ‘*[number]* shifted by *[exponent]* decimal places’ (such as ``1.25e2``). All the exponent does is to shift the number right or left by that many decimal places. Positive exponents move the number to the left; negative exponents move it to the right. So, ``1.25e2`` means ‘``1.25`` shifted ``2`` places to the left’ (aka ``125.0``), and ``1.25e-2`` means ‘``1.25`` shifted ``2`` places to the right’ (aka ``0.0125``).

All of these integer literals have a decimal value of ``17``:

.. testcode:: numberLiterals

    (swift) var decimalInteger = 17
    // decimalInteger : Int = 17
    (swift) var binaryInteger = 0b10001    // 17 in binary notation
    // binaryInteger : Int = 17
    (swift) var octalInteger = 0o21        // 17 in octal notation
    // octalInteger : Int = 17
    (swift) var hexadecimalInteger = 0x11  // 17 in hexadecimal notation
    // hexadecimalInteger : Int = 17

All of these floating-point literals have a decimal value of ``12.5``:

.. testcode:: numberLiterals

    (swift) var decimalDouble = 12.5
    // decimalDouble : Double = 12.5
    (swift) var exponentDouble = 1.25e1
    // exponentDouble : Double = 12.5
    (swift) var hexadecimalDouble = 0xC.8p0
    // hexadecimalDouble : Double = 12.5

Number literals can contain extra formatting to make them easier to read. Both integers and floats can be padded with :term:`extra zeroes` on the beginning (so ``01234 == 1234``), and can contain underscores to help with readability. Neither type of formatting affects the underlying value of the literal.

.. glossary::

    extra zeroes
        In C, adding an extra zero to the beginning of an integer literal indicates that the literal is in octal notation. This isn't the case in Swift. Always add the ``0o`` prefix if your numbers are in octal notation.

All of these literals are valid in Swift:

.. testcode:: numberLiterals

    (swift) var oneMillion = 1_000_000
    // oneMillion : Int = 1000000
    (swift) var justOverOneMillion = 1_000_000.000_000_1
    // justOverOneMillion : Double = 1e+06
    (swift) var paddedDouble = 000123.456
    // paddedDouble : Double = 123.456

Booleans
--------

Swift has a basic :term:`boolean` type, called ``Bool``. Values of type ``Bool`` can be either ``true`` or ``false``:

.. glossary::

    boolean
        A data type is said to be ‘boolean’ if it can only ever have one of two values: true or false.

.. testcode:: booleans

    (swift) var orangesAreOrange = true
    // orangesAreOrange : Bool = true
    (swift) var turnipsAreDelicious = false
    // turnipsAreDelicious : Bool = false

Note that Swift has inferred the types of ``orangesAreOrange`` and ``turnipsAreDelicious`` from the fact that we initialized them with ``Bool`` values. As with ``Int`` and ``Double`` above, we don't need to declare variables as being ``Bool`` if we set them to ``true`` or ``false`` as soon as we create them. Type inference helps to make Swift code much more concise and readable when initializing variables with known values.

Tuples
------

Tuples are a way to group multiple values together in a simple and flexible way. Here's an example of a tuple:

.. testcode:: tuples

    (swift) var someTuple = (3.14159, "pi")
    // someTuple : (Double, String) = (3.14159, "pi")

``(3.14159, "pi")`` is a tuple that groups together a ``Double`` value and a ``String`` value. It could be described as “a tuple of type ``(Double, String)``”.

You can create tuples from whatever permutation of types you like, and they can contain as many values as you like. There's nothing stopping you from having a tuple of type ``(Int, Int, Int)``, or ``(String, Bool)``, or any other combination you need.

You can access the individual contents of a tuple using index numbers starting at zero:

.. testcode:: tuples

    (swift) someTuple.0
    // r0 : Double = 3.14159
    (swift) someTuple.1
    // r1 : String = "pi"

You can also optionally name the elements in a tuple, and retrieve them using dot syntax:

.. testcode:: tuples

    (swift) var webPageRetrievalError = (statusCode : 404, statusString : "Not Found")
    // webPageRetrievalError : (statusCode: Int, statusString: String) = (404, "Not Found")
    (swift) webPageRetrievalError.statusCode
    // r2 : Int = 404
    (swift) webPageRetrievalError.statusString
    // r3 : String = "Not Found"

Tuples are particularly useful as the return values of functions. A function that tries to retrieve a web page might return our ``webPageRetrievalError`` tuple if it is unable to find the page we have requested. By returning a tuple with two distinct values, each of a different type, the function is able to provide much more useful information about its outcome than if it could only return a single value of a single type.


.. refnote:: References

    * https://[Internal Staging Server]/docs/LangRef.html#integer_literal ✔︎
    * https://[Internal Staging Server]/docs/LangRef.html#floating_literal
    * https://[Internal Staging Server]/docs/LangRef.html#expr-delayed-identifier
    * https://[Internal Staging Server]/docs/whitepaper/TypesAndValues.html#types-and-values
    * https://[Internal Staging Server]/docs/whitepaper/TypesAndValues.html#integer-types ✔︎
    * https://[Internal Staging Server]/docs/whitepaper/TypesAndValues.html#no-integer-suffixes
    * https://[Internal Staging Server]/docs/whitepaper/TypesAndValues.html#no-implicit-integer-promotions-or-conversions
    * https://[Internal Staging Server]/docs/whitepaper/TypesAndValues.html#no-silent-truncation-or-undefined-behavior
    * https://[Internal Staging Server]/docs/whitepaper/TypesAndValues.html#separators-in-literals ✔︎
    * https://[Internal Staging Server]/docs/whitepaper/TypesAndValues.html#floating-point-types
    * https://[Internal Staging Server]/docs/whitepaper/TypesAndValues.html#bool
    * https://[Internal Staging Server]/docs/whitepaper/TypesAndValues.html#tuples
    * https://[Internal Staging Server]/docs/whitepaper/TypesAndValues.html#arrays
    * https://[Internal Staging Server]/docs/whitepaper/TypesAndValues.html#enumerations
    * https://[Internal Staging Server]/docs/whitepaper/LexicalStructure.html#identifiers-and-operators
    * https://[Internal Staging Server]/docs/whitepaper/LexicalStructure.html#integer-literals
    * https://[Internal Staging Server]/docs/whitepaper/LexicalStructure.html#floating-point-literals
    * https://[Internal Staging Server]/docs/whitepaper/GuidedTour.html#declarations-and-basic-syntax
    * https://[Internal Staging Server]/docs/whitepaper/GuidedTour.html#tuples
    * https://[Internal Staging Server]/docs/whitepaper/GuidedTour.html#enums
