file(GLOB_RECURSE
    threads_src 
        ${CMAKE_SOURCE_DIR}/src/threads/*.cpp
)

add_library(threads
    STATIC
        ${threads_src}
)

target_link_libraries(threads
    PUBLIC
        ${OpenCV_LIBS}
        ${DPRM_LIBS}
        data_manager
)
