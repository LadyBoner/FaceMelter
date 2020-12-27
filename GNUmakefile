################################################################################
################################################################################
##
##			FaceMelter  < github.com/LadyBoner/FaceMelter >
##
#
#  MIT License  < https://opensource.org/licenses/MIT >
#  Copyright 2020 Nathan Smile  - Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
#  The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
#  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
#
#  Brief:  Drop FaceMelter into root folder of a project and I'll wash your future sins.  <3<3<3
#  Note:  Editing a makefile for readability causes impotence later in life!  Particularly $(call ).
#  WARNING:  Will not work with spaces in path/file names.
#
################################################################################
################################################################################


#  $(NL) $(info )
#  C_OPTIMIZE :=  -fPIE  $(if $(COMSPEC), -mthreads, -pthread )
#  $(subst $(FACE_DIR),^,$@)  ##  Windows prepends extra SLASH.
#  Start target recipes with @ on own line.
##  -Orecurse causes loss of colored compiler output (text is buffered).  WITH MULTIPLE JOBS.
##  Does Wondows DRY_RUN in $(firstword MAKEFLAGS)?


################################################################################
##
##			@VARIABLES you ought to want to adapt.  And can be automatically reset.
##



#/**

##	Comment generation atop every file.  Change these here, or via CLI:
##  $make update [<license>] [<year>] [<authors>]
COPY_YEAR   	:=  <YEAR>
COPY_NAME   	:=  <AUTHORS>
COPY_LICENSE	:=  # $(call License, MIT)  # MIT BSD NCSA Apache LGPL GPL
REPOSITORY  	:=  <REPOSITORY>


C_COMPILER		:=  gcc
CPP_COMPILER 	:=  g++
M_COMPILER		:=  gcc
MM_COMPILER		:=  gcc
GO_COMPILER		:=  gccgo
PY_COMPILER		:=  python


##	System-installed libraries to be passed to the linker.
##	If the library, or a link, is not already present within the project tree,
##  you may place the -l & -L entries here to be parsed.
C_LIBRARIES		:=  # ncurses gtk/gtk
C_STANDARD		:=  -std=c11
C_WARNINGS		:=  -Wextra


##  Comment-out COLORS declaration to remove FaceMelter colored formatting.
COLORS	:=  COLORS

##  Pre-requisites of .PRECIOUS are kept even if process is killed before completion.
.PRECIOUS :
IGNORE    :=
GITIGNORE :=


#<3<3<3**/



##
##			VARIABLES you ought to want to adapt.
##
################################################################################




################################################################################
##
##			@FILES, FUNCTIONS, Other VARIABLES
##



##  Only the first line of a recipe is checked for @ - +.
##  Only the final line of a recipe can fail the shell.
.ONESHELL :
.DELETE_ON_ERROR :
.SILENT :
##  .SILENT is actually deprecated.


$(IGNORE) : ;
.INTERMEDIATE : $(IGNORE)


##  Every MicroSoft OS has this environment variable.
WINDOWS :=  $(COMSPEC)
##  MicroSoft seems to be incorporating much of GNU/Linux into its OS.
ifdef WINDOWS
	Include	 =  $(eval  -include $1)
	SLASH	:=  /
	TOUCH	:=  @touch
	MKDIR	:=  @mkdir -p
	MV		:=  @mv -f
	RM		:=  -@rm -fr
else
	Include	 =  $(eval  sinclude $1)
	SLASH	:=  /
	TOUCH	:=  @touch
	MKDIR	:=  mkdir -p
	MV		:=  @mv -f
	RM		:=  -@rm -fr
endif


loadAvg		:=	$(if $(WINDOWS),, -j -l$(strip $(shell nproc) ))
MAKEFLAGS	+=  -Riskr $(loadAvg) -Orecurse  --no-print-directory
##  -Orecurse causes loss of colored compiler output (text is buffered).



LIB_SUFFIX	:=  .a .so .dll .lib
INC_SUFFIX	:=  .h .H .hh .hp .hpp .HPP .h++ .hxx
SRC_SUFFIX 	:=  .c .C .cc .cp .cpp .CPP .c++ .cxx .m .mm .M #.go .py .pr  ##  Need to link libobjc.			


ifndef C_COMPILER
	C_COMPILER :=  gcc
endif

ifndef CPP_COMPILER
	CPP_COMPILER :=  g++
endif


COMPILE.c 	=  $(C_COMPILER) $(CFLAGS)
COMPILE.C	=  $(C_COMPILER) $(CFLAGS)
COMPILE.cc	=  $(CPP_COMPILER) $(CFLAGS)
COMPILE.cp	=  $(CPP_COMPILER) $(CFLAGS)
COMPILE.cpp	=  $(CPP_COMPILER) $(CFLAGS)
COMPILE.CPP	=  $(CPP_COMPILER) $(CFLAGS)
COMPILE.c++	=  $(CPP_COMPILER) $(CFLAGS)
COMPILE.cxx	=  $(CPP_COMPILER) $(CFLAGS)
COMPILE.m	=  $(M_COMPILER)
COMPILE.M 	=  $(M_COMPILER)
COMPILE.mm 	=  $(MM_COMPILER)
COMPILE.go 	=  $(GO_COMPILER)
COMPILE.py 	=  $(PY_COMPILER)


