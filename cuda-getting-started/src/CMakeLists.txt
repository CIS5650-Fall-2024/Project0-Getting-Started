set(SOURCE_FILES
    "glslUtility.hpp"
    "glslUtility.cpp"
    "kernel.h"
    "kernel.cu"
    )

add_library(src
    ${SOURCE_FILES}
    )
