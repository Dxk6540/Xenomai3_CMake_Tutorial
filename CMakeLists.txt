#########################################################################
# CMakeLists.txt file for building                      #
#                                                                       #
# This file is free software: you can redistribute it and/or modify     #
# it under the terms of the GNU General Public License as published by  #
# the Free Software Foundation, either version 3 of the License, or     #
# (at your option) any later version.                                   #
#                                                                       #
# This program is distributed in the hope that it will be useful,       #
# but WITHOUT ANY WARRANTY; without even the implied warranty of        #
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the         #
# GNU General Public License for more details.                          #
#                                                                       #
# You should have received a copy of the GNU General Public License     #
# along with this program.  If not, see <http://www.gnu.org/licenses/>. #
#########################################################################

cmake_minimum_required (VERSION 2.8.12)

project(xenoCmakeTutorial)

set(ENV{XENOMAI_ROOT_DIR} /usr/xenomai)

# Needed Modules
include(GNUInstallDirs)
include(CMakePackageConfigHelpers)
include(FindPkgConfig)
include(${PROJECT_SOURCE_DIR}/cmake-modules/CMakeFunctions.cmake)

# Set policy for LINK_INTERFACE
cmake_policy(SET CMP0022 NEW)

set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake-modules)

#common commands for building c++ executables and libraries
find_package(Xenomai)

#add_subdirectory(src)
set(EXAMPLES rtprint trivial-periodic)

add_executable(rtprint rtprint.c)
target_include_directories(rtprint PUBLIC ${Xenomai_NATIVE_INCLUDE_DIRS})
target_link_libraries(rtprint ${Xenomai_NATIVE_DL_FLAGS})
set_target_properties(rtprint PROPERTIES COMPILE_FLAGS ${Xenomai_NATIVE_DEFINITIONS})


add_executable(trivial-periodic trivial-periodic.c)
target_include_directories(trivial-periodic PUBLIC ${Xenomai_NATIVE_INCLUDE_DIRS})
target_link_libraries(trivial-periodic ${Xenomai_NATIVE_DL_FLAGS})
set_target_properties(trivial-periodic PROPERTIES COMPILE_FLAGS ${Xenomai_NATIVE_DEFINITIONS})


