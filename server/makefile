# default value which can be overridden by env variable
BUFLEN ?= 4
DELAY  ?= 2000
port   ?= 8080

build: server.sv server.c
	verilator --cc --exe --build --timing --main \
	-CFLAGS "-DBUFLEN=${BUFLEN} -I${PWD}/.." +incdir+.. \
	server.sv server.c --top-module server \
	-LDFLAGS "-lssl -lcrypto"
# "make link" only if --build is not used
link:
	make -j -C obj_dir -f Vserver.mk Vserver 
run:
	obj_dir/Vserver
run_verbose:
	obj_dir/Vserver +verbose +delay=40
run_stats:
	obj_dir/Vserver +delay=${DELAY}
clean:
	rm -rf obj_dir

-include ssl.mk
