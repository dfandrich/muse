#=============================================================================
#  MusE
#  Linux Music Editor
#  $Id:$
#
#  Copyright (C) 1999-2011 by Werner Schweer and others
#
#  This program is free software; you can redistribute it and/or modify
#  it under the terms of the GNU General Public License
#  as published by the Free Software Foundation; either version 2
#  of the License, or (at your option) any later version.
#
#  This program is distributed in the hope that it will be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
#
#  You should have received a copy of the GNU General Public License
#  along with this program; if not, write to the
#  Free Software Foundation, Inc.,
#  51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA
#=============================================================================

##
## Expand Qt macros in source files
##
QT5_WRAP_CPP (cliplist_mocs
      cliplist.h
      )

##
## UI files
##
file (GLOB cliplist_ui_files
      cliplisteditorbase.ui
      )
QT5_WRAP_UI ( cliplist_uis ${cliplist_ui_files} )

##
## List of source files to compile
##
file (GLOB cliplist_source_files
      cliplist.cpp 
      )

##
## Define target
##
add_library ( cliplist ${MODULES_BUILD}
      ${cliplist_source_files}
      ${cliplist_mocs}
      ${cliplist_uis}
      )

##
## Append to the list of translations
##
set (FILES_TO_TRANSLATE
      ${FILES_TO_TRANSLATE}
      ${cliplist_source_files}
      ${cliplist_ui_files}
      CACHE INTERNAL ""
      )

##
## Compilation flags and target name
##
set_target_properties( cliplist
      PROPERTIES OUTPUT_NAME muse_cliplist
      )

##
## Linkage
##
target_link_libraries ( cliplist
      ${QT_LIBRARIES}
      widgets
      )

##
## Install location
##
if ( ${MODULES_BUILD} STREQUAL SHARED )
      install(TARGETS cliplist
            DESTINATION ${MusE_MODULES_DIR}
            )
endif ( ${MODULES_BUILD} STREQUAL SHARED )

