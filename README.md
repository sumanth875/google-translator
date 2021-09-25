#you use this code to implement google translator
#in output you need to give the languages of input and destination
from tkinter import *
from tkinter import ttk,messagebox
import googletrans
from googletrans import Translator
from gtts import gTTS 
import os
import speech_recognition as sr
import pyttsx3


root=Tk()
root.title("sumanth translator")
root.geometry("1080x350")

def label_change():
    c=combo1.get()
    c1=combo2.get()
    label1.configure(text=c)
    label2.configure(text=c1)
    root.after(1000,label_change)

def translate_now():  #translateNow()
    global language
    try:
        text_=text1.get(1.0,END)
        c2=combo1.get()
        c3=combo2.get()
        translator = Translator()
        translation = translator.translate(text_, dest=c3)
        text2.delete(1.0,END)
        text2.insert(END,translation.text)  

    except Exception as e:
         messagebox.showerror("googletrans","please try again")
         print(e)

def spe_now():
    global language
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Speak Anything :")
        audio = r.listen(source)
        print("I heard  !!!")
    try:
        global language
        my_dict={'af': 'afrikaans', 'sq': 'albanian', 'am': 'amharic', 'ar': 'arabic', 'hy': 'armenian', 'az': 'azerbaijani',
           'eu': 'basque', 'be': 'belarusian', 'bn': 'bengali', 'bs': 'bosnian', 'bg': 'bulgarian', 'ca': 'catalan',
           'ceb': 'cebuano', 'ny': 'chichewa', 'zh-cn': 'chinese (simplified)', 'zh-tw': 'chinese (traditional)',
           'co': 'corsican', 'hr': 'croatian', 'cs': 'czech', 'da': 'danish', 'nl': 'dutch', 'en': 'english',
           'eo': 'esperanto', 'et': 'estonian', 'tl': 'filipino', 'fi': 'finnish', 'fr': 'french', 'fy': 'frisian',
           'gl': 'galician', 'ka': 'georgian', 'de': 'german', 'el': 'greek', 'gu': 'gujarati', 'ht': 'haitian creole',
           'ha': 'hausa', 'haw': 'hawaiian', 'iw': 'hebrew', 'hi': 'hindi', 'hmn': 'hmong', 'hu': 'hungarian',
           'is': 'icelandic', 'ig': 'igbo', 'id': 'indonesian', 'ga': 'irish', 'it': 'italian', 'ja': 'japanese',
           'jw': 'javanese', 'kn': 'kannada', 'kk': 'kazakh', 'km': 'khmer', 'ko': 'korean', 'ku': 'kurdish (kurmanji)',
           'ky': 'kyrgyz', 'lo': 'lao', 'la': 'latin', 'lv': 'latvian', 'lt': 'lithuanian', 'lb': 'luxembourgish',
           'mk': 'macedonian', 'mg': 'malagasy', 'ms': 'malay', 'ml': 'malayalam', 'mt': 'maltese', 'mi': 'maori',
           'mr': 'marathi', 'mn': 'mongolian', 'my': 'myanmar (burmese)', 'ne': 'nepali', 'no': 'norwegian',
           'ps': 'pashto', 'fa': 'persian', 'pl': 'polish', 'pt': 'portuguese', 'pa': 'punjabi', 'ro': 'romanian',
           'ru': 'russian', 'sm': 'samoan', 'gd': 'scots gaelic', 'sr': 'serbian', 'st': 'sesotho', 'sn': 'shona',
           'sd': 'sindhi', 'si': 'sinhala', 'sk': 'slovak', 'sl': 'slovenian', 'so': 'somali', 'es': 'spanish',
           'su': 'sundanese', 'sw': 'swahili', 'sv': 'swedish', 'tg': 'tajik', 'ta': 'tamil', 'te': 'telugu',
           'th': 'thai', 'tr': 'turkish', 'uk': 'ukrainian', 'ur': 'urdu','uz': 'uzbek', 'vi': 'vietnamese',
           'cy': 'welsh', 'xh': 'xhosa', 'yi': 'yiddish', 'yo': 'yoruba', 'zu': 'zulu', 'fil': 'Filipino', 'he': 'Hebrew'}
        
        key_list = list(my_dict.keys())
        val_list = list(my_dict.values())
        position= val_list.index(str(input("enter the input language")))
        lan=str(key_list[position])
        print(lan)
        text = r.recognize_google (audio,language=lan)
        print("You said :" , text)
        try:
            c3=combo2.get()
            translator = Translator()
            translation = translator.translate(text, dest=c3)
            text2.delete(1.0,END)
            text2.insert(END,translation.text)
            text3=translation.text
            
            # Words to voice
            my_dict={'af': 'afrikaans', 'sq': 'albanian', 'am': 'amharic', 'ar': 'arabic', 'hy': 'armenian', 'az': 'azerbaijani',
           'eu': 'basque', 'be': 'belarusian', 'bn': 'bengali', 'bs': 'bosnian', 'bg': 'bulgarian', 'ca': 'catalan',
           'ceb': 'cebuano', 'ny': 'chichewa', 'zh-cn': 'chinese (simplified)', 'zh-tw': 'chinese (traditional)',
           'co': 'corsican', 'hr': 'croatian', 'cs': 'czech', 'da': 'danish', 'nl': 'dutch', 'en': 'english',
           'eo': 'esperanto', 'et': 'estonian', 'tl': 'filipino', 'fi': 'finnish', 'fr': 'french', 'fy': 'frisian',
           'gl': 'galician', 'ka': 'georgian', 'de': 'german', 'el': 'greek', 'gu': 'gujarati', 'ht': 'haitian creole',
           'ha': 'hausa', 'haw': 'hawaiian', 'iw': 'hebrew', 'hi': 'hindi', 'hmn': 'hmong', 'hu': 'hungarian',
           'is': 'icelandic', 'ig': 'igbo', 'id': 'indonesian', 'ga': 'irish', 'it': 'italian', 'ja': 'japanese',
           'jw': 'javanese', 'kn': 'kannada', 'kk': 'kazakh', 'km': 'khmer', 'ko': 'korean', 'ku': 'kurdish (kurmanji)',
           'ky': 'kyrgyz', 'lo': 'lao', 'la': 'latin', 'lv': 'latvian', 'lt': 'lithuanian', 'lb': 'luxembourgish',
           'mk': 'macedonian', 'mg': 'malagasy', 'ms': 'malay', 'ml': 'malayalam', 'mt': 'maltese', 'mi': 'maori',
           'mr': 'marathi', 'mn': 'mongolian', 'my': 'myanmar (burmese)', 'ne': 'nepali', 'no': 'norwegian',
           'ps': 'pashto', 'fa': 'persian', 'pl': 'polish', 'pt': 'portuguese', 'pa': 'punjabi', 'ro': 'romanian',
           'ru': 'russian', 'sm': 'samoan', 'gd': 'scots gaelic', 'sr': 'serbian', 'st': 'sesotho', 'sn': 'shona',
           'sd': 'sindhi', 'si': 'sinhala', 'sk': 'slovak', 'sl': 'slovenian', 'so': 'somali', 'es': 'spanish',
           'su': 'sundanese', 'sw': 'swahili', 'sv': 'swedish', 'tg': 'tajik', 'ta': 'tamil', 'te': 'telugu',
           'th': 'thai', 'tr': 'turkish', 'uk': 'ukrainian', 'ur': 'urdu','uz': 'uzbek', 'vi': 'vietnamese',
           'cy': 'welsh', 'xh': 'xhosa', 'yi': 'yiddish', 'yo': 'yoruba', 'zu': 'zulu', 'fil': 'Filipino', 'he': 'Hebrew'}
        
            key_list = list(my_dict.keys())
            val_list = list(my_dict.values())
            position= val_list.index(str(input("enter the destination language")))
            lan=str(key_list[position])
            print(lan)
            myobj = gTTS(text=text3, lang=lan, slow=False) 
            myobj.save("output.mp3") 
            os.system("start output.mp3")

        except:
             print("sorry could not convert to audio")



    except sr.UnknownValueError:
        print("Sorry could not recognize what you said")

