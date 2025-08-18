file(GLOB_RECURSE
    garage_src
        ${CMAKE_SOURCE_DIR}/src/garage/*.cpp      
)

add_library(garage
    STATIC
        ${garage_src}
)

target_link_libraries(garage
    PUBLIC
        ${DPRM_LIBS}
        data_manager
)