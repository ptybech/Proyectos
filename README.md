# Generador-de-Contraseñas
El Generador de contraseñas, puede mezclar aleatoriamente, letras, números y simbolos,  y tambien se le adapta una logitud para generar un password con un nivel de seguridad mas fuerte.

#Importamos las librerias y funciones
import tkinter
import string, random, os
from typing import Self
import customtkinter
from PIL import Image

#Configuracion del ambiente (apariencia, color)
customtkinter.set_appearance_mode("dark")  # Modes: system (default), light, dark
customtkinter.set_default_color_theme("blue")  # Themes: blue (default), dark-blue, green

#PRIMER BLOQUE
#Creación de la ventana principal, configuración y personalización del app.
black = '010101'
app = customtkinter.CTk()  # create CTk window like you do with the Tk window
app.geometry("380x675+620+75")
app.config(bg ="black")
app.title('PASSWORD GENERATOR')
app.iconbitmap('C:\\Users\\jguadamuz\\Documents\\PROYECTOS PY\\iconoCSS3.ico')#Insertamos la imagen del logo como Icono del app.

#insertamos las Imagenes del logo y del fondo bg.
logo = customtkinter.CTkImage(dark_image=Image.open('CSS3.jpg'), size =(280, 100)) 
fondo_bg = customtkinter.CTkImage(dark_image=Image.open('DarkBlue.jpg'), size =(940, 675))

#Creacion de widgets frame y Label para almacenar la imagen del fondo bg.
frame_bg=customtkinter.CTkFrame(master=app,
                              #image=fondo_bg,
                              width=940,
                              height=675,
                              bg_color='black',
                              fg_color=('light gray', 'white'),
                              corner_radius=10)
frame_bg.place(relx=0.5, rely=0.5, anchor=tkinter.CENTER)

lbl_fondobg=customtkinter.CTkLabel(master=app,
                          image=fondo_bg,
                          text="",
                          bg_color='black',
                          #fg_color=('gray'),
                          width=281,
                          height=105,
                          corner_radius=5)
lbl_fondobg.place(relx=0.5, rely=0.5, anchor=tkinter.CENTER) 

#Creación del label para mostrar y almacenar el logo del app en la parte superior
lbl_logoapp=customtkinter.CTkLabel(master=app,
                          image=logo,
                          text="",
                          bg_color='black',
                          #fg_color=('gray'),
                          width=281,
                          height=105,
                          corner_radius=5)
lbl_logoapp.place(relx=0.5, rely=0.15, anchor=tkinter.CENTER)


#SEGUNDO BLOQUE
#Creación de widgets para operar las funciones.

Title_Password = customtkinter.CTkLabel(master=app,
                               text="PASSWORD",
                               width=100,
                               height=30,
                               bg_color='black',
                               fg_color=('transparent'),
                               font=customtkinter.CTkFont(size=17, weight="bold"),
                               corner_radius=8)
Title_Password.place(relx=0.5, rely=0.3, anchor=tkinter.CENTER)

Title_Lenght = customtkinter.CTkLabel(master=app,
                               text="LENGHT",
                               width=50,
                               height=30,
                               bg_color='black',
                               corner_radius=8, fg_color='transparent')
Title_Lenght.place(relx=0.5, rely=0.415, anchor=tkinter.CENTER)

Title_Language = customtkinter.CTkLabel(master=app,
                               text="LANGUAGE",
                               width=50,
                               height=30,
                               bg_color='black',
                               fg_color='transparent',
                               font=customtkinter.CTkFont(size=15, weight="bold"),
                               corner_radius=8)
Title_Language.place(relx=0.5, rely=0.798, anchor=tkinter.CENTER)


   
def slider_event(value):
    label_slider.configure(text=int(value))
    #print(value)

  
def button_function():
    slider_value = int(slider.get())
    
    chars = string.ascii_uppercase

    if checkbox_letters.get():
        chars += string.ascii_letters
    
    if checkbox_digits.get():    
        chars += string.digits
        
    if  checkbox_punctuation.get():  
        chars += string.punctuation    
        
    password = ''.join(random.choice(chars) for i in range(slider_value))
    
    label_password.configure(text=password)   
    