F_PIE	  =  -fPIC
CFLAGS    =  $(strip $(C_STANDARD) $(C_WARNINGS) $(C_IQUOTE) $(C_FLAGS))
C_FLAGS   =  $(strip $(C_DEBUG) $(C_PROFILE) $(C_ARCH) $(C_OPTIMIZE))
LD_FLAGS :=  $(if $(C_LIBFLAGS), $(LD_FLAGS) )
LINKER.c  =  $(LD_FLAGS) $(C_LIBFLAGS) $(foreach)
C_OBJECT :=  $(F_PIE)


##  Some of these flags are also defined elsewhere.  Your contributions here should override conflicting flags.
C_ARCH     :=  
C_OPTIMIZE :=  -fPIE  $(if $(COMSPEC), -mthread, -pthread ) #-fsanitize=undefined -Wl,-pie -pipe  ##  Move to linker and add for shared.
C_SHARED	=  -fPIC --shared -Wl,-export-dynamic -Wl,--no-undefined -Wl,-zdefs  ##  http://tldp.org/HOWTO/Program-Library-HOWTO/shared-libraries.html
C_IQUOTE    =  -iquote "." $(foreach _dir, $(INC_DIRS), -iquote "$(_dir)") -DFaceMelter #-frecord-command-switches #-frecord-gcc-switches
C_MATH		=  
C_ANDROID	=  
C_FUZZING	=  -fsanitize-coverage=trace-pc -fsanitize-coverage=trace-cmp
C_SECURE	=  -fsanitize-recover=all -fsanitize=address -fsanitize=pointer-compare -fsanitize=pointer-subtract -fsanitize=leak -fsanitize=undefined -fsanitize=bounds-strict -fsanitize=float-divide-by-zero -fsanitize=float-cast-overflow -fsanitize-address-use-after-scope -fsanitize-undefined-trap-on-error -fcf-protection=full -fstack-protector-strong -fstack-clash-protection -fvtable-verify=std -fasynchronous-unwind-tables (already) -fexceptions -mcet -Werror=format-security -Werror=implicit-function-declaration -Wl,-z,defs -Wl,-z,relro -Wl,-z,now -Wl,-z,noexecstack -Wl,-z,relro -Wl,--as-needed --param ssp-buffer-size=4 (superfulous?)
##  Some of the C_SECURE flags are not utilized unless an $ENVIRONMENT_VARIABLE is set.  Read your compiler documentation.
##  Once you get into threading you'll need to write your own C_SECURE flags.


LD_FLAGS    =  -L$(MOD_DIR)
C_LIBFLAGS  =  
ADD_LATER	=  -Wl,--hash-style=gnu -Wl,--no-copy-dt-needed-entries



findRoot =  $(eval _dir :=$(SLASH))  \
			$(foreach _tmp, $(subst $(SLASH), ,$(CURDIR) )  \
				, $(eval _dir :=$(_dir)$(_tmp)$(SLASH))  \
				  $(if $(hasMakefile), $(_dir) ))


##  Changing ?= to := makes all directories absolute, and adds root to INC_DIRS, & MOD_DIRS (reduntant).  Have not looked into why.
ROOT_MAKE	?=  $(firstword  $(findRoot) )
PROJECT		?=  $(lastword $(subst $(SLASH), ,$(ROOT_MAKE)))
##  Changing ?= to := makes all directories absolute, and adds root to INC_DIRS, & MOD_DIRS (reduntant).  Have not looked into why.
ITSELF		:=  $(lastword $(subst $(SLASH), ,$(CURDIR)))
ARCHIVE		:=  $(ITSELF).a
SHARED		:=  $(ITSELF).so
FACE_DIR	:=  .face$(SLASH)
OBJ_DIR		:=  .obj$(SLASH)
DEP_DIR		:=  .dep$(SLASH)
MAKECMDGOALS :=  $(filter-out $(ITSELF), $(MAKECMDGOALS))


MAKEFILE_LIST :=  GNUmakefile BSDmakefile Makefile makefile
hasMakefile	=  $(filter  $(MAKEFILE_LIST), $(notdir $(getFiles)) )


##  $(wildcard ) can return only directories (*/) for $(CURDIR).  All files otherwise.
getFiles =	$(wildcard  $(_dir)*$(_suffix) )
getDirs	 =  $(filter-out  $(_dir), $(sort  $(dir  $(wildcard  $(_dir)*$(SLASH)) )))

