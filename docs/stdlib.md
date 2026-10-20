# Standard Library Reference

Complete reference for the Aimi standard library modules.

## Core Module

Basic runtime functions and types.

### Functions

```aimi
function: print(format: string, args...) -> void
function: print_format(format: string, args...) -> void
function: exit(code: i32) -> void
function: strlen(s: string) -> i32
function: strcmp(a: string, b: string) -> i32
function: strcpy(dest: string, src: string) -> string
function: strncpy(dest: string, src: string, n: i32) -> string
function: memset(ptr: *mut u8, value: i8, n: i64) -> void
function: memcpy(dest: *mut u8, src: *const u8, n: i64) -> void
function: memcmp(a: *const u8, b: *const u8, n: i64) -> i32
function: malloc(size: i64) -> *mut u8
function: realloc(ptr: *mut u8, size: i64) -> *mut u8
function: free(ptr: *mut u8) -> void
function: calloc(count: i64, size: i64) -> *mut u8
function: time() -> i64
function: getpid() -> i32
function: open(path: string, flags: i32) -> i32
function: read(fd: i32, buf: *mut u8, count: i64) -> i32
function: write(fd: i32, buf: *const u8, count: i64) -> i32
function: close(fd: i32) -> i32
function: calc(a: i64, op: string, b: i64) -> i64
```

### Constants

```aimi
const: EXIT_SUCCESS = 0
const: EXIT_FAILURE = 1
const: STDIN_FILENO = 0
const: STDOUT_FILENO = 1
const: STDERR_FILENO = 2
```

## Collections Module

Data structures and containers.

### Vector<T>

Dynamic array with amortized O(1) push/pop.

```aimi
function: Vector::new() -> Vector<T>
function: Vector::with_capacity(cap: usize) -> Vector<T>
function: Vector::from_slice(slice: &[T]) -> Vector<T>

method: push(self: &mut Vector<T>, value: T) -> void
method: pop(self: &mut Vector<T>) -> Option<T>
method: get(self: &Vector<T>, index: usize) -> Option<&T>
method: get_mut(self: &mut Vector<T>, index: usize) -> Option<&mut T>
method: set(self: &mut Vector<T>, index: usize, value: T) -> bool
method: len(self: &Vector<T>) -> usize
method: cap(self: &Vector<T>) -> usize
method: is_empty(self: &Vector<T>) -> bool
method: clear(self: &mut Vector<T>) -> void
method: reserve(self: &mut Vector<T>, cap: usize) -> void
method: shrink_to_fit(self: &mut Vector<T>) -> void
method: insert(self: &mut Vector<T>, index: usize, value: T) -> void
method: remove(self: &mut Vector<T>, index: usize) -> T
method: retain(self: &mut Vector<T>, f: fn(&T) -> bool) -> void
method: sort(self: &mut Vector<T>) where T: Ord -> void
method: sort_by(self: &mut Vector<T>, f: fn(&T, &T) -> Ordering) -> void
method: reverse(self: &mut Vector<T>) -> void
method: iter(self: &Vector<T>) -> Iter<T>
method: iter_mut(self: &mut Vector<T>) -> IterMut<T>
method: into_iter(self: Vector<T>) -> IntoIter<T>
```

### HashMap<K, V>

Hash table with O(1) average operations.

```aimi
function: HashMap::new() -> HashMap<K, V>
function: HashMap::with_capacity(cap: usize) -> HashMap<K, V>
function: HashMap::from_iter(iter: IntoIter<(K, V)>) -> HashMap<K, V>

method: insert(self: &mut HashMap<K, V>, key: K, value: V) -> Option<V>
method: get(self: &HashMap<K, V>, key: &K) -> Option<&V>
method: get_mut(self: &mut HashMap<K, V>, key: &K) -> Option<&mut V>
method: remove(self: &mut HashMap<K, V>, key: &K) -> Option<V>
method: contains_key(self: &HashMap<K, V>, key: &K) -> bool
method: len(self: &HashMap<K, V>) -> usize
method: is_empty(self: &HashMap<K, V>) -> bool
method: clear(self: &mut HashMap<K, V>) -> void
method: reserve(self: &mut HashMap<K, V>, cap: usize) -> void
method: keys(self: &HashMap<K, V>) -> Keys<K, V>
method: values(self: &HashMap<K, V>) -> Values<K, V>
method: iter(self: &HashMap<K, V>) -> Iter<K, V>
method: iter_mut(self: &mut HashMap<K, V>) -> IterMut<K, V>
```

