<h1 align="center"> PDF Text Extractor</h1>

[![Made With - Python](https://img.shields.io/badge/Made_With-Python-2ea44f?style=for-the-badge&logo=python)](https://python.org)

---
This repository contains a python file that allows you to extract the text of a pdf file.

<h3 align="center">Code Structure </h3>
The code is composed of the following parts:

1. Import the required libraries:
```py
import tkinter as tk
import PyPDF2
from PIL import Image, ImageTk
from tkinter.filedialog import askopenfile
```
2. Create the basic grid of our app:
```py
root = tk.Tk()

canvas = tk.Canvas(root, width=600, height=300)
canvas.grid(columnspan=3, rowspan=3)


#Logo
logo = Image.open('image.png')
logo = ImageTk.PhotoImage(logo)
logo_label = tk.Label(image=logo)
logo_label.image = logo
logo_label.grid(column=1, row=0)
```
3. We will now create the basic instructions and the function thath will allow us to open the file and extract the text:
```py
#Instructions
instructions = tk.Label(root, text="Select a PDF file on your computer to extract its text: ", font="Raleway")
instructions.grid(columnspan=3, column=0, row=1)

#Function to open file:
def open_file():
    browse_text.set("Loading...")
    file = askopenfile(parent=root, mode='rb', title="Choose a file", filetype=[("Pdf file", "*.pdf")])
    if file:
       read_pdf = PyPDF2.PdfFileReader(file)
       page = read_pdf.getPage(0)
       page_content = page.extractText()

       #Text Box
       text_box = tk.Text(root, height=10, width=50, padx=15, pady=15)
       text_box.insert(1.0, page_content)
       text_box.tag_configure("center", justify="center", font="Raleway")
       text_box.tag_add("center", 1.0, "end")
       text_box.grid(column=1, row=3)

       #Browse Text
       browse_text.set("Browse")
```
4. The next step is to create the browse button, which will allow us to search for our pdf file:
```py
#Browse button
browse_text = tk.StringVar()
browse_btn = tk.Button(root, textvariable=browse_text, command=lambda:open_file(), font="Raleway", bg="#20bebe", fg="white", height=2, width=15)
browse_text.set("Browse")
browse_btn.grid(column=1, row=2)
```

5. In this final part of the code, we create a "blank space" at the bottom, so that the button or extracted text is not right above the margin, and whe call the funtion **root mainloop()** which ends the program:
```py
canvas = tk.Canvas(root, width=600, height=250)
canvas.grid(columnspan=3)

root.mainloop()
```