#widgets generadores de password aleatorio
    
slider = customtkinter.CTkSlider(master=app,
                                 from_=0,
                                 to=30,
                                 width=250,
                                 height=16,
                                 border_width=5.5,
                                 bg_color='black',
                                 command=slider_event)
slider.place(relx=0.5, rely=0.45, anchor=tkinter.CENTER)
#repositorio
label_password = customtkinter.CTkLabel(master=app,
                                text= "",
                                text_color='black',
                                width=250,
                                height=30,
                                bg_color='transparent',
                                corner_radius=20, 
                                font=customtkinter.CTkFont(size=12, weight="bold"),
                                fg_color=('light gray'))
label_password.place(relx=0.5, rely=0.35, anchor='center')    
    
label_slider = customtkinter.CTkLabel(master=app,
                                text= "",
                                text_color='white',
                                width=50,
                                height=30,
                                bg_color='black',
                                corner_radius=15, 
                                font=customtkinter.CTkFont(size=12, weight="bold"),
                                fg_color=('transparent'))
label_slider.place(relx=0.52, rely=0.415, anchor='center')

button_Generador = customtkinter.CTkButton(master=app,
                                 text="GENERATE",
                                 fg_color='blue',
                                 command=button_function,
                                 width=60,
                                 height=30,
                                 border_width=0,
                                 corner_radius=8)
button_Generador.place(relx=0.5, rely=0.73, anchor=tkinter.CENTER)


#marco para abmientar los checkbox, en este bloque definimos las funciones para los checkbox
frame_Checkbox = customtkinter.CTkFrame(master=app,
                               width=350,
                               height=150,
                               bg_color='black',
                               fg_color='black',
                               corner_radius=10)
frame_Checkbox.place(relx=0.5, rely=0.6, anchor='center')

def checkbox_event1():
    string.ascii_letters
    #ack(padx=20, pady=10, anchor='w')

def checkbox_event2():
    string.digits
    #print("string.digits")

def checkbox_event3():
    string.punctuation
    #print("string.punctuation")

checkbox_letters = customtkinter.CTkCheckBox(frame_Checkbox, text="LETTER", 
                                       command=checkbox_event1)
checkbox_letters.pack(padx=20, pady=10, anchor='w')
    
checkbox_digits = customtkinter.CTkCheckBox(frame_Checkbox, text="NUMBERS", 
                                       command=checkbox_event2)
checkbox_digits.pack(padx=20, pady=10, anchor='w')    

checkbox_punctuation = customtkinter.CTkCheckBox(frame_Checkbox, text="PUNCTUATION",
                                       command=checkbox_event3)
checkbox_punctuation.pack(padx=20, pady=10, anchor='w')

#Definimos las funciones de los botones para el cambio de lenguaje
frame_Botones= customtkinter.CTkFrame(master=app,
                               width=250,
                               height=100,
                               bg_color='black',
                               fg_color='black',
                               corner_radius=10)
frame_Botones.place(relx=0.5, rely=0.9, anchor='center')

