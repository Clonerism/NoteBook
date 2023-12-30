[COURSE] GNU Debugger Megaprimer
--------------------------------

- Find binary file info (if debug symbols exist)
```
info functions
info variables              # for global variables
info registers              # inspect CPU registers
info scope <scope_name>     # for local variables
info brakpoints             # review all breakpoints
```

- Ripping symbols off a binary file
```
objcopy --only-keep-debug <file_with_debug_symbols> <output_file>
```

- Stripping symbols off a binary file
```
strip --strip-debug --strip-unneeded <file_with_debug_symbols>
```

- Adding debug symbols to a binary itself
```
objcopy --add-gnu-debuglink=<debug_file> <binary_file>
```

- Load symbol file within GDB
```
symbol-file <symbole_file>
```

- List symbols from object file
```
man nm                  # see a full list of symbol types
nm <object_file>
nm -A <object_file> | grep <function_name>
nm -n <object_file>     # display in address sorted order
nm -g <object_file>     # list external symbols
nm -S <object_file>     # display size
```

- Important symbol types
```
| Symbol Type | Meaning                                 |
|-------------|-----------------------------------------|
| A           | Absolute Symbol                         |
| B           | In the Uninitialized Data Section (BSS) |
| D           | In the Initialized Data Section         |
| N           | Debugging Symbol                        |
| T           | In the Text Section                     |
| U           | Symbol Undefined right now              |
```

- `Strace` helps to understand how program interact with OS by tracing all System Calls made by the program. It also tells us about arguments passed and has great filtering capabilities.
```
| Flag            | Meaning                     |
|-----------------|-----------------------------|
| -o <file_name>  | Redirect outout to a file   |
| -t              | Add Absolute Timestamp      |
| -r              | Add Relative Timestamp      |
| -e <syscall>    | Trace by specific Syscall   |
| -p <process_id> | Attach to a running process |
| -c              | Print Statistics            |
```

- Breakpoints
```
break *<address>
break <function_name>
break <line_num>
enable <breakpoint_num>         # breakpoint_num can be found from info breakpoints command
disable <breakpoint_num>
delete <breakpoint_num>
```



- Memory examination
```
help x          # additional info
x/FMT address   # FMT is <repeat_count><format_letter><size_letter> 
```

- Disassemble a specific function
```
disassemble <func_name>
```

- General commands
```
continue
stepi  <>     # per instruction
step <N>       # per line
help <command>
set {<data_type>} <mem_addr> = <value>     # modify value in mem
```

- variables in GDB
```
set $i = 10
set argv[1] = $i                            # change argument value
set $dyn = (char *)malloc(10)               # assign a part of mem
x/10xb $dyn                                 # examine allocated mem
call strcpy($dyn, argv[0]);                 # use any functions which is linked to binary (find them by info functions)
```

- Use strings utility to display all strings which is inside binary
```
strings main
```

- Change disassebly format
```
set disassembly-flavor intel
```

- Conditional breakpoint
```
condition <bp_num> <condition>      # for e.g. condition 1 counter == 5
```

- ARM calling conventions
```
| Register | Functionality                      |
|----------|------------------------------------|
| r0 - r3  | function arguments & return values |
| r4 - r11 | local variables                    |
| r13      | stack pointer                      |
| r14      | link registe                       |
| r15      | program counter                    |
```
