NEED_GPERFTOOLS=1
NEED_GTEST=1
NEED_GMOCK=1
include ../config.mk
CPPFLAGS=-DBTHREAD_USE_FAST_PTHREAD_MUTEX -D__const__= -D_GNU_SOURCE -DUSE_SYMBOLIZE -DNO_TCMALLOC -D__STDC_FORMAT_MACROS -D__STDC_LIMIT_MACROS -D__STDC_CONSTANT_MACROS
CPPFLAGS+=-DUNIT_TEST -Dprivate=public -Dprotected=public -DBVAR_NOT_LINK_DEFAULT_VARIABLES
CXXFLAGS=$(CPPFLAGS) -g -pipe -Wall -W -fPIC -fstrict-aliasing -Wno-invalid-offsetof -Wno-unused-parameter -fno-omit-frame-pointer -std=c++0x
CFLAGS=$(CPPFLAGS) -g -pipe -Wall -W -fPIC -fstrict-aliasing -Wno-unused-parameter -fno-omit-frame-pointer

ifeq ($(shell test $(shell $(CXX) -dumpversion | sed -e 's/\..*$$//g') -ge 7; echo $$?),0)
CXXFLAGS+=-Wno-aligned-new
endif

HDRPATHS=-I. -I.. $(addprefix -I, $(HDRS))
LIBPATHS=$(addprefix -L, $(LIBS))

TEST_BASE_SOURCES = \
    at_exit_unittest.cc \
    atomicops_unittest.cc \
    barrier_closure_unittest.cc \
    base64_unittest.cc \
    big_endian_unittest.cc \
    bind_unittest.cc \
    bits_unittest.cc \
    callback_helpers_unittest.cc \
    callback_list_unittest.cc \
    callback_unittest.cc \
    cancelable_callback_unittest.cc \
    command_line_unittest.cc \
    hash_tables_unittest.cc \
    linked_list_unittest.cc \
    mru_cache_unittest.cc \
    small_map_unittest.cc \
    stack_container_unittest.cc \
    cpu_unittest.cc \
    crash_logging_unittest.cc \
    leak_tracker_unittest.cc \
    proc_maps_linux_unittest.cc \
    stack_trace_unittest.cc \
    environment_unittest.cc \
    file_util_unittest.cc \
    dir_reader_posix_unittest.cc \
    file_path_unittest.cc \
    file_unittest.cc \
    path_service_unittest.cc \
    scoped_temp_dir_unittest.cc \
    guid_unittest.cc \
    hash_unittest.cc \
    lazy_instance_unittest.cc \
    md5_unittest.cc \
    aligned_memory_unittest.cc \
    linked_ptr_unittest.cc \
    ref_counted_memory_unittest.cc \
    ref_counted_unittest.cc \
    scoped_ptr_unittest.cc \
    scoped_vector_unittest.cc \
    singleton_unittest.cc \
    weak_ptr_unittest.cc \
    observer_list_unittest.cc \
    file_descriptor_shuffle_unittest.cc \
    process_metrics_unittest.cc \
    process_util_unittest.cc \
    rand_util_unittest.cc \
    safe_numerics_unittest.cc \
    scoped_clear_errno_unittest.cc \
    scoped_generic_unittest.cc \
    security_unittest.cc \
    sha1_unittest.cc \
    stl_util_unittest.cc \
    nullable_string16_unittest.cc \
    safe_sprintf_unittest.cc \
    string16_unittest.cc \
    stringprintf_unittest.cc \
    string_number_conversions_unittest.cc \
    string_piece_unittest.cc \
    string_split_unittest.cc \
    string_tokenizer_unittest.cc \
    string_util_unittest.cc \
    stringize_macros_unittest.cc \
    sys_string_conversions_unittest.cc \
    utf_offset_string_conversions_unittest.cc \
    utf_string_conversions_unittest.cc \
    cancellation_flag_unittest.cc \
    condition_variable_unittest.cc \
    lock_unittest.cc \
    waitable_event_unittest.cc \
    sys_info_unittest.cc \
    type_traits_unittest.cc \
    non_thread_safe_unittest.cc \
    platform_thread_unittest.cc \
    simple_thread_unittest.cc \
    thread_checker_unittest.cc \
    thread_collision_warner_unittest.cc \
    thread_id_name_manager_unittest.cc \
    thread_local_storage_unittest.cc \
    thread_local_unittest.cc \
    watchdog_unittest.cc \
    pr_time_unittest.cc \
    time_unittest.cc \
    version_unittest.cc \
    logging_unittest.cc \
    tuple_unittest.cc \
    xdg_util_unittest.cc \
    cacheline_unittest.cpp \
    class_name_unittest.cpp \
    endpoint_unittest.cpp \
    unique_ptr_unittest.cpp \
    errno_unittest.cpp \
    fd_guard_unittest.cpp \
    file_watcher_unittest.cpp \
    find_cstr_unittest.cpp \
    scoped_lock_unittest.cpp \
    status_unittest.cpp \
    string_printf_unittest.cpp \
    string_splitter_unittest.cpp \
    synchronous_event_unittest.cpp \
    temp_file_unittest.cpp \
    baidu_thread_local_unittest.cpp \
    baidu_time_unittest.cpp \
    flat_map_unittest.cpp \
    crc32c_unittest.cc \
    multiprocess_func_list.cc \
    test_switches.cc \
    test_timeouts.cc \
    scoped_locale.cc \
    multiprocess_test.cc \
    test_file_util.cc \
    test_file_util_linux.cc \
    base_unittest_main.cpp