def button_event1():
   
    def slider_event(value):
        label_slider.configure(text=int(value))
    
    def button_function():
        slider_value = int(slider.get())
    
        chars = string.ascii_uppercase

        if checkbox_letters.get():
            chars += string.ascii_letters
    
        if checkbox_digits.get():    
            chars += string.digits
        
        if  checkbox_punctuation.get():  
            chars += string.punctuation    
        
        password = ''.join(random.choice(chars) for i in range(slider_value))
    
        label_password.configure(text=password)   
    
    label_password = customtkinter.CTkLabel(master=app,
                                text= "",
                                text_color='black',
                                width=250,
                                height=30,
                                bg_color='transparent',
                                corner_radius=20, 
                                font=customtkinter.CTkFont(size=12, weight="bold"),
                                fg_color=('light gray'))
    label_password.place(relx=0.5, rely=0.35, anchor='center')
    
    Title_Password = customtkinter.CTkLabel(master=app,
                               text="PASSWORD",
                               width=150,
                               height=30,
                               bg_color='black',
                               fg_color=('transparent'),
                               font=customtkinter.CTkFont(size=17, weight="bold"),
                               corner_radius=8)
    Title_Password.place(relx=0.5, rely=0.3, anchor=tkinter.CENTER)
    
    Title_Lenght = customtkinter.CTkLabel(master=app,
                               text="LENGHT",
                               width=50,
                               height=30,
                               bg_color='black',
                               corner_radius=8, fg_color='transparent')
    Title_Lenght.place(relx=0.5, rely=0.415, anchor=tkinter.CENTER)
    
    Title_Language = customtkinter.CTkLabel(master=app,
                               text="LANGUAGE",
                               width=50,
                               height=30,
                               bg_color='black',
                               fg_color='transparent',
                               font=customtkinter.CTkFont(size=15, weight="bold"),
                               corner_radius=8)
    Title_Language.place(relx=0.5, rely=0.798, anchor=tkinter.CENTER)
    
    frame_Botones= customtkinter.CTkFrame(master=app,
                               width=250,
                               height=100,
                               bg_color='black',
                               fg_color='black',
                               corner_radius=10)
    frame_Botones.place(relx=0.5, rely=0.9, anchor='center')
    
    button_Generador = customtkinter.CTkButton(master=app,
                                 text="GENERATE",
                                 fg_color='blue',
                                 command=button_function,
                                 width=100,
                                 height=30,
                                 border_width=0,
                                 corner_radius=8)
    button_Generador.place(relx=0.5, rely=0.73, anchor=tkinter.CENTER)
    
    button_English = customtkinter.CTkButton(frame_Botones,
                                 text="ENGLISH",
                                 fg_color='blue',
                                 command=button_event1,
                                 width=100,
                                 height=30,
                                 border_width=0,
                                 corner_radius=8)
    button_English.pack(padx=20, pady=10, anchor='center')
    
    button_Spanish = customtkinter.CTkButton(frame_Botones,
                                 text="SPANISH",
                                 fg_color='blue',
                                 command=button_event2,
                                 width=100,
                                 height=30,
                                 border_width=0,
                                 corner_radius=8)
    button_Spanish.pack(padx=20, pady=10, anchor='center')
    
    frame_Checkbox = customtkinter.CTkFrame(master=app,
                               width=350,
                               height=150,
                               bg_color='black',
                               fg_color='black',
                               corner_radius=10)
    frame_Checkbox.place(relx=0.5, rely=0.6, anchor='center')
   
    checkbox_letters = customtkinter.CTkCheckBox(frame_Checkbox, text="LETTER", 
                                       command=checkbox_event1)
    checkbox_letters.pack(padx=20, pady=10, anchor='w')
    
    checkbox_digits = customtkinter.CTkCheckBox(frame_Checkbox, text="NUMBERS", 
                                       command=checkbox_event2)
    checkbox_digits.pack(padx=20, pady=10, anchor='w')    

    checkbox_punctuation = customtkinter.CTkCheckBox(frame_Checkbox, text="PUNCTUATION",
                                       command=checkbox_event3)
    checkbox_punctuation.pack(padx=20, pady=10, anchor='w')
    
button_English = customtkinter.CTkButton(frame_Botones,
                                 text="ENGLISH",
                                 fg_color='blue',
                                 command=button_event1,
                                 width=60,
                                 height=30,
                                 border_width=0,
                                 corner_radius=8)
button_English.pack(padx=20, pady=10, anchor='center')

