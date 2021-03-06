# assuming DNSSD_FOUND

add_executable(asebatargetadvertise
	targetadvertise.cpp
)
target_link_libraries(asebatargetadvertise ${ASEBA_ZEROCONF_LIBRARIES} ${ASEBA_CORE_LIBRARIES})

# Using DashelhubZeroconf

add_executable(asebatargetlist-dashelhub
	targetlist-dashelhub.cpp
)
target_link_libraries(asebatargetlist-dashelhub ${ASEBA_ZEROCONF_LIBRARIES} ${ASEBA_CORE_LIBRARIES})

# Using ThreadZeroconf

add_executable(asebatargetlist-thread
	targetlist-thread.cpp
)
target_link_libraries(asebatargetlist-thread ${ASEBA_ZEROCONF_LIBRARIES} ${ASEBA_CORE_LIBRARIES})

# Using QtZeroconf

if (QT4_FOUND)
	set(QT_USE_QTNETWORK ON)
	set(QT_DONT_USE_QTGUI ON)
	qt4_wrap_cpp(examples_targetlist_qt_MOCS
		targetlist-qt.h
	)
	include(${QT_USE_FILE})

	include_directories (${CMAKE_BINARY_DIR} ${CMAKE_CURRENT_BINARY_DIR})

	add_executable(asebatargetlist-qt
		${examples_targetlist_qt_MOCS}
		targetlist-qt.cpp
	)
	target_link_libraries(asebatargetlist-qt ${ASEBA_ZEROCONFQT_LIBRARIES} ${ASEBA_CORE_LIBRARIES} ${QT_LIBRARIES})
endif (QT4_FOUND)