#speaker
sp_image=r"C:\Users\user\OneDrive\Desktop\visual studio\speaker-2488096_1280.png"
sp_image_for_button = PhotoImage(file=sp_image)



#icon
img_icon=PhotoImage(file=r"C:\Users\user\AppData\Local\Programs\Python\Python39\google.png")
root.iconphoto(False,img_icon)


#arrow
arrow_image=PhotoImage(file=r"C:\Users\user\AppData\Local\Programs\Python\Python39\arrow.png")
image_label=Label(root,image=arrow_image,width=150)
image_label.place(x=460,y=50)



language=googletrans.LANGUAGES
languageV=list(language.values())
lang1=language.keys()


combo1=ttk.Combobox(root,values=languageV,font="Roboto 14",state="r")
combo1.place(x=110,y=20)
combo1.set("english")

label1=Label(root,text="ENGLISH",font="segoe 30 bold",bg="blue",width=18,bd=5,relief=GROOVE)
label1.place(x=10,y=50)

#***
f=Frame(root,bg="black",bd=5)
f.place(x=10,y=118,width=440,height=210)

text1=Text(f,font="Robote 20",bg="white",relief=GROOVE,wrap=WORD)
text1.place(x=0,y=0,width=430,height=200)

scrollbar1=Scrollbar(f)
scrollbar1.pack(side="right",fill="y")

scrollbar1.configure(command=text1.yview)
text1.configure(yscrollcommand=scrollbar1.set)



combo2=ttk.Combobox(root,values=languageV,font="RobotV 14",state="r")
combo2.place(x=730,y=20)
combo2.set("select language")

label2=Label(root,text="ENGLISH",font="segoe 30 bold",bg="blue",width=18,bd=5,relief=GROOVE)
label2.place(x=620,y=50)

#***
f1=Frame(root,bg="Black",bd=5)
f1.place(x=620,y=118,width=440,height=210)

text2=Text(f1,font="Robote 20",bg="white",relief=GROOVE,wrap=WORD)
text2.place(x=0,y=0,width=430,height=200)

scrollbar2=Scrollbar(f1)
scrollbar2.pack(side="right",fill="y")

scrollbar2.configure(command=text2.yview)
text2.configure(yscrollcommand=scrollbar2.set)

#translate buttons
translate=Button(root,text="Translate",font="Roboto 15 bold italic",
                 activebackground="violet",cursor="hand2",bd=5,
                 bg="green",fg="white",command=translate_now)
translate.place(x=480,y=290)


#speech button 
speech=Button(root,image=sp_image_for_button  ,command=spe_now, height=28 , width=28)
speech.place(x=390 , y=290 )



# calling the program
label_change()


root.configure(bg="black")
root.mainloop()


