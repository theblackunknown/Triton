# Defaut build type defined as Release
if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE Release)
endif()

if(NOT ${CMAKE_SYSTEM_NAME} MATCHES "Windows")
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -g")
    set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O3")
endif()

if(${CMAKE_SYSTEM_NAME} MATCHES "Windows")
    set(PYTHON_SUFFIX .pyd)
else()
    set(PYTHON_SUFFIX .so)
endif()

# Define all source files
set(LIBTRITON_SOURCE_FILES
    api/api.cpp
    arch/architecture.cpp
    arch/arm/aarch64/aarch64Cpu.cpp
    arch/arm/aarch64/aarch64Semantics.cpp
    arch/arm/aarch64/aarch64Specifications.cpp
    arch/arm/arm32/arm32Cpu.cpp
    arch/arm/arm32/arm32Semantics.cpp
    arch/arm/arm32/arm32Specifications.cpp
    arch/arm/armOperandProperties.cpp
    arch/bitsVector.cpp
    arch/immediate.cpp
    arch/instruction.cpp
    arch/irBuilder.cpp
    arch/memoryAccess.cpp
    arch/operandWrapper.cpp
    arch/register.cpp
    arch/x86/x8664Cpu.cpp
    arch/x86/x86Cpu.cpp
    arch/x86/x86Semantics.cpp
    arch/x86/x86Specifications.cpp
    ast/ast.cpp
    ast/astContext.cpp
    ast/representations/astPythonRepresentation.cpp
    ast/representations/astRepresentation.cpp
    ast/representations/astSmtRepresentation.cpp
    callbacks/callbacks.cpp
    engines/lifters/liftingToDot.cpp
    engines/lifters/liftingToPython.cpp
    engines/lifters/liftingToSMT.cpp
    engines/solver/solverEngine.cpp
    engines/solver/solverModel.cpp
    engines/symbolic/pathConstraint.cpp
    engines/symbolic/pathManager.cpp
    engines/symbolic/symbolicEngine.cpp
    engines/symbolic/symbolicExpression.cpp
    engines/symbolic/symbolicSimplification.cpp
    engines/symbolic/symbolicVariable.cpp
    engines/synthesis/oracleTable.cpp
    engines/synthesis/synthesisResult.cpp
    engines/synthesis/synthesizer.cpp
    engines/taint/taintEngine.cpp
    modes/modes.cpp
    utils/coreUtils.cpp
)

# Define all header files
set(LIBTRITON_HEADER_FILES
    includes/triton/aarch64.spec
    includes/triton/aarch64Cpu.hpp
    includes/triton/aarch64Semantics.hpp
    includes/triton/aarch64Specifications.hpp
    includes/triton/api.hpp
    includes/triton/archEnums.hpp
    includes/triton/architecture.hpp
    includes/triton/arm32.spec
    includes/triton/arm32Cpu.hpp
    includes/triton/arm32Semantics.hpp
    includes/triton/arm32Specifications.hpp
    includes/triton/armOperandProperties.hpp
    includes/triton/ast.hpp
    includes/triton/astContext.hpp
    includes/triton/astEnums.hpp
    includes/triton/astPythonRepresentation.hpp
    includes/triton/astRepresentation.hpp
    includes/triton/astRepresentationInterface.hpp
    includes/triton/astSmtRepresentation.hpp
    includes/triton/bitsVector.hpp
    includes/triton/bitwuzlaSolver.hpp
    includes/triton/callbacks.hpp
    includes/triton/callbacksEnums.hpp
    includes/triton/comparableFunctor.hpp
    includes/triton/coreUtils.hpp
    includes/triton/cpuInterface.hpp
    includes/triton/cpuSize.hpp
    includes/triton/dllexport.hpp
    includes/triton/exceptions.hpp
    includes/triton/externalLibs.hpp
    includes/triton/immediate.hpp
    includes/triton/instruction.hpp
    includes/triton/irBuilder.hpp
    includes/triton/liftingEngine.hpp
    includes/triton/liftingToDot.hpp
    includes/triton/liftingToLLVM.hpp
    includes/triton/liftingToPython.hpp
    includes/triton/liftingToSMT.hpp
    includes/triton/llvmToTriton.hpp
    includes/triton/memoryAccess.hpp
    includes/triton/modes.hpp
    includes/triton/modesEnums.hpp
    includes/triton/operandWrapper.hpp
    includes/triton/oracleEntry.hpp
    includes/triton/pathConstraint.hpp
    includes/triton/pathManager.hpp
    includes/triton/register.hpp
    includes/triton/semanticsInterface.hpp
    includes/triton/shortcutRegister.hpp
    includes/triton/solverEngine.hpp
    includes/triton/solverEnums.hpp
    includes/triton/solverInterface.hpp
    includes/triton/solverModel.hpp
    includes/triton/symbolicEngine.hpp
    includes/triton/symbolicEnums.hpp
    includes/triton/symbolicExpression.hpp
    includes/triton/symbolicSimplification.hpp
    includes/triton/symbolicVariable.hpp
    includes/triton/synthesisResult.hpp
    includes/triton/synthesizer.hpp
    includes/triton/taintEngine.hpp
    includes/triton/tritonToBitwuzla.hpp
    includes/triton/tritonToLLVM.hpp
    includes/triton/tritonToZ3.hpp
    includes/triton/tritonTypes.hpp
    includes/triton/uintwide_t.h
    includes/triton/x86.spec
    includes/triton/x8664Cpu.hpp
    includes/triton/x86Cpu.hpp
    includes/triton/x86Semantics.hpp
    includes/triton/x86Specifications.hpp
    includes/triton/z3Solver.hpp
    includes/triton/z3ToTriton.hpp
)

