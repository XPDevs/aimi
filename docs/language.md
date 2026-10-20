# Language Reference

Complete reference for the Aimi programming language syntax and semantics.

## Lexical Structure

### Keywords

```
function struct enum trait impl type module import export
let const mut ref own move
if else match case
while for loop break continue
return yield async await spawn
goto checkpoint compare
print ask exit calc
true false
```

### Operators

| Category | Operators |
|----------|-----------|
| Arithmetic | `+ - * / % **` |
| Comparison | `== != < > <= >=` |
| Logical | `&& || !` |
| Bitwise | `& | ^ ~ << >>` |
| Assignment | `= += -= *= /= %= &= |= ^= <<= >>=` |
| Other | `-> => . :: : ; , ( ) { } [ ] ?` |

### Literals

```aimi
// Integers
42          // decimal
0x2A        // hexadecimal
0o52        // octal
0b101010    // binary

// Floats
3.14
1.5e-10
2.

// Strings
"hello"
'world'
"line1\nline2"
r"raw\nstring"

// Characters
'a'
'\n'
'\u{1F600}'

// Booleans
true
false
```

## Type System

### Primitive Types

```aimi
// Signed integers
i8  i16  i32  i64  i128  isize

// Unsigned integers
u8  u16  u32  u64  u128  usize

// Floating point
f32  f64

// Other
bool
char      // Unicode scalar value
string    // UTF-8 owned string
void      // No value
```

### Type Constructors

```aimi
// References
&Type           // immutable reference
&mut Type       // mutable reference

// Pointers
*Type           // raw pointer
*mut Type       // mutable raw pointer

// Arrays
[Type; N]       // fixed-size array
[Type]          // slice (fat pointer)

// Tuples
(Type1, Type2, ...)

// Functions
fn(Arg1, Arg2) -> Return
```

### User-Defined Types

```aimi
// Structs
struct: Name<Generics> {
    field1: Type1;
    field2: Type2;
    // ...
}

// Enums
enum: Name<Generics> {
    Variant1 { field: Type };
    Variant2(Type1, Type2);
    Variant3;
}

// Type aliases
type: Name<Generics> = ExistingType;

// Traits
trait: Name<Generics>: SuperTrait1 + SuperTrait2 {
    function: method(self: Self, args) -> Return;
    const: CONSTANT: Type;
    type: AssociatedType;
}

// Implementations
impl: Trait<Generics> for Type<Generics> where Bounds {
    // method implementations
}
```

## Expressions

### Literals and Variables

```aimi
42              // integer literal
3.14            // float literal
"hello"         // string literal
true            // boolean
variable        // variable reference
```

### Operators

```aimi
// Arithmetic
a + b
a - b
a * b
a / b
a % b
a ** b          // power

// Comparison
a == b
a != b
a < b
a > b
a <= b
a >= b

// Logical
a && b
a || b
!a

// Bitwise
a & b
a | b
a ^ b
~a
a << b
a >> b

// Assignment
a = b
a += b
// ... other compound assignments
```

### Function Calls

```aimi
function_name()
function_name(arg1, arg2)
Type::method(instance, args)
instance.method(args)
```

### Field Access

```aimi
struct.field
pointer->field
array[index]
slice[start..end]
tuple.0
```

### Control Flow Expressions

```aimi
// If expression
if: { condition } { then_expr } else: { else_expr }

// Match expression
match: expr {
    case: pattern => { body }
    case: pattern if guard => { body }
}

// Loop expressions
while: { condition } { body }
for: item in iterable { body }
loop: { body }
```

### Blocks

```aimi
{
    statement1;
    statement2;
    expression  // last expression is the value
}
```

### Async/Await

```aimi
async { body }
await: future
spawn: || { body }
```

### Goto/Checkpoint

```aimi
goto: 'label';
checkpoint: label;
```

### Compare Blocks

```aimi
compare: {
    if: { condition } { body }
    else if: { condition } { body }
    else: { body }
}
```

## Statements

### Declaration Statements

```aimi
let: name = value;
let: mut name = value;
let: name: Type = value;
const: NAME = value;
```

### Function Definition

```aimi
function: name<Generics>(params) -> ReturnType where Bounds {
    body
}
```

### Struct Definition

```aimi
struct: Name<Generics>: Traits {
    field1: Type1;
    field2: Type2;
}
```

### Enum Definition

```aimi
enum: Name<Generics>: Traits {
    Variant1 { field: Type };
    Variant2(Type);
    Variant3;
}
```

### Trait Definition

