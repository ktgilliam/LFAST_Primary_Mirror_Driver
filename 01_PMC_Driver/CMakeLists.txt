########## LFAST Mount Driver ##############
# do the replacement in the config.h and lfast_mount_driver.xml
configure_file(
	${CMAKE_CURRENT_SOURCE_DIR}/config.h.cmake
	${CMAKE_CURRENT_BINARY_DIR}/config.h
)

configure_file(
	${CMAKE_CURRENT_SOURCE_DIR}/lfast_pmc_driver.xml.cmake  
	${CMAKE_CURRENT_BINARY_DIR}/lfast_pmc_driver.xml)

# set our include directories to look for header files
include_directories( ${CMAKE_BINARY_DIR})
include_directories( ${CMAKE_CURRENT_BINARY_DIR})
include_directories( ${CMAKE_CURRENT_SOURCE_DIR})

add_executable(lfast_pmc_driver lfast_pmc_driver.cc)
# add_executable(lfast_mount_driver_testable lfast_mount_driver.cc)

target_link_libraries(lfast_pmc_driver   
			 ${INDI_LIBRARIES}
			 )

# tell cmake where to install our executable
install(TARGETS lfast_pmc_driver RUNTIME DESTINATION bin)

# and where to put the driver's xml file.
install(
    FILES
    ${CMAKE_CURRENT_BINARY_DIR}/lfast_pmc_driver.xml
    DESTINATION ${INDI_DATA_DIR}
)