# Define all resource files
set(LIBTRITON_RESOURCE_FILES
    includes/triton/version.hpp.in
    includes/triton/config.hpp.in
)

if(Z3_INTERFACE)
    set(Z3_INTERFACE_SOURCE_FILES
        ast/z3/tritonToZ3.cpp
        ast/z3/z3ToTriton.cpp
        engines/solver/z3/z3Solver.cpp
    )
else()
    set(Z3_INTERFACE_SOURCE_FILES)
endif()

if(BITWUZLA_INTERFACE)
    set(BITWUZLA_INTERFACE_SOURCE_FILES
        ast/bitwuzla/tritonToBitwuzla.cpp
        engines/solver/bitwuzla/bitwuzlaSolver.cpp
    )
else()
    set(BITWUZLA_INTERFACE_SOURCE_FILES)
endif()

if(LLVM_INTERFACE)
    set(LLVM_INTERFACE_SOURCE_FILES
        ast/llvm/llvmToTriton.cpp
        ast/llvm/tritonToLLVM.cpp
        engines/lifters/liftingToLLVM.cpp
    )
else()
    set(LLVM_INTERFACE_SOURCE_FILES)
endif()

if(PYTHON_BINDINGS)
    set(LIBTRITON_PYTHON_SOURCE_FILES
        bindings/python/init.cpp
        bindings/python/modules/tritonCallbacks.cpp
        bindings/python/namespaces/initArchNamespace.cpp
        bindings/python/namespaces/initAstNodeNamespace.cpp
        bindings/python/namespaces/initAstRepresentationNamespace.cpp
        bindings/python/namespaces/initCallbackNamespace.cpp
        bindings/python/namespaces/initConditionsNamespace.cpp
        bindings/python/namespaces/initCpuSizeNamespace.cpp
        bindings/python/namespaces/initExtendNamespace.cpp
        bindings/python/namespaces/initModeNamespace.cpp
        bindings/python/namespaces/initOpcodesNamespace.cpp
        bindings/python/namespaces/initOperandNamespace.cpp
        bindings/python/namespaces/initPrefixesNamespace.cpp
        bindings/python/namespaces/initRegNamespace.cpp
        bindings/python/namespaces/initShiftsNamespace.cpp
        bindings/python/namespaces/initSolverNamespace.cpp
        bindings/python/namespaces/initSolverStateNamespace.cpp
        bindings/python/namespaces/initSymbolicNamespace.cpp
        bindings/python/namespaces/initVersionNamespace.cpp
        bindings/python/objects/pyAstContext.cpp
        bindings/python/objects/pyAstNode.cpp
        bindings/python/objects/pyBitsVector.cpp
        bindings/python/objects/pyImmediate.cpp
        bindings/python/objects/pyInstruction.cpp
        bindings/python/objects/pyMemoryAccess.cpp
        bindings/python/objects/pyPathConstraint.cpp
        bindings/python/objects/pyRegister.cpp
        bindings/python/objects/pySolverModel.cpp
        bindings/python/objects/pySymbolicExpression.cpp
        bindings/python/objects/pySymbolicVariable.cpp
        bindings/python/objects/pyTritonContext.cpp
        bindings/python/pyXFunctions.cpp
        bindings/python/utils.cpp
    )
    set(LIBTRITON_PYTHON_HEADER_FILES
        includes/triton/py3c_compat.h
        includes/triton/pythonBindings.hpp
        includes/triton/pythonObjects.hpp
        includes/triton/pythonUtils.hpp
        includes/triton/pythonXFunctions.hpp
    )
else()
    set(LIBTRITON_PYTHON_SOURCE_FILES)
    set(LIBTRITON_PYTHON_HEADER_FILES)
endif()

# We generate the version numbers information
configure_file(
    ${CMAKE_CURRENT_SOURCE_DIR}/includes/triton/version.hpp.in
    ${CMAKE_CURRENT_BINARY_DIR}/includes/triton/version.hpp
    IMMEDIATE @ONLY
)

# We generate the config header based on configuation of CMake
configure_file(
    ${CMAKE_CURRENT_SOURCE_DIR}/includes/triton/config.hpp.in
    ${CMAKE_CURRENT_BINARY_DIR}/includes/triton/config.hpp
    IMMEDIATE @ONLY
)

