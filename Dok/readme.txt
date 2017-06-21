Installation on OsX Sierra

 install xFitter on Sierra 
with XCode8.3+gfortran6.3 and after some failures found a bug in the
make files.

Actually the xFitter with XCode should be linked to c++  (from clang)
library and not to stdc++ (from gcc).

This means the src/Makefile.am  should be like


XFLIBS = ../DY/src/libmydy.a\
../Cascade/src/libcasutil.a \
../common/libHFcommon.a \
../RT/src/libmyrt.a \
../ACOT/src/libmyacot.a \
../SACOT/src/libmysacot.a \
../FONLL/src/libmyfonll.a \
../EW/src/libmyew.a \
../ABM/src/libmyabm.a \
../FastNLO/src/libFastNLO.a \
../DIPOLE/src/libmydipole.a \
../DiffDIS/src/libDiffDIS.a\
../interfaces/src/libinterfaces.a\
../minuit/src/libmyminuit.a $(CERNLIBS) @FLIBS@ \
../genetic/src/libgenetic.a \
../QEDevol/src/libQEDevol.a \
../common/num_utils/libnum_utils.a \
../tools/draw/src/pdferrors.o

#Pseudocode
if (   compiler is  gcc    )
XFLIBS+=  -lstdc++ 
end if 

if (   compiler is  clang    )
XFLIBS+=  -lc++ 
end if 

Change:
_______________________________________________
in src/Makefile.am und src/Makefile.in

../ABM/src/libmyabm.a \
../FastNLO/src/libFastNLO.a \
../DIPOLE/src/libmydipole.a \
../DiffDIS/src/libDiffDIS.a\
../interfaces/src/libinterfaces.a\
../minuit/src/libmyminuit.a $(CERNLIBS) @FLIBS@ \
 -lstdc++ \						->lc++\
../genetic/src/libgenetic.a \
../QEDevol/src/libQEDevol.a \
../common/num_utils/libnum_utils.a \
../tools/draw/src/pdferrors.o
________________________________________________