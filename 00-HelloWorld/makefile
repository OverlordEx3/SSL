# Se define el compilador que se va a usar y sus flags.
CC = gcc
CFlags = -std=c23

# Regla de compilación: Toma como dependencia el archivo hello.c,
# y se lo pasa a GCC a través de la variable CC
hello: hello.c
	$(CC) hello.c -o hello

# Regla de ejecución: Toma el ejecutable compilado, lo ejecuta,
# y envía la salida al archivo 'output.txt' a la vez que lo
# muestra en pantalla con el comando 'tee'
run: hello
	./hello | tee output.txt

# Regla de limpieza: Borro el ejecutable y los archivos objeto.
# Nota: dejo el output para commitear.
clean:
	rm -f *.o hello

# Regla de limpieza 
clean-all: | clean
	rm -f output.txt