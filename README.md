from tkinter import *

#Variable
textbox_width = 40
textbox_height = 1
button_width = 10
alphabet = "abcdefghijklmnopqrstuvwxyz"

#Functions
def quit_cypher():
    window.withdraw()
    window.quit()

def encode():
    coded_text =""
    text = encode_text.get()
    key = cypher_key.get()
    
    for letter in text:
        if letter in alphabet:

            #Add key to the index of the original letter
            i =alphabet.find(letter) + key

            #Update the code text
            coded_text = coded_text + alphabet[i % 26]

        else:
            coded_text =  coded_text + letter
            
        decode_text.delete(0, END)
        decode_text.insert(0, coded_text)
    
def decode():
    coded_text = ""
    text = decode_text.get()
    key = cypher_key.get()
    
    for letter in text:
        if letter in alphabet:
            
            #Add key to the index of the original letter
            i =alphabet.find(letter) - key
                
            #Update the code text
            coded_text = coded_text + alphabet[i % 26]
                    
        else:
            coded_text =  coded_text + letter
            
        encode_text.delete(0, END)
        encode_text.insert(0, coded_text)   

def clear_text():
    encode_text.delete(0, END)
    decode_text.delete(0, END)

###Main
window=Tk()
window.title("cypher")

#Do Stuff
input_label = Label(window, text="Input:")
input_label.grid(row=0, column=0)
encode_text = Entry(window, width=textbox_width, background="white")
encode_text.grid(row=0, column=1, columnspan=3, sticky=W)

output_label = Label(window, text="Output:")
output_label.grid(row=1, column=0)
decode_text = Entry(window, width=textbox_width, background="white")
decode_text.grid(row=1, column=1, columnspan=3, sticky=W)

#Create the cypher key dropdown
options = tuple(range(1,27))
cypher_key = IntVar()
cypher_key.set("1") #initial value
dropdown = OptionMenu(window, cypher_key, *options)
dropdown.grid(row=0, column=4, sticky=E)

#Create Title

#Add Buttons
button_quit = Button(window, text ="Quit", width=10, command=quit_cypher)
button_quit.grid(row=2, column=4, sticky=N)

button_encode = Button(window, text="Encode", width=button_width, command=encode)
button_encode.grid(row=2, column=1)

button_decode = Button(window, text="Decode", width=button_width, command=decode)
button_decode.grid(row=2, column=2)

button_clear = Button(window, text="Clear", width=button_width, command=clear_text)
button_clear.grid(row=2, column=3)

###Run Main loop
window.mainloop()
