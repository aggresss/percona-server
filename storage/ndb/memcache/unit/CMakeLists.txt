# Copyright (c) 2015, 2019, Oracle and/or its affiliates. All rights reserved.
#
# This program is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License, version 2.0,
# as published by the Free Software Foundation.
#
# This program is also distributed with certain software (including
# but not limited to OpenSSL) that is licensed under separate terms,
# as designated in a particular file or component or in included license
# documentation.  The authors of MySQL hereby grant you an additional
# permission to link the program and your derivative works with the
# separately licensed software that they have included with MySQL.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License, version 2.0, for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, write to the Free Software
# Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA 02110-1301  USA

######### run_unit_tests ##############
SET(UNIT_SOURCE_FILES
  harness.cc
  alloc.cc
  cas.cc
  casbits.cc
  connpool.cc
  incr.cc
  queue.cc
  stub_logger.cc
  tsv.cc
  lookuptable.cc
 )
ADD_EXECUTABLE(run_unit_tests ${UNIT_SOURCE_FILES})
TARGET_LINK_LIBRARIES(run_unit_tests ndbmemcache)
##########################################


### test_workqueue #####################
SET(TEST_WORKQUEUE_SOURCES test_workqueue.cc ../src/workqueue.cc)
IF(HAVE_SOLARIS_ATOMICS)
  SET(TEST_WORKQUEUE_SOURCES ${TEST_WORKQUEUE_SOURCES} ../src/atomics.cc)
ENDIF()

SET(libs)

IF(LIBRT)
  SET(libs rt)
ENDIF()
#NDB_ADD_TEST(test_workqueue-t "${TEST_WORKQUEUE_SOURCES}" LIBS "${libs}")
##########################################
