# python_miniproject
from tkinter import *
import random
from tkinter import messagebox
window=Tk()
window.title("Quiz App")
window.geometry("700x600")
window.resizable(0,0)
window.config(bg="#ffffff")

questions=[
    "Who developed Python Programming Language?",
    "Which of the following is not a complex number?",
    " Is Python case sensitive when dealing with identifiers?",
    " What does ~4 evaluate to?",
    " Is Python code compiled or interpreted?",
    " All keywords in Python are in _________",
    " What will be the value of the expression 4 + 3 % 5",
    " What is the result of cmp(3, 1)?",
    " Which keyword is used for function in Python language?",
    " What is the type of inf?",
    ]

options=[['a) Wick van Rossum',
          'b) Rasmus Lerdorf',
          'c) Guido van Rossum',
          'd) Niene Stom',],
         
         ['a) k = 2 + 3j',
          'b) k = complex(2, 3)',
          'c) k = 2 + 3l',
          'd) k = 2 + 3',],
         
         ['a) no',
          'b) yes',
          'c) machine dependent',
          'd) none of the mentioned',],
         
         ['a) -5',
          'b) -4',
          'c) -3',
          'd) +3',],
         
         ['a) Python code is both compiled and interpreted',
          'b) Python code is neither compiled nor interpreted',
          'c) Python code is only compiled',
          'd) Python code is only interpreted',],
         
         ['a) Capitalized',
          'b) lower case',
          'c) UPPER CASE',
          'd) None of the mentioned',],
         
         ["a) 7",
          "b) 2",          
          "c) 4",
          "d) 1",],
         
         ['a) 1',
          'b) 0',
          'c) True',
          'd) False',],
         
         ['a) Function',
          'b) def',
          'c) Fun',
          'd) Define',],
         
         ['a) Boolean', 
          'b) Integer',
          'c) Float',
          'd) Complex',],]

answers=[2,2,1,0,0,3,0,0,1,2]

ques=1

        
def showresult():
    global score,NextButton
    QuestionLabel.destroy()
    r1.destroy()
    r2.destroy()
    r3.destroy()
    r4.destroy()
    NextButton.destroy()
    window.destroy()
    
def calculate():
    global indexes,user_answer,answers
    x=0
    score=0
    for i in indexes:
        if user_answer[x]==answers[i]:
            score+=1
        x+=1
    messagebox.showinfo("Result","You got "f"{score}" " Marks")
    
def selected():
    global radiovar,user_answer,r1,r2,r3,r4,QuestionLabel,ques
    x=radiovar.get()
    if x<0:
        messagebox.showinfo("Error", "Please select an option")
    else:
        user_answer.append(x)
        radiovar.set(-1)
        if ques<5:
            QuestionLabel.config(text=questions[indexes[ques]])
            r1['text']=options[indexes[ques]][0]
            r2['text']=options[indexes[ques]][1]
            r3['text']=options[indexes[ques]][2]
            r4['text']=options[indexes[ques]][3]
            ques+=1
        else:
            calculate()
            showresult()
        
user_answer=[]

indexes=[]

def randomgen():
    global indexes
    while(len(indexes)<5):
        x=random.randint(0,9)
        if x in indexes:
            continue
        else:
            indexes.append(x)

def StartButton():
    QuizImgLabel.destroy()
    StartButton.destroy()

    randomgen()
    StartQuiz()


def StartQuiz():
    global radiovar,QuestionLabel,r1,r2,r3,r4,NextButton
    QuestionLabel=Label(window,text=questions[indexes[0]],font=('times',16,),width=500,justify='center',bg="#ffffff",)
    QuestionLabel.pack(pady=(40,60))
    
    radiovar=IntVar()
    radiovar.set(-1)

    r1=Radiobutton(window,text=options[indexes[0]][0],font=("times",12),value=0,variable=radiovar,bg="#ffffff",)
    r1.pack(pady=(0,10))

    r2=Radiobutton(window,text=options[indexes[0]][1],font=("times",12),value=1,variable=radiovar,bg="#ffffff",)
    r2.pack(pady=(0,10))

    r3=Radiobutton(window,text=options[indexes[0]][2],font=("times",12),value=2,variable=radiovar,bg="#ffffff",)
    r3.pack(pady=(0,10))

    r4=Radiobutton(window,text=options[indexes[0]][3],font=("times",12),value=3,variable=radiovar,bg="#ffffff",)
    r4.pack(pady=(0,50))
    
    
    NextButton=Button(window,image=NextImage,relief=FLAT,border=0,bg="#ffffff",command=selected,)
    NextButton.pack()
    

QuizImg=PhotoImage(file="./quiz.png")
NextImage=PhotoImage(file="./next.png")
QuizImgLabel=Label(window,image=QuizImg,bg="#ffffff",)
QuizImgLabel.pack(pady=(50,40))
StartImg=PhotoImage(file="./start1.png")
StartButton=Button(window,image=StartImg,relief=FLAT,border=0,bg="#ffffff",command=StartButton)
StartButton.pack()

window.mainloop()

