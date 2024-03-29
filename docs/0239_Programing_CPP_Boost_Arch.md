---
Title | Programing CPP Boost Arch
-- | --
Created @ | `2023-04-06T13:46:21Z`
Updated @| `2023-04-06T13:46:21Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/239)

---
# Boost Arch

## Algorithms

- [Algorithm](https://www.boost.org/doc/libs/1_81_0/libs/algorithm/index.html) - A collection of useful generic algorithms, from Marshall Clow
- [Foreach](https://www.boost.org/doc/libs/1_81_0/libs/foreach/index.html) - In C++, writing a loop that iterates over a sequence is tedious. We can either use iterators, which requires a considerable amount of boiler-plate, or we can use the std::for_each() algorithm and move our loop body into a predicate, which requires no less boiler-plate and forces us to move our logic far from where it will be used. In contrast, some other languages, like Perl, provide a dedicated "foreach" construct that automates this process. BOOST_FOREACH is just such a construct for C++. It iterates over sequences for us, freeing us from having to deal directly with iterators or write predicates, from Eric Niebler
- [Geometry](https://www.boost.org/doc/libs/1_81_0/libs/geometry/index.html) - The Boost.Geometry library provides geometric algorithms, primitives and spatial index, from Barend Gehrels, Bruno Lalande, Mateusz Loskot, Adam Wulkiewicz, Menelaos Karavelas and Vissarion Fisikopoulos
- [GIL](https://www.boost.org/doc/libs/1_81_0/libs/gil/index.html) - (C++14) Generic Image Library, from Lubomir Bourdev, Hailin Jin and Christian Henning
- [Graph](https://www.boost.org/doc/libs/1_81_0/libs/graph/index.html) - The BGL graph interface and graph components are generic, in the same sense as the Standard Template Library (STL), from Jeremy Siek and a University of Notre Dame team.
- [GraphParallel](https://www.boost.org/doc/libs/1_81_0/libs/graph_parallel/index.html) - The PBGL graph interface and graph components are generic, in the same sense as the Standard Template Library (STL), from Jeremy Siek, Doug Gregor, and a University of Notre Dame team.
- [Histogram](https://www.boost.org/doc/libs/1_81_0/libs/histogram/index.html) - Fast multi-dimensional histogram with convenient interface for C++14, from Hans Dembinski
- [Min-Max](https://www.boost.org/doc/libs/1_81_0/libs/algorithm/minmax/index.html) - Standard library extensions for simultaneous min/max and min/max element computations, from Hervé Brönnimann
- [Polygon](https://www.boost.org/doc/libs/1_81_0/libs/polygon/index.html) - Voronoi diagram construction and booleans/clipping, resizing/offsetting and more for planar polygons with integral coordinates, from Lucanus Simonson and Andrii Sydorchuk
- [QVM](https://www.boost.org/doc/libs/1_81_0/libs/qvm/index.html) - Generic C++ library for working with Quaternions Vectors and Matrices, from Emil Dotchevski
- [Range](https://www.boost.org/doc/libs/1_81_0/libs/range/index.html) - A new infrastructure for generic algorithms that builds on top of the new iterator concepts, from Niel Groves and Thorsten Ottosen
- [Sort](https://www.boost.org/doc/libs/1_81_0/libs/sort/index.html) - High-performance templated sort functions, from Steven Ross
- [String Algo](https://www.boost.org/doc/libs/1_81_0/libs/algorithm/string/index.html) - String algorithms library, from Pavol Droba
- [Utility](https://www.boost.org/doc/libs/1_81_0/libs/utility/utility.htm) - Class noncopyable plus checked_delete(), checked_array_delete(), next(), prior() function templates, plus base-from-member idiom, from Dave Abrahams and others

## Broken compiler workarounds

- [Compatibility](https://www.boost.org/doc/libs/1_81_0/libs/compatibility/index.html) - Help for non-conforming standard libraries, from Ralf Grosse-Kunstleve and Jens Maurer
- [Config](https://www.boost.org/doc/libs/1_81_0/libs/config/doc/html/index.html) - Helps Boost library developers adapt to compiler idiosyncrasies; not intended for library users

## Concurrent Programming

- [Asio](https://www.boost.org/doc/libs/1_81_0/libs/asio/index.html) - Portable networking and other low-level I/O, including sockets, timers, hostname resolution, socket iostreams, serial ports, file descriptors and Windows HANDLEs, from Chris Kohlhoff
- [Atomic](https://www.boost.org/doc/libs/1_81_0/libs/atomic/index.html) - C++11-style atomic<>, from Helge Bahmann, Tim Blechmann and Andrey Semashev
- [Beast](https://www.boost.org/doc/libs/1_81_0/libs/beast/index.html) - Portable HTTP, WebSocket, and network operations using only C++11 and Boost.Asio, from Vinnie Falco
- [Compute](https://www.boost.org/doc/libs/1_81_0/libs/compute/index.html) - Parallel/GPU-computing library, from Kyle Lutz
- [Context](https://www.boost.org/doc/libs/1_81_0/libs/context/index.html) - (C++11) Context switching library, from Oliver Kowalke
- [Coroutine](https://www.boost.org/doc/libs/1_81_0/libs/coroutine/index.html) - Coroutine library, from Oliver Kowalke
- [Coroutine2](https://www.boost.org/doc/libs/1_81_0/libs/coroutine2/index.html) - (C++11) Coroutine library, from Oliver Kowalke
- [Fiber](https://www.boost.org/doc/libs/1_81_0/libs/fiber/index.html) - (C++11) Userland threads library, from Oliver Kowalke
- [Interprocess](https://www.boost.org/doc/libs/1_81_0/libs/interprocess/index.html) - Shared memory, memory mapped files, process-shared mutexes, condition variables, containers and allocators, from Ion Gaztañaga
- [Lockfree](https://www.boost.org/doc/libs/1_81_0/libs/lockfree/index.html) - Lockfree data structures, from Tim Blechmann
- [MPI](https://www.boost.org/doc/libs/1_81_0/libs/mpi/index.html) - Message Passing Interface library, for use in distributed-memory parallel application programming, from Douglas Gregor and Matthias Troyer
- [Thread](https://www.boost.org/doc/libs/1_81_0/libs/thread/index.html) - Portable C++ multi-threading. C++03, C++11, C++14, C++17, from Anthony Williams and Vicente J. Botet Escriba

## Containers

- [Array](https://www.boost.org/doc/libs/1_81_0/libs/array/index.html) - STL compliant container wrapper for arrays of constant size, from Nicolai Josuttis
- [Bimap](https://www.boost.org/doc/libs/1_81_0/libs/bimap/index.html) - Bidirectional maps library for C++. With Boost.Bimap you can create associative containers in which both types can be used as key, from Matias Capeletto
- [Circular Buffer](https://www.boost.org/doc/libs/1_81_0/libs/circular_buffer/index.html) - A STL compliant container also known as ring or cyclic buffer, from Jan Gaspar
- [Container](https://www.boost.org/doc/libs/1_81_0/libs/container/index.html) - Standard library containers and extensions, from Ion Gaztañaga
- [Dynamic Bitset](https://www.boost.org/doc/libs/1_81_0/libs/dynamic_bitset/dynamic_bitset.html) - The dynamic_bitset class represents a set of bits. It provides accesses to the value of individual bits via an operator[] and provides all of the bitwise operators that one can apply to builtin integers, such as operator& and operator<<. The number of bits in the set is specified at runtime via a parameter to the constructor of the dynamic_bitset, from Jeremy Siek and Chuck Allison
- [GIL](https://www.boost.org/doc/libs/1_81_0/libs/gil/index.html) - (C++14) Generic Image Library, from Lubomir Bourdev, Hailin Jin and Christian Henning
- [Graph](https://www.boost.org/doc/libs/1_81_0/libs/graph/index.html) - The BGL graph interface and graph components are generic, in the same sense as the Standard Template Library (STL), from Jeremy Siek and a University of Notre Dame team.
- [GraphParallel](https://www.boost.org/doc/libs/1_81_0/libs/graph_parallel/index.html) - The PBGL graph interface and graph components are generic, in the same sense as the Standard Template Library (STL), from Jeremy Siek, Doug Gregor, and a University of Notre Dame team.
- [ICL](https://www.boost.org/doc/libs/1_81_0/libs/icl/index.html) - Interval Container Library, interval sets and maps and aggregation of associated values, from Joachim Faulhaber
- [Intrusive](https://www.boost.org/doc/libs/1_81_0/libs/intrusive/index.html) - Intrusive containers and algorithms, from Ion Gaztañaga
- [JSON](https://www.boost.org/doc/libs/1_81_0/libs/json/index.html) - JSON parsing, serialization, and DOM in C++11, from Vinnie Falco and Krystian Stasiowski
- [Multi-Array](https://www.boost.org/doc/libs/1_81_0/libs/multi_array/index.html) - Boost.MultiArray provides a generic N-dimensional array concept definition and common implementations of that interface, from Ron Garcia
- [Multi-Index](https://www.boost.org/doc/libs/1_81_0/libs/multi_index/index.html) - The Boost Multi-index Containers Library provides a class template named multi_index_container which enables the construction of containers maintaining one or more indices with different sorting and access semantics, from Joaquín M López Muñoz
- [Pointer Container](https://www.boost.org/doc/libs/1_81_0/libs/ptr_container/index.html) - Containers for storing heap-allocated polymorphic objects to ease OO-programming, from Thorsten Ottosen
- [PolyCollection](https://www.boost.org/doc/libs/1_81_0/libs/poly_collection/index.html) - Fast containers of polymorphic objects, from Joaquín M López Muñoz
- [Property Map](https://www.boost.org/doc/libs/1_81_0/libs/property_map/index.html) - Concepts defining interfaces which map key objects to value objects, from Jeremy Siek
- [Property Map (Parallel)](https://www.boost.org/doc/libs/1_81_0/libs/property_map_parallel/index.html) - Parallel extensions to Property Map for use with Parallel Graph, from Jeremy Siek
- [Property Tree](https://www.boost.org/doc/libs/1_81_0/libs/property_tree/index.html) - A tree data structure especially suited to storing configuration data, from Marcin Kalicinski and Sebastian Redl
- [String_ref](https://www.boost.org/doc/libs/1_81_0/libs/utility/doc/html/string_ref.html) - String view templates, from Marshall Clow
- [Unordered](https://www.boost.org/doc/libs/1_81_0/libs/unordered/index.html) - Unordered associative containers, from Daniel James
- [URL](https://www.boost.org/doc/libs/1_81_0/libs/url/index.html) - URL parsing in C++11, from Vinnie Falco and Alan de Freitas
- [Variant](https://www.boost.org/doc/libs/1_81_0/libs/variant/index.html) - Safe, generic, stack-based discriminated union container, from Eric Friedman and Itay Maman
- [Variant2](https://www.boost.org/doc/libs/1_81_0/libs/variant2/index.html) - A never-valueless, strong guarantee implementation of std::variant, from Peter Dimov

## Correctness and testing

- [Assert](https://www.boost.org/doc/libs/1_81_0/libs/assert/index.html) - Customizable assert macros, from Peter Dimov
- [Concept Check](https://www.boost.org/doc/libs/1_81_0/libs/concept_check/index.html) - Tools for generic programming, from Jeremy Siek
- [Contract](https://www.boost.org/doc/libs/1_81_0/libs/contract/index.html) - Contract programming for C++. All contract programming features are supported: Subcontracting, class invariants, postconditions (with old and return values), preconditions, customizable actions on assertion failure (e.g., terminate or throw), optional compilation and checking of assertions, etc, from Lorenzo Caminiti
- [Safe Numerics](https://www.boost.org/doc/libs/1_81_0/libs/safe_numerics/index.html) - Guaranteed Correct Integer Arithmetic, from Robert Ramey
- [Stacktrace](https://www.boost.org/doc/libs/1_81_0/libs/stacktrace/index.html) - Gather, store, copy and print backtraces, from Antony Polukhin
- [Static Assert](https://www.boost.org/doc/libs/1_81_0/libs/static_assert/index.html) - Static assertions (compile time assertions), from John Maddock
- [Test](https://www.boost.org/doc/libs/1_81_0/libs/test/index.html) - Support for simple program testing, full unit testing, and for program execution monitoring, from Gennadiy Rozental and Raffi Enficiaud

## Data structures

- [Any](https://www.boost.org/doc/libs/1_81_0/libs/any/index.html) - Safe, generic container for single values of different value types, from Kevlin Henney
- [Bimap](https://www.boost.org/doc/libs/1_81_0/libs/bimap/index.html) - Bidirectional maps library for C++. With Boost.Bimap you can create associative containers in which both types can be used as key, from Matias Capeletto
- [Compressed Pair](https://www.boost.org/doc/libs/1_81_0/libs/utility/compressed_pair.htm) - Empty member optimization, from John Maddock, Howard Hinnant, et al
- [Container](https://www.boost.org/doc/libs/1_81_0/libs/container/index.html) - Standard library containers and extensions, from Ion Gaztañaga
- [Fusion](https://www.boost.org/doc/libs/1_81_0/libs/fusion/doc/html/index.html) - Library for working with tuples, including various containers, algorithms, etc, from Joel de Guzman, Dan Marsden and Tobias Schwinger
- [Geometry](https://www.boost.org/doc/libs/1_81_0/libs/geometry/index.html) - The Boost.Geometry library provides geometric algorithms, primitives and spatial index, from Barend Gehrels, Bruno Lalande, Mateusz Loskot, Adam Wulkiewicz, Menelaos Karavelas and Vissarion Fisikopoulos
- [Heap](https://www.boost.org/doc/libs/1_81_0/libs/heap/index.html) - Priority queue data structures, from Tim Blechmann
- [Histogram](https://www.boost.org/doc/libs/1_81_0/libs/histogram/index.html) - Fast multi-dimensional histogram with convenient interface for C++14, from Hans Dembinski
- [ICL](https://www.boost.org/doc/libs/1_81_0/libs/icl/index.html) - Interval Container Library, interval sets and maps and aggregation of associated values, from Joachim Faulhaber
- [JSON](https://www.boost.org/doc/libs/1_81_0/libs/json/index.html) - JSON parsing, serialization, and DOM in C++11, from Vinnie Falco and Krystian Stasiowski
- [Multi-Index](https://www.boost.org/doc/libs/1_81_0/libs/multi_index/index.html) - The Boost Multi-index Containers Library provides a class template named multi_index_container which enables the construction of containers maintaining one or more indices with different sorting and access semantics, from Joaquín M López Muñoz
- [Optional](https://www.boost.org/doc/libs/1_81_0/libs/optional/index.html) - A value-semantic, type-safe wrapper for representing 'optional' (or 'nullable') objects of a given type. An optional object may or may not contain a value of the underlying type, from Fernando Cacciola
- [PFR](https://www.boost.org/doc/libs/1_81_0/libs/pfr/index.html) - Basic reflection for user defined types, from Antony Polukhin
- [Pointer Container](https://www.boost.org/doc/libs/1_81_0/libs/ptr_container/index.html) - Containers for storing heap-allocated polymorphic objects to ease OO-programming, from Thorsten Ottosen
- [Polygon](https://www.boost.org/doc/libs/1_81_0/libs/polygon/index.html) - Voronoi diagram construction and booleans/clipping, resizing/offsetting and more for planar polygons with integral coordinates, from Lucanus Simonson and Andrii Sydorchuk
- [Property Tree](https://www.boost.org/doc/libs/1_81_0/libs/property_tree/index.html) - A tree data structure especially suited to storing configuration data, from Marcin Kalicinski and Sebastian Redl
- [Tuple](https://www.boost.org/doc/libs/1_81_0/libs/tuple/index.html) - Ease definition of functions returning multiple values, and more, from Jaakko Järvi
- [Type Erasure](https://www.boost.org/doc/libs/1_81_0/libs/type_erasure/index.html) - Runtime polymorphism based on concepts, from Steven Watanabe
- [URL](https://www.boost.org/doc/libs/1_81_0/libs/url/index.html) - URL parsing in C++11, from Vinnie Falco and Alan de Freitas
- [Uuid](https://www.boost.org/doc/libs/1_81_0/libs/uuid/index.html) - A universally unique identifier, from Andy Tompkins
- [Variant](https://www.boost.org/doc/libs/1_81_0/libs/variant/index.html) - Safe, generic, stack-based discriminated union container, from Eric Friedman and Itay Maman
- [Variant2](https://www.boost.org/doc/libs/1_81_0/libs/variant2/index.html) - A never-valueless, strong guarantee implementation of std::variant, from Peter Dimov

## Domain Specific

- [Chrono](https://www.boost.org/doc/libs/1_81_0/libs/chrono/index.html) - Useful time utilities. C++11, from Howard Hinnant, Beman Dawes and Vicente J. Botet Escriba
- [CRC](https://www.boost.org/doc/libs/1_81_0/libs/crc/index.html) - The Boost CRC Library provides two implementations of CRC (cyclic redundancy code) computation objects and two implementations of CRC computation functions. The implementations are template-based, from Daryle Walker
- [Date Time](https://www.boost.org/doc/libs/1_81_0/libs/date_time/index.html) - A set of date-time libraries based on generic programming concepts, from Jeff Garland
- [Units](https://www.boost.org/doc/libs/1_81_0/libs/units/index.html) - Zero-overhead dimensional analysis and unit/quantity manipulation and conversion, from Matthias Schabel and Steven Watanabe
- [Uuid](https://www.boost.org/doc/libs/1_81_0/libs/uuid/index.html) - A universally unique identifier, from Andy Tompkins

## Error handling and recovery

- [Assert](https://www.boost.org/doc/libs/1_81_0/libs/assert/index.html) - Customizable assert macros, from Peter Dimov
- [LEAF](https://www.boost.org/doc/libs/1_81_0/libs/leaf/index.html) - A lightweight error handling library for C++11, from Emil Dotchevski
- [System](https://www.boost.org/doc/libs/1_81_0/libs/system/index.html) - Extensible error reporting, from Beman Dawes
- [ThrowException](https://www.boost.org/doc/libs/1_81_0/libs/throw_exception/index.html) - A common infrastructure for throwing exceptions from Boost libraries, from Emil Dotchevski and Peter Dimov

## Function objects and higher-order programming

- [Bind](https://www.boost.org/doc/libs/1_81_0/libs/bind/index.html) - boost::bind is a generalization of the standard functions std::bind1st and std::bind2nd. It supports arbitrary function objects, functions, function pointers, and member function pointers, and is able to bind any argument to a specific value or route input arguments into arbitrary positions, from Peter Dimov
- [Container Hash](https://www.boost.org/doc/libs/1_81_0/libs/container_hash/index.html) - An STL-compatible hash function object that can be extended to hash user defined types, from Daniel James
- [Function](https://www.boost.org/doc/libs/1_81_0/libs/function/index.html) - Function object wrappers for deferred calls or callbacks, from Doug Gregor
- [Functional](https://www.boost.org/doc/libs/1_81_0/libs/functional/index.html) - The Boost.Function library contains a family of class templates that are function object wrappers, from Mark Rodgers
- [Functional/Factory](https://www.boost.org/doc/libs/1_81_0/libs/functional/factory/index.html) - Function object templates for dynamic and static object creation, from Glen Fernandes and Tobias Schwinger
- [Functional/Forward](https://www.boost.org/doc/libs/1_81_0/libs/functional/forward/index.html) - Adapters to allow generic function objects to accept arbitrary arguments, from Tobias Schwinger
- [Functional/Overloaded Function](https://www.boost.org/doc/libs/1_81_0/libs/functional/overloaded_function/index.html) - Overload different functions into a single function object, from Lorenzo Caminiti
- [HOF](https://www.boost.org/doc/libs/1_81_0/libs/hof/index.html) - Higher-order functions for C++, from Paul Fultz II
- [Lambda](https://www.boost.org/doc/libs/1_81_0/libs/lambda/index.html) - Define small unnamed function objects at the actual call site, and more, from Jaakko Järvi and Gary Powell
- [Lambda2](https://www.boost.org/doc/libs/1_81_0/libs/lambda2/index.html) - A C++14 lambda library, from Peter Dimov
- [Local Function](https://www.boost.org/doc/libs/1_81_0/libs/local_function/index.html) - Program functions locally, within other functions, directly within the scope where they are needed, from Lorenzo Caminiti
- [Member Function](https://www.boost.org/doc/libs/1_81_0/libs/bind/mem_fn.html) - Generalized binders for function/object/pointers and member functions, from Peter Dimov
- [Phoenix](https://www.boost.org/doc/libs/1_81_0/libs/phoenix/index.html) - Define small unnamed function objects at the actual call site, and more, from Joel de Guzman, Dan Marsden, Thomas Heller and John Fletcher
- [Ref](https://www.boost.org/doc/libs/1_81_0/libs/core/ref.html) - A utility library for passing references to generic functions, from Jaako Järvi, Peter Dimov, Doug Gregor and Dave Abrahams
- [Result Of](https://www.boost.org/doc/libs/1_81_0/libs/utility/utility.htm#result_of) - Determines the type of a function call expression
- [Signals2](https://www.boost.org/doc/libs/1_81_0/libs/signals2/index.html) - Managed signals & slots callback implementation (thread-safe version 2), from Frank Mori Hess
- [Utility](https://www.boost.org/doc/libs/1_81_0/libs/utility/utility.htm) - Class noncopyable plus checked_delete(), checked_array_delete(), next(), prior() function templates, plus base-from-member idiom, from Dave Abrahams and others

## Generic Programming

- [Call Traits](https://www.boost.org/doc/libs/1_81_0/libs/utility/call_traits.htm) - Defines types for passing parameters, from John Maddock, Howard Hinnant, et al
- [Concept Check](https://www.boost.org/doc/libs/1_81_0/libs/concept_check/index.html) - Tools for generic programming, from Jeremy Siek
- [Enable If](https://www.boost.org/doc/libs/1_81_0/libs/core/doc/html/core/enable_if.html) - Selective inclusion of function template overloads, from Jaakko Järvi, Jeremiah Willcock and Andrew Lumsdaine
- [Function Types](https://www.boost.org/doc/libs/1_81_0/libs/function_types/index.html) - Boost.FunctionTypes provides functionality to classify, decompose and synthesize function, function pointer, function reference and pointer to member types, from Tobias Schwinger
- [GIL](https://www.boost.org/doc/libs/1_81_0/libs/gil/index.html) - (C++14) Generic Image Library, from Lubomir Bourdev, Hailin Jin and Christian Henning
- [In Place Factory, Typed In Place Factory](https://www.boost.org/doc/libs/1_81_0/libs/utility/in_place_factories.html) - Generic in-place construction of contained objects with a variadic argument-list, from Fernando Cacciola
- [Operators](https://www.boost.org/doc/libs/1_81_0/libs/utility/operators.htm) - Templates ease arithmetic classes and iterators, from Dave Abrahams and Jeremy Siek
- [Property Map](https://www.boost.org/doc/libs/1_81_0/libs/property_map/index.html) - Concepts defining interfaces which map key objects to value objects, from Jeremy Siek
- [Property Map (Parallel)](https://www.boost.org/doc/libs/1_81_0/libs/property_map_parallel/index.html) - Parallel extensions to Property Map for use with Parallel Graph, from Jeremy Siek
- [QVM](https://www.boost.org/doc/libs/1_81_0/libs/qvm/index.html) - Generic C++ library for working with Quaternions Vectors and Matrices, from Emil Dotchevski
- [Static Assert](https://www.boost.org/doc/libs/1_81_0/libs/static_assert/index.html) - Static assertions (compile time assertions), from John Maddock
- [Stl_interfaces](https://www.boost.org/doc/libs/1_81_0/libs/stl_interfaces/index.html) - C++14 and later CRTP templates for defining iterators, views, and containers, from T. Zachary Laine
- [TTI](https://www.boost.org/doc/libs/1_81_0/libs/tti/index.html) - [Type Traits](https://www.boost.org/doc/libs/1_81_0/libs/type_traits/index.html) Introspection library, from Edward Diener
- Type Traits - Templates for fundamental properties of types, from John Maddock, Steve Cleary, et al
- [YAP](https://www.boost.org/doc/libs/1_81_0/libs/yap/index.html) - An expression template library for C++14 and later, from T. Zachary Laine

## Image processing

- [GIL](https://www.boost.org/doc/libs/1_81_0/libs/gil/index.html) - (C++14) Generic Image Library, from Lubomir Bourdev, Hailin Jin and Christian Henning

## Input/Output

- [Asio](https://www.boost.org/doc/libs/1_81_0/libs/asio/index.html) - Portable networking and other low-level I/O, including sockets, timers, hostname resolution, socket iostreams, serial ports, file descriptors and Windows HANDLEs, from Chris Kohlhoff
- [Assign](https://www.boost.org/doc/libs/1_81_0/libs/assign/index.html) - Filling containers with constant or generated data has never been easier, from Thorsten Ottosen
- [Beast](https://www.boost.org/doc/libs/1_81_0/libs/beast/index.html) - Portable HTTP, WebSocket, and network operations using only C++11 and Boost.Asio, from Vinnie Falco
- [Endian](https://www.boost.org/doc/libs/1_81_0/libs/endian/index.html) - Types and conversion functions for correct byte ordering and more regardless of processor endianness, from Beman Dawes
- [Format](https://www.boost.org/doc/libs/1_81_0/libs/format/index.html) - The format library provides a type-safe mechanism for formatting arguments according to a printf-like format-string, from Samuel Krempp
- [IO](https://www.boost.org/doc/libs/1_81_0/libs/io/doc/html/io.html) - Utilities for the standard I/O library, from Daryle Walker, Beman Dawes and Glen Fernandes
- [Iostreams](https://www.boost.org/doc/libs/1_81_0/libs/iostreams/index.html) - Boost.IOStreams provides a framework for defining streams, stream buffers and i/o filters, from Jonathan Turkanis
- [JSON](https://www.boost.org/doc/libs/1_81_0/libs/json/index.html) - JSON parsing, serialization, and DOM in C++11, from Vinnie Falco and Krystian Stasiowski
- [Program Options](https://www.boost.org/doc/libs/1_81_0/libs/program_options/index.html) - The program_options library allows program developers to obtain program options, that is (name, value) pairs from the user, via conventional methods such as command line and config file, from Vladimir Prus
- [Serialization](https://www.boost.org/doc/libs/1_81_0/libs/serialization/index.html) - Serialization for persistence and marshalling, from Robert Ramey
- [URL](https://www.boost.org/doc/libs/1_81_0/libs/url/index.html) - URL parsing in C++11, from Vinnie Falco and Alan de Freitas

## Inter-language support

- [Python](https://www.boost.org/doc/libs/1_81_0/libs/python/index.html) - The Boost Python Library is a framework for interfacing Python and C++. It allows you to quickly and seamlessly expose C++ classes functions and objects to Python, and vice-versa, using no special tools -- just your C++ compiler, from Dave Abrahams

## Iterators

- [GIL](https://www.boost.org/doc/libs/1_81_0/libs/gil/index.html) - (C++14) Generic Image Library, from Lubomir Bourdev, Hailin Jin and Christian Henning
- [Graph](https://www.boost.org/doc/libs/1_81_0/libs/graph/index.html) - The BGL graph interface and graph components are generic, in the same sense as the Standard Template Library (STL), from Jeremy Siek and a University of Notre Dame team.
- [GraphParallel](https://www.boost.org/doc/libs/1_81_0/libs/graph_parallel/index.html) - The PBGL graph interface and graph components are generic, in the same sense as the Standard Template Library (STL), from Jeremy Siek, Doug Gregor, and a University of Notre Dame team.
- [Iterator](https://www.boost.org/doc/libs/1_81_0/libs/iterator/index.html) - The Boost Iterator Library contains two parts. The first is a system of concepts which extend the C++ standard iterator requirements. The second is a framework of components for building iterators based on these extended concepts and includes several useful iterator adaptors, from Dave Abrahams, Jeremy Siek and Thomas Witt
- [Operators](https://www.boost.org/doc/libs/1_81_0/libs/utility/operators.htm) - Templates ease arithmetic classes and iterators, from Dave Abrahams and Jeremy Siek
- [Tokenizer](https://www.boost.org/doc/libs/1_81_0/libs/tokenizer/index.html) - Break of a string or other character sequence into a series of tokens, from John Bandela

## Language Features Emulation

- [Describe](https://www.boost.org/doc/libs/1_81_0/libs/describe/index.html) - A C++14 reflection library, from Peter Dimov
- [Exception](https://www.boost.org/doc/libs/1_81_0/libs/exception/doc/boost-exception.html) - The Boost Exception library supports transporting of arbitrary data in exception objects, and transporting of exceptions between threads, from Emil Dotchevski
- [Foreach](https://www.boost.org/doc/libs/1_81_0/libs/foreach/index.html) - In C++, writing a loop that iterates over a sequence is tedious. We can either use iterators, which requires a considerable amount of boiler-plate, or we can use the std::for_each() algorithm and move our loop body into a predicate, which requires no less boiler-plate and forces us to move our logic far from where it will be used. In contrast, some other languages, like Perl, provide a dedicated "foreach" construct that automates this process. BOOST_FOREACH is just such a construct for C++. It iterates over sequences for us, freeing us from having to deal directly with iterators or write predicates, from Eric Niebler
- [Move](https://www.boost.org/doc/libs/1_81_0/libs/move/index.html) - Portable move semantics for C++03 and C++11 compilers, from Ion Gaztañaga
- [Outcome](https://www.boost.org/doc/libs/1_81_0/libs/outcome/index.html) - A deterministic failure handling library partially simulating lightweight exceptions, from Niall Douglas
- [Parameter](https://www.boost.org/doc/libs/1_81_0/libs/parameter/index.html) - Boost.Parameter Library - Write functions that accept arguments by name, from David Abrahams and Daniel Wallin
- [Parameter Python Bindings](https://www.boost.org/doc/libs/1_81_0/libs/parameter_python/index.html) - Boost.Parameter Library Python bindings, from David Abrahams and Daniel Wallin
- [Scope Exit](https://www.boost.org/doc/libs/1_81_0/libs/scope_exit/index.html) - Execute arbitrary code at scope exit, from Alexander Nasonov
- [ThrowException](https://www.boost.org/doc/libs/1_81_0/libs/throw_exception/index.html) - A common infrastructure for throwing exceptions from Boost libraries, from Emil Dotchevski and Peter Dimov
- [Type Index](https://www.boost.org/doc/libs/1_81_0/libs/type_index/index.html) - Runtime/Compile time copyable type info, from Antony Polukhin
- [Typeof](https://www.boost.org/doc/libs/1_81_0/libs/typeof/index.html) - Typeof operator emulation, from Arkadiy Vertleyb and Peder Holt

## Math and numerics

- [Accumulators](https://www.boost.org/doc/libs/1_81_0/libs/accumulators/index.html) - Framework for incremental calculation, and collection of statistical accumulators, from Eric Niebler
- [Endian](https://www.boost.org/doc/libs/1_81_0/libs/endian/index.html) - Types and conversion functions for correct byte ordering and more regardless of processor endianness, from Beman Dawes
- [Geometry](https://www.boost.org/doc/libs/1_81_0/libs/geometry/index.html) - The Boost.Geometry library provides geometric algorithms, primitives and spatial index, from Barend Gehrels, Bruno Lalande, Mateusz Loskot, Adam Wulkiewicz, Menelaos Karavelas and Vissarion Fisikopoulos
- [Histogram](https://www.boost.org/doc/libs/1_81_0/libs/histogram/index.html) - Fast multi-dimensional histogram with convenient interface for C++14, from Hans Dembinski
- [Integer](https://www.boost.org/doc/libs/1_81_0/libs/integer/index.html) - The organization of boost integer headers and classes is designed to take advantage of <stdint.h> types from the 1999 C standard without resorting to undefined behavior in terms of the 1998 C++ standard. The header <boost/cstdint.hpp> makes the standard integer types safely available in namespace boost without placing any names in namespace std
- [Interval](https://www.boost.org/doc/libs/1_81_0/libs/numeric/interval/doc/interval.htm) - Extends the usual arithmetic functions to mathematical intervals, from Guillaume Melquiond, Hervé Brönnimann and Sylvain Pion
- [Math](https://www.boost.org/doc/libs/1_81_0/libs/math/index.html) - Boost.Math includes several contributions in the domain of mathematics: The Greatest Common Divisor and Least Common Multiple library provides run-time and compile-time evaluation of the greatest common divisor (GCD) or least common multiple (LCM) of two integers. The Special Functions library currently provides eight templated special functions, in namespace boost. The Complex Number Inverse Trigonometric Functions are the inverses of trigonometric functions currently present in the C++ standard. Quaternions are a relative of complex numbers often used to parameterise rotations in three dimentional space. Octonions, like quaternions, are a relative of complex numbers, from various
- [Math Common Factor](https://www.boost.org/doc/libs/1_81_0/libs/math/doc/html/gcd_lcm.html) - Greatest common divisor and least common multiple, from Daryle Walker
- [Math Octonion](https://www.boost.org/doc/libs/1_81_0/libs/math/doc/html/octonions.html) - Octonions, from Hubert Holin
- [Math Quaternion](https://www.boost.org/doc/libs/1_81_0/libs/math/doc/html/quaternions.html) - Quaternions, from Hubert Holin
- [Math/Special Functions](https://www.boost.org/doc/libs/1_81_0/libs/math/doc/html/special.html) - A wide selection of mathematical special functions, from John Maddock, Paul Bristow, Hubert Holin and Xiaogang Zhang
- [Math/Statistical Distributions](https://www.boost.org/doc/libs/1_81_0/libs/math/doc/html/dist.html) - A wide selection of univariate statistical distributions and functions that operate on them, from John Maddock and Paul Bristow
- [Multi-Array](https://www.boost.org/doc/libs/1_81_0/libs/multi_array/index.html) - Boost.MultiArray provides a generic N-dimensional array concept definition and common implementations of that interface, from Ron Garcia
- [Multiprecision](https://www.boost.org/doc/libs/1_81_0/libs/multiprecision/index.html) - Extended precision arithmetic types for floating point, integer andrational arithmetic, from John Maddock and Christopher Kormanyos
- [Numeric Conversion](https://www.boost.org/doc/libs/1_81_0/libs/numeric/conversion/index.html) - Optimized Policy-based Numeric Conversions, from Fernando Cacciola
- [Odeint](https://www.boost.org/doc/libs/1_81_0/libs/numeric/odeint/index.html) - Solving ordinary differential equations, from Karsten Ahnert and Mario Mulansky
- [Operators](https://www.boost.org/doc/libs/1_81_0/libs/utility/operators.htm) - Templates ease arithmetic classes and iterators, from Dave Abrahams and Jeremy Siek
- [Polygon](https://www.boost.org/doc/libs/1_81_0/libs/polygon/index.html) - Voronoi diagram construction and booleans/clipping, resizing/offsetting and more for planar polygons with integral coordinates, from Lucanus Simonson and Andrii Sydorchuk
- [QVM](https://www.boost.org/doc/libs/1_81_0/libs/qvm/index.html) - Generic C++ library for working with Quaternions Vectors and Matrices, from Emil Dotchevski
- [Random](https://www.boost.org/doc/libs/1_81_0/libs/random/index.html) - A complete system for random number generation, from Jens Maurer
- [Ratio](https://www.boost.org/doc/libs/1_81_0/libs/ratio/index.html) - Compile time rational arithmetic. C++11, from Howard Hinnant, Beman Dawes and Vicente J. Botet Escriba
- [Rational](https://www.boost.org/doc/libs/1_81_0/libs/rational/index.html) - A rational number class, from Paul Moore
- [Safe Numerics](https://www.boost.org/doc/libs/1_81_0/libs/safe_numerics/index.html) - Guaranteed Correct Integer Arithmetic, from Robert Ramey
- [uBLAS](https://www.boost.org/doc/libs/1_81_0/libs/numeric/ublas/index.html) - uBLAS provides tensor, matrix, and vector classes as well as basic linear algebra routines. Several dense, packed and sparse storage schemes are supported, from Joerg Walter and Mathias Koch

## Memory

- [Align](https://www.boost.org/doc/libs/1_81_0/libs/align/index.html) - Memory alignment functions, allocators, traits, from Glen Fernandes
- [Pool](https://www.boost.org/doc/libs/1_81_0/libs/pool/index.html) - Memory pool management, from Steve Cleary
- [Smart Ptr](https://www.boost.org/doc/libs/1_81_0/libs/smart_ptr/index.html) - Smart pointer class templates, from Greg Colvin, Beman Dawes, Peter Dimov, Darin Adler and Glen Fernandes
- [Utility](https://www.boost.org/doc/libs/1_81_0/libs/utility/utility.htm) - Class noncopyable plus checked_delete(), checked_array_delete(), next(), prior() function templates, plus base-from-member idiom, from Dave Abrahams and others

## Parsing

- [Spirit](https://www.boost.org/doc/libs/1_81_0/libs/spirit/index.html) - LL parser framework represents parsers directly as EBNF grammars in inlined C++, from Joel de Guzman, Hartmut Kaiser and Dan Nuffer
- [Spirit Classic](https://www.boost.org/doc/libs/1_81_0/libs/spirit/classic/index.html) - LL parser framework represents parsers directly as EBNF grammars in inlined C++, from Joel de Guzman, Hartmut Kaiser and Dan Nuffer
- [Spirit Repository](https://www.boost.org/doc/libs/1_81_0/libs/spirit/repository/index.html) - The Spirit repository is a community effort collecting different reusable components (primitives, directives, grammars, etc.) for Qi parsers and Karma generators, from Joel de Guzman, Hartmut Kaiser and Dan Nuffer

## Patterns and Idioms

- [Compressed Pair](https://www.boost.org/doc/libs/1_81_0/libs/utility/compressed_pair.htm) - Empty member optimization, from John Maddock, Howard Hinnant, et al
- [Flyweight](https://www.boost.org/doc/libs/1_81_0/libs/flyweight/index.html) - Design pattern to manage large quantities of highly redundant objects, from Joaquín M López Muñoz
- [Outcome](https://www.boost.org/doc/libs/1_81_0/libs/outcome/index.html) - A deterministic failure handling library partially simulating lightweight exceptions, from Niall Douglas
- [Signals2](https://www.boost.org/doc/libs/1_81_0/libs/signals2/index.html) - Managed signals & slots callback implementation (thread-safe version 2), from Frank Mori Hess
- [Utility](https://www.boost.org/doc/libs/1_81_0/libs/utility/utility.htm) - Class noncopyable plus checked_delete(), checked_array_delete(), next(), prior() function templates, plus base-from-member idiom, from Dave Abrahams and others

## Preprocessor Metaprogramming

- [Identity Type](https://www.boost.org/doc/libs/1_81_0/libs/utility/identity_type/index.html) - Wrap types within round parenthesis so they can always be passed as macro parameters, from Lorenzo Caminiti
- [Preprocessor](https://www.boost.org/doc/libs/1_81_0/libs/preprocessor/index.html) - Preprocessor metaprogramming tools including repetition and recursion, from Vesa Karvonen and Paul Mensonides
- [VMD](https://www.boost.org/doc/libs/1_81_0/libs/vmd/index.html) - Variadic Macro Data library, from Edward Diener

## Programming Interfaces

- [Function](https://www.boost.org/doc/libs/1_81_0/libs/function/index.html) - Function object wrappers for deferred calls or callbacks, from Doug Gregor
- [Outcome](https://www.boost.org/doc/libs/1_81_0/libs/outcome/index.html) - A deterministic failure handling library partially simulating lightweight exceptions, from Niall Douglas
- [Parameter](https://www.boost.org/doc/libs/1_81_0/libs/parameter/index.html) - Boost.Parameter Library - Write functions that accept arguments by name, from David Abrahams and Daniel Wallin
- [Parameter Python Bindings](https://www.boost.org/doc/libs/1_81_0/libs/parameter_python/index.html) - Boost.Parameter Library Python bindings, from David Abrahams and Daniel Wallin
- [System](https://www.boost.org/doc/libs/1_81_0/libs/system/index.html) - Extensible error reporting, from Beman Dawes

## State Machines

- [Meta State Machine](https://www.boost.org/doc/libs/1_81_0/libs/msm/index.html) - A very high-performance library for expressive UML2 finite state machines, from Christophe Henry
- [Statechart](https://www.boost.org/doc/libs/1_81_0/libs/statechart/index.html) - Boost.Statechart - Arbitrarily complex finite state machines can be implemented in easily readable and maintainable C++ code, from Andreas Huber Dönni

## String and text processing

- [Convert](https://www.boost.org/doc/libs/1_81_0/libs/convert/index.html) - An extendible and configurable type-conversion framework, from Vladimir Batov
- [Format](https://www.boost.org/doc/libs/1_81_0/libs/format/index.html) - The format library provides a type-safe mechanism for formatting arguments according to a printf-like format-string, from Samuel Krempp
- [Iostreams](https://www.boost.org/doc/libs/1_81_0/libs/iostreams/index.html) - Boost.IOStreams provides a framework for defining streams, stream buffers and i/o filters, from Jonathan Turkanis
- [Lexical Cast](https://www.boost.org/doc/libs/1_81_0/libs/lexical_cast/index.html) - General literal text conversions, such as an int represented a string, or vice-versa, from Kevlin Henney
- [Locale](https://www.boost.org/doc/libs/1_81_0/libs/locale/index.html) - Provide localization and Unicode handling tools for C++, from Artyom Beilis
- [Regex](https://www.boost.org/doc/libs/1_81_0/libs/regex/index.html) - Regular expression library, from John Maddock
- [Spirit](https://www.boost.org/doc/libs/1_81_0/libs/spirit/index.html) - LL parser framework represents parsers directly as EBNF grammars in inlined C++, from Joel de Guzman, Hartmut Kaiser and Dan Nuffer
- [Spirit Classic](https://www.boost.org/doc/libs/1_81_0/libs/spirit/classic/index.html) - LL parser framework represents parsers directly as EBNF grammars in inlined C++, from Joel de Guzman, Hartmut Kaiser and Dan Nuffer
- [Spirit Repository](https://www.boost.org/doc/libs/1_81_0/libs/spirit/repository/index.html) - The Spirit repository is a community effort collecting different reusable components (primitives, directives, grammars, etc.) for Qi parsers and Karma generators, from Joel de Guzman, Hartmut Kaiser and Dan Nuffer
- [Static String](https://www.boost.org/doc/libs/1_81_0/libs/static_string/index.html) - A fixed capacity dynamically sized string, from Krystian Stasiowski and Vinnie Falco
- [String Algo](https://www.boost.org/doc/libs/1_81_0/libs/algorithm/string/index.html) - String algorithms library, from Pavol Droba
- [Tokenizer](https://www.boost.org/doc/libs/1_81_0/libs/tokenizer/index.html) - Break of a string or other character sequence into a series of tokens, from John Bandela
- [Wave](https://www.boost.org/doc/libs/1_81_0/libs/wave/index.html) - The Boost.Wave library is a Standards conformant, and highly configurable implementation of the mandated C99/C++ preprocessor functionality packed behind an easy to use iterator interface, from Hartmut Kaiser
- [Xpressive](https://www.boost.org/doc/libs/1_81_0/libs/xpressive/index.html) - Regular expressions that can be written as strings or as expression templates, and which can refer to each other and themselves recursively with the power of context-free grammars, from Eric Niebler
- 

## System

- [Chrono](https://www.boost.org/doc/libs/1_81_0/libs/chrono/index.html) - Useful time utilities. C++11, from Howard Hinnant, Beman Dawes and Vicente J. Botet Escriba
- [Context](https://www.boost.org/doc/libs/1_81_0/libs/context/index.html) - (C++11) Context switching library, from Oliver Kowalke
- [Date Time](https://www.boost.org/doc/libs/1_81_0/libs/date_time/index.html) - A set of date-time libraries based on generic programming concepts, from Jeff Garland
- [DLL](https://www.boost.org/doc/libs/1_81_0/libs/dll/index.html) - Library for comfortable work with DLL and DSO, from Antony Polukhin and Renato Tegon Forti
- [Fiber](https://www.boost.org/doc/libs/1_81_0/libs/fiber/index.html) - (C++11) Userland threads library, from Oliver Kowalke
- [Filesystem](https://www.boost.org/doc/libs/1_81_0/libs/filesystem/index.html) - The Boost Filesystem Library provides portable facilities to query and manipulate paths, files, and directories, from Beman Dawes
- [Nowide](https://www.boost.org/doc/libs/1_81_0/libs/nowide/index.html) - Standard library functions with UTF-8 API on Windows, from Artyom Beilis
- [Process](https://www.boost.org/doc/libs/1_81_0/libs/process/index.html) - Library to create processes in a portable way, from Merino Vidal, Ilya Sokolov, Felipe Tanus, Jeff Flinn, Thomas Jarosch, Boris Schaeling and Klemens D. Morgenstern
- [Stacktrace](https://www.boost.org/doc/libs/1_81_0/libs/stacktrace/index.html) - Gather, store, copy and print backtraces, from Antony Polukhin
- [System](https://www.boost.org/doc/libs/1_81_0/libs/system/index.html) - Extensible error reporting, from Beman Dawes
- [Thread](https://www.boost.org/doc/libs/1_81_0/libs/thread/index.html) - Portable C++ multi-threading. C++03, C++11, C++14, C++17, from Anthony Williams and Vicente J. Botet Escriba


## Template Metaprogramming

- [CallableTraits](https://www.boost.org/doc/libs/1_81_0/libs/callable_traits/index.html) - A spiritual successor to Boost.FunctionTypes, Boost.CallableTraits is a header-only C++11 library for the compile-time inspection and manipulation of all 'callable' types. Additional support for C++17 features, from Barrett Adair
- [Describe](https://www.boost.org/doc/libs/1_81_0/libs/describe/index.html) - A C++14 reflection library, from Peter Dimov
- [Function Types](https://www.boost.org/doc/libs/1_81_0/libs/function_types/index.html) - Boost.FunctionTypes provides functionality to classify, decompose and synthesize function, function pointer, function reference and pointer to member types, from Tobias Schwinger
- [Fusion](https://www.boost.org/doc/libs/1_81_0/libs/fusion/doc/html/index.html) - Library for working with tuples, including various containers, algorithms, etc, from Joel de Guzman, Dan Marsden and Tobias Schwinger
- [Hana](https://www.boost.org/doc/libs/1_81_0/libs/hana/index.html) - A modern C++ metaprogramming library. It provides high level algorithms to manipulate heterogeneous sequences, allows writing type-level computations with a natural syntax, provides tools to introspect user-defined types and much more, from Louis Dionne
- [HOF](https://www.boost.org/doc/libs/1_81_0/libs/hof/index.html) - Higher-order functions for C++, from Paul Fultz II
- [Metaparse](https://www.boost.org/doc/libs/1_81_0/libs/metaparse/index.html) - A library for generating compile time parsers parsing embedded DSL code as part of the C++ compilation process, from Abel Sinkovics
- [Mp11](https://www.boost.org/doc/libs/1_81_0/libs/mp11/index.html) - A C++11 metaprogramming library, from Peter Dimov
- [MPL](https://www.boost.org/doc/libs/1_81_0/libs/mpl/index.html) - The Boost.MPL library is a general-purpose, high-level C++ template metaprogramming framework of compile-time algorithms, sequences and metafunctions. It provides a conceptual foundation and an extensive set of powerful and coherent tools that make doing explict metaprogramming in C++ as easy and enjoyable as possible within the current language, from Aleksey Gurtovoy
- [PFR](https://www.boost.org/doc/libs/1_81_0/libs/pfr/index.html) - Basic reflection for user defined types, from Antony Polukhin
- [Proto](https://www.boost.org/doc/libs/1_81_0/libs/proto/index.html) - Expression template library and compiler construction toolkit for domain-specific embedded languages, from Eric Niebler
- [Static Assert](https://www.boost.org/doc/libs/1_81_0/libs/static_assert/index.html) - Static assertions (compile time assertions), from John Maddock
- [TTI](https://www.boost.org/doc/libs/1_81_0/libs/tti/index.html) - [Type Traits](https://www.boost.org/doc/libs/1_81_0/libs/type_traits/index.html) Introspection library, from Edward Diener
- Type Traits - Templates for fundamental properties of types, from John Maddock, Steve Cleary, et al
- [YAP](https://www.boost.org/doc/libs/1_81_0/libs/yap/index.html) - An expression template library for C++14 and later, from T. Zachary Laine

## Miscellaneous

- [Conversion](https://www.boost.org/doc/libs/1_81_0/libs/conversion/index.html) - Polymorphic casts, from Dave Abrahams and Kevlin Henney
- [Convert](https://www.boost.org/doc/libs/1_81_0/libs/convert/index.html) - An extendible and configurable type-conversion framework, from Vladimir Batov
- [Core](https://www.boost.org/doc/libs/1_81_0/libs/core/index.html) - A collection of simple core utilities with minimal dependencies, from Peter Dimov, Glen Fernandes and Andrey Semashev
- [Endian](https://www.boost.org/doc/libs/1_81_0/libs/endian/index.html) - Types and conversion functions for correct byte ordering and more regardless of processor endianness, from Beman Dawes
- [Lexical Cast](https://www.boost.org/doc/libs/1_81_0/libs/lexical_cast/index.html) - General literal text conversions, such as an int represented a string, or vice-versa, from Kevlin Henney
- [Log](https://www.boost.org/doc/libs/1_81_0/libs/log/index.html) - Logging library, from Andrey Semashev
- [Numeric Conversion](https://www.boost.org/doc/libs/1_81_0/libs/numeric/conversion/index.html) - Optimized Policy-based Numeric Conversions, from Fernando Cacciola
- [Predef](https://www.boost.org/doc/libs/1_81_0/libs/predef/index.html) - This library defines a set of compiler, architecture, operating system, library, and other version numbers from the information it can gather of C, C++, Objective C, and Objective C++ predefined macros or those defined in generally available headers, from René Ferdinand Rivera Morell
- [Program Options](https://www.boost.org/doc/libs/1_81_0/libs/program_options/index.html) - The program_options library allows program developers to obtain program options, that is (name, value) pairs from the user, via conventional methods such as command line and config file, from Vladimir Prus
- [Swap](https://www.boost.org/doc/libs/1_81_0/libs/core/swap.html) - Enhanced generic swap function, from Joseph Gauterin
- [Timer](https://www.boost.org/doc/libs/1_81_0/libs/timer/index.html) - Event timer, progress timer, and progress display classes, from Beman Dawes
- [Tribool](https://www.boost.org/doc/libs/1_81_0/doc/html/tribool.html) - 3-state boolean type library, from Doug Gregor
- [Utility](https://www.boost.org/doc/libs/1_81_0/libs/utility/utility.htm) - Class noncopyable plus checked_delete(), checked_array_delete(), next(), prior() function templates, plus base-from-member idiom, from Dave Abrahams and others
- [Value Initialized](https://www.boost.org/doc/libs/1_81_0/libs/utility/value_init.htm) - Wrapper for uniform-syntax value initialization, based on the original idea of David Abrahams, from Fernando Cacciola
