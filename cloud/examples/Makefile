include ../../make_config.mk

ifndef DISABLE_JEMALLOC
	ifdef JEMALLOC
		PLATFORM_CXXFLAGS += "-DROCKSDB_JEMALLOC"
	endif
	EXEC_LDFLAGS := $(JEMALLOC_LIB) $(EXEC_LDFLAGS) -lpthread
	PLATFORM_CXXFLAGS += $(JEMALLOC_INCLUDE)
endif

.PHONY: clean librocksdb-cloud

all: cloud_durable_example clone_example cloud_dump

cloud_durable_example: librocksdb-cloud cloud_durable_example.cc
	$(CXX) $(CXXFLAGS) $@.cc -o $@ ../../librocksdb-cloud.a -I../../include $(OPT) -std=c++11 $(PLATFORM_LDFLAGS) $(PLATFORM_CXXFLAGS) $(EXEC_LDFLAGS)

clone_example: librocksdb-cloud clone_example.cc
	$(CXX) $(CXXFLAGS) $@.cc -o $@ ../../librocksdb-cloud.a -I../../include $(OPT) -std=c++11 $(PLATFORM_LDFLAGS) $(PLATFORM_CXXFLAGS) $(EXEC_LDFLAGS)

cloud_dump: librocksdb-cloud cloud_dump.cc
	$(CXX) $(CXXFLAGS) $@.cc -o $@ ../../librocksdb-cloud.a -I../../include $(OPT) -std=c++11 $(PLATFORM_LDFLAGS) $(PLATFORM_CXXFLAGS) $(EXEC_LDFLAGS)

clean:
	rm -rf ./cloud_durable_example  ./clone_example ./cloud_dump

librocksdb-cloud:
	cd ../.. && $(MAKE) static_lib