### LinkedList<T>

Doubly-linked list.

```aimi
function: LinkedList::new() -> LinkedList<T>

method: push_front(self: &mut LinkedList<T>, value: T) -> void
method: push_back(self: &mut LinkedList<T>, value: T) -> void
method: pop_front(self: &mut LinkedList<T>) -> Option<T>
method: pop_back(self: &mut LinkedList<T>) -> Option<T>
method: front(self: &LinkedList<T>) -> Option<&T>
method: back(self: &LinkedList<T>) -> Option<&T>
method: len(self: &LinkedList<T>) -> usize
method: is_empty(self: &LinkedList<T>) -> bool
method: clear(self: &mut LinkedList<T>) -> void
method: iter(self: &LinkedList<T>) -> Iter<T>
method: iter_mut(self: &mut LinkedList<T>) -> IterMut<T>
```

### Array<T, N>

Fixed-size array.

```aimi
function: Array::new(default: T) -> Array<T, N> where T: Default
function: Array::from_fn(f: fn(usize) -> T) -> Array<T, N>

method: get(self: &Array<T, N>, index: usize) -> Option<&T>
method: get_mut(self: &mut Array<T, N>, index: usize) -> Option<&mut T>
method: set(self: &mut Array<T, N>, index: usize, value: T) -> bool
method: len(self: &Array<T, N>) -> usize
method: fill(self: &mut Array<T, N>, value: T) -> void
method: iter(self: &Array<T, N>) -> Iter<T>
method: iter_mut(self: &mut Array<T, N>) -> IterMut<T>
```

### String

UTF-8 owned string.

```aimi
function: String::new() -> String
function: String::from(s: &str) -> String
function: String::with_capacity(cap: usize) -> String

method: push(self: &mut String, c: char) -> void
method: push_str(self: &mut String, s: &str) -> void
method: pop(self: &mut String) -> Option<char>
method: len(self: &String) -> usize
method: is_empty(self: &String) -> bool
method: as_str(self: &String) -> &str
method: split(self: &String, sep: &str) -> Vec<String>
method: join(self: &String, parts: &[String]) -> String
method: trim(self: &String) -> String
method: to_lowercase(self: &String) -> String
method: to_uppercase(self: &String) -> String
method: replace(self: &String, from: &str, to: &str) -> String
method: contains(self: &String, pat: &str) -> bool
method: starts_with(self: &String, pat: &str) -> bool
method: ends_with(self: &String, pat: &str) -> bool
method: chars(self: &String) -> Chars
method: bytes(self: &String) -> Bytes
```

### Option<T>

Optional value type.

```aimi
enum: Option<T> {
    Some { value: T }
    None
}

static: Option::none() -> Option<T>
static: Option::some(value: T) -> Option<T>

method: is_some(self: &Option<T>) -> bool
method: is_none(self: &Option<T>) -> bool
method: unwrap(self: Option<T>) -> T
method: unwrap_or(self: Option<T>, default: T) -> T
method: unwrap_or_else(self: Option<T>, f: fn() -> T) -> T
method: map(self: Option<T>, f: fn(T) -> U) -> Option<U>
method: map_or(self: Option<T>, default: U, f: fn(T) -> U) -> U
method: map_or_else(self: Option<T>, default: fn() -> U, f: fn(T) -> U) -> U
method: and_then(self: Option<T>, f: fn(T) -> Option<U>) -> Option<U>
method: or(self: Option<T>, other: Option<T>) -> Option<T>
method: or_else(self: Option<T>, f: fn() -> Option<T>) -> Option<T>
method: filter(self: Option<T>, f: fn(&T) -> bool) -> Option<T>
method: expect(self: Option<T>, msg: &str) -> T
```

### Result<T, E>

Error handling type.

