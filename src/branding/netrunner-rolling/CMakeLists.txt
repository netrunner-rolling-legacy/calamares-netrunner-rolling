set( COMPONENT_NAME "netrunner-debian" )

set( BRANDING_DIR ${CMAKE_INSTALL_SYSCONFDIR}/calamares/branding )
set( BRANDING_COMPONENT_DESTINATION ${BRANDING_DIR}/${COMPONENT_NAME} )

if( IS_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/lang" )
    add_subdirectory( lang )
endif()

# We glob all the files inside the subdirectory, and we make sure they are
# synced with the bindir structure and installed.
file( GLOB BRANDING_COMPONENT_FILES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "*" )
foreach( BRANDING_COMPONENT_FILE ${BRANDING_COMPONENT_FILES} )
    if( NOT IS_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/${BRANDING_COMPONENT_FILE} AND
        NOT ${BRANDING_COMPONENT_FILE} STREQUAL "CMakeLists.txt" )
        configure_file( ${BRANDING_COMPONENT_FILE} ${BRANDING_COMPONENT_FILE} COPYONLY )

        install( FILES ${CMAKE_CURRENT_BINARY_DIR}/${BRANDING_COMPONENT_FILE}
                 DESTINATION ${BRANDING_COMPONENT_DESTINATION} )
    endif()
endforeach()
