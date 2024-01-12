# assertC usage guide

## What is assertC
assertC is a test library for makro based testing.
i wanted an easy to use and easy to modify testing framework.
i did not need many features except asserts and little fancy logging, thats it.
that is what u get when using it.
plus a few utilities for comfy setup for multi-testfile usecases.

## how to use assertC in a single-testfile case
like this
```C
#include "../../lib/test/assert.h"
#include <string.h>
DESCRIBE("describe something", {
    WITH_FILE("mytest.txt",
       TEST("does stuff", {
           ASSERT_INT_EQUALS(1, 1);
           ASSERT_STR_EQUALS("c", "c");
           ASSERT_CHAR_EQUALS('c', 'c');
           ASSERT_EQUALS(1.1, 1.1);
           ASSERT_NOT_EQUALS(1,2);
       })
    )
    TEST("does something else", {
        ASSERT_EQUALS(1,1);
    })
})
```


## how to use assertC in a multi-testfile case

in 'testfile.c'
```C
#include "../../lib/test/assert.h"
#include <string.h>
MODULAR_DESCRIBE(valid_function_name, {
    WITH_FILE("mytest.txt",
       TEST("does stuff", {
           ASSERT_INT_EQUALS(1, 1);
           ASSERT_STR_EQUALS("c", "c");
           ASSERT_CHAR_EQUALS('c', 'c');
           ASSERT_EQUALS(1.1, 1.1);
           ASSERT_NOT_EQUALS(1,2);
       })
    )
    TEST("does something else", {
        ASSERT_EQUALS(1,1);
    })
})
```
in 'testfile.h'
```C
#include "../../lib/test/assert.h"
MODULAR_DESCRIBE_H(valid_function_name);
```

in 'main.c'
```C
#include "../lib/test/assert.h"
#include "testfile.h"
int main() {
    RUN_DESCRIBE_MODULE(valid_function_name);
}
```