```aimi
trait: Name<Generics>: SuperTraits {
    function: method(self: Self, params) -> Return;
    const: CONSTANT: Type;
    type: AssociatedType;
}
```

### Implementation

```aimi
impl: Trait<Generics> for Type<Generics> where Bounds {
    // implementations
}

impl: Type<Generics> {
    // inherent methods
}
```

### Module System

```aimi
module: name {
    // items
}

import: "path" -> { item1, item2 };
import: "path" as alias;

export: { item1, item2 };
```

### Control Flow Statements

```aimi
if: { condition } { then_block } else: { else_block }
match: expr { cases }
while: { condition } { body }
for: pattern in expr { body }
loop: { body }
break;
continue;
return: expr;
yield: expr;
```

### Special Statements

```aimi
print: (format, args...);
ask: (prompt, variable);
exit: (code);
calc: (expression, output_format);
goto: 'label';
checkpoint: label;
label:
```

## Patterns

```aimi
// Literal patterns
42
"hello"
true

// Variable patterns
name
_              // wildcard

// Struct patterns
Point { x, y }
Point { x: 0, .. }

// Enum patterns
Option::Some { value }
Option::None
Result::Ok(value)
Result::Err(error)

// Tuple patterns
(a, b, c)

// Slice patterns
[first, rest..]
[.., last]

// Or patterns
A | B | C

// Guard patterns
pattern if condition
```

## Generics and Bounds

### Generic Parameters

```aimi
function: name<T, U>(a: T, b: U) -> T { ... }
struct: Name<T: Trait> { field: T }
impl: Trait for Type<T> where T: OtherTrait { ... }
```

### Where Clauses

```aimi
function: foo<T, U>(a: T, b: U) -> V
where
    T: Clone + Debug,
    U: Into<T>,
    V: Default,
{ ... }
```

### Trait Bounds

```aimi
T: Trait
T: Trait1 + Trait2
T: 'lifetime
T: ?Sized
```

## Attributes

```aimi
#[inline]
#[no_mangle]
#[export_name = "name"]
#[link_section = "section"]
#[repr(C)]
#[repr(transparent)]
#[derive(Debug, Clone)]
#[cfg(feature = "feature")]
```

## Built-in Traits

### Core Traits

```aimi
trait: Clone {
    function: clone(self: Self) -> Self;
}

trait: Copy { }  // marker trait

trait: Drop {
    function: drop(self: Self);
}

trait: Default {
    function: default() -> Self;
}

trait: Debug {
    function: fmt(self: Self, f: &mut Formatter) -> Result;
}

trait: Display {
    function: fmt(self: Self, f: &mut Formatter) -> Result;
}

trait: PartialEq {
    function: eq(self: Self, other: Self) -> bool;
    function: ne(self: Self, other: Self) -> bool;
}

trait: Eq: PartialEq { }

trait: PartialOrd {
    function: partial_cmp(self: Self, other: Self) -> Option<Ordering>;
}

trait: Ord: Eq + PartialOrd {
    function: cmp(self: Self, other: Self) -> Ordering;
}

trait: Hash {
    function: hash(self: Self, state: &mut Hasher);
}
```

### Operator Traits

```aimi
trait: Add<Rhs = Self> {
    type: Output;
    function: add(self: Self, rhs: Rhs) -> Output;
}

trait: Sub<Rhs = Self> { ... }
trait: Mul<Rhs = Self> { ... }
trait: Div<Rhs = Self> { ... }
trait: Rem<Rhs = Self> { ... }

trait: Neg { ... }
trait: Not { ... }

trait: BitAnd<Rhs = Self> { ... }
trait: BitOr<Rhs = Self> { ... }
trait: BitXor<Rhs = Self> { ... }

trait: Shl<Rhs = Self> { ... }
trait: Shr<Rhs = Self> { ... }

trait: Index<Idx> {
    type: Output;
    function: index(self: Self, idx: Idx) -> &Output;
}

trait: IndexMut<Idx>: Index<Idx> {
    function: index_mut(self: Self, idx: Idx) -> &mut Output;
}
```

### Concurrency Traits

```aimi
trait: Send { }  // safe to send between threads
trait: Sync { }  // safe to share between threads
```

## Standard Library Prelude

The following items are automatically imported:

```aimi
// Types
i8 i16 i32 i64 i128 isize
u8 u16 u32 u64 u128 usize
f32 f64
bool char string void

// Traits
Clone Copy Drop Default Debug Display
PartialEq Eq PartialOrd Ord Hash
Add Sub Mul Div Rem Neg Not
BitAnd BitOr BitXor Shl Shr
Index IndexMut
Send Sync

// Functions
print ask exit calc
drop clone

// Types
Option Result
Vector HashMap String
Box Rc Arc Mutex RwLock Channel
Thread Future
```

