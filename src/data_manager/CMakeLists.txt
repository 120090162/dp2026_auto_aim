file(GLOB_RECURSE
    data_src 
        ${CMAKE_SOURCE_DIR}/src/data_manager/*.cpp
)


add_library(data_manager
    STATIC
        ${data_src}    
)

target_link_libraries(data_manager
    PUBLIC
        ${OpenCV_LIBS}
        ${DPRM_LIBS}
)
