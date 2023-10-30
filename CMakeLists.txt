cmake_minimum_required (VERSION 3.8 FATAL_ERROR)

project ("VulkanVSCode")



set(CMAKE_CXX_STANDARD 17)
find_package(Vulkan REQUIRED)
set(glm_DIR ${PROJECT_SOURCE_DIR}/lib/glm/cmake/glm) 
find_package(glm REQUIRED)

add_library(glfw STATIC IMPORTED)
set_target_properties(glfw PROPERTIES
    IMPORTED_LOCATION "${PROJECT_SOURCE_DIR}/lib/glfw/lib-vc2022/glfw3.lib"
    INTERFACE_INCLUDE_DIRECTORIES "${PROJECT_SOURCE_DIR}/lib/glfw/include"
)

include_directories(${PROJECT_SOURCE_DIR}/lib/glm/glm)
include_directories(${PROJECT_SOURCE_DIR}/lib/glfw/include)
SET(GLM_TEST_ENABLE OFF CACHE BOOL "GLM Build unit tests")

add_executable(${PROJECT_NAME} main.cpp)

target_link_libraries(${PROJECT_NAME} glfw ${GLFW_LIBRARIES} Vulkan::Vulkan glm::glm)