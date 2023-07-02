-----

| Title     | Programing CPP STD MSVC                              |
| --------- | ---------------------------------------------------- |
| Created @ | `2023-06-04T04:23:46Z`                               |
| Updated @ | `2023-06-04T04:23:46Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/250) |

-----

# MSVC STL

| C++ standard library | Characteristics                                                      | Option | Preprocessor directives |
| -------------------- | -------------------------------------------------------------------- | ------ | ----------------------- |
| libcpmt.lib          | Multithreaded, static link                                           | /MT    | \_MT                    |
| msvcprt.lib          | Multithreaded, dynamic link (import library for msvcp<version>.dll)  | /MD    | \_MT, \_DLL             |
| libcpmtd.lib         | Multithreaded, static link                                           | /MTd   | \_DEBUG, \_MT           |
| msvcprtd.lib         | Multithreaded, dynamic link (import library for msvcp<version>d.dll) | /MDd   | \_DEBUG, \_MT, \_DLL    |

## Reference

  - [C runtime (CRT) and C++ standard library (STL) .lib
    files](https://learn.microsoft.com/en-us/cpp/c-runtime-library/crt-library-features)
