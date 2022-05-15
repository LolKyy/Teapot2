from tkinter import *
class TestQuestion: # класс Тестовый вопрос
	def __init__(self,text,correct_variant,variant_of_ansver):
		self.text = text # текст вопроса
		self.correct_variant = correct_variant # правильный вариант
		self.variant_of_answer= variant_of_ansver # варианты ответа
class Test: # класс Тест
	def __init__(self,title='test',test_question_list = []):
		self.title = title # название теста
		self.test_question_list = test_question_list # список тестовых вопросов
		self.total_questions = len(test_question_list) # количество вопросов в тесте
	def add_test_question(self): # добавить тестовый вопрос в тест
		# чтобы увидеть код,перечислите 1$
		pass
	def remove_test_question(self): # удалить тестовый вопрос в тест
		# чтобы увидеть код,перечислите 1$
		pass
	def show_test_question_list(self): # просмотреть список тестовых вопросов
		# чтобы увидеть код,перечислите 1$
		pass
class TestInterface: # интерфейс для теста
	def __init__(self,test):
		self.root = Tk() # основное окно
		self.root.title(test.title) # надпись вверху окна
		self.root.geometry("300x300")# геометрия окна
		self.font = "Arial 12 bold"# шрифт виджетов
		self.lbl_text = StringVar()# переменная lbl
		self.lbl_text.set("Для начала теста нажмите 'начать'")
		self.lbl = Label(textvariable=self.lbl_text,font = self.font,wraplength =300)
		self.lbl.pack(side=TOP)#расположение вверху окна
		self.checkbtn_list =[] #список галочек
		self.score = 0 #счет
		self.variant = StringVar() # вариант ответа выбранный пользователем
		self.variant.set(0) # вариант не выбран
		self.n = 0 # счетчик шагов
		self.lbl_checked = Label(font = "Arial 12 bold") # lbl который пишет Правильно\ неправильно
		self.lbl_checked.pack(side=BOTTOM) # внизу окна
		self.btn = Button(text="Начать",font = "Arial 12 bold",bg = "red",foreground="white",bd= 6,width = 10, command=self.change_lbl_text) # кнопка
		self.btn.pack(side=BOTTOM) #
		self.root.mainloop() #обновление окна
	def change_lbl_text(self): #изменение текста верхнего lbl
		if self.n< test.total_questions:# если число шагов меньше количества вопросов в тесте:
			self.btn.config(text="Следующий>", bg = "red",foreground="white",bd= 6,width = 10, state=DISABLED,command = self.next_quest) #кнопка меняет текст и тд...
			self.lbl_text.set("Вопрос № {}\n{}".format(self.n+1,test.test_question_list[self.n].text)) # меняется текст лейбла
			self.set_check_btn()# метод установки галочек
			self.lbl_checked.config(text="\nНабрано баллов: {}".format(self.score)) # изменяется текст другог лейбла
		else:
			print("usyo pizdec") # чтобы понять что вопросы кончились
			self.end() # метод конец
	def set_check_btn(self): #метод установки галочек
		for key,value in test.test_question_list[self.n].variant_of_answer.items(): # для ключ,значение присвоить ключ,значение из каждого варианта ответа тестового вопроса
			ch =Checkbutton(text ="{}) {}".format(key,value),font = "Arial 12 bold",onvalue =key,variable =self.variant,command = self.checked)# создает галочку
			ch.pack() # прикручивает к окну
			self.checkbtn_list.append(ch) # добавляет в список галочек
	def remove_check_btn(self): # метод удаляет галочки с окна
		if self.checkbtn_list: # если список не пустой
			for ch in self.checkbtn_list: # каждую галочку
				ch.destroy() # убирает с окна
			self.checkbtn_list.clear() # очищает список
	def change_check_btn(self):# метод изменяет свойства галочек
		for ch in self.checkbtn_list:
			ch.config(state=DISABLED)#отключает
			if ch["onvalue"] == test.test_question_list[self.n].correct_variant: # если правильный вариант
				ch.config( disabledforeground="#000", bg="#0f0") # зеленый
			elif ch["onvalue"]== self.variant.get():# иначе
				ch.config(disabledforeground="#000", bg="#f00") # красный
	def checked(self): # проверка варианта с вариантом ответа
		if self.variant.get() == test.test_question_list[self.n].correct_variant: # если сходится
			self.score+=1 # прибавлет балл
			self.btn.config(state = NORMAL)#делает кнопку активной
			self.lbl_checked.config(text="Правильно\nНабрано баллов: {}".format(self.score))#изменяет лейбл
		else:
			self.lbl_checked.config(text="Вы ошиблись\nНабрано баллов: {}".format(self.score))#изменяет лейбл
			self.btn.config(text ="Попробовать снова",bg = "red",foreground="white",bd= 6,width = 12, command = self.reset,state = NORMAL)# изменяет свойства кнопки
		self.change_check_btn() # изменяет цвет галочки
	def reset(self): # обнуляет переменные в начальное положение
		self.n = 0
		self.score = 0
		self.variant.set(0)
		self.remove_check_btn()
		self.lbl_text.set("для начала теста нажмите 'начать'")
		self.lbl_checked.config(text='')
		self.btn.config(text="начать", command=self.change_lbl_text)
	def next_quest(self): # следующий шаг
		self.n+=1
		self.variant.set(0)# обнуляет вариант ответа
		self.remove_check_btn()# удаляет старые галки
		self.change_lbl_text() # изменяет лейбл на следующий вопрос
	def end(self): # титры в конце
		self.remove_check_btn()
		self.lbl_checked.config(text="Тест пройден.Вы свободны\nНабрано баллов: {}".format(self.score))
		self.lbl_text.set("Вопросы закончились")
		self.btn.config(text="Пройти тест снова", bg = "red",foreground="white",bd= 6,width = 16, command=self.reset)
test_question_list=[]
test_question_list.append(TestQuestion("...about his new book?", 'd', {'a': 'How do you think', 'b': 'How you think', 'c': 'What you think', 'd': 'What do you think'}))
test_question_list.append(TestQuestion("...to buy a new car?", 'b', {'a': 'Where you are going', 'b': 'When are you going'}))
test = Test("Тест по английскому",test_question_list) #  класс тест принимает на вход список из тестовыйх вопросов
TestInterface(test) # интерфейс принимает тест
