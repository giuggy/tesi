CC     = gcc
CFLAGS = -ggdb -Wall
LDFLAGS = -lpthread -lrt


all: md5crack md5crack_verbose
	
enum_v.o: enum.h sort.h enum.c
	$(CC) $(CFLAGS) -DVERBOSE -c enum.c -o enum_v.o

enum.o: enum.h sort.h enum.c
	$(CC) $(CFLAGS) -c enum.c -o enum.o

md5.o:  md5.h md5.c
	$(CC) $(CFLAGS) -c md5.c -o md5.o
	
main.o: md5.h enum.h sort.h main.c 
	$(CC) $(CFLAGS) -c main.c -o main.o
	
sort.o: sort.h sort.c 
	$(CC) $(CFLAGS) -c sort.c -o sort.o

md5crack: md5.o enum.o main.o sort.o
	$(CC) $(CFLAGS) main.o md5.o enum.o sort.o -o md5crack $(LDFLAGS)
		

md5crack_verbose: md5.o enum_v.o main.o sort.o
	$(CC) $(CFLAGS) main.o md5.o enum_v.o sort.o -o md5crack_verbose $(LDFLAGS)
	

.PHONY : test test-osx
test:
	@rm -f list.tmp	
	@echo -n 'pctips' | md5sum >> list.tmp
	@echo -n 'a5' | md5sum >> list.tmp
	@echo -n 'uno' | md5sum >> list.tmp
	@echo -n 'lupin71' | md5sum >> list.tmp
	@echo -n 'x' | md5sum >> list.tmp
	@echo -n 'test' | md5sum >> list.tmp
	@echo -n 'ida13' | md5sum >> list.tmp
	@./md5crack_verbose list.tmp

test-osx:
	@rm -f list.tmp	
	md5 -q -s pctips >> list.tmp
	md5 -q -s a5 >> list.tmp
	md5 -q -s uno >> list.tmp
	md5 -q -s lupin71 >> list.tmp
	md5 -q -s x >> list.tmp
	md5 -q -s test >> list.tmp
	@./md5crack_verbose list.tmp

.PHONY : clean	
clean:
	rm -f md5crack md5crack_verbose *.o list.tmp