def button_event2():
    def slider_event(value):
        label_slider.configure(text=int(value))
    
    def button_function():
        slider_value = int(slider.get())
    
        chars = string.ascii_uppercase

        if checkbox_letters.get():
            chars += string.ascii_letters
    
        if checkbox_digits.get():    
            chars += string.digits
        
        if  checkbox_punctuation.get():  
            chars += string.punctuation    
        
        password = ''.join(random.choice(chars) for i in range(slider_value))
    
        label_password.configure(text=password)   
    
    label_password = customtkinter.CTkLabel(master=app,
                                text= "",
                                text_color='black',
                                width=250,
                                height=30,
                                bg_color='transparent',
                                corner_radius=20, 
                                font=customtkinter.CTkFont(size=12, weight="bold"),
                                fg_color=('light gray'))
    label_password.place(relx=0.5, rely=0.35, anchor='center')   
    
    Title_Password = customtkinter.CTkLabel(master=app,
                               text="CONTRASEÑA",
                               width=100,
                               height=30,
                               bg_color='black',
                               fg_color=('transparent'),
                               font=customtkinter.CTkFont(size=17, weight="bold"),
                               corner_radius=8)
    Title_Password.place(relx=0.5, rely=0.3, anchor=tkinter.CENTER)
    
    Title_Lenght = customtkinter.CTkLabel(master=app,
                               text="LONGITUD",
                               width=50,
                               height=30,
                               bg_color='black',
                               corner_radius=8, fg_color='transparent')
    Title_Lenght.place(relx=0.5, rely=0.415, anchor=tkinter.CENTER)
    
    Title_Language = customtkinter.CTkLabel(master=app,
                               text="IDIOMA",
                               width=100,
                               height=30,
                               bg_color='black',
                               fg_color='transparent',
                               font=customtkinter.CTkFont(size=15, weight="bold"),
                               corner_radius=8)
    Title_Language.place(relx=0.5, rely=0.798, anchor=tkinter.CENTER)
    
    frame_Botones= customtkinter.CTkFrame(master=app,
                               width=250,
                               height=100,
                               bg_color='black',
                               fg_color='black',
                               corner_radius=10)
    frame_Botones.place(relx=0.5, rely=0.9, anchor='center')
    
    button_Generador = customtkinter.CTkButton(master=app,
                                 text="GENERADOR",
                                 fg_color='blue',
                                 command=button_function,
                                 width=100,
                                 height=30,
                                 border_width=0,
                                 corner_radius=8)
    button_Generador.place(relx=0.5, rely=0.73, anchor=tkinter.CENTER)
    
    button_English = customtkinter.CTkButton(frame_Botones,
                                 text="INGLES",
                                 fg_color='blue',
                                 command=button_event1,
                                 width=100,
                                 height=30,
                                 border_width=0,
                                 corner_radius=8)
    button_English.pack(padx=20, pady=10, anchor='center')
    
    button_Spanish = customtkinter.CTkButton(frame_Botones,
                                 text="ESPAÑOL",
                                 fg_color='blue',
                                 command=button_event2,
                                 width=100,
                                 height=30,
                                 border_width=0,
                                 corner_radius=8)
    button_Spanish.pack(padx=20, pady=10, anchor='center')
    
    frame_Checkbox = customtkinter.CTkFrame(master=app,
                               width=350,
                               height=150,
                               bg_color='black',
                               fg_color='black',
                               corner_radius=10)
    frame_Checkbox.place(relx=0.5, rely=0.6, anchor='center')
    
    checkbox_letters = customtkinter.CTkCheckBox(frame_Checkbox, text="LETRAS", 
                                       command=checkbox_event1)
    checkbox_letters.pack(padx=20, pady=10, anchor='w')
    
    checkbox_digits = customtkinter.CTkCheckBox(frame_Checkbox, text="NUMEROS", 
                                       command=checkbox_event2)
    checkbox_digits.pack(padx=20, pady=10, anchor='w')    

    checkbox_punctuation = customtkinter.CTkCheckBox(frame_Checkbox, text="SIMBOLOS",
                                       command=checkbox_event3)
    checkbox_punctuation.pack(padx=20, pady=10, anchor='w')
    
button_Spanish = customtkinter.CTkButton(frame_Botones,
                                 text="SPANISH",
                                 fg_color='blue',
                                 command=button_event2,
                                 width=60,
                                 height=30,
                                 border_width=0,
                                 corner_radius=8)
button_Spanish.pack(padx=20, pady=10, anchor='center')

app.mainloop()