```aimi
enum: Result<T, E> {
    Ok { value: T }
    Err { error: E }
}

static: Result::ok(value: T) -> Result<T, E>
static: Result::err(error: E) -> Result<T, E>

method: is_ok(self: &Result<T, E>) -> bool
method: is_err(self: &Result<T, E>) -> bool
method: unwrap(self: Result<T, E>) -> T
method: unwrap_err(self: Result<T, E>) -> E
method: unwrap_or(self: Result<T, E>, default: T) -> T
method: unwrap_or_else(self: Result<T, E>, f: fn(E) -> T) -> T
method: map(self: Result<T, E>, f: fn(T) -> U) -> Result<U, E>
method: map_err(self: Result<T, E>, f: fn(E) -> F) -> Result<T, F>
method: and_then(self: Result<T, E>, f: fn(T) -> Result<U, E>) -> Result<U, E>
method: or_else(self: Result<T, E>, f: fn(E) -> Result<T, F>) -> Result<T, F>
method: expect(self: Result<T, E>, msg: &str) -> T
method: expect_err(self: Result<T, E>, msg: &str) -> E
```

## IO Module

File and stream operations.

### File

```aimi
function: File::open(path: &str) -> Result<File, IOError>
function: File::create(path: &str) -> Result<File, IOError>
function: File::open_append(path: &str) -> Result<File, IOError>
function: File::open_read_write(path: &str) -> Result<File, IOError>

method: read(self: &mut File, buf: &mut [u8]) -> Result<usize, IOError>
method: read_to_end(self: &mut File, buf: &mut Vec<u8>) -> Result<usize, IOError>
method: read_to_string(self: &mut File, buf: &mut String) -> Result<usize, IOError>
method: read_line(self: &mut File, buf: &mut String) -> Result<usize, IOError>
method: write(self: &mut File, buf: &[u8]) -> Result<usize, IOError>
method: write_all(self: &mut File, buf: &[u8]) -> Result<void, IOError>
method: write_line(self: &mut File, line: &str) -> Result<usize, IOError>
method: flush(self: &mut File) -> Result<void, IOError>
method: seek(self: &mut File, pos: SeekFrom) -> Result<u64, IOError>
method: tell(self: &File) -> Result<u64, IOError>
method: metadata(self: &File) -> Result<Metadata, IOError>
method: set_len(self: &mut File, size: u64) -> Result<void, IOError>
method: sync_all(self: &mut File) -> Result<void, IOError>
method: sync_data(self: &mut File) -> Result<void, IOError>
method: try_clone(self: &File) -> Result<File, IOError>
```

### Stdin / Stdout / Stderr

```aimi
function: Stdin::read_line() -> Result<String, IOError>
function: Stdin::read_all() -> Result<String, IOError>
function: Stdin::read_bytes(n: usize) -> Result<Vec<u8>, IOError>
function: Stdin::lock() -> StdinLock

function: Stdout::write(s: &str) -> Result<usize, IOError>
function: Stdout::write_line(line: &str) -> Result<usize, IOError>
function: Stdout::flush() -> Result<void, IOError>
function: Stdout::print(args...) -> void
function: Stdout::lock() -> StdoutLock

function: Stderr::write(s: &str) -> Result<usize, IOError>
function: Stderr::write_line(line: &str) -> Result<usize, IOError>
function: Stderr::flush() -> Result<void, IOError>
function: Stderr::lock() -> StderrLock
```

### Filesystem Operations

```aimi
function: file_exists(path: &str) -> bool
function: is_file(path: &str) -> bool
function: is_dir(path: &str) -> bool
function: file_size(path: &str) -> Result<u64, IOError>
function: remove_file(path: &str) -> Result<void, IOError>
function: rename_file(old: &str, new: &str) -> Result<void, IOError>
function: copy_file(src: &str, dst: &str) -> Result<void, IOError>
function: list_dir(path: &str) -> Result<Vec<String>, IOError>
function: create_dir(path: &str) -> Result<void, IOError>
function: create_dir_all(path: &str) -> Result<void, IOError>
function: remove_dir(path: &str) -> Result<void, IOError>
function: remove_dir_all(path: &str) -> Result<void, IOError>
function: current_dir() -> Result<String, IOError>
function: change_dir(path: &str) -> Result<void, IOError>
function: canonicalize(path: &str) -> Result<String, IOError>
function: read_link(path: &str) -> Result<String, IOError>
function: symlink(src: &str, dst: &str) -> Result<void, IOError>
```

## Memory Module

Memory management utilities.

### Layout

