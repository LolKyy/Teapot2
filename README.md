# Multi-frame tkinter application v2.2
from distutils import command
import tkinter as tk


class SampleApp(tk.Tk):
    def __init__(self):
        tk.Tk.__init__(self)
        self._frame = None
        self.switch_frame(StartPage)

    def switch_frame(self, frame_class):
        """Destroys current frame and replaces it with a new one."""
        new_frame = frame_class(self)
        if self._frame is not None:
            self._frame.destroy()
        self._frame = new_frame
        self.geometry('800x600')
        self.resizable(width= False, height= False)
        self.title("Teapot")
        self._frame.pack()


class StartPage(tk.Frame):
    def __init__(self, master):
        tk.Frame.__init__(self, master)

        start_label = tk.Label(self, text="Welcome",font=("Comic Sans MS", int(48.0)))
        page_1_button = tk.Button(self, text="Войти",font =("Comic Sans MS", int(24.0)), foreground="white", bg = "blue", bd= 4,
                                  command=lambda: master.switch_frame(PageOne))
        start_label.pack()
        page_1_button.pack()

#Выбор тренажера
class PageOne(tk.Frame):
    def __init__(self, master):
        tk.Frame.__init__(self, master)

        page_1_label = tk.Label(self, text="Main menu:",font=("Comic Sans MS", int(48.0)))
        start_button = tk.Button(self, text="Справочник",font =("Comic Sans MS", int(12.0)), foreground="white", bg = "blue", bd= 4,width =15,
                                 command=lambda: master.switch_frame(PageTwo))
        entoru= tk.Button(self, text='Перевод слов',font =("Comic Sans MS", int(12.0)), foreground="white", bg = "blue", bd= 4,width =15)
        page_1_label.pack(side="top", fill="x", pady=10)
        start_button.pack()
        entoru.pack()

#Справочник
class PageTwo(tk.Frame):
    def __init__(self, master):
        tk.Frame.__init__(self, master)
        page_2_label = tk.Label(self, text="Present simple",font=("Comic Sans MS", int(42.0)))

        start_button = tk.Button(self, text="Далее",font =("Ariel", int(12.0)),bg = "red",foreground="white",bd= 4,width = 8,
                                 command=lambda: master.switch_frame(PageThree))
        back_button = tk.Button(self, text='Обратно в меню',font =("Ariel", int(12.0)),bg = "red",foreground="white",bd= 4,width = 15,
                                 command=lambda: master.switch_frame(PageOne))               
        page_2_label.pack(side="top", fill="x", pady=10)
        start_button.pack()
        back_button.pack()

# Справочник
class PageThree(tk.Frame):
    def __init__(self,master):
        tk.Frame.__init__(self, master)

        page_3_label = tk.Label(self, text="Present Continuous",font=("Comic Sans MS", int(42.0)))
        start_button = tk.Button(self, text="Далее",font =("Ariel", int(12.0)),bg = "red",foreground="white",bd= 4,width = 8,
                                 command=lambda: master.switch_frame(PageFour))
        back_button = tk.Button(self, text='Назад',font =("Ariel", int(12.0)),bg = "red",foreground="white",bd= 4,width = 8,
                                 command=lambda: master.switch_frame(PageTwo))
        menu_button = tk.Button(self,text='Вернуться в меню',font =("Ariel", int(12.0)),bg = "red",foreground="white",bd= 4,width = 15,
                                command=lambda: master.switch_frame(PageOne))
        page_3_label.pack(side="top", fill="x", pady=10)
        start_button.pack()
        back_button.pack()
        menu_button.pack()       
# Справочник 
class PageFour(tk.Frame):
    def __init__(self,master):
        tk.Frame.__init__(self, master) 

        page_4_label = tk.Label(self, text="Present Perfect Continuous",font=("Comic Sans MS", int(42.0)))
        start_button = tk.Button(self, text="Далее",font =("Ariel", int(12.0)),bg = "red",foreground="white",bd= 4,width = 8,
                                 command=lambda: master.switch_frame())
        back_button = tk.Button(self, text='Назад',font =("Ariel", int(12.0)),bg = "red",foreground="white",bd= 4,width = 8,
                                 command=lambda: master.switch_frame(PageThree))
        menu_button = tk.Button(self,text='Вернуться в меню',font =("Ariel", int(12.0)),bg = "red",foreground="white",bd= 4,width = 15,
                                command=lambda: master.switch_frame(PageOne))
        page_4_label.pack(side="top", fill="x", pady=10)
        start_button.pack()
        back_button.pack()
        menu_button.pack()              

if __name__ == "__main__":
    app = SampleApp()
    app.mainloop()
