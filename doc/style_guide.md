# C Style Guide

## Contents

- [Formatting](#formatting)
  - [Alignment](#alignment)
  - [Brackets](#brackets)
  - [Characters Per Line](#characters-per-line)
  - [Empty Lines](#empty-lines)
  - [Indentation](#indentation)
  - [Single Line Rules](#single-line-rules)
  - [Spaces](#spaces)
- [Naming](#naming)
  - [Case](#case)
  - [Suffix](#suffix)
- [Documenting](#documenting)
  - [Formatting](#documentation-formatting)
  - [Tags](#tags)
  - [Order](#order)
  - [Spaces](#tags-spaces)
  - [Dot](#dot)
  - [Examples](#examples)

## Formatting

### Alignment

Always break curly brackets:

```c
// Good
void foo()
{
    int number = 10;

    if (number == 5)
    {
        return;
    }
}

// Bad
void foo() {
    int number = 10;

    if (number == 5) {
        return;
    }
}
```

If the code inside round brackets doesn't fit in a line, break each argument/parameter onto a new line and break the closing bracket.

```c
// Doesn't fit in a line, break
void function_one(
    unsigned int value_one,
    unsigned int value_two,
    unsigned int value_three
)
{
}

// Fits in a line, don't break
void function_two(unsigned int value)
{
}

int main()
{
    const unsigned int very_long_variable_name1 = 1;
    const unsigned int very_long_variable_name2 = 2;
    const unsigned int very_long_variable_name3 = 3;

    // Doesn't fit in a line, break
    function_one(
        very_long_variable_name1,
        very_long_variable_name2,
        very_long_variable_name3
    );

    const unsigned int value = 10;

    // Fits in a line, don't break
    function_two(value);
}
```

Align operands:

```c
int aaa = bbbbbbbbbbbbbbb
        + ccccccccccccccc;
```

Align pointers to the left:

```c
// Good
int* ptr_one;

// Bad
int *ptr_two;
```

### Brackets

Always use brackets, even for short statements.

```c
// Good
for (size_t i = 0; i < 100; ++i)
{
    puts("Hello world!");
}

// Bad: No brackets used
for (size_t i = 0; i < 100; ++i)
    puts("Hello world!");
```

### Characters Per Line

Each line must have a maximum of `80` characters.

```c
int main()
{
    int very_long_variable_name1 = 1;
    int very_long_variable_name2 = 1;
    int very_long_variable_name3 = 1;
    
    // Good, no more than 80 characters per line
    int result = very_long_variable_name1 
               + very_long_variable_name2 
               + very_long_variable_name3;
}
```

### Empty Lines

Maximum empty lines to keep: `1`.

```c
int main()
{
    // Good
    int my_variable1;

    int my_variable2;

    // Bad
    int my_variable3;


    int my_variable4;
}
```

### Indentation

Don't use tabs; use `4` spaces for indenting your code.

```c
int main()
{
    int random_variable = 10;

    if (random_variable)
    {
        return 0;
    }
}
```

Don't indent pre-processor directives.

```c
// Good
#if FOO
#if BAR
#include <foo>
#endif
#endif

// Bad
#if FOO
  #if BAR
    #include <foo>
  #endif
#endif
```

Don't indent `case` and `default` keywords.

```c
int main()
{
    int random_variable = 10;

    // Good
    switch (random_variable)
    {
    case 1:
        break;
    default:
        break;
    }

    // Bad
    switch (random_variable)
    {
        case 1:
            break;
        default:
            break;
    }
}
```

### Single Line Rules

Don't put curly brackes in a single line.

```c
// Bad
void empty_function() {}

// Good
void empty_function()
{
}

int main()
{
    int random_variable = 10;

    // Bad
    if (random_variable == 1) { return; }

    // Good
    if (random_variable == 1)
    {
        return;
    }
}
```

### Spaces

Put a space between `for`, `if`, `else if`, and `while` keywords and open brackets.

```c
int main()
{
    // Bad
    for(int i = 0; i < 100; ++i)
    {
    }

    // Good
    for (int i = 0; i < 100; ++i)
    {
    }

    // Bad
    while(some_variable)
    {
    }

    // Goood
    while (some_variable)
    {
    }

    // Bad
    if(some_variable)
    {
    }

    // Good
    if (some_variable)
    {
    }
}
```

## Naming

### Case

Use `underscore_style` everywhere except for macros.

```c
// Good
struct random_struct
{
};

// Bad
struct RandomStruct
{
};

int main()
{
    // Bad
    int myVariable;

    // Good
    int my_variable;
}
```

For macros, use `UPPER_CASE`.

```c
// Bad
#define my_macro

// Good
#define MY_MACRO
```

### Suffix

Put `_t` as a suffix for all defined types.

```c
// Bad
typedef int16_t custom_type;

// Good
typedef int16_t custom_type_t;
```

## Documenting

### Documentation Formatting

Use the following formatting.

```c
/**
 * @tag <An optional attribute> Description
 * @tag <An option attribute> Description
 * @tag <An optional attribute> Description
 */
```

```c
// Good:

/**
 * @brief Calculates the area of a rectangle.
 *
 * @param length The longer side measurement.
 * @param width The shorter side measurement.
 * @return Product of length and width.
 */
float area(float length, float width);

// Bad:

/**
 * Calculates the area of a rectangle.
 *
 * length The longer side measurement.
 * Product of length and width.
 * width The shorter side measurement.
 */
float area(float length, float width);

// Bad:

// @brief Calculates the area of a rectangle.
// @param length The longer side measurement.
// @return Product of length and width.
// @param width The shorter side measurement.
float area(float length, float width);
```

### Tags

Use `@brief` to give a general short description.

Use `@param` to give a short description about that specific parameter.

Use `@return` to give a short description about the function return type.

Use `@warning` to warn about correct usage that otherwise might cause a bug.

Use `@see` to reference an external information that is part of this code.

### Order

Put tags in the following order:
 1. `@brief`
 3. `@param`
 4. `@return`
 6. `@warning`
 7. `@see`

```c
// Good:

/**
 * @brief Calculates the area of a rectangle.
 *
 * @param length The longer side measurement.
 * @param width The shorter side measurement.
 * @return Product of length and width.
 * @throws std::runtime_exception when the length and width are equal.
 */
float area(float length, float width);

// Bad:

/**
 * @brief Calculates the area of a rectangle.
 *
 * @throws std::runtime_exception when the length and width are equal.
 * @param length The longer side measurement.
 * @return Product of length and width.
 * @param width The shorter side measurement.
 */
float area(float length, float width);
```

### Tags Spaces

Put empty lines between `@brief` and other tags. All other tags should not have a empty line between them.

```c
// Bad:

/**
 * @brief Calculates the area of a rectangle.
 * @param length The longer side measurement.
 * @param width The shorter side measurement.
 * @return Product of length and width.
 */
float area(float length, float width);

// Bad:

/**
 * @brief Calculates the area of a rectangle.
 *
 * @param length The longer side measurement.
 *
 * @param width The shorter side measurement.
 *
 * @return Product of length and width.
 */
float area(float length, float width);

// Good:

/**
 * @brief Calculates the area of a rectangle.
 *
 * @param length The longer side measurement.
 * @param width The shorter side measurement.
 * @return Product of length and width.
 * @throws std::runtime_exception when the length and width are equal.
 */
float area(float length, float width);
```

### Dot

End all descriptions with a dot.

```c
// Good:

/**
 * @brief Calculates the area of a rectangle.
 *
 * @param length The longer side measurement.
 * @param width The shorter side measurement.
 * @return Product of length and width.
 * @throws std::runtime_exception when the length and width are equal.
 */
float area(float length, float width);

// Bad:

/**
 * @brief Calculates the area of a rectangle
 *
 * @param length The longer side measurement
 * @param width The shorter side measurement
 * @return Product of length and width
 * @throws std::runtime_exception when the length and width are equal
 */
float area(float length, float width);
```

### Examples

```c
// Function example:

/**
 * @brief Adds two integers.
 *
 * @param a The first integer to add.
 * @param b The second integer to add.
 * @return The sum of a and b.
 * @throws std::invalid_argument if either parameter is negative.
 * @see subtract() for the inverse operation.
 */
int add(int a, int b)
{
    return a + b;
}

// Macro example:

/**
 * @brief Computes the absolute value of a number.
 *
 * @param x The input value (integer or floating point).
 * @warning Avoid using with expressions that have side effects (e.g., `ABS(x++)`).
 */
#define ABS(x) ((x) < 0 ? -(x) : (x))
```

