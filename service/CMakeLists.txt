find_package(Boost)

ADD_DEFINITIONS(
	-std=c++11 # Or -std=c++0x
	# Other flags
	)

include_directories(${Boost_INCLUDE_DIRS} ../handlers)

add_executable(
	my_service
	main.cpp
	mime_types.cpp
	reply.cpp
	request_handler.cpp
	request_parser.cpp
	)
