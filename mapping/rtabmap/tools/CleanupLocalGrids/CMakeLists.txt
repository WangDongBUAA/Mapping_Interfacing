
SET(RTABMap_INCLUDE_DIRS 
    ${PROJECT_SOURCE_DIR}/utilite/include
	${PROJECT_SOURCE_DIR}/corelib/include
)
SET(RTABMap_LIBRARIES 
    rtabmap_core
	rtabmap_utilite
)  

SET(INCLUDE_DIRS
	${RTABMap_INCLUDE_DIRS}
    ${OpenCV_INCLUDE_DIRS}
    ${PCL_INCLUDE_DIRS}
)

SET(LIBRARIES
	${RTABMap_LIBRARIES}
	${OpenCV_LIBRARIES}
	${PCL_LIBRARIES}
)

INCLUDE_DIRECTORIES(${INCLUDE_DIRS})

ADD_EXECUTABLE(cleanupLocalGrids main.cpp)
  
TARGET_LINK_LIBRARIES(cleanupLocalGrids ${LIBRARIES})

SET_TARGET_PROPERTIES( cleanupLocalGrids 
  PROPERTIES OUTPUT_NAME ${PROJECT_PREFIX}-cleanupLocalGrids)

INSTALL(TARGETS cleanupLocalGrids
		RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}" COMPONENT runtime
		BUNDLE DESTINATION "${CMAKE_BUNDLE_LOCATION}" COMPONENT runtime)


