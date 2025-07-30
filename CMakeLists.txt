cmake_minimum_required(VERSION 3.16)
project(StockManagementSystem)

# Set C++ version
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# Set include and source directories
include_directories(include)
file(GLOB SOURCES "src/*.cpp")

# Add external libraries (assuming you use FetchContent)
include(FetchContent)

# === Fetch tabulate ===
FetchContent_Declare(
  tabulate
  GIT_REPOSITORY https://github.com/p-ranav/tabulate.git
  GIT_TAG        master
)
FetchContent_MakeAvailable(tabulate)

# === Fetch xlnt ===
FetchContent_Declare(
  xlnt
  GIT_REPOSITORY https://github.com/tfussell/xlnt.git
  GIT_TAG        master
)
FetchContent_MakeAvailable(xlnt)

# Add the executable
add_executable(StockManagement ${SOURCES})

# Link external libraries
target_link_libraries(StockManagement
    PRIVATE
    tabulate::tabulate
    xlnt
)

# Optional: Set output directory
set_target_properties(StockManagement PROPERTIES
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
)