```aimi
struct: Layout {
    size: usize
    align: usize
}

static: Layout::new(size: usize, align: usize) -> Layout
static: Layout::array(count: usize, elem: Layout) -> Result<Layout, LayoutError>
static: Layout::from_size_align(size: usize, align: usize) -> Result<Layout, LayoutError>

method: size(self: Layout) -> usize
method: align(self: Layout) -> usize
method: repeat(self: Layout, n: usize) -> Result<Layout, LayoutError>
method: extend(self: Layout, next: Layout) -> Result<(Layout, usize), LayoutError>
method: padding_needed_for(self: Layout, next: Layout) -> usize
method: pad_to_align(self: Layout) -> Layout
```

### Allocator

```aimi
trait: Allocator {
    function: allocate(self: &Self, layout: Layout) -> Result<*mut u8, AllocError>
    function: deallocate(self: &Self, ptr: *mut u8, layout: Layout) -> void
    function: reallocate(self: &Self, ptr: *mut u8, old_layout: Layout, new_layout: Layout) -> Result<*mut u8, AllocError>
    function: allocate_zeroed(self: &Self, layout: Layout) -> Result<*mut u8, AllocError>
}

struct: GlobalAllocator;

static: GlobalAllocator::instance() -> &'static GlobalAllocator
```

### Smart Pointers

```aimi
// Box - unique ownership
struct: Box<T> {
    function: new(value: T) -> Box<T>
    function: into_inner(self: Box<T>) -> T
    method: as_ref(self: &Box<T>) -> &T
    method: as_mut(self: &mut Box<T>) -> &mut T
}

// Rc - reference counted (single-threaded)
struct: Rc<T> {
    function: new(value: T) -> Rc<T>
    function: clone(self: &Rc<T>) -> Rc<T>
    function: strong_count(self: &Rc<T>) -> usize
    function: try_unwrap(self: Rc<T>) -> Result<T, Rc<T>>
    method: as_ref(self: &Rc<T>) -> &T
}

// Arc - atomic reference counted (thread-safe)
struct: Arc<T> {
    function: new(value: T) -> Arc<T>
    function: clone(self: &Arc<T>) -> Arc<T>
    function: strong_count(self: &Arc<T>) -> usize
    function: try_unwrap(self: Arc<T>) -> Result<T, Arc<T>>
    method: as_ref(self: &Arc<T>) -> &T
}

// UniquePtr - unique pointer with custom deleter
struct: UniquePtr<T, D> {
    function: new(ptr: *mut T, deleter: D) -> UniquePtr<T, D>
    function: release(self: UniquePtr<T, D>) -> *mut T
    function: reset(self: &mut UniquePtr<T, D>, ptr: *mut T) -> void
    method: as_ptr(self: &UniquePtr<T, D>) -> *mut T
    method: as_mut_ptr(self: &mut UniquePtr<T, D>) -> *mut T
}
```

### Raw Memory Operations

```aimi
function: copy_nonoverlapping(src: *const u8, dst: *mut u8, count: usize) -> void
function: copy_overlapping(src: *const u8, dst: *mut u8, count: usize) -> void
function: set_memory(dst: *mut u8, val: u8, count: usize) -> void
function: compare_memory(a: *const u8, b: *const u8, count: usize) -> i32
function: swap(a: *mut u8, b: *mut u8, size: usize) -> void
function: zero_memory(dst: *mut u8, count: usize) -> void
function: align_up(addr: usize, align: usize) -> usize
function: align_down(addr: usize, align: usize) -> usize
function: is_aligned(addr: usize, align: usize) -> bool
```

## Concurrency Module

Threading and synchronization primitives.

### Thread

```aimi
struct: Thread {
    function: spawn(f: fn() -> T) -> Thread
    function: current() -> Thread
    function: sleep(dur: Duration) -> void
    function: yield_now() -> void
    function: park() -> void
    function: park_timeout(dur: Duration) -> void
    
    method: join(self: Thread) -> Result<T, Box<dyn Any + Send>>
    method: id(self: &Thread) -> ThreadId
    method: name(self: &Thread) -> Option<String>
    method: is_alive(self: &Thread) -> bool
}
```

### Mutex

```aimi
struct: Mutex<T> {
    function: new(value: T) -> Mutex<T>
    function: lock(self: &Mutex<T>) -> MutexGuard<T>
    function: try_lock(self: &Mutex<T>) -> Option<MutexGuard<T>>
    function: into_inner(self: Mutex<T>) -> T
    function: get_mut(self: &mut Mutex<T>) -> &mut T
}

struct: MutexGuard<'a, T> {
    method: as_ref(self: &MutexGuard<'a, T>) -> &T
    method: as_mut(self: &mut MutexGuard<'a, T>) -> &mut T
}
```

