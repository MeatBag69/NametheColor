# NametheColor
#RawFile

import tkinter as t
import time
from tkinter import messagebox as m
import random as r

colorleft=20
scoress=0
last=0
start =0
timeleft = 20
flag =0


class app():
    
    def __init__(s):
        increment=0
        s.root=t.Tk()
        s.white="white"
        s.black="black"
        s.a="#ffc107"
        s.root.geometry("580x400+30+30")
        s.root.wm_resizable(0,0)
        s.root.configure(bg=s.a)
        s.root.title("Name the color")
        intro_frame=t.Frame(s.root,height=100,width=100,bg=s.a)
        intro_frame.grid(row=0,column=0)
        intro=t.Label(intro_frame,text="     Write the color what you see and not what you read!\n",
                      font=("arieal",15,"bold"),bg=s.a).grid()
       
       
        intro_frame_time=t.Frame(s.root,height=70,width=100,bg=s.a)
        intro_frame_time.grid(row=1,column=0)
        s.timeLabel = t.Label(intro_frame_time, text = "Time left: " + str(timeleft),
                              font = ("arieal",15,"bold"),bg=s.a)
        s.timeLabel.grid()

        s.score=t.Label(intro_frame,text="Score: "+str(scoress)+"\n",font=("arieal",15,"bold"),bg=s.a)
        s.score.grid(row=3)
        s.label=t.Label(text="Color Left :"+"\n",font=("arieal",15,"bold"),bg=s.a)
        s.label.grid()
        
        
     #   s.countdown()

        s.display_colors()
        s.root.mainloop()
        
    def up(s):
        global colorleft
        if colorleft>0:
            colorleft-=1
            
        s.label.configure(text="Colors Left :"+str(colorleft)+"\n",font=("arieal",15,"bold"))
        
        if colorleft==0:
            end=time.time()
            global scoress
            global start
            colorleft=20
            scoress=0
           
            times=end-start
            m.showinfo("Time Taken ","You Take"+str(times)+"Sec TO Find 20 Colors")
            
    def countdown(s):
        global timeleft 
        global scoress
        
        if timeleft == 0:
            
            m.showinfo("Score","Your score: "+str(scoress))
        
        if timeleft > 0: 
            timeleft -= 1
            s.timeLabel.config(text = "Time left: " + str(timeleft)) 
            s.timeLabel.after(1000, s.countdown) 
            
    
    
    def checking(s,event):
        global scoress
        global flag
        
        if flag == 0 :
            s.countdown()
            flag=1
            
            
        if str(s.entry.get().upper())==str(s.colors[0].upper()):
            scoress+=1
            s.score["text"]="Score :"+str(scoress)+"\n"
            s.color_label["text"]=" "
            s.entry.delete(0,"end")
            s.display_colors()
            
    def display_colors(s):
         global last
         s.up()
         global start
         start=time.time()
        # s.colors=["red","green","yellow","orange","blue","black","brown","gray"]
         s.colors=['Red','Blue','Green','Pink','Black','Yellow','Orange','White','Purple','Brown']
         r.shuffle(s.colors)
         color_frame=t.Frame(s.root,height=100,width=100,bg=s.a)
         color_frame.grid(row=4,column=0)
         last=s.colors[0]
         while last ==s.colors[0]:
          r.shuffle(s.colors)
         s.color_label=t.Label(s.root,text=s.colors[1].upper(),fg=s.colors[0],font=("arieal",40,"bold"),bg=s.a)
         s.color_label.grid(row=3,column=0)
         s.entry=t.Entry( s.root,width=20,bd=6)
         s.entry.grid(row=4,column=0)
         s.entry.focus_set()
         s.entry.bind("<Return>",s.checking)
            
p=app()
