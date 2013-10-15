#-----------------------------------------------------------------------------
# include directories
#-----------------------------------------------------------------------------
include_directories(${CMAKE_CURRENT_SOURCE_DIR})
if(WIN32)
  include_directories(${FASTBIT_SOURCE_DIR}/win)
  set(FASTBIT_WIN32_LIBS psapi)
endif(WIN32)

#-----------------------------------------------------------------------------
# main ibis lib src files
#-----------------------------------------------------------------------------
set(FASTBIT_SRCS 
	array_t.cpp      category.cpp     fromLexer.cc   idirekte.cpp   isapid.cpp   ixpack.cpp     part.cpp      party.cpp         selectParser.cc
	bitvector.cpp    colValues.cpp    fromParser.cc  ifade.cpp      isbiad.cpp   ixpale.cpp     parth.cpp     qExpr.cpp         tafel.cpp
	bitvector64.cpp  column.cpp       ibin.cpp       ikeywords.cpp  iskive.cpp   ixzona.cpp     parth2d.cpp   quaere.cpp        util.cpp
	blob.cpp         countQuery.cpp   icegale.cpp    imesa.cpp      islice.cpp   ixzone.cpp     parth3d.cpp   query.cpp         utilidor.cpp
	bord.cpp         dictionary.cpp   icentre.cpp    index.cpp      ixambit.cpp  jnatural.cpp   parth3da.cpp  resource.cpp      whereClause.cpp
	bordm.cpp        fileManager.cpp  icmoins.cpp    irange.cpp     ixbylt.cpp   jrange.cpp     parth3db.cpp  rids.cpp          whereLexer.cc
	bundle.cpp       filter.cpp       idbak.cpp      irelic.cpp     ixfuge.cpp   mensa.cpp      parth3dw.cpp  selectClause.cpp  whereParser.cc
	capi.cpp         fromClause.cpp   idbak2.cpp     iroster.cpp    ixfuzz.cpp   meshQuery.cpp  parti.cpp     selectLexer.cc
)

add_library(fastbit ${FASTBIT_SRCS})

target_link_libraries(fastbit 
  ${FASTBIT_WIN32_LIBS} 
  ${CMAKE_THREAD_LIBS_INIT}
)
