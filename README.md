# Calculator
from dis import dis
from multiprocessing.connection import answer_challenge
import parser
import imp
from re import I
from tkinter import *
from unittest import result
from requests import get

root = Tk()
root.title("Calculator")
display = Entry(root)
display.grid(row = 0 , columnspan = 6)

#calling functions
#fuction for numbers
i=0
def get_varib(num):
    global i
    display.insert(i,num)
    i+=1

#function for AC button
def clear_all():
    display.delete(0,END)

#function for undo
def undo():
    entire_strng = display.get()
    if len(entire_strng):
        new_strng = entire_strng[:-1]
        clear_all()
        display.insert(0,new_strng)
    else:
        clear_all()
        display.insert(0,"error")

#function for operations

def get_opr(opr):
    global i
    length = len(opr)
    display.insert(i,opr)
    i+=length

#function for calculation

def calculate_ans():
    entire_strn = display.get()
    try:
        a = parser.expr(entire_strn).compile()
        result=eval(a)
        clear_all()
        display.insert(0,result)
    except:
        clear_all()
        display.insert(0,'error')


# adding button to the calculator
Button(root,text="1",command=lambda:get_varib(1)).grid(row=1,column=0)
Button(root,text="2",command=lambda:get_varib(2)).grid(row=1,column=1)
Button(root,text="3",command=lambda:get_varib(3)).grid(row=1,column=2)
Button(root,text="4",command=lambda:get_varib(4)).grid(row=2,column=0)
Button(root,text="5",command=lambda:get_varib(5)).grid(row=2,column=1)
Button(root,text="6",command=lambda:get_varib(6)).grid(row=2,column=2)
Button(root,text="7",command=lambda:get_varib(7)).grid(row=3,column=0)
Button(root,text="8",command=lambda:get_varib(8)).grid(row=3,column=1)
Button(root,text="9",command=lambda:get_varib(9)).grid(row=3,column=2)
Button(root,text="0",command=lambda:get_varib(0)).grid(row=4,column=1)
Button(root,text=".",command=lambda:get_varib('.')).grid(row=4,column=0)
#Button(root,text="0",command=lambda:get_varib(0)).grid(row=4,column=1)
Button(root,text="+",command=lambda:get_opr('+')).grid(row=5,column=0)
Button(root,text="-",command=lambda:get_opr('-')).grid(row=5,column=1)
Button(root,text="*",command=lambda:get_opr('*')).grid(row=5,column=2)
Button(root,text="/",command=lambda:get_opr('/')).grid(row=6,column=0)
Button(root,text="%",command=lambda:get_opr('%')).grid(row=6,column=1)Button(root,text="0",command=lambda:get_varib(0)).grid(row=4,column=1)
Button(root,text="(",command=lambda:get_opr('(')).grid(row=6,column=2)
Button(root,text=")",command=lambda:get_opr(')')).grid(row=7,column=0)
Button(root,text="^2",command=lambda:get_opr('**2')).grid(row=7,column=1)
Button(root,text="UN",command=lambda:undo()).grid(row=2,column=3)
Button(root,text="AC",command=lambda:clear_all()).grid(row=3,column=3)
Button(root,text="=",command=lambda:calculate_ans()).grid(row=7,column=2)



root.mainloop()