##  $(call  FindSuffix,{SRC|INC})  :: SRC_DIRS or INC_DIRS
FindSuffix  =	$(foreach _suffix, $($1_SUFFIX)  \
					, $(if  $(getFiles)  \
						, FindSuffix  \
						  $(eval  $1_DIRS += $(_dir) )  \
						  $(if  $(filter SRC, $1)  \
							, $(eval  SOURCES += $(getFiles) ))))


IGNORE_DIRS :=  .* broken test tests
ignoreDir =  $(filter IGNORE, $(foreach _ignoreDir, $(IGNORE_DIRS)  \
				, $(subst $(SLASH)$(_ignoreDir)$(SLASH), IGNORE , $(_dir) )))


createModuleVars =	$(eval  MOD_DIRS += $(_dir) )  \
					$(eval  temp     := $(lastword $(subst $(SLASH), ,$(_dir) )))  \
					$(eval  MODULES  += $(temp) )  \
					$(eval  FACE_$(temp)_MELTER := $(_dir))


##  $(call  FindDirs,<directory>)  :: SRC_DIRS, INC_DIRS, & MOD_DIRS
FindDirs =	$(foreach _dir, $(getDirs)  \
				, $(if  $(hasMakefile)  \
					, $(createModuleVars)  \
					, $(call  FindDirs) )  \
				$(if  $(ignoreDir),  \
					, $(call  FindSuffix,LIB)  \
					, $(call  FindSuffix,SRC)  \
					  $(call  FindSuffix,INC) ))


FIND_FILES 	:=	$(if  $(strip  $(call  FindSuffix,SRC)),  $(eval  SRC_DIRS += .$(SLASH) ))  \
				$(FindDirs)  \
				$(eval  SRC_DIRS := $(sort $(SRC_DIRS) ))  \
				$(eval  INC_DIRS := $(sort $(INC_DIRS) ))  \

MAKE_DIRS	:=  $(shell  $(MKDIR) $(FACE_DIR)$(_src)$(DEP_DIR) )  \
				$(foreach _src, $(SRC_DIRS)  \
					, $(shell  $(MKDIR) $(FACE_DIR)$(_src)$(DEP_DIR) )  \
					  $(shell  $(MKDIR) $(FACE_DIR)$(_src)$(OBJ_DIR) ))

DERIVE_FILES :=	$(eval  DEPENDS :=  $(foreach _src, $(SOURCES), $(FACE_DIR)$(subst .$(SLASH),,$(dir $(_src) ))$(DEP_DIR)$(notdir $(_src:.c=.d) )))  \
				$(eval  OBJECTS :=  $(foreach _src, $(SOURCES), $(FACE_DIR)$(subst .$(SLASH),,$(dir $(_src) ))$(OBJ_DIR)$(notdir $(_src:.c=.o) )))  \
				$(eval  OBJECTS-fPIE :=  $(foreach _obj, $(OBJECTS), $(_obj:.o=-fPIE.o) ))  \
				$(eval  OBJECTS-fPIC :=  $(foreach _obj, $(OBJECTS), $(_obj:.o=-fPIC.o) ))  \
				$(eval  OBJECTS :=  $(OBJECTS-fPIE) $(OBJECTS-fPIC) )

##  Print <root> if directory is ./ , remove superfulous instances of it otherwise.
##  Replace directory instances of $(FACE_DIR) with ^/ to shorten output.
##  Dim the directory portion of filenames.
##  Dim the flags appended to OBJECTS names (-fPIE,-fPIC).
##  $(call  FormatOutput,<output>)
FormatOutput =  $(if  $(filter .$(SLASH), $1 )  \
					, $(GRAY)<$(DIM)root$(GRAY)>$(RESET)  \
					, $(DIM) $(strip  $(if  $(filter  .$(SLASH), $(dir $1))  \
						, $(subst .$(SLASH),,$(dir $1))  \
						, $(if  $(FACE_DIR)  \
							, $(subst $(FACE_DIR),^$(SLASH),$(dir $1)))  \
						))$(WHITE)$(notdir $(basename $(subst -fPIC$(suffix $1),$(GRAY)-fPIC, $(subst -fPIE$(suffix $1),$(GRAY)-fPIE, $1 ))))$(if $(suffix $1),$(COLOR$(suffix $1 )))$(RESET))



##
##			FILES, FUNCTIONS, Other VARIABLES
##
################################################################################




################################################################################
##
##			@FORMATTING
##



##  $(info ) always prints first from anywhere.
##  $(info ) defeats DRY_RUN; adding "+" to a recipe printed DRY_RUN anyways.
##  DO NOT simple-expand $(info ).

export DRY_RUN	?=  $(findstring n, $(firstword $(MAKEFLAGS) ))