## Error Handling

### Option Type

```aimi
enum: Option<T> {
    Some { value: T };
    None;
}

// Methods
function: is_some(self: Option<T>) -> bool;
function: is_none(self: Option<T>) -> bool;
function: unwrap(self: Option<T>) -> T;
function: unwrap_or(self: Option<T>, default: T) -> T;
function: map(self: Option<T>, f: fn(T) -> U) -> Option<U>;
function: and_then(self: Option<T>, f: fn(T) -> Option<U>) -> Option<U>;
```

### Result Type

```aimi
enum: Result<T, E> {
    Ok { value: T };
    Err { error: E };
}

// Methods
function: is_ok(self: Result<T, E>) -> bool;
function: is_err(self: Result<T, E>) -> bool;
function: unwrap(self: Result<T, E>) -> T;
function: unwrap_err(self: Result<T, E>) -> E;
function: map(self: Result<T, E>, f: fn(T) -> U) -> Result<U, E>;
function: map_err(self: Result<T, E>, f: fn(E) -> F) -> Result<T, F>;
function: and_then(self: Result<T, E>, f: fn(T) -> Result<U, E>) -> Result<U, E>;
function: or_else(self: Result<T, E>, f: fn(E) -> Result<T, F>) -> Result<T, F>;
```

### Error Propagation

```aimi
function: read_file(path: String) -> Result<String, IOError> {
    let: file = File::open(path)?;  // ? operator propagates error
    let: content = file.read_to_string()?;
    return: Ok(content);
}
```

## Macros

### Declarative Macros

```aimi
macro: vec {
    () => { Vector::new() };
    ($($x:expr),*) => {
        {
            let: mut v = Vector::new();
            $(v.push($x);)*
            v
        }
    };
}

let: v = vec![1, 2, 3];
```

### Procedural Macros

```aimi
#[derive(Debug)]
struct: Point { x: i32, y: i32 }

#[async_trait]
trait: AsyncTrait { ... }
```

## Unsafe Code

```aimi
unsafe {
    // dereference raw pointers
    let: value = *ptr;
    
    // call unsafe functions
    unsafe_function();
    
    // access mutable static
    static mut COUNTER: i32 = 0;
    COUNTER = COUNTER + 1;
}

// Unsafe functions
unsafe function: dangerous() { ... }

// Unsafe traits
unsafe trait: Send { }
```

## Compile-Time Execution

```aimi
const: COMPUTED = {
    let: sum = 0;
    for: i in 0..100 {
        sum = sum + i;
    }
    sum
};

function: const_fn(x: i32) -> i32 {
    return: x * 2;
}

let: arr = [const_fn(i) for i in 0..10];
```

## Modules and Crates

### Module Declaration

```aimi
// Inline module
module: math {
    function: add(a: i32, b: i32) -> i32 { a + b }
    function: sub(a: i32, b: i32) -> i32 { a - b }
}

// File module (math.aimi or math/mod.aimi)
// Exported with `export` keyword
```

### Visibility

```aimi
pub function: public_func() { }   // public
function: private_func() { }      // private (default)
pub(crate) function: crate_func() { }  // crate-visible
pub(super) function: parent_func() { } // parent module
pub(in path::to::module) function: scoped() { }
```

## Testing

```aimi
#[test]
function: test_addition() {
    assert_eq!(add(2, 3), 5);
}

#[test]
#[should_panic]
function: test_division_by_zero() {
    let: _ = 1 / 0;
}

#[bench]
function: bench_addition(b: &mut Bencher) {
    b.iter(|| { add(1, 2); });
}
```

## Conditional Compilation

```aimi
#[cfg(target_os = "linux")]
function: linux_only() { }

#[cfg(feature = "serde")]
function: serialize() { }

#[cfg(all(target_arch = "x86_64", target_os = "windows"))]
function: windows_x64() { }
```

## Inline Assembly

```aimi
unsafe {
    asm!(
        "mov {}, {}", 
        out(reg) result, 
        in(reg) input,
        options(nostack)
    );
}
```

## Foreign Function Interface

```aimi
extern "C" {
    function: c_function(arg: i32) -> i32;
}

#[link(name = "library")]
extern "C" {
    function: library_function();
}

extern "system" {
    function: windows_api();
}
```