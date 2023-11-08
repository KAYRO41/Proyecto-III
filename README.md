### Titulo Proyecto III
### Curso: Algoritmos
### Nombre: Elmer Yunior Roblero Santos
### Carnter: 7690-23-14847
```python
from tkinter import *
import sys
from tkinter import filedialog

ventana = Tk()
ventana.geometry('1080x1020')

entrada_ubicacion = Text(ventana, font=('arial', 10))
entrada_ubicacion.grid(row=2, column=0, padx=20, pady=15)
entrada_ubicacion.config(width=40, height=2)

def buscar():
   
   ubicacion = entrada_ubicacion.get("1.0", "end-1c") 
   caja_principal.tag_delete("ubicacion") 
   inicio = "1.0" 
   while True:
        inicio = caja_principal.search(ubicacion, inicio, stopindex="end")
        if not inicio:
            break
        fin = f"{inicio}+{len(ubicacion)}c"
        caja_principal.tag_add("ubicacion", inicio, fin)
        inicio = fin 
        caja_principal.tag_configure("ubicacion", background="yellow") 
        caja_principal.see("ubicacion")


def copiar():
    caja_principal.event_generate("<<Copy>>")

def pegar():
    caja_principal.event_generate("<<Paste>>")

def hacer():
    caja_principal.event_generate("<<Undo>>")

def deshacer():
    caja_principal.event_generate("<<Redo>>")


def guardar_como():
    nuevo_path = filedialog.asksaveasfilename(defaultextension=".txt", filetypes=[("Archivos de texto", "*.txt")])
    
    if nuevo_path:
        contenido = caja_principal.get("1.0", "end-1c")
        if contenido:
            with open(nuevo_path, 'w') as archivo:
                archivo.write(contenido)
        else:
            print("No hay contenido para guardar.")
    else:
        print("Guardado cancelado o el nombre de archivo esta vacio.")

menu = Menu(ventana)
ventana.config(menu=menu)

menu_editar = Menu(menu)
menu.add_cascade(label="Editar", menu=menu_editar)
menu_editar.add_command(label="Copiar (Ctrl+C)", command=copiar)
menu_editar.add_command(label="Pegar (Ctrl+V)", command=pegar)
menu_editar.add_command(label="Hacer (Ctrl+Z)", command=hacer)
menu_editar.add_command(label="Deshacer (Ctrl+Y)", command=deshacer)

 
mensaje = Label(ventana, text='ruta', font=('Verdana', 18))
mensaje.grid(row=0, column=0)

def abrir():
   'proyecto.txt' 
   archivo = open(__path__, 'r')  
   print(caja_principal)
    
caja_principal=Text(ventana, font=('arial', 10))
caja_principal.grid(row= 4, column=0, padx= 20, pady= 15)
caja_principal.config(yscrollcommand=caja_principal.yview)
caja_principal = Scrollbar(ventana, command=caja_principal.yview)


botonabrir=Button(ventana,text="Abrir", command=abrir)
botonabrir.config(width=10, height=3)
botonabrir.grid(row=1, column=5, padx= 20, pady= 15)
def leer():
    path = 'proyecto.txt'
    archivo = open(path,'r')
    print  (caja_principal.insert(END, archivo.read()))

botonleer=Button(ventana, text='Leer', command=leer)
botonleer.config(width=10, height=3)
botonleer.grid(row=200, column=100, padx= 20, pady= 15)

ruta_archivo = Text(ventana, font=('arial', 10))
ruta_archivo.grid(row=1, column=0, padx=20, pady=15)
ruta_archivo.config(width=40, height=2)

scrollvertical = Scrollbar(ventana, command=ruta_archivo.yview)
scrollvertical.grid(row=1, column=1, sticky='nsew')

ruta_archivo.config(yscrollcommand=scrollvertical.set)

ruta_archivo.insert(END, "Ruta del archivo: /ruta/del/archivo.txt")

def salir():
    sys.exit()
    
def guardar():
    path = 'proyecto.txt'
    with open(path, 'w') as archivo:
        contenido = caja_principal.get("1.0", END)
        archivo.write(contenido)
    

guardar_boton = Button(ventana, text='Guardar', command=guardar)
guardar_boton.config(width=10, height=3)
guardar_boton.grid(row= 200, column=300)

salir_boton = Button(ventana, text='Salir', command=salir)
salir_boton.config(width=10, height=3)
salir_boton.grid(row= 200, column=2000)

if __name__ == '__main__':
 ventana.mainloop() 
```