### RwLock

```aimi
struct: RwLock<T> {
    function: new(value: T) -> RwLock<T>
    function: read(self: &RwLock<T>) -> RwLockReadGuard<T>
    function: try_read(self: &RwLock<T>) -> Option<RwLockReadGuard<T>>
    function: write(self: &RwLock<T>) -> RwLockWriteGuard<T>
    function: try_write(self: &RwLock<T>) -> Option<RwLockWriteGuard<T>>
    function: into_inner(self: RwLock<T>) -> T
    function: get_mut(self: &mut RwLock<T>) -> &mut T
}

struct: RwLockReadGuard<'a, T> { ... }
struct: RwLockWriteGuard<'a, T> { ... }
```

### Condvar

```aimi
struct: Condvar {
    function: new() -> Condvar
    function: wait(self: &Condvar, guard: MutexGuard<T>) -> MutexGuard<T>
    function: wait_timeout(self: &Condvar, guard: MutexGuard<T>, dur: Duration) -> (MutexGuard<T>, WaitTimeoutResult)
    function: notify_one(self: &Condvar) -> void
    function: notify_all(self: &Condvar) -> void
}
```

### Barrier

```aimi
struct: Barrier {
    function: new(n: usize) -> Barrier
    function: wait(self: &Barrier) -> BarrierWaitResult
}
```

### Channel

```aimi
struct: Channel<T> {
    function: new(cap: usize) -> (Sender<T>, Receiver<T>)
    function: unbounded() -> (Sender<T>, Receiver<T>)
}

struct: Sender<T> {
    function: send(self: &Sender<T>, value: T) -> Result<void, SendError<T>>
    function: try_send(self: &Sender<T>, value: T) -> Result<void, TrySendError<T>>
    function: is_empty(self: &Sender<T>) -> bool
    function: len(self: &Sender<T>) -> usize
    function: close(self: Sender<T>) -> void
}

struct: Receiver<T> {
    function: recv(self: &Receiver<T>) -> Result<T, RecvError>
    function: try_recv(self: &Receiver<T>) -> Result<T, TryRecvError>
    function: iter(self: &Receiver<T>) -> Iter<T>
    function: len(self: &Receiver<T>) -> usize
    function: is_empty(self: &Receiver<T>) -> bool
}
```

### Async Runtime

```aimi
struct: AsyncRuntime {
    function: new() -> AsyncRuntime
    function: run(self: &mut AsyncRuntime, future: Future<T>) -> T
    function: spawn(self: &AsyncRuntime, future: Future<T>) -> Task<T>
    function: block_on(self: &AsyncRuntime, future: Future<T>) -> T
}

async function: sleep(dur: Duration) -> void
async function: yield_now() -> void
async function: timeout(dur: Duration, future: Future<T>) -> Result<T, Elapsed>
async function: gather(futures: Vec<Future<T>>) -> Vec<T>
async function: join_all(futures: Vec<Future<T>>) -> Vec<T>
```

### Atomic Types

```aimi
struct: AtomicBool {
    function: new(value: bool) -> AtomicBool
    function: load(self: &AtomicBool, order: Ordering) -> bool
    function: store(self: &AtomicBool, value: bool, order: Ordering) -> void
    function: swap(self: &AtomicBool, value: bool, order: Ordering) -> bool
    function: compare_and_swap(self: &AtomicBool, current: bool, new: bool, order: Ordering) -> Result<bool, bool>
    function: fetch_and(self: &AtomicBool, value: bool, order: Ordering) -> bool
    function: fetch_or(self: &AtomicBool, value: bool, order: Ordering) -> bool
    function: fetch_xor(self: &AtomicBool, value: bool, order: Ordering) -> bool
}

struct: AtomicI32 { ... }
struct: AtomicU32 { ... }
struct: AtomicI64 { ... }
struct: AtomicU64 { ... }
struct: AtomicUsize { ... }
struct: AtomicIsize { ... }
```

## FFI Module

Foreign function interface.

### CLibrary

