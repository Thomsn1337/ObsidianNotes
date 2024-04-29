# JavaScript data types

There are a total of 8 basic data types in [JavaScript](javascript.md). They are categorized as 7 **primitive** types and 1 **non-primitive** type.

The seven primitive data types are:
- `number` for any kind of number, both integer and floating point, integers are limited by $\pm(2^{53}-1)$
- `bigint` for integer numbers which exceed this limitation
- `string` for strings of text with zero or more characters, there is no separate type for single characters
- `boolean` for `true / false`
- `null` for unknown values - a standalone type with the single value `null`
- `undefined` for unassigned values - a standalone type with the single value `undefined`
- `symbol` for unique identifiers - often used by JavaScript engines, not that commonly used by developers directly

The one non-primitive data type is:
- `object` for the creation of more complex data structures and custom types