#-----------------------------------------------------------------------------
# Examples
#-----------------------------------------------------------------------------
include_directories(${FASTBIT_SOURCE_DIR}/src)

add_executable(ardea ardea.cpp)
target_link_libraries(ardea fastbit)


add_executable(ibis  ibis.cpp)
target_link_libraries(ibis fastbit)

add_executable(rara  rara.cpp)
target_link_libraries(rara fastbit)

add_executable(thula thula.cpp)
target_link_libraries(thula fastbit)

add_executable(tcapi tcapi.c)
target_link_libraries(tcapi fastbit)

#-----------------------------------------------------------------------------
# Tests
#-----------------------------------------------------------------------------

ADD_TEST(
  #----------------------------------------------------------------
  # Name of test (as appears on dashboard)
  #----------------------------------------------------------------   
  ardea_test_1 
    
  #----------------------------------------------------------------
  # Executable that will perform the test 
  #----------------------------------------------------------------
  ${PROJECT_BINARY_DIR}/bin/ardea
    
  #----------------------------------------------------------------
  # Args
  #----------------------------------------------------------------
  -d ${FASTBIT_TEST_DIR}/t0 
  -m "a:key, b:text, c:ushort" 
  -t ${FASTBIT_SOURCE_DIR}/tests/test0.csv

)   

ADD_TEST(
  ardea_test_acmpub
  ${PROJECT_BINARY_DIR}/bin/ardea
    
  #----------------------------------------------------------------
  # Args
  #----------------------------------------------------------------
	-d ${FASTBIT_TEST_DIR}/acmpub 
  -m "id:u, t:t, a:t, v:k, y:u" 
  -t ${FASTBIT_SOURCE_DIR}/tests/acmpub.csv 
)   

ADD_TEST(
  ardea_test_ibis
  ${PROJECT_BINARY_DIR}/bin/ardea
    
  #----------------------------------------------------------------
  # Args
  #----------------------------------------------------------------
	-d ${FASTBIT_TEST_DIR}/acmpub 
	-b "a:keywords delimiters=','" 
  -b "id:noindex" 
  -b "<binning none>" 
  -v 
)   

#-----------------------------------------------------------------------------
# Tests
#-----------------------------------------------------------------------------
#check-thula: $(THULAEXE) $(TESTDIR)/t1/-part.txt $(TESTDIR)/t2/t2a/-part.txt $(TESTDIR)/t2/t2b/-part.txt $(TESTDIR)/t2/t2c/-part.txt
#	@rm -f $(TESTDIR)/thula-0 $(TESTDIR)/thula-1
#	@$(THULAEXE) -d $(TESTDIR)/t1/ -w "a = 0" 2>&1 | if [ `fgrep " produced 2 hits out of 200 records" - | wc -l` -eq 1 ] ; then echo Passed $@ case 1; else echo Did NOT pass $@ case 1; fi
#	@$(THULAEXE) -d $(TESTDIR)/t1 -w "a = b and -1 < c < 10" 2>&1 | if [ `fgrep " produced 18 hits out of 200 records" - | wc -l` -eq 1 ] ; then echo Passed $@ case 2; else echo Did NOT pass $@ case 2; fi
#	@$(THULAEXE) -d $(TESTDIR)/t1 -w "-2 <= c < 10" -s "min(a/b), max(a/b), avg(a/b)" -x $(TESTDIR)/thula-0 >> $(TESTDIR)/std.log 2>&1 && if [ `diff -w vault/thula-0 $(TESTDIR)/thula-0 | wc -l` -eq 0 ] ; then echo Passed $@ case 3; else echo Did NOT pass $@ case 3; fi
#	@$(THULAEXE) -d $(TESTDIR)/t1 -w "a < c and b > 30" -s "b, min(b/c*c), max(sqrt(a/c)^2*c), countdistinct(a)/count(*)" -x $(TESTDIR)/thula-1 >> $(TESTDIR)/std.log 2>&1 && if [ `diff -w vault/thula-1 $(TESTDIR)/thula-1 | wc -l` -eq 0 ] ; then echo Passed $@ case 4; else echo Did NOT pass $@ case 4; fi
#	@$(THULAEXE) -d $(TESTDIR)/t2 -w "a between -1 and 1" 2>&1 | if [ `fgrep "t2) contains 14 rows but no column" - | wc -l` -eq 1 ] ; then echo Passed $@ case 5; else echo Did NOT pass $@ case 5; fi
#
ADD_TEST(
  thula_test_1
  ${PROJECT_BINARY_DIR}/bin/thula
    
  #----------------------------------------------------------------
  # Args
  #----------------------------------------------------------------
	-d ${FASTBIT_TEST_DIR}/t1 
	-w "a = 0"
)   
