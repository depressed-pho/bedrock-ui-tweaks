#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ([2.69])
AC_INIT([Bedrock UI Tweaks],
        [1.1.1],
        [https://github.com/depressed-pho/bedrock-ui-tweaks/issues],
        [],
        [https://github.com/depressed-pho/bedrock-ui-twekas])
AM_INIT_AUTOMAKE([1.9])
AC_CONFIG_SRCDIR([src/manifest.json.in])
AC_CONFIG_MACRO_DIR([m4])
m4_pattern_forbid([^AX_])

AM_MAINTAINER_MODE
AM_SILENT_RULES([yes])

# Checks for options.
AX_MCPACK_INSTALLATION_DIRECTORY([resource])
AX_MCPACK_GENERATE_DIFF_FILE([no])

# Checks for programs.
AC_ARG_VAR([SED], [The sed command @<:@autodetected@:>@])
AC_PROG_SED
AS_IF([test "x$SED" = x],
      [AC_MSG_ERROR([You need to install a sed command.])])

AC_ARG_VAR([JQ], [The jq command @<:@autodetected@:>@])
AC_CHECK_PROGS([JQ], [jq])
AS_IF([test "x$JQ" = x],
      [AC_MSG_ERROR([You need to install the jq command.])])

AC_ARG_VAR([ZIP], [The Info-Zip zip command @<:@autodetected@:>@])
AC_CHECK_PROGS([ZIP], [zip])
AS_IF([test "x$ZIP" = x],
      [AC_MSG_ERROR([You need to install the Info-Zip zip command.])])

AC_ARG_VAR([UNZIP], [The Info-Zip unzip command @<:@autodetected@:>@])
AC_CHECK_PROGS([UNZIP], [unzip])
AS_IF([test "x$UNZIP" = x],
      [AC_MSG_ERROR([You need to install the Info-Zip unzip command.])])

AC_ARG_VAR([INKSCAPE], [The inkscape command @<:@autodetected@:>@])
AC_CHECK_PROGS([INKSCAPE], [inkscape])
AS_IF([test x"$INKSCAPE" = x],
      [AC_MSG_WARN([You need to install Inkscape, or you won't be able to regenerate the pack icon.])
       INKSCAPE=false])

# Checks for libraries.

# Checks for header files.

# Checks for typedefs, structures, and compiler characteristics.

# Checks for library functions.

AC_CONFIG_FILES([
    Makefile
    src/Makefile
])
AC_OUTPUT