TEST_BASE_OBJS = $(addsuffix .o, $(basename $(TEST_BASE_SOURCES))) 

TEST_BVAR_SOURCES = $(wildcard bvar_*_unittest.cpp)
TEST_BVAR_OBJS = $(addsuffix .o, $(basename $(TEST_BVAR_SOURCES))) 

TEST_BTHREAD_SOURCES = $(wildcard bthread_*unittest.cpp)

TEST_BRPC_SOURCES = $(wildcard brpc_*unittest.cpp)

TEST_PROTO_SOURCES = $(wildcard *.proto)
TEST_PROTO_OBJS =  $(TEST_PROTO_SOURCES:.proto=.pb.o)

TEST_BINS = test_base test_bvar $(TEST_BTHREAD_SOURCES:.cpp=) $(TEST_BRPC_SOURCES:.cpp=)

.PHONY:all
all: $(TEST_BINS)

.PHONY:clean
clean:clean_bins
	@echo "Cleaning"
	@rm -rf $(TEST_BASE_OBJS) $(TEST_BVAR_OBJS) $(TEST_BTHREAD_OBJS) \
		$(TEST_BRPC_OBJS) $(TEST_PROTO_OBJS)

.PHONY:clean_bins
clean_bins:
	@rm -rf $(TEST_BINS)

../libbase.dbg.a:
	@$(MAKE) -C.. libbase.dbg.a

../libbvar.dbg.a:
	@$(MAKE) -C.. libbvar.dbg.a

../libbthread.dbg.a:
	@$(MAKE) -C.. libbthread.dbg.a

../libbrpc.dbg.a:
	@$(MAKE) -C.. libbrpc.dbg.a

../libmcpack2pb.dbg.a:
	@$(MAKE) -C.. libmcpack2pb.dbg.a

../libjson2pb.dbg.a:
	@$(MAKE) -C.. libjson2pb.dbg.a

test_base:$(TEST_BASE_OBJS) ../libbase.dbg.a
	@echo "Linking $@"
	@$(CXX) -o $@ $(LIBPATHS) -Xlinker "-(" $^ -Wl,-Bstatic $(STATIC_LINKINGS) -Wl,-Bdynamic -Xlinker "-)" $(DYNAMIC_LINKINGS)

test_bvar:$(TEST_BVAR_OBJS) ../libbase.dbg.a ../libbvar.dbg.a
	@echo "Linking $@"
	@$(CXX) -o $@ $(LIBPATHS) -Xlinker "-(" $^ -Wl,-Bstatic $(STATIC_LINKINGS) -Wl,-Bdynamic -Xlinker "-)" $(DYNAMIC_LINKINGS)

bthread%unittest:bthread%unittest.o ../libbase.dbg.a ../libbvar.dbg.a ../libbthread.dbg.a
	@echo "Linking $@"
	@$(CXX) -o $@ $(LIBPATHS) -Xlinker "-(" $^ -Wl,-Bstatic $(STATIC_LINKINGS) -Wl,-Bdynamic -Xlinker "-)" $(DYNAMIC_LINKINGS)

brpc_%_unittest:$(TEST_PROTO_OBJS) brpc_%_unittest.o ../libbase.dbg.a ../libbvar.dbg.a ../libbthread.dbg.a ../libbrpc.dbg.a ../libmcpack2pb.dbg.a ../libjson2pb.dbg.a
	@echo "Linking $@"
	@$(CXX) -o $@ $(LIBPATHS) -Xlinker "-(" $^ -Wl,-Bstatic $(STATIC_LINKINGS) -Wl,-Bdynamic -Xlinker "-)" $(DYNAMIC_LINKINGS)

%.pb.cc:%.proto
	@echo "Generating $@"
	@$(PROTOC) --cpp_out=. --proto_path=. --proto_path=.. --proto_path=$(PROTOBUF_HDR) $<

%.o:%.cpp
	@echo "Compiling $@"
	@$(CXX) -c $(HDRPATHS) $(CXXFLAGS) $< -o $@

%.o:%.cc
	@echo "Compiling $@"
	@$(CXX) -c $(HDRPATHS) $(CXXFLAGS) $< -o $@

%.o:%.c
	@echo "Compiling $@"
	@$(CC) -c $(HDRPATHS) $(CFLAGS) $< -o $@