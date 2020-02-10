# Protocol Buffers

## Fields

```proto
syntax = "proto3";

message MyMessage {
  int32 id = 1;
  string first_name = 2;
  bool is_validated = 3;
}
```

- `syntax = proto3` = Must declare using proto version
- `message MyMessage` = We must define messages in protocol buffers.
- `string` = Field Type
- `first_name` = Field Name
- `2` = Field Tag (e.g. Number)

## Scalar Types

### Numbers 

Numbers can take various forms based on what values you expect them to have:

`double`, `float`, `int32`, `int64`, `uint32`, `uint64`, `sint32`, `sint64`, `fixed32`, `fixed64`, `sfixed32`, `sfixed64`.

For now, let's use `int32` for integers.

Floating point numbers:

- `float` (32 bits)
- `double` (64 bits) -- for more precision if you need it

Its default value is 0.

### Boolean

Boolean can be either True or False. It's represented as `bool` it protobuf. Its default value is `false`.

### String

A length of text, represented as `string` in Protobuf. Must always contain UTF-8 encoded or 7-bit ASCII text.

### Bytes

Represents any sequence of byte array, represented as `bytes`. It's up to you to interpret it, e.g. sending an image.

## Repeated Fields

- To make lists or an array, you can use the concept of repeated fields. 
- The list can take any number (0 or more) of elements you want.

Its default value is an empty list.

`repeated string phone_numbers = 7;`

## Enums

If you know all the values a field can take in advance, you can leverage the Enum (enumeration) type.

- **The first value of an Enum is the default value.**
- Enum must start by the tag 0 (which is the default value).

```java
// we currently only consider 3 eye colors
enum EyeColor {
  UNKNOWN_EYE_COLOR = 0;
  EYE_GREEN = 1;
  EYE_BROWN = 2;
  EYE_BLUE = 3;
}

EyeColor eye_color = 8;
```

## Nesting Types

It's possible to define types within types.

- Avoid naming conflicts
- Enforce some level of locality for that typ
- You can nest types as deeply as you want.

## Importing Types

You can also have different types in different proto files. This is useful if you want to re-use code and import other `.proto` files created by people in your team.

```java
syntax = "proto3";

// Must include the full root of the protocol buffer
import "cheatsheets/date.proto";
```

## Packages

It is very important to define the packages in which your protocol buffer messages live. 

- When your code gets compiled, it will be placed at the package you indicated.
- It also helps to prevent name conflicts between messages (my.package.Person)

Packages will help all the different languages compiles correctly from `.proto` files (Java, C#, Python, Go, etc.).

## protoc

You will need to download and install `protoc` first. Then in the CLI, use the following commands to take protocol buffer files and convert them into other languages.

- `protoc -I=proto --python_out=python proto/*.proto`
- `protoc -I=proto --java_out=java proto/*.proto`
- `protoc -I=proto --csharp_out=csharp proto/*.proto`
- `protoc -I=proto --php_out=php proto/*.proto`
- `protoc -I=proto --js_out=js proto/*.proto`

And then a breakdown:

- `protoc`: The compiler for protocol buffers.
- `-I=proto`: The source directory we use.
- `--python_out=example`: We're exporting the compiled code as Python to a directory titled "example"
- `proto/*.proto`: Reference of the path that has the protocol buffer files.

## Updating Protocol Rules

If you need to update your schema (i.e. add more fields, deprecate old fields), follow these guidelines.

1. Don't change the numeric tags for any existing fields.
   1. `string first_name = 1` cannot be changed to `string_first_name = 2`
2. You can add new fields, and old code will just ignore them.
3. Likewise, if the old / new code reads unknown data, the default will take place.
4. Fields can be removed, as long as the tag number is not used again in your updated message type.
   1. You may want to rename the field instead, perhaps adding the prefix "OBSOLETE_", or make the tag resered so that future users of your `.proto` can't accidentally reuse the number.
5. For data type changes (int32 to int64 for example), please refer to the documentation.

If you remove a field, make sure to reserve it so it doesn't get used.

- You can reserve tags and field names.
- You can't mix tags and field names in the same reserved statement.
- We reserve tags to prevent new fields from re-using tags (which would break old code at runtime)
- We reserve field names to prevent code bugs.
- **Do not ever remove any reserved tags.**

```java
message MyMessage {
  int32 id = 1;
  string first_name = 2;
}
```

```java
message MyMessage {
  reserved 2;
  reserved "first_name";
  int32 id = 1;
}
```

```java
message Foo {
  reserved 2, 15, 9 to 11;
  reserved "foo", "bar"
}
```