# Define library's properties
add_library(triton
    ${LIBTRITON_SOURCE_FILES}
    ${LIBTRITON_HEADER_FILES}
    ${LIBTRITON_RESOURCE_FILES}
    ${Z3_INTERFACE_SOURCE_FILES}
    ${BITWUZLA_INTERFACE_SOURCE_FILES}
    ${LLVM_INTERFACE_SOURCE_FILES}
    ${LIBTRITON_PYTHON_SOURCE_FILES}
    ${LIBTRITON_PYTHON_HEADER_FILES}
)
add_dependencies(check triton)

set_target_properties(triton PROPERTIES PUBLIC_HEADER
    "${LIBTRITON_HEADER_FILES};${CMAKE_CURRENT_BINARY_DIR}/includes/triton/version.hpp;${CMAKE_CURRENT_BINARY_DIR}/includes/triton/config.hpp"
)

target_include_directories(triton PUBLIC
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/includes>"
    "$<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}/includes>"
)

# Link Triton's dependencies
target_link_libraries(triton PUBLIC
    ${PYTHON_LIBRARIES}
    ${Boost_LIBRARIES}
    ${Z3_LIBRARIES}
    ${LLVM_LIBRARIES}
    ${BITWUZLA_LIBRARIES}
    ${CAPSTONE_LIBRARIES}
)

# Workaround to allow building 'namespace linux' (defined by -std=gnu++11)
if(NOT MSVC AND (CMAKE_CXX_COMPILER_ID MATCHES "Clang" OR CMAKE_CXX_COMPILER_ID STREQUAL "GNU"))
    target_compile_options(triton PRIVATE -std=c++14)
endif()

# Enable static msvc runtime.
if(MSVC AND MSVC_STATIC)
    set_property(TARGET triton PROPERTY MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
endif()

if(WIN32 AND BUILD_SHARED_LIBS)
    target_compile_definitions(triton PRIVATE BUILDING_DLL)
endif()

# Install tritonTargets.cmake
install(
    EXPORT tritonTargets
    DESTINATION lib/cmake/triton
    NAMESPACE triton::
)

# Install triton
install(
    TARGETS triton
    EXPORT tritonTargets
    PUBLIC_HEADER DESTINATION include/triton
    INCLUDES DESTINATION include
    RUNTIME DESTINATION bin
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

# Configure tritonConfig.cmake and tritonConfigVersion.cmake
include(CMakePackageConfigHelpers)
configure_package_config_file(
    Config.cmake.in
    "${PROJECT_BINARY_DIR}/tritonConfig.cmake"
    INSTALL_DESTINATION lib/cmake/triton
    NO_SET_AND_CHECK_MACRO
    NO_CHECK_REQUIRED_COMPONENTS_MACRO
)

write_basic_package_version_file("${PROJECT_BINARY_DIR}/tritonConfigVersion.cmake"
    COMPATIBILITY SameMajorVersion
)

# Install tritonConfig.cmake and tritonConfigVersion.cmake
install(
    FILES
        "${PROJECT_BINARY_DIR}/tritonConfig.cmake"
        "${PROJECT_BINARY_DIR}/tritonConfigVersion.cmake"
    DESTINATION lib/cmake/triton
)

# Install Python bindings
if(PYTHON_BINDINGS)
    add_custom_target(python-triton ALL
        COMMAND ${CMAKE_COMMAND} -E copy "${CMAKE_CURRENT_BINARY_DIR}/${CMAKE_CFG_INTDIR}/${CMAKE_SHARED_MODULE_PREFIX}triton${CMAKE_SHARED_LIBRARY_SUFFIX}" "${CMAKE_CURRENT_BINARY_DIR}/${CMAKE_CFG_INTDIR}/triton${PYTHON_SUFFIX}"
        DEPENDS triton
    )
    if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
        execute_process (COMMAND ${PYTHON_EXECUTABLE} -c "from sysconfig import get_path; print(get_path('platlib'))" OUTPUT_VARIABLE PYTHON_SITE_PACKAGES OUTPUT_STRIP_TRAILING_WHITESPACE)
        if(${CMAKE_SYSTEM_NAME} MATCHES "Windows" AND NOT ${CMAKE_CXX_COMPILER_ID} MATCHES "GNU")
            install (FILES ${CMAKE_CURRENT_BINARY_DIR}/\${CMAKE_INSTALL_CONFIG_NAME}/triton${PYTHON_SUFFIX} DESTINATION ${PYTHON_SITE_PACKAGES})
        else()
            install (FILES ${CMAKE_CURRENT_BINARY_DIR}/triton${PYTHON_SUFFIX} DESTINATION ${PYTHON_SITE_PACKAGES})
        endif()
    else()
        execute_process (COMMAND ${PYTHON_EXECUTABLE} -c "from sys import version_info; print(f'lib/python{version_info[0]}.{version_info[1]}/site-packages')" OUTPUT_VARIABLE PYTHON_SITE_PACKAGES OUTPUT_STRIP_TRAILING_WHITESPACE)
        install (FILES ${CMAKE_CURRENT_BINARY_DIR}/triton${PYTHON_SUFFIX} DESTINATION ${CMAKE_INSTALL_PREFIX}/${PYTHON_SITE_PACKAGES})
    endif()
endif()