```aimi
struct: CLibrary {
    function: load(name: &str) -> Result<CLibrary, FFIError>
    function: get_function(self: &CLibrary, name: &str, args: &[CType], ret: CType) -> CFunction
    function: call(self: &CLibrary, name: &str, args...) -> Result<CValue, FFIError>
    function: close(self: CLibrary) -> void
}
```

### CFunction

```aimi
struct: CFunction {
    function: call(self: &CFunction, args...) -> CValue
    function: as_ptr(self: &CFunction) -> *const c_void
}
```

### CStruct / CUnion

```aimi
macro: c_struct! {
    struct Name {
        field1: CType,
        field2: CType,
        ...
    }
}

macro: c_union! {
    union Name {
        field1: CType,
        field2: CType,
        ...
    }
}
```

### CString / CWString

```aimi
struct: CString {
    function: new(s: &str) -> Result<CString, NulError>
    function: from_ptr(ptr: *const c_char) -> CString
    method: as_ptr(self: &CString) -> *const c_char
    method: as_bytes(self: &CString) -> &[u8]
    method: to_string(self: &CString) -> Result<String, Utf8Error>
}

struct: CWString {
    function: new(s: &str) -> CWString
    function: from_ptr(ptr: *const c_wchar) -> CWString
    method: as_ptr(self: &CWString) -> *const c_wchar
    method: to_string(self: &CWString) -> String
}
```

### CArray

```aimi
struct: CArray<T> {
    function: new(len: usize) -> CArray<T> where T: Default
    function: from_slice(slice: &[T]) -> CArray<T> where T: Clone
    method: len(self: &CArray<T>) -> usize
    method: as_ptr(self: &CArray<T>) -> *const T
    method: as_mut_ptr(self: &mut CArray<T>) -> *mut T
    method: get(self: &CArray<T>, index: usize) -> Option<&T>
    method: get_mut(self: &mut CArray<T>, index: usize) -> Option<&mut T>
}
```

### CPointer

```aimi
struct: CPointer<T> {
    function: null() -> CPointer<T>
    function: from_ptr(ptr: *mut T) -> CPointer<T>
    method: as_ptr(self: CPointer<T>) -> *mut T
    method: is_null(self: CPointer<T>) -> bool
    method: offset(self: CPointer<T>, count: isize) -> CPointer<T>
}
```

### CTypes

```aimi
enum: CType {
    Void
    Bool
    Char
    UChar
    Short
    UShort
    Int
    UInt
    Long
    ULong
    LongLong
    ULongLong
    Float
    Double
    LongDouble
    Pointer
    String
    WString
    Struct(name: String)
    Union(name: String)
    Array(element: CType, len: usize)
    Function(args: Vec<CType>, ret: CType)
}
```

### FFI Helpers

```aimi
function: load_library(name: &str) -> Result<CLibrary, FFIError>
function: find_library(name: &str) -> Option<String>
function: get_errno() -> i32
function: set_errno(value: i32) -> void
function: strerror(errno: i32) -> String
function: align_of(ctype: CType) -> usize
function: size_of(ctype: CType) -> usize
function: offset_of(struct: CType, field: &str) -> usize
```

## Prelude

The following are automatically available in every module:

```aimi
// Types
i8 i16 i32 i64 i128 isize
u8 u16 u32 u64 u128 usize
f32 f64
bool char string void

// Core traits
Clone Copy Drop Default Debug Display
PartialEq Eq PartialOrd Ord Hash
Add Sub Mul Div Rem Neg Not
BitAnd BitOr BitXor Shl Shr
Index IndexMut
Send Sync

// Error handling
Option Result

// Collections
Vector HashMap String

// Smart pointers
Box Rc Arc

// Concurrency
Thread Mutex RwLock Channel Sender Receiver
MutexGuard RwLockReadGuard RwLockWriteGuard
Condvar Barrier Once Lazy

// Async
Future Task AsyncRuntime

// FFI
CLibrary CFunction CString CPointer CType

// Memory
Layout GlobalAllocator
copy_nonoverlapping copy_overlapping set_memory
compare_memory swap zero_memory align_up align_down is_aligned

// IO
File Stdin Stdout Stderr
open_file create_file append_file
read_to_string read_to_bytes write_string write_bytes
file_exists is_file is_dir file_size
remove_file rename_file copy_file list_dir
create_dir remove_dir current_dir change_dir
```