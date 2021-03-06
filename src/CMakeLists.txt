add_library(greylock SHARED exception.cpp)
set_target_properties(greylock PROPERTIES
	VERSION ${GREYLOCK_MAJOR_VERSION}
	SOVERSION ${GREYLOCK_FULL_VERSION}
	LINKER_LANGUAGE CXX
)
target_link_libraries(greylock
	${Boost_LIBRARIES}
	${JEMALLOC_LIBRARIES}
	${MSGPACK_LIBRARIES}
	${RIBOSOME_LIBRARIES}
	${ROCKSDB_LIBRARIES}
	${SWARM_LIBRARIES}
	${THEVOID_LIBRARIES}
	pthread
)
add_executable(greylock_server server.cpp)
target_link_libraries(greylock_server
	greylock
)

add_executable(greylock_list list.cpp)
target_link_libraries(greylock_list
	greylock
)
add_executable(greylock_meta meta.cpp)
target_link_libraries(greylock_meta
	greylock
)
add_executable(greylock_check check.cpp)
target_link_libraries(greylock_check
	greylock
)
add_executable(greylock_compact compact.cpp)
target_link_libraries(greylock_compact
	greylock
)

add_executable(greylock_merge merge.cpp)
target_link_libraries(greylock_merge
	greylock
)

install(TARGETS	greylock
	LIBRARY DESTINATION lib${LIB_SUFFIX}
	ARCHIVE DESTINATION lib${LIB_SUFFIX}
	BUNDLE DESTINATION library
)
install(TARGETS	greylock_server greylock_meta greylock_check greylock_compact greylock_merge
	RUNTIME DESTINATION bin COMPONENT runtime
)

