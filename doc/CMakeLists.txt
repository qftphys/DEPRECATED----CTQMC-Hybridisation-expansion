# generate the conf.py
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/conf.py.in ${CMAKE_CURRENT_BINARY_DIR}/conf.py)

# all rst files of the documentation
file(GLOB_RECURSE doc_sources *.rst)

# create documentation target
set(sphinx_top ${CMAKE_CURRENT_BINARY_DIR}/html/index.html)
add_custom_command(OUTPUT ${sphinx_top} DEPENDS ${doc_sources} py_copy cthyb_matrix cthyb_matrix_c cython_cthyb_matrix
                   COMMAND ${CMAKE_BINARY_DIR}/build_pytriqs ${TRIQS_SPHINXBUILD_EXECUTABLE} -c . -b html ${CMAKE_CURRENT_SOURCE_DIR} html)
add_custom_target(doc_sphinx ALL DEPENDS ${sphinx_top})

# install
install(DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/html/ COMPONENT documentation DESTINATION share/doc/cthyb_matrix
 FILES_MATCHING 
 PATTERN "*.html" 
 PATTERN "*.png"
 PATTERN "*.js"
 PATTERN "_*"
 PATTERN "*.png" 
 PATTERN "*.jpg" 
 PATTERN "*.gif" 
 PATTERN "*.xsl" 
 PATTERN "*.css"
 PATTERN "*.pdf"
 PATTERN "*.py"
 PATTERN "*.txt"
 PATTERN "*.inv"
 PATTERN "*.bib"
 )
