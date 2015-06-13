foreach( lang ${CALAMARES_NETRUNNER_BRANDING_TRANSLATION_LANGUAGES} )
   list( APPEND TS_FILES "${CMAKE_CURRENT_SOURCE_DIR}/calamares-${COMPONENT_NAME}_${lang}.ts" )
endforeach()
qt5_add_translation( QM_FILES ${TS_FILES} )

add_custom_target( translations ALL DEPENDS ${QM_FILES} )
install( FILES ${QM_FILES} DESTINATION "${BRANDING_COMPONENT_DESTINATION}/lang" )