

CPPFLAGS=-I../interfaces
BIN_DIR=../bin
COMPONENTS_NEEDED=Hash
COMPONENTS_DIR=../lib
COMPONENTS_FILES=${COMPONENTS_NEEDED:%=${COMPONENTS_DIR}/lib%.so}
LD_COMPONENTS=${COMPONENTS_NEEDED:%=-l%}
LDFLAGS=-L ${COMPONENTS_DIR} ${LD_COMPONENTS}
EXE = main
OBJS = main.o

include ../gcc.mk

all: ${COMPONENTS_FILES} ${EXE}

${COMPONENTS_FILES}:
	echo "entrer le repertoire contenant la hash" && read COMPONENTS_DIRNAMES && echo $${COMPONENTS_DIRNAMES}; \
	for component in $${COMPONENTS_DIRNAMES}; do \
		cd ../$$component; \
		${MAKE} install;  \
	done

clean:
	rm -f ${OBJS} ${EXE} ${COMPONENTS_FILES}; \
	for component in $${COMPONENTS_DIRNAMES}; do \
                cd ../$$component; \
                ${MAKE} clean;  \
        done; \
	rm -fr ${BIN_DIR}

install:${BIN_DIR} all
	cp ${EXE} ${BIN_DIR}; \
	cp ${COMPONENTS_FILES} ${BIN_DIR}

${BIN_DIR}:
	mkdir $@

