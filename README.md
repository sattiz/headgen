# `C headers` files generator

# Requiers
```
python >= 3.5
```

# Instalation
```bash
pip install headgen
pip3 install headgen
```
# Run
```bash
cd path/to/your/prject
python -m headgen.headgen <flags>
python3 -m headgen.headgen <flags>
```

# Flags

|Short flag|   Long flag   |          Description        | Default | 
|----------|---------------|-----------------------------|---------|
|`-p`      |`--pragma`     | Sets protection with pragma |  False  |
|`-if`     |`--ifndef`     | Sets protection with ifndef |  True   |
|`-enc`    |`--encoding`   | Sets encoding of the file   | `utf-8` |
|`-a`      |`--ask`        | Asking before doing         | False   |


# Functions

- For automatic adding of the signature of any function
type ` //>signature`.

```c
int sum_integers(int first, int second) //>signature
{
    return first + second;
}
```
 - After running to your header file this line will be added
```c
int sum_integers(int first, int second);
```

# Functions with documentation

 - Example for function with documentation
 - Add `//>documentation` before documentation
 - Does not work inside function!

```c
//>documentation
/*!
@brief add two numbers
@param[in] int first number
@param[in] int second number
@return int 
*/
int sum_integers(int first, int second) //>signature
{
    return first + second;
}
```

#### Added to header:
```c
/*!
@brief add two numbers
@param[in] int first number
@param[in] int second number
@return int 
*/
int sum_integers(int first, int second);
```

# Structures
#### Place the struct you want into:
```c
/* >structure

place typedef struct
or just a struct here

*/
```
#### Example:
```c
/* >structure
typedef struct 
{
    int a;
    int b;
} example
*/
```

#### Added to header:
```c
typedef struct 
{
    int a;
    int b;
} example
```


# Enums
#### Place the enum you want into:
```c
/* >enum

Place enum here

*/
```

#### Example
```c
/* >enum
enum codes
{
    no error,
    error,
};
*/
```
#### Added to header:
```c
enum codes
{
    no error,
    error,
};
```

# Defines
#### Example:
```c
/* >defines
#define 1 0 
#define and or
#define + -
#define * /
*/
```
#### Added to header:
```c
#define 1 0 
#define and or
#define + -
#define * /
```

# Includes 
You do not have to write
`#include` before lib name
#### Example:
```c
/* >includes
<math.h>
"your_lib.h"
<string.h>
<stdio.h>
*/
```
#### Added to header:
```c
#include <stdlib.h>
#include <stdio.h>
#include <math.h>
#include "your_lib.h"
```

# Information at top of the header
- Time of the generation
- Amount of the functions
- Amount of the documentated functions
- Check if they are all documentated
- Amount of the structures
- Amount of the enums
- Functions names (sorted by alphabet)


# Protection
## `Pragma`
If you want to set protection of your file with `#pragma onсe`
run program with flag `-p`
```bash
python -m headgen.headgen -p
python -m headgen.headgen --pragma True
```
#### Added to header:
```c
#pragma once
```

## `ifndef` (Defautlt protection)
If you want to set protection of your file with `ifndef`
run program with flag `-if`

```bash
python -m headgen.headgen -if True
python -m headgen.headgen --ifndef True
```
#### Added to header
```c
// Default file is list.h
#ifndef __LIST_H__
#define __LIST_H__

...

#endif // __LIST_H__
```


# Links
- [Github link](https://github.com/YoungMeatBoy/headgen.git)
- Email : `d2ms2nk@gmail.com`

## On any issue report in GitHub!



# Example

#### Base file
```c
/* >structure

typedef struct {
				int size;
				int capacity;
				double * data;
				} array_d;

*/

/* >includes

<stdio.h>
"my_lib.h"

*/

#include "array_d.h"


// >documentation
/*!
@brief Frees data in array
@param[in] d_array * array pointer to an array
@warning will free data inside!
*/
void array_free_d(array_d * array) // >signature
{
	free(array -> data);
	array -> data = NULL;
	array -> size = 0;
	array -> capacity = 0;
}
```

### Generated header
```c
/*
This header file was generated automaticaly!
Generated at: 26 October 2019 (26.10.2019) At: 17:24:00
Amount of functions        : 1
Amount of documentated     : 1
All functions documentated : True
Amount of structures       : 1
Amount of enums            : 0
Function's names: 
   1 > array_free_d
*/

#ifndef __ARRAY_D_H__
#define __ARRAY_D_H__

#include <stdio.h>
#include "my_lib.h"

typedef struct {
				int size;
				int capacity;
				double * data;
				} array_d;

/*!
@brief Frees data in array
@param[in] d_array * array pointer to an array
@warning will free data inside!
*/
void array_free_d(array_d * array);

```