BLANK	:=
SPACE	:=  $(BLANK) $(BLANK)
TAB		:=  $(SPACE)$(SPACE)$(SPACE)$(SPACE)$(SPACE)$(SPACE)$(SPACE)$(SPACE)
##  DO NOT simple-expand $(info ).
NL		=  $(info )
ECHO	=  $(if $(DRY_RUN), -@echo, -@printf)
BREAK	=  $(info $(PURPLE)************************************************************$(RESET))
CTRL_C	=  $(info CTRL-C to quit $(YELLOW)$(BOLD)F$(REDER)a$(ORANGE)c$(RED)e$(YELLOW)M$(REDER)e$(ORANGE)l$(RED)t$(ORANGE)e$(REDER)$(BOLD)r$(RESET).  $(WHITE)(Credit: $(GRAY)Unknown$(WHITE))$(RESET) )



ifdef COLORS
	
	ESC		:=	[
	RESET	:=	$(ESC)0m
	BOLD	:=	$(ESC)1m
	SEQ		:=	$(RESET)$(ESC)
	
	BLACK	:=	$(SEQ)30m
	RED		:=	$(SEQ)31m
	GREEN	:=	$(SEQ)32m
	ORANGE	:=	$(SEQ)33m
	BLUE	:=	$(SEQ)34m
	PURPLE	:=	$(SEQ)35m
	CYAN	:=	$(SEQ)36m
	GRAY	:=	$(SEQ)37m
	##  The default color is only RESET, but terminals are using custom GRAY.
	ifdef WINDOWPATH  ##  Linux PTY
		
		##  If pseudo-terminal has custom white background, give WHITE a black background.
		WHITE	:=	$(SEQ)40;97m
		REDER	:=	$(SEQ)91m
		GREENER	:=	$(SEQ)92m
		YELLOW	:=	$(SEQ)93m
		BLUER	:=	$(SEQ)94m
		PURPLY	:=	$(SEQ)95m
		CYANER	:=	$(SEQ)96m
		DIM		:=	$(SEQ)90m
		UNBOLD	:=	$(RESET)$(WHITE)
	else  ##  Windows, Linux TTY
		
		##  If pseudo-terminal has custom white background, give WHITE a black background.
		WHITE	:=	$(RESET)$(BOLD)$(ESC)40m
		REDER	:=	$(SEQ)31m$(BOLD)
		GREENER	:=	$(SEQ)32m$(BOLD)
		YELLOW	:=	$(SEQ)33m$(BOLD)
		BLUER	:=	$(SEQ)34m$(BOLD)
		PURPLY	:=	$(SEQ)35m$(BOLD)
		CYANER	:=	$(SEQ)36m$(BOLD)
		DIM		:=	$(GRAY)
		UNBOLD	:=	$(GRAY)
	endif
	
	ifeq  "$(strip $(C_COMPILER) )"  "gcc"
		C_WARNINGS +=  -fno-diagnostics-color
	endif
	ifeq  "$(strip $(C_COMPILER) )"  "clang"
		C_WARNINGS +=  -fno-color-diagnostics
	endif
	
	MARKER	:=	$(REDER)\#$(YELLOW)\#$(GREENER)\#$(CYANER)\#$(BLUER)\#$(PURPLY)\#$(RESET)
else
	MARKER	:= \#\#\#\#\#\#
endif


COLOR.d  :=  $(YELLOW).d$(RESET)
COLOR.o  :=  $(ORANGE).o$(RESET)
$(foreach _inc, $(INC_SUFFIX)  \
	, $(eval  COLOR$(_inc) := $(PURPLE)$(_inc)$(RESET)) )
COLOR.c    :=  $(BLUE).c$(RESET)
COLOR.C    :=  $(BLUE).C$(RESET)
COLOR.cc   :=  $(COLOR.c)$(BLUER)c$(RESET)
COLOR.cp   :=  $(COLOR.c)$(BLUER)p$(RESET)
COLOR.cpp  :=  $(COLOR.c)$(BLUER)pp$(RESET)
COLOR.CPP  :=  $(COLOR.C)$(BLUER)PP$(RESET)
COLOR.c++  :=  $(COLOR.c)$(BLUER)++$(RESET)
COLOR.cpp  :=  $(COLOR.c)$(BLUER)xx$(RESET)
COLOR.m    :=  $(RED).m$(RESET)
COLOR.mm   :=  $(COLOR.m)$(ORANGE)m$(RESET)
COLOR.M    :=  $(RED).M$(RESET)
COLOR.go   :=  $(GREEN).go$(RESET)
COLOR.py   :=  $(CYAN).py$(RESET)
COLOR.pr   :=  $(GREEN).p$(GREENER)r$(RESET)


#.PHONY : break
break :  #FACE_gitignore_MELTER
	$(BREAK)



##
##			FORMATTING
##
################################################################################




################################################################################
##
##			@SOURCES
##



#SOURCES   :=  $(wildcard   $(SRC_DIRS)*.c )
#MAIN      :=  $(findstring $(SRC_DIRS)main.c, $(SOURCES) )
#  SOURCES :=  $(filter-out $(MAIN),      $(SOURCES) )
#  SOURCES :=  $(filter-out $(PROJECT).c, $(SOURCES) )
#MAIN      +=  $(findstring $(PROJECT).c, $(SOURCES) )




##
##			SOURCES
##
################################################################################




################################################################################
##
##			@OBJECTS
##



##	The un-necessary slashes at end of recipes aid output spacing.  Dry-runs too!

.SECONDEXPANSION:
appendObj  =  $(@:*.o=$(F_PIE).o)
fmtSource  =  $(DIM)$(basename $(notdir $(firstword $?)))$(COLOR$(suffix $(firstword $?)))$(RESET)
#fmtTarget =  $(DIM)$(dir $@)$(RESET)$(BOLD)$(notdir $(basename $(@:*.o=.o)) )$(GRAY)$(strip $(foreach _tmp,$(C_OBJECT), $(_tmp) ))$(COLOR$(suffix $@))$(RESET)
fmtTarget  =  $(strip $(call  FormatOutput,$(appendObj)))
$(OBJECTS) :
	$(info  $(SPACE)$(MARKER) $(fmtTarget)  ($(fmtSource))  )
	$(NL)  $(COMPILE.c) -c   \
	$(if $<,  $<,  $(info $(REDER)<source error>$(RESET) ))  \
	  -o $@  \


##
##			OBJECTS
##
################################################################################




################################################################################
##
##			@DEPENDENCIES  -  WARNING: .SECONDEXPANSION happens here.
##



##  MAKEFILES do not auto-generate.
##  Windows needs the -.  Apparenty 's' is more portable.
$(call Include, $(DEPENDS) )  # $(DEP_DIR)$(PROJECT)mk.d #$(LOVE_FILE)


$(DEP_DIR)$(PROJECT)mk.d :
	$(ECHO) '$$(shell $$(strip $$(if $$(DRY_RUN),, rm -f $$(DB) )))'  \
		> $@


##  DEPENDS are auto-made if not exist.  This will not show up in DRY_RUN.  Depend on SOURCES also needed.
.SECONDEXPANSION:
$(DEPENDS) : CFLAGS = $(C_IQUOTE)  -MM -MT '$(subst $(DEP_DIR),$(OBJ_DIR),$(@:.d=-fPIE.o)) $(subst $(DEP_DIR),$(OBJ_DIR),$(@:.d=-fPIC.o))' -MF '$@'
$(DEPENDS) : %.d : $$(subst $(FACE_DIR),,$$(subst $(DEP_DIR),,%)).c  ##  I have no honest clue why this needs .SECONDEXPANSION & no other approach works.
	$(COMPILE.c)  \
	  "$<"



##
##			DEPENDENCIES
##
################################################################################




################################################################################
##
##			@LINKING (Recipes & Pre-Requisites)  -  WARNING: .SECONDEXPANSION happens here.
##



##  NEED TO REMOVE COMPILED OBJECT FLAGS !!
## 	The un-necessary slashes at end of recipes aid output spacing.  Dry-runs too!


$(SHARED) : $(OBJECTS-fPIC)
	$(NL)
	$(info $(TAB) $(WHITE)Create $(YELLOW)SHARED$(RESET)  )
	$(NL)
	$(COMPILE.c) -shared  \
	  $(OBJECTS-fPIC)  $(LINKER.c)  \
	  -o "$@"  \

# (DIM)$(notdir $(basename $(_obj)))$(COLOR$(suffix $(_obj) ))
archiveObjs  =  $(foreach _obj, $?  \
					, $(shell  $(MV) $(_obj) $(_obj:$(F_PIE).o=.o) )  \
					  $(_obj:$(F_PIE).o=.o)  \
					  $(shell  $(MV) $(_obj:$(F_PIE).o=.o) $(_obj) ))
##  .SECONDEXPANSION here.
$(ARCHIVE) :  $$(OBJECTS$(F_PIE))
	$(NL)
	$(info  $(TAB) $(WHITE)Update $(YELLOW)ARCHIVE  $(GRAY)($(DIM)$(F_PIE)$(GRAY))  )
	$(info  $(SPACE)$(SPACE)$(WHITE)($(strip  $(fmtObjects))$(WHITE))$(RESET)  )
	$(NL)
	cd "$(OBJ_DIR)";  \
	ar crs  "$(ROOT_DIR)$@"  \
	  $(archiveObjs)  \
##  Do not use $ar -u.  We want to jump between -fPIE & -fPIC objects.



$(PROJECT) : $(OBJECTS$(F_PIE))
	$(NL)
	$(info $(TAB) $(WHITE)Create $(YELLOW)BINARY$(RESET)  )
	$(NL)
	$(CC) "$(MAIN)"  $(OBJECTS$(F_PIE))  \
	  $(CFLAGS)  \
	  -o $(PROJECT)  \



##
##			LINKING (Recipes & Pre-Requisites)
##
################################################################################




################################################################################
##
##			@HOUSE-KEEPING
##



##  Do not generate .gitignore during DRY_RUN.


##  Only filenames (with suffix) which will be generated by FaceMelter.
##  $(call  Filenames,<suffix>)  ::  <project.suffix>  <modules.suffix>
AddSuffix =	$(PROJECT)$(strip $1)  \
			$(foreach _mod, $(MODULES), $(_mod)$(strip $1) )


_GITIGNORE :=	$(PROJECT)  \
				$(PROJECT).exe  \
				$(call AddSuffix, .so)  \
				$(call AddSuffix, .a)  \
				$(FACE_DIR)  $(DEP_DIR)  $(OBJ_DIR)  .d  .o  .out


##  Prepend each GITIGNORE.  Note the asterick.
##  $(call  PrependGitignore,<prepend>)  ::  <prepend>*_GITIGNORE
PrependGitignore =	$(foreach _tmp, $(_GITIGNORE)  \
						,$(if $(basename $(_tmp) ),$(strip $1$(_tmp)),$(strip $1*$(_tmp))))


define  $(if $(DRY_RUN), db, FACE_Gitignore_MELTER)
	$(ECHO)  "####  FaceMelter\n\n"                                             >  .gitignore
	$(ECHO)  "##  DO NOT edit here.  Append GITIGNORE in GNUmakefile.\n"        >> .gitignore
	$(ECHO)  "##  Contents of FaceMelter GITIGNORE: $(if  $(GITIGNORE)  \
								, \n$(foreach _tmp, $(GITIGNORE),\n$(_tmp))  \
								, nothing.)\n\n"                                >> .gitignore
	$(ECHO)  "##  WARNING:  All following will get deleted by: \$$make clean\n" >> .gitignore
	$(ECHO)  "##  Matched output to SOURCES.\n"                                 >> .gitignore
	$(ECHO)  "$(foreach _src, $(basename $(SOURCES)),\n$(_src))\n\n\n"          >> .gitignore
	$(ECHO)  "##  Generic PATTERNS.\n"                                          >> .gitignore
	$(ECHO)  "$(call PrependGitignore,\n)\n\n\n"                                >> .gitignore
	$(ECHO)  "##  Duplicated PATTERNS within ANY directory.\n"                  >> .gitignore
	$(ECHO)  "$(call PrependGitignore,\n**$(SLASH))"                            >> .gitignore
	$(RM)	 $(DB)
endef



define FACE_Source_MELTER
	mkdir -p    src$(SLASH)inc$(SLASH)  \
	  && touch  src$(SLASH)$(strip $1).$(strip $2)  \
				src$(SLASH)inc$(SLASH)$(strip $1)-in.h
endef


define FACE_Simple_MELTER
	mkdir -p  src$(SLASH)broken$(SLASH)  \
			  src$(SLASH)test$(SLASH)src  \
	  &&  $(call FACE_Source_MELTER, $1, $2)
endef


define FACE_Module_MELTER
	mkdir -p  src$(SLASH)$(strip $1)  &&  cd src$(SLASH)$(strip $1)  \
	  &&  $(call FACE_Simple_MELTER, $1, $2)  \
	  &&  touch  $(strip $1).h    \
	  &&  cd  $(ROOT_DIR)  \
	  &&  cp  Makefile  src$(SLASH)$(strip $1)
endef


.PHONY : init tree project
init tree project :  # $(call src_template)  $(call header_guards)
	$(MKDIR)	dev$(SLASH)           \
	&& $(TOUCH)	dev$(SLASH)BUGS       \
				dev$(SLASH)ChangeLog  \
				dev$(SLASH)ToDo
	$(MKDIR)	doc$(SLASH)
	$(MKDIR)	res$(SLASH)icon       \
				res$(SLASH)lib
	
	$(call FACE_Simple_MELTER, $(PROJECT),c)
	$(call FACE_Module_MELTER, $(MODULE) )
	$(TOUCH)  	$(PROJECT).h  src$(SLASH)inc$(SLASH)$(PROJECT)-in.h
	$(TOUCH)	LICENSE  \
				README
	$(FACE_Gitignore_MELTER)


.PHONY : FACE_GITINGORE_MELTER
FACE_GITINGORE_MELTER :
	$(FACE_Gitignore_MELTER)


.PHONY : mod module
mod module :
	$(call FACE_Module_MELTER, $(MODULE),c)


.PHONY : simple
simple :
	$(call FACE_Simple_MELTER, $(PROJECT),c)


# WTF, fix this.
src = source
source = $(src)
#.PHONY : src source
$(source) :
	$(call FACE_Source_MELTER, $(src) )


.PHONY : touch
touch :
	$(TOUCH) $(SOURCES)


.PHONY : clean clear
clean clear : | FACE_GITINGORE_MELTER
	$(RM)  $(call PrependGitignore)
	$(RM)  $(call PrependGitignore, **$(SLASH))



##
##			HOUSE-KEEPING
##
################################################################################




################################################################################
##
##			@OPTIMIZATIONS
##



.PHONY : opt optimize
opt optimize : fast

.PHONY : pro prof profile
pro prof profile : C_PROFILE :=  -gp
pro prof profile : touch all

## Add sanitizer options.
.PHONY : db debug
db debug : C_DEBUG     =  -O0 -ggdb3
db debug : touch all

.PHONY : size
size     : C_OPTIMIZE +=  -flto -Os
size     : touch all

.PHONY : fast
fast     : C_OPTIMIZE +=  -flto -O2 -ftree-vectorize -ftree-slp-vectorize
fast     : touch all

.PHONY : faster
faster   : C_OPTIMIZE +=  -flto -O3 -march=native -ftree-vectorize
faster   : touch all

## May lose ABI compatibility.
.PHONY : fastest
fastest  : C_OPTIMIZE +=  -flto -Ofast -march=native -fomit-frame-pointer  ##  Change -fPIE to -pie.
fastest  : touch all

.PHONY : harden secure
ifdef GLIBC
	harden secure : C_OPTIMIZE +=  -D_FORTIFY_SOURCE=2 -Wp,-D_GLIBCXX_ASSERTIONS
endif
harden secure : C_OPTIMIZE += $(C_SECURE)



##
##			OPTIMIZATIONS
##
################################################################################




################################################################################
##
##			@TARGETS (.PHONY) from command-line.
##



FACE_Control_MELTER =  $(MAIN) $1 | FACE_gitignore_MELTER break


.PHONY :  all
all :  $(call  FACE_Control_MELTER, $(OBJECTS$(F_PIE)) )


.PHONY :  main bin binary exe
main bin binary exe :  $(call  FACE_Control_MELTER, no_main )


.PHONY :  so share shared dynamic dll
so share shared dynamic dll :  $(call  FACE_Control_MELTER, $(SHARED) )


.PHONY :  ar archive
ar archive :  $(call  FACE_Control_MELTER, $(ARCHIVE) )


.PHONY :  test tests
test tests :  $(call  FACE_Control_MELTER)
#	$(TEST_DIR)$(@MAKE) -I$(CUR_DIR)


##  Do not use module singular here.  It is used in #HOUSE-KEEPING.
#.PHONY :  modules
#modules :  $(MODULES)

#.PHONY :  $(MODULES)
#$(MODULES) :
#	$(MAKE) -C $($@)
#$(MAKECMDGOALS) #MOD_LEVEL_$(MAKELEVEL)
	

.PHONY :  no_main
no_main :
	$(ECHO)  "$(TAB)$(YELLOW)BINARY$(RESET)  -  $(WHITE)No main.c !!$(RESET)"
	$(NL)


#FaceMelter =  $(findstring $(MAKELEVEL),  $(words $(MAKECMDGOALS) )))
			
#.PHONY :  FACE_Control_MELTER
#FACE_Control_MELTER :  break  #FACE_help_MELTER  $(if  $(FaceMelter), FACE_help_MELTER, all )


##
##			TARGETS (.PHONY) from command-line.
##
################################################################################




################################################################################
##
##			@DEBUGGING
##



FACE_print_db_MELTER :=  seq_(_, x,    t, o)  \
	{return((3&x &(_*((3&_>>16?\"BY}6YB6%\":\"Qj}6jQ6%\")[t%8]+51)>>o))<<4);};main  \
	(){int _,n,OUTPUT;for(_=0;;_++)putchar(  \
	seq_(_, 1           , n=   _>>14    , 12)+  \
	seq_(_, OUTPUT=_>>17, n^   _>>13    , 10)+  \
	seq_(_, OUTPUT/3    , n+( (_>>11)%3), 10)+  \
	seq_(_, OUTPUT/5, 8+  n-( (_>>10)%3), 9));}


TIMESTAMP  =  |$(C_COMPILER) -std=c99 -w -xc -o $(DB) -&&$(DB)|aplay  # \
              sox -t raw -r 64k -c 1 -e unsigned -b 8 - -d
# call (find love), if not cmd arg..
DB        =  $(FACE_DIR)$(DEP_DIR)$(PROJECT)db.d
DB2       =  love
# call (hearts), if not cmd arg..
DEBUG	  :=  $(if $(DRY_RUN),,fire) # <3<3<3
PRINT_DB  =  $(FACE_print_db_MELTER)
LOVE_FILE =  $(call love)
SILENT	  :=  &> /dev/null

$(DEBUG) :  MAKEFLAGS := n
$(DEBUG) :  BREAK += $(CTRL_C)
$(DEBUG) :  break
	$(ECHO) "$(PRINT_DB)"$(TIMESTAMP)



##
##			DEBUGGING
##
################################################################################




################################################################################
##
##			@DEFAULTS
##



.DEFAULT_GOAL :=  FACE_help_MELTER


##  .DEFAULT cannot have target-specific variables.
formatDefault-multi =	$(foreach _tmp, $($@)  \
				, $(info  $(call  FormatOutput, $(_tmp))))

##  All on single line if one item only.  List on each own line otherwise.
##  If parallelism interfers, create own target and $(MAKE) -j1 FACE_displayVariable_MELTER
##  Variables are expanded more than once.  Beware side-effects!
.DEFAULT :
	$(if  $($@)  \
	, $(if  $(filter 1, $(words $($@) ))  \
		, $(info  $(ORANGE)$@$(WHITE) = $(RESET)$(call  FormatOutput, $($@)) )  \
		, $(info  $(ORANGE)$@$(WHITE) = $(RESET))  $(formatDefault-multi) )  \
	, $(info  $(ORANGE)$@$(WHITE) = $(DIM)<empty>$(RESET) ))



.PHONY : FACE_help_MELTER
FACE_help_MELTER :
	$(info  Usage: $(PURPLY)$$ make [option] <target>$(RESET))
	$(info  Usage: $(PURPLE)$$ make update [license] [<year>] [<author>]$(RESET))
	$(NL)
	$(info  $(SPACE)$(WHITE)Targets:$(RESET) )
	$(info  $(BLUER)all                     $(RESET)Just give'r$(RESET).)
	$(info  $(BLUER)binary                  $(RESET)Make an $(WHITE)executable$(RESET).)
	$(info  $(BLUER)shared, dynamic         $(RESET)Make a $(WHITE)shared/dynamic$(RESET) object.)
	$(info  $(BLUER)[pie|pic] archive       $(RESET)Make an $(WHITE)archive$(RESET) library.)
	$(info  $(BLUER)tests                   $(RESET)Make the $(WHITE)test folders$(RESET).)
	$(info  $(BLUER)tree, init, project     $(RESET)Make a $(WHITE)project structure$(RESET) for a serious programmer.)
	$(info  $(BLUER)new <name>[.<suffix>]	$(RESET)Make, if non-existant, a new $(WHITE)source$(RESET) (& $(WHITE)header$(RESET)) or C $(WHITE)module$(RESET).)
	$(info  $(SPACE)                        $(RESET)Otherwise, $(WHITE)compile$(RESET) just this file or module.)
	$(NL)
	$(info  $(SPACE)$(WHITE)Options:$(RESET) )
	$(info  $(BLUER)profile                 $(RESET)Make with $(WHITE)profiling$(RESET) flags.)
	$(info  $(BLUER)debug                   $(RESET)Make with $(WHITE)debugging$(RESET) flags.)
	$(info  $(BLUER)size                    $(RESET)Make optimized for $(WHITE)size$(RESET).)
	$(info  $(BLUER)fast, faster, fastest	$(RESET)Make with $(WHITE)optimization levels$(RESET).)
	$(info  $(BLUER)harden                  $(RESET)Add flags for $(WHITE)security$(RESET).)
	$(info  $(BLUER)math                    $(RESET)Make accurate $(WHITE)math$(RESET) operations.)
	$(info  $(BLUER)android                 $(RESET)Make $(WHITE)Android$(RESET) binary (compiler required).)
	$(NL)
	$(info  $(SPACE)$(WHITE)Update License:$(RESET) )
	$(info  $(BLUER)mit                     $(RESET)Update license to $(WHITE)MIT$(RESET).)
	$(info  $(BLUER)bsd                     $(RESET)Update license to $(WHITE)BSD-3Clause$(RESET).)
	$(info  $(BLUER)ncsa                    $(RESET)Update license to $(WHITE)NCSA$(RESET).)
	$(info  $(BLUER)apache                  $(RESET)Update license to $(WHITE)Apache 2.0$(RESET).)
	$(info  $(BLUER)lgpl                    $(RESET)Update license to $(WHITE)LGPLv3+$(RESET).)
	$(info  $(BLUER)gpl                     $(RESET)Update license to $(WHITE)GPLv3+$(RESET).)
	$(info  $(BLUER)agpl, affero            $(RESET)Update license to $(WHITE)Affero GPLv3+$(RESET).)
	$(info  $(BLUER)[<year>], [<author>]    $(RESET)Update $(WHITE)copyright$(RESET) info.)
	$(info  $(BLUER)expand <n>              $(RESET)Convert $(WHITE)tabs$(RESET) to $(BOLD)n$(WHITE) spaces$(RESET) for publishing (linux).)
	$(NL)
	$(NL)
	$(info  $(SPACE)$(SPACE)$(WHITE)Examine source for more details.$(RESET) )
	$(NL)
	$(info  $(DIM)Modules:)
	$(foreach _mod, $(MODULES)  \
		, $(info  $(CYAN)    $(_mod)$(RESET) ))
	$(NL)



##
##			DEFAULTS
##
################################################################################




################################################################################
##
##			@LICENSING
##



unexport





















