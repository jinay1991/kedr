set(target_detector_module_name "target_detector_module")
set(test_module_name "target_detector_test_module")

rule_copy_file("${CMAKE_CURRENT_BINARY_DIR}/kedr_target_detector.c"
    "${CORE_SOURCE_DIR}/kedr_target_detector.c")

kbuild_add_module(${target_detector_module_name}
    "kedr_target_detector.c"
    "target_detector_module_simple.c")

kedr_test_install_module(${target_detector_module_name})

add_subdirectory(test_module)

configure_file("${CMAKE_CURRENT_SOURCE_DIR}/test.sh.in"
    "${CMAKE_CURRENT_BINARY_DIR}/test.sh"
    @ONLY
)

kedr_test_add_script("core.components.target_detector.01"
    "test.sh")

