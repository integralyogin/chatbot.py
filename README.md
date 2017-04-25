header ='Divine Intervention'
backupCounter =8085
questiontoggle =0
todaysquestion='2017-04-25'
timestamp='2017-04-25 03:29:57'
body='"k" still works'
bodytoggle=0
dateswitch=0
todaysdate='2017-04-25'
howmanymuch=0
whichaction=0
anum =5
todaysofferingscounter=1
dailyanumstandard=5
anumscore=410000
headertoggle=0
todo=''
todotoggle=0
secondquestiontimestamp=1493103062
currenttime=1493105667
difference=currenttime-secondquestiontimestamp
body2=''
bodytoggle2=0
bodyname='body'
body2name='body2'
thirdquestiontimestamp=1493105583
fourthquestiontimestamp=1493105276
savitriTimer=1493104134
num_lines=0
daily_ideal=2
reloadTimer=1491432840
todays_num=')'
history_lines=8100
sixthquestiontimestamp=1493104134

import subprocess
import signal
import os
import time
import readline
import random
import re
from chatbottest import test

target = 0
RANDOM20 = random.randrange(1,20)
RANDOM202 = random.randrange(1,20)

# starter process and questions

# functions 
# body (sa ==)

# responses

signal.signal(signal.SIGTTOU, signal.SIG_IGN)


class bcolors:
    HEADER = '\033[95m'
    BLUE = '\033[94m'
    GREEN = '\033[92m'
    WARNING = '\033[93m'
    FAIL = '\033[91m'
    ENDC = '\033[0m'
    BOLD = '\033[1m'
    UNDERLINE = '\033[4m'
    RED = '\033[91m'
    CYAN = '\033[96m'
    WHITE = '\033[97m'
    YELLOW = '\033[93m'
    MAGENTA = '\033[95m'
    GREY = '\033[90m'
    BLACK = '\033[90m'
    DEFAULT = '\033[99m'
















def fHeader():
    global num_lines
    dLogCount()
    if headertoggle == 1:
        print header, "-", history_lines
        print todays_num, "-", num_lines, "-", anumscore
        print "1QT", (60 - ((currenttime-secondquestiontimestamp)/60)), "- 3QT", (15 - ((currenttime-thirdquestiontimestamp)/60)) #i know.
        print "4QT", (10 - ((currenttime-fourthquestiontimestamp)/60)), "- 6QT", (60*4 - ((currenttime-sixthquestiontimestamp)/60))


def fTodo():
    if todotoggle == 1: 
        os.environ['TODO'] = str(todo)
        subprocess.call(["echo todo: $TODO | fold -s"], shell=True)


def fBody():
    if bodytoggle == 1: 
        os.environ['BODY'] = str(body)
        os.environ['BODYNAME'] = str(bodyname)
        subprocess.call(["echo $BODYNAME: $BODY | fold -s"], shell=True)

def fBody2():
    if bodytoggle2 == 1: 
        os.environ['BODY2'] = str(body2)
        os.environ['BODY2NAME'] = str(body2name)
        subprocess.call(["echo $BODY2NAME: $BODY2 | fold -s"], shell=True)

def questionFilter():
    fHeader()
    fTodo()
    fBody()
    fBody2()

def programStart ():
    anumStandard()
    dailyQuestion()
    timerQuestions()
    whichQuestion()

def anumStandard(): # the Golden function
    if anum < dailyanumstandard:
        #question13() # You have yet to reach your daily anum stanard, will you?
        print ""

def dailyQuestion():
    if todaysquestion != todaysdate: 
        subprocess.call(['sed -i "4s/=.*/=\'$(date "+%Y-%m-%d")\'/" ~/Documents/Notes/chatbot.py'], shell=True) 
        subprocess.call(['sed -i "9s/=.*/=\'$(date "+%Y-%m-%d")\'/" ~/Documents/Notes/chatbot.py'], shell=True) 
        #question6() # Did you consciously make an offering to God today? is this suppose to be a midday question?
        

def timerQuestions():
    if currenttime - secondquestiontimestamp > 60*60:
        subprocess.call(['sed -i "19s/=.*/=$(date "+%s")/" ~/Documents/Notes/chatbot.py'], shell=True)          
        #question1() # 1QT: Did you move closer to God today? > q14

    elif currenttime - thirdquestiontimestamp > 5*60:
        subprocess.call(['sed -i "26s/=.*/=$(date "+%s")/" ~/Documents/Notes/chatbot.py'], shell=True)          
        print "----------------------------------------------------"
        print "--- 3QT: every day you are going to read Savitri ---"
        print "----------------------------------------------------"
        #question20() # why did god create the universe?
        #question16() # Do you want the Divine Grace to transform you? > q18 > q17

    elif currenttime - fourthquestiontimestamp > 10*60:
        subprocess.call(['sed -i "27s/=.*/=$(date "+%s")/" ~/Documents/Notes/chatbot.py'], shell=True)          
        #randomQuestion()
        print "--------------------------------------------------------"
        print "--- 4QT: Four hours of concentrated study is enough. ---"
        print "--------------------------------------------------------"
    
    elif currenttime - sixthquestiontimestamp > 4*60*60:
        subprocess.call(['sed -i "34s/=.*/=$(date "+%s")/" ~/Documents/Notes/chatbot.py'], shell=True)          
        #randomQuestion()
        print "---------------------------------------------------------------"
        print "--- 6QT: Did you consciously make an offering to God today? ---"
        print "---------------------------------------------------------------"



    elif currenttime - savitriTimer > 12*60*60:
        subprocess.call(['sed -i "28s/=.*/=$(date "+%s")/" ~/Documents/Notes/chatbot.py'], shell=True)          
        #savitriQuestion() # Did you read Savitri today?

    # possible questions:?
    # morning question super-function that blocks other questions till morning is done.        
    # 6 hours in: have you done your sun salutations and pranayam yet?
    # 12 hours into the day: have you read Savitri yet? 


def randomQuestion():
        global questiontoggle
        global RANDOM20
        questiontoggle = RANDOM20        
        os.environ['RAND'] = str(questiontoggle)
        subprocess.call(['sed -i "3s/=.*/=\"$RAND\"/" ~/Documents/Notes/chatbot.py'], shell=True)          

def whichQuestion ():
    questionFilter()
    global questiontoggle    
    if questiontoggle == -1: questionKnowOrDo()
    elif questiontoggle == 0: minus1()
    elif questiontoggle == 1: question1()
    elif questiontoggle == 2: question2() 
    elif questiontoggle == 3: question3()
    elif questiontoggle == 4: question4()
    elif questiontoggle == 5: question5()
    elif questiontoggle == 6: question6()
    elif questiontoggle == 7: question7()
    elif questiontoggle == 8: question8()
    elif questiontoggle == 9: question9()
    elif questiontoggle == 10: savitriQuestion()
    elif questiontoggle == 11: question11()
    elif questiontoggle == 12: question12()
    elif questiontoggle == 13: question13()
    elif questiontoggle == 14: question14()
    elif questiontoggle == 15: question15()
    elif questiontoggle == 16: question16()
    elif questiontoggle == 17: question17()
    elif questiontoggle == 18: question18()
    elif questiontoggle == 19: question19()
    elif questiontoggle == 20: question20()

    off()
    questionKnowOrDo()

#QUESTIONS (RANK!!!! or SORT BY ALPHA?)
def question1(): print "Q1: Did you move closer to God today? [q1]"; fBinary(); question14() #response1()
def question6(): print "Did you consciously make a offering to God today? [q6]"; off(); response1()
def savitriQuestion(): print "Did you read Savitri today? [q10]"; fBinary(); howMuchLogAnum("read Savitri")
#def question13(): print "You have yet reach your set anum standard, will you?"; fBinary(); answerYes()
def question13(): print "You would like to add an offering to the Divine Log?"; fBinary(); answerYes()
def question16(): print "Do you want the Divine Grace to transform you?"; fBinary(); question18(); fBinary(); question17()
def question22(): print "Would you be willing to offer up one minute to God?"; fBinary(); answerYes() 
def question21(): print "Do you want to move closer to God?"; fBinary(); question17();
def question20(): print "Why did God create the Universe?";
def question8(): print "Did you do at least one Sun Salutation? [q8]"; off(); #howMany()
def question4(): print "Did you turn away from God today? [q4]"; off()
def question7(): print "Did you masterbate today? [q7]"; off()
def question12(): print "Did you make good progress with programming today? [q12]"; off()
def question2(): print "How can you move closer to God? [q2]"; #response2()
def question3(): print "What is most important? [q3]"; off()
def question5(): print "Why do you forget about God? [q5]"; off(); 
def question9(): print "If you had to choose between yourself and God? [q9]"; off()
def question11(): print "Do you remember that God is most important? [q11]"
def question14(): print "How much did you move towards God today? ENT to skip."; response1()
def question15(): print "Do you wish to make an offering to God?"; fBinary()
def question19(): print "What do you currently think is most important?" #needs a special response method?
# Did you study today?

# Why did you create me / why are you making me?
# did you back me up today on the external? (it should know)
def question18(): print " Are you currently rejecting or pushing the Grace away or closing it out?"
# do you want God to transform you? or
def question17(): print "Are you willing to offer an action to God?"; fBinary(); answerYes()
# How are you?
# Did you have lucid dreams?
# Do you want to know why suffering exists?
# Do you want to know why God created the universe?
# What do you want?
# What do you think?
# What are you feeling?

# do you think its worth it?
# can you do it?
# do you want the results?
# do you want to do it?

def questionKnowOrDo ():    
    bodyOfProgram()


























def profile():
    print ""
    print "USER PROFILE"
    print "supramental development = .00000000000001"
    print "Name: Josh?"
    print "title: "
    print "class: Wizard-Hacker? "
    print "class: breath centered monk"
    print "age: 30/72"
    print "anumscore =", anumscore
    print "powerlevel/willpower = 472"
    
    print "num of todays offerings = 1 (= lines in divine log for today)"
    print "num of total offerings recorded = 4 (= lines in divine log)"
    print "???"
    print ""
    print ""
    print "PROGRAM PROFILE"
    print "header =", header
    print "backupcounter =", backupCounter
    print ""

def exit (): subprocess.call(["echo; bash"], shell=True)

def secondsTimeStamp():
    subprocess.call(['sed -i "20s/=.*/=$(date "+%s")/" ~/Documents/Notes/chatbot.py'], shell=True)          


def reloadTimer():
    subprocess.call(['sed -i "31s/=.*/=$(date "+%s")/" ~/Documents/Notes/chatbot.py'], shell=True)          

def fReload(): 
    secondsTimeStamp()
    subprocess.call(['sed -i "9s/=.*/=\'$(date "+%Y-%m-%d")\'/" ~/Documents/Notes/chatbot.py'], shell=True) #setting todays date          
    subprocess.call(["python ~/Documents/Notes/chatbot.py"], shell=True)

def clear(): subprocess.call(["clear"], shell=True)

def edit():
    subprocess.call(["vim ~/Documents/Notes/chatbot.py"], shell=True)
    subprocess.call(["python ~/Documents/Notes/chatbot.py"], shell=True)

def subEdit():
    subprocess.call(["sublime-text ~/Documents/Notes/chatbot.py &"], shell=True)
    subprocess.call(["python ~/Documents/Notes/chatbot.py"], shell=True)


def check():
    print "Check: "
    print "header = ", header
    print "historylines = ", history_lines
    print "todays date = ", todaysdate 
    print "anum = ", anum
    print "daily anum standard = ", dailyanumstandard
    print "questiontoggle = ", questiontoggle
    print "2nd question countdown = ",(60 - ((currenttime-secondquestiontimestamp)/60)), "minutes"
    print "3rd question countdown = ",(15 - ((currenttime-thirdquestiontimestamp)/60)), "minutes"
    print "random question timer = ",(10 - ((currenttime-fourthquestiontimestamp)/60)), "minutes"
    print "last backup timestamp = ", timestamp
    os.environ['COUNT'] = str(backupCounter)
    subprocess.call(["ls ~/Documents/Notes/chatbot*$COUNT*"], shell=True) 
    #subprocess.call(["python ~/Documents/Notes/chatbot.py"], shell=True)
    print ""
    
def on():
    global questiontoggle
    questiontoggle= 1
    os.environ['LOG'] = str(questiontoggle)
    subprocess.call(['sed -i "3s/=.*/=\"$LOG\"/" ~/Documents/Notes/chatbot.py'], shell=True)          

def off():
    global questiontoggle
    questiontoggle = 0
    os.environ['LOG'] = str(questiontoggle)
    subprocess.call(['sed -i "3s/=.*/=\"$LOG\"/" ~/Documents/Notes/chatbot.py'], shell=True)          


def minus1():
    global questiontoggle
    questiontoggle = questiontoggle - 1
    os.environ['LOG'] = str(questiontoggle)
    subprocess.call(['sed -i "3s/=.*/=\"$LOG\"/" ~/Documents/Notes/chatbot.py'], shell=True)          
    fReload()

def add():
    global dailyanumstandard
    global anum
    dailyanumstandard = (anum + 1)
    os.environ['DAS'] = str(dailyanumstandard)
    subprocess.call(['sed -i "14s/=.*/=\"$DAS\"/" ~/Documents/Notes/chatbot.py'], shell=True)
    fReload()

def addScore():
    global anumscore
    addanumscore = input (">>> ")
    anumscore = (anumscore + addanumscore)
    os.environ['ANUMSCORE'] = str(anumscore)
    subprocess.call(['sed -i "15s/=.*/=\"$ANUMSCORE\"/" ~/Documents/Notes/chatbot.py'], shell=True)
    fReload()

def headerOn():
    global headertoggle
    headertoggle = 1
    os.environ['HT'] = str(headertoggle)
    subprocess.call(['sed -i "16s/=.*/=\"$HT\"/" ~/Documents/Notes/chatbot.py'], shell=True)          

def headerOff():
    global headertoggle
    headertoggle = 0
    os.environ['HT'] = str(headertoggle)
    subprocess.call(['sed -i "16s/=.*/=\"$HT\"/" ~/Documents/Notes/chatbot.py'], shell=True)          

def bodyon():
    #global bodytoggle
    bodytoggle = 1
    os.environ['BT'] = str(bodytoggle)
    subprocess.call(['sed -i "7s/=.*/=\"$BT\"/" ~/Documents/Notes/chatbot.py'], shell=True)          

def bodyoff():
    #global bodytoggle
    bodytoggle = 0
    os.environ['BT'] = str(bodytoggle)
    subprocess.call(['sed -i "7s/=.*/=\"$BT\"/" ~/Documents/Notes/chatbot.py'], shell=True)          

def body2On():
    #global bodytoggle
    bodytoggle2 = 1
    os.environ['BT2'] = str(bodytoggle2)
    subprocess.call(['sed -i "23s/=.*/=\"$BT2\"/" ~/Documents/Notes/chatbot.py'], shell=True)          

def body2Off():
    #global bodytoggle
    bodytoggle2 = 0
    os.environ['BT2'] = str(bodytoggle2)
    subprocess.call(['sed -i "23s/=.*/=\"$BT2\"/" ~/Documents/Notes/chatbot.py'], shell=True)          

def todoOn():
    #global bodytoggle
    todotoggle = 1
    os.environ['TTT'] = str(todotoggle)
    subprocess.call(['sed -i "18s/=.*/=\"$TTT\"/" ~/Documents/Notes/chatbot.py'], shell=True)          

def todoOff():
    #global bodytoggle
    todotoggle = 0
    os.environ['TTT'] = str(todotoggle)
    subprocess.call(['sed -i "18s/=.*/=\"$TTT\"/" ~/Documents/Notes/chatbot.py'], shell=True)          
        
def setBody():            
    print "Set Body:"
    BODY = raw_input (">>> ")
    os.environ['BODY'] = BODY
    subprocess.call(['sed -i "6s/=.*/=\'\""$BODY"\"\'/" ~/Documents/Notes/chatbot.py'], shell=True)   
    subprocess.call(['echo $(date "+%Y-%m-%d %T") =  $BODY >> ~/Documents/Notes/chatbotbodies'], shell=True)
    subprocess.call(["python ~/Documents/Notes/chatbot.py"], shell=True)


def setlog():
    global log
    os.environ['LOG'] = str(log)
    subprocess.call(['sed -i "3s/=.*/=\"$LOG\"/" ~/Documents/Notes/chatbot.py'], shell=True)

def set():
    global backupCounter
    print "Set Counter to: "
    backupCounter = input (">>> ")
    os.environ['COUNT'] = str(backupCounter)
    subprocess.call(['sed -i "2s/=.*/=\"$COUNT\"/" ~/Documents/Notes/chatbot.py'], shell=True)

def setq():
    global questiontoggle
    print "Set questiontoggle to: "
    questiontoggle = input (">>> ")
    os.environ['QT'] = str(questiontoggle)
    subprocess.call(['sed -i "3s/=.*/=\"$QT\"/" ~/Documents/Notes/chatbot.py'], shell=True)

def setBodyName():    
    print "Set Body Name:"
    BODYNAME = raw_input (">>> ")
    os.environ['BODYNAME'] = BODYNAME
    subprocess.call(['sed -i "24s/=.*/=\'\""$BODYNAME"\"\'/" ~/Documents/Notes/chatbot.py'], shell=True)   
    subprocess.call(['echo $(date "+%Y-%m-%d %T") =  $BODYNAME >> ~/Documents/Notes/chatbotbodyname'], shell=True)
    subprocess.call(["python ~/Documents/Notes/chatbot.py"], shell=True)


def setBody2():
    print "Set Body2:"
    BODY2 = raw_input (">>> ")
    os.environ['BODY2'] = BODY2
    subprocess.call(['sed -i "22s/=.*/=\'\""$BODY2"\"\'/" ~/Documents/Notes/chatbot.py'], shell=True)   
    subprocess.call(['echo $(date "+%Y-%m-%d %T") =  $BODY2 >> ~/Documents/Notes/chatbotbodies2'], shell=True)
    subprocess.call(["python ~/Documents/Notes/chatbot.py"], shell=True)


def setBody2Name():
    print "Set Body2 Name:"
    BODYNAME2 = raw_input (">>> ")
    os.environ['BODYNAME2'] = BODYNAME2
    subprocess.call(['sed -i "25s/=.*/=\'\""$BODYNAME2"\"\'/" ~/Documents/Notes/chatbot.py'], shell=True)   
    subprocess.call(['echo $(date "+%Y-%m-%d %T") =  $BODYNAME2 >> ~/Documents/Notes/chatbotbodyname2'], shell=True)
    subprocess.call(["python ~/Documents/Notes/chatbot.py"], shell=True)


def setToDo():
    print "Set Todo:"
    TODO = raw_input (">>> ")
    os.environ['TODO'] = TODO
    subprocess.call(['sed -i "17s/=.*/=\'\""$TODO"\"\'/" ~/Documents/Notes/chatbot.py'], shell=True)   
    subprocess.call(['echo $(date "+%Y-%m-%d %T") =  $TODO >> ~/Documents/Notes/chatbottodohistory'], shell=True)
    subprocess.call(["python ~/Documents/Notes/chatbot.py"], shell=True)

def resettq():
    global todaysquestion
    todaysquestion=0
    subprocess.call(['sed -i "4s/=.*/=0/" ~/Documents/Notes/chatbot.py'], shell=True)
    fReload()

def backup():
    os.environ['COUNT'] = str(history_lines)
    subprocess.call(['cp ~/Documents/Notes/chatbot.py ~/Documents/Notes/chatbot.py.bak$COUNT'], shell=True)
    subprocess.call(['sed -i "2s/=.*/=\"$COUNT\"/" ~/Documents/Notes/chatbot.py'], shell=True)          
    check()
    subprocess.call(['sed -i "5s/=.*/=\'$(date "+%Y-%m-%d %T")\'/" ~/Documents/Notes/chatbot.py'], shell=True)          
    time.sleep(1)
    fReload()
    
        
def d20():
    #subprocess.call(["cat d20 | head -n 30"], shell=True)  
    global RANDOM202
    os.environ['RAND'] = str(RANDOM202+5)
    subprocess.call(['sed -n "$RAND"p d20'], shell=True)
    reloadPass()

def swap():
    print "Insert new header:"
    HEADER = raw_input (">>> ")
    print HEADER
    os.environ['HEADER'] = HEADER
    subprocess.call(['echo $HEADER'], shell=True)
    subprocess.call(['sed -i "1s/=.*/=\'\""$HEADER"\"\'/" ~/Documents/Notes/chatbot.py'], shell=True)   
    subprocess.call(['echo $(date "+%Y-%m-%d %T") =  $HEADER >> ~/Documents/Notes/chatbotheaders'], shell=True)
    subprocess.call(["python ~/Documents/Notes/chatbot.py"], shell=True)

def pop():
    subprocess.call([" cat ~/Documents/Notes/always; cat ~/Documents/Notes/daily | head -n 4; cat ~/Documents/Notes/super-temp | head -n 4; cat ~/Documents/Notes/today | head -n 4; cat ~/Documents/Notes/now | head -n 4; cat ~/Documents/Notes/do | head -n 4; cat ~/Documents/Notes/projects | head -n 4; cat ~/Documents/Notes/jb-joshua-belisle | head -n 4; cat ~/Documents/Notes/becoming | head -n 4"], shell=True)

def dLogCount():
    global num_lines
    global todays_num
    global history_lines
    x = todaysdate
    item = 0
    with open("chatbotdivinelog") as origin:
        num_lines = sum(1 for line in origin)
    with open("chatbotcommandhistory") as origin:
        history_lines = sum(1 for line in origin)
    os.environ["HL"] = str(history_lines)
    subprocess.call(['sed -i "33s/=.*/=\"$HL\"/" ~/Documents/Notes/chatbot.py'], shell=True)
    os.environ["TD"] = todaysdate
    TNN = subprocess.check_output(['grep $TD ~/Documents/Notes/chatbotdivinelog | wc -l'], shell=True)
    todays_num = TNN.rstrip()

def runCommandInShell(cmd):
    subprocess.call([os.getenv('SHELL'), '-i', '-c', cmd])
    os.tcsetpgrp(0, os.getpgrp())

def keySearch(fKT): #"k"
    os.environ["fKT"] = fKT
    subprocess.call(['export GREP_COLOR="1;34"'], shell=True)
    subprocess.call(['grep --color=always -ni "$fKT" ~/Documents/Code/keys | more'], shell=True)
    #subprocess.call([os.getenv('SHELL'), '-i', '-c', "cgrep -n '$fKT' ~/Documents/Code/keys"]) 
    #os.tcsetpgrp(0, os.getpgrp())
    #os.environ ["keyterm"] = keyterm
    #subprocess.call(['grep --color=auto -n "$keyterm" ~/Documents/Code/keys'], shell=True)

def keySearch2(fKS): #"k"
    
    #keys = open('keys')

    subprocess.call(['cat keys | awk \'{ print length, $0 }\' | sort -n > keys.sortBSL'], shell=True)
    keys = open('keys.sortBSL')
 
    #if " " in PAT:
    WC = fKS.count(" ")
    paras = WC + 1
    sPAT = fKS.split(" ")
    BPAT = fKS.split(" ")
    reline = 0
    c = 0

    for line in keys:  
        reline = line
        for i in range (0,paras):  
            #for i in reversed(line):
            if sPAT[i] in reline:
                BPAT[i] = bcolors.BLUE + sPAT[i] + bcolors.ENDC
                BPAT[i] = bcolors.BOLD + BPAT[i] + bcolors.ENDC
                #BPAT[i] = bcolors.BLUE + bcolors.BOLD + sPAT[i] + bcolors.ENDC
                reline = re.sub(sPAT[i], BPAT[i], reline)
                #print sPAT[i]
                c = c + 1
            else:
                c = 0
            
        if c == paras:
            print reline

def keysSortedByLength(fKSBL):
    os.environ["fKSBL"] = fKSBL
    subprocess.call(['grep --color=always -ni "$fKSBL" ~/Documents/Code/keys.sortbystringlength | more'], shell=True) 

def fSlog(fSLOG):  
    os.environ ["fSLOG"] = fSLOG
    subprocess.call(['grep --color=always -ni "$fSLOG" ~/Documents/Notes/chatbotlog | more'], shell=True)

def fSBot(fSBOT):  
    os.environ ["fSBOT"] = fSBOT
    subprocess.call(['grep --color=always -ni "$fSBOT" ~/Documents/Notes/chatbot.py | more'], shell=True)
            

def SEARCH_KEYS(PAT): #"kr"  
    WC = PAT.count(" ")
    paras = WC + 1
    paras2 = WC + 1
    sPAT = PAT.split(" ")
    BPAT = PAT.split(" ")
    reline = 0
    c = 0
    print sPAT
    print BPAT
  
    authorslist = open('authorslist')
    for line in authorslist:
        for i in range (0,paras):  
            sLINE = line.split("=")
            if sPAT[i] in sLINE[0]:
                sPAT[i] = sLINE[1]
                sPAT = sPAT[i].split(" ")
                sPAT[1] = sPAT[1].rstrip("\n")
                BPAT = sPAT
                paras = paras + 1
                print sPAT
    authorslist.close()
                

    # keys = open('keys.sortBRSL')
    # for line in keys:  
    #     reline = line
    #     for i in range (0,paras):  
    #         #for i in reversed(line):
    #         if sPAT[i] in reline:
    #             #BPAT[i] = bcolors.BLUE + sPAT[i] + bcolors.ENDC
    #             #BPAT[i] = bcolors.BOLD + BPAT[i] + bcolors.ENDC
    #             #BPAT[i] = bcolors.BLUE + bcolors.BOLD + sPAT[i] + bcolors.ENDC
    #             #reline = re.sub(sPAT[i], BPAT[i], reline)
    #             #print sPAT[i]
    #             c = c + 1
    #         else:
    #             c = 0
        
    #     if c == paras:
    #         print reline
    # keys.close()


    # print "c =", c
    # print "paras =", paras
    # print "paras2 =", paras2
    # print "WC =", WC
    # print "sPAT =", sPAT
    # print "BPAT =", BPAT
    # for i in range (0,paras):
    #     print "sPAT[", i, "] =", sPAT[i]
    
    # for i in range (0,paras):
    #     print "BPAT[", i, "] =", BPAT[i]
    
   
def searchMajor(term):
    os.environ["term"] = term
    subprocess.call(['cd ~/Documents/Full; grep --color=always $term  * | awk \'{ print length, $0 }\' | sort -n | more'], shell=True)
    #subprocess.call(['grep --color=always $term ~/Documents/Full/tempfile1 | more'], shell=True)


#cat keys.bak | awk '{ print length, $0 }' | sort -n | cut -d" " -f2- >> keys.sortbystringlength

































#def reloadingTimer():
#if currenttime - reloadtimer == 60*5:
#    reloadTimer()
#    fReload()

#BODYOFPROGRAM
def bodyOfProgram():  #333
     



    sa = raw_input(">>> ")
    os.environ['sa'] = sa
    subprocess.call(['echo $(date "+%Y-%m-%d %T") =  $sa >> ~/Documents/Notes/chatbotcommandhistory'], shell=True)
        
    if sa == "": fReload()
    
    elif sa == "s" or sa == "swap": swap()
    elif sa == "x" or sa == "exit": exit()      

    elif sa[0] == "i" and sa[1] == " ": searchMajor(sa[2:])
    elif sa[0] == "b" and sa[1] == " ": runCommandInShell(sa[2:])
    
    elif sa == "slog" or sa == "sl": 
        SLOG = raw_input ("slog for: >>> ")
        os.environ ["SLOG"] = SLOG
        subprocess.call(['grep --color=always -n $SLOG chatbotlog'], shell=True) 
    
    elif sa[0] == "s" and sa [1] == "l" and sa [2] == "o" and sa [3] == "g" and sa [4] == " ": fSlog(sa[5:]) 
    elif sa[0] == "s" and sa [1] == "l" and sa[2] == " ": fSlog(sa[3:])
    elif sa[0] == "h" and sa [1] == "e" and sa [2] == "r" and sa [3] == "e" and sa [4] == " ": fSlog(sa[5:]) 
    elif sa[0] == "s" and sa [1] == "b" and sa [2] == "o" and sa [3] == "t" and sa [4] == " ": fSBot(sa[5:])         
    elif sa[0] == "k" and sa [1] == " ": keySearch2(sa[2:])
    elif sa[0] == "k" and sa [1] == "l" and sa [2] == " ": keysSortedByLength(sa[3:])
    elif sa[0] == "k" and sa [1] == "r" and sa [2] == " ": SEARCH_KEYS(sa[3:])
    elif sa[0] == "l" and sa [1] == " ": fRegKey(sa[2:])

    #if sa2[0] == "b":
     #   print "bash!"
        #os.environ['sa21'] = sa2[1]
        #subprocess.call([' '], shell=True)


    elif sa == "r" or sa == "reload" or sa == "rf": fReload() 
    elif sa == "add": add()
    elif sa == "addscore": addScore()
    elif sa == "addanum": addAnum()
    elif sa == "e": edit()
    elif sa == "sub": subEdit()
    elif sa == "dlogcount": dLogCount()
    elif sa == "rand": randomQuestion()
    elif sa == "q1": question1()
    elif sa == "q2": question2()
    elif sa == "q3": question3()
    elif sa == "q6": question6()
    elif sa == "set": set()
    elif sa == "ss" or sa == "setanumstandard": setAnumStandard()
    elif sa == "reset" or sa == "rs": resettq()
    elif sa == "sq": setq()
    elif sa == "count": count()
    elif sa == "which": whichQuestion()
    elif sa == "setbodyname": setBodyName()
    elif sa == "setbody2": setBody2()
    elif sa == "setbody2name": setBody2Name()
    elif sa == "settodo": setToDo()
    elif sa == "help": question16()
    elif sa == "bb" or sa == "backup": backup()
    elif sa == "headeron": headerOn(); fReload()
    elif sa == "headeroff": headerOff(); fReload()
    elif sa == "hideall" or sa == "hide all": headerOff(); todoOff(); bodyoff(); body2Off(); fReload()
    elif sa == "showall" or sa == "show all": headerOn(); todoOn(); bodyon(); body2On(); fReload()
    elif sa == "todoon": todoOn(); fReload()
    elif sa == "todooff": todoOff(); fReload()
    elif sa == "bodyon" or sa == "showbody": bodyon(); fReload()
    elif sa == "bodyoff" or sa == "hidebody": bodyoff(); fReload()
    elif sa == "body2on" or sa == "showbody2": body2On(); fReload()
    elif sa == "body2off" or sa == "hidebody2": body2Off(); fReload()
    elif sa == "off": off()
    elif sa == "on": on()
    elif sa == "action?" or sa == "d20": d20()
    elif sa == "check" or sa == "k": check()
    elif sa == "u" or sa == "update": update()
    elif sa == "log on" or sa == "set 1": on()
    elif sa == "log off" or sa == "set 0": off()
    elif sa == "todays": dailyQuestion() 
    elif sa == "c" or sa == "cl": subprocess.call(["clear"], shell=True)
    elif sa == "p": profile()
    elif sa == "guidance" or sa == "guide me" or sa == "guide me please" or sa == "guide" or sa == "ask me": question1 ()    
    elif sa == "setbody": setBody()
    elif sa == "pop": pop()
    elif sa == "test": test()

    elif sa == "v":
        vsearch = raw_input (">>> ")
        os.environ['vsearch'] = vsearch 
        subprocess.call(['vim +/"$vsearch" ~/Documents/Notes/chatbot.py'], shell=True)
    
    elif sa == "vk": subprocess.call(['vim +/"333" ~/Documents/Notes/chatbot.py'], shell=True)
    elif sa == "vn": subprocess.call(['vim +/"NOTES" ~/Documents/Notes/saai'], shell=True)
    elif sa == "vi": subprocess.call(['vim +/"INTENTIONS" ~/Documents/Notes/chatbot.py'], shell=True)
    elif sa == "vm": subprocess.call(['vim +/"MY QUESTIONS" ~/Documents/Notes/chatbotuserquestions'], shell=True)
    elif sa == "v?" or sa == "???": subprocess.call(['vim +/"QUESTIONS" ~/Documents/Notes/chatbot.py'], shell=True)
    elif sa == "vh": subprocess.call(['vim +/"OLD HEADERS" ~/Documents/Notes/chatbotheaders'], shell=True)
    elif sa == "vq": subprocess.call(['vim +/"HIS QUESTIONS" ~/Documents/Notes/chatbothelperquestions'], shell=True)
    elif sa == "vp": subprocess.call(['vim +/"USER PROFILE" ~/Documents/Notes/chatbot.py'], shell=True)
    elif sa == "vl": subprocess.call(['vim +/"LIST" ~/Documents/Notes/chatbottodolist'], shell=True)
    elif sa == "vd": subprocess.call(['vim +/"DONE" ~/Documents/Notes/chatbottodolist'], shell=True)
    elif sa == "vc": subprocess.call(['vim +/"COMMANDS" ~/Documents/Notes/chatbotcommands'], shell=True)
    elif sa == "new": subprocess.call(["vim +/NEWSA ~/Documents/Notes/chatbot.py"], shell=True)
    elif sa == "bop": subprocess.call(['vim +/"BODYOFPROGRAM" ~/Documents/Notes/chatbot.py'], shell=True)
    elif sa == "vhowg": subprocess.call(["vim ~/Documents/Notes/how-to-move-closer-to-god"], shell=True)
    elif sa == "vanum" or sa == "va": subprocess.call(["vim ~/Documents/Notes/anumscale"], shell=True)
    elif sa == "vhow": subprocess.call(["vim ~/Documents/Notes/how"], shell=True)
    elif sa == "vwhat": subprocess.call(["vim ~/Documents/Notes/what"], shell=True)
    elif sa == "vwhy": subprocess.call(["vim ~/Documents/Notes/why"], shell=True)
    elif sa == "vlog": subprocess.call(["vim ~/Documents/Notes/chatbotlog"], shell=True)
    elif sa == "anum" or sa == "a": subprocess.call(["echo; cat ~/Documents/Notes/anumscale | head -n 32; echo"], shell=True)
    elif sa == "q": subprocess.call(["echo; cat ~/Documents/Notes/chatbothelperquestions | head -n 28; echo"], shell=True)
    elif sa == "?": subprocess.call(["echo; cat ~/Documents/Notes/chatbotcommands | head -n 28; echo"], shell=True) #!
    elif sa == "headers" or sa == "names": subprocess.call(["echo; cat ~/Documents/Notes/chatbotheaders; echo"], shell=True)
    elif sa == "bodies": subprocess.call(["echo; cat ~/Documents/Notes/chatbotbodies | tail -n 40; echo"], shell=True)
    elif sa == "bodies2": subprocess.call(["echo; cat ~/Documents/Notes/chatbotbodies2 | tail -n 40; echo"], shell=True)
    elif sa == "log": subprocess.call(["cat -n ~/Documents/Notes/chatbotlog | tail -n 30; echo"], shell=True)
    elif sa == "hist": subprocess.call(["cat -n ~/Documents/Notes/chatbotcommandhistory; echo"], shell=True)
    elif sa == "dlog": subprocess.call(["cat -n ~/Documents/Notes/chatbotdivinelog"], shell=True)
    elif sa == "l": subprocess.call(["cat -n ~/Documents/Notes/chatbottodolist | tail -n 22; echo"], shell=True)
    elif sa == "d": subprocess.call(["echo; cat -n ~/Documents/Notes/chatbottodolist | head -n 37; echo"], shell=True)
    #elif sa == "p": subprocess.call(["echo; cat ~/Documents/Notes/chatbotuserprofile | head -n 37; echo"], shell=True)
    elif sa == "n" or sa == "saai": subprocess.call(["echo; cat ~/Documents/Notes/saai | head -n 25; echo"], shell=True)    
    elif sa == "m" or sa == "my": subprocess.call(["echo; cat ~/Documents/Notes/chatbotuserquestions | head -n 25; echo"], shell=True)  
    elif sa == "ym": subprocess.call(["grep -n YM chatbot.py"], shell=True)






































    #MY QUESTIONS AND STATEMENTS
    elif sa == "m???" or sa == "m?": subprocess.call(['vim +/"MY QUESTIONS AND STATEMENTS" ~/Documents/Notes/chatbot.py'], shell=True)

# YM 1) can you help me to never forget that God is most important
# YM 2) can you help me to only think of God?
# YM 3) do i want to invoke the Divine Grace to transform me?
# YM 4) I keep on failing to reject my lower nature.. with sleep, masturbating, coffee, weed
# YM 5) can you help me to overcome ego and desire?
# YM 6) how to adjust program such that it helps me move towards God? and be successful in programming, and financially.

# how to make the most of dads noises? > how to allow it to make me strong?  to widen my consciousness?
# best way to develop golden question chains?
# how to become a divine worker?
# do i want to change? to progress?
#question1 comes before question14.  link em together and getting working.
#question1 comes before question14.  link em together and getting working.
# i want to masturbate > do you not also want to become strong? a master of oneself? a conscious servant of the Divine? also do you wish to repel Her most glorious Majesty?
# i masturbated
#can i drink coffee please? >
#can i smoke weed please? >
#i want to smoke >> what would the Mother like?
# i feel lost..
# mother...
# i want to understand the meaning of my state of isness...
# do i feel this way because i havent read Savitri? 
# what am i experiencing? what is the meaning?
# elon talks about putting in 80-100 hours of work a week.  surely that would progress my project quickly indeed.  but there must be a intelligent way of doing so.  
# how to get inspiration / vision? > open to divine force?

    elif sa == "why god?":
        print "It is God's Will"
        print "The soul knows that it does not give itself to God in vain; claiming nothing, it yet receives the infinite riches of the divine Power and Presence."



    elif sa == "how do i move closer to god?" or sa == "how to move closer to god?" or sa == "how can i make amends?" or sa == "how to move closer to god" or sa == "god?" or sa == "howg":
        subprocess.call(["clear; echo; cat ~/Documents/Notes/how-to-move-closer-to-god | head -n 25; echo"], shell=True)
        
    elif sa == "how?" or sa == "how": 
        subprocess.call(["clear; echo; cat ~/Documents/Notes/how | head -n 30; echo"], shell=True)
    
    elif sa == "what is most important?" or sa == "what is most important":
        print "fill in plz"

    elif sa == "what immediate action should i take?":
        print "link to something"

    elif sa == "how do i make a sacrifice?" or sa == "how to make sacrifice?" or sa == "sacrifice?":
        print "offer an action to God. any action"

    elif sa == "did i move closer to god today?" or sa == "did i?":
        print "you will probably have to look within yourself for this answer. in the grand scheme..."

    elif sa == "what should i do?" or sa == "what should i do" or sa == "what":
        subprocess.call(["clear; echo; cat ~/Documents/Notes/what | head -n 30; echo"], shell=True)

    elif sa == "why" or sa == "why?" or sa == "why god?" or sa == "why god":
        subprocess.call(["echo; cat ~/Documents/Notes/why | head -n 30; echo"], shell=True)

    elif sa == "how to make progres?":
        print "aspiration, rejection and surrender?"

    elif sa == "i dont want to turn towards god" or sa == "i dont want":
            print """
    It seems like you dont want to turn towards God.  But really you do.
    That deeper or higher truth is just currently obscured, which is why
    you cannot remember or sense it.
    Doing things based on what you want will never bring you satisfaction.
    Desire based action is like...
    Your soul decided to embark on the adventure of consciousness
    So that it could enjoy losing and finding God in the material world.

                """

    elif sa == "toggle":
        if questiontoggle == 0:
            on()
        elif questiontoggle == 1:
            off()
        else:
            print "im confused"

        
    elif sa == "sbot":
            SBOT = raw_input (">>> ")
            os.environ ["SBOT"] = SBOT
            subprocess.call(['grep --color=auto -n $SBOT ~/Documents/Notes/chatbot.py'], shell=True)
        
    else:
        #print "entry not found - logging.."
                os.environ['sa'] = sa
                subprocess.call(['echo $(date "+%Y-%m-%d %T") =  $sa >> ~/Documents/Notes/chatbotlog'], shell=True)
                clear()
                print "chatbotlog:"
                subprocess.call(["cat -n ~/Documents/Notes/chatbotlog | tail -n 22; echo"], shell=True)
                #runCommandInShell(sa)
                questionKnowOrDo()


        #print Header,"-", counter
                whichQuestion() 
        #End of qkod2







































#### chatbotquestioncheck
# were u asked q6 yet?
# how to check?



#### chatbotquestionlog

# question = raw_input (">>> ")
# os.environ['question'] = str(question)

# subprocess.call(['echo $(date "+%Y-%m-%d") =  $question >> ~/Documents/Notes/chatbotanswers'], shell=True)
# subprocess.call(['sed -i "5s/=.*/=\'$(date "+%Y-%m-%d")\' $question/" ~/Documents/Notes/chatbotanswers.py'], shell=True)          

# if question == '':
    #


#???
# create a chatbotanswers note. set only to $date, such that when you first answer a question, you can
# keep answering it till the end of the day, improving your score.  very nice.

def response1():
    
    global anum
    answer = raw_input(">>> ")
    
    if answer == 'not yet': 
            anum = -1; result()

    elif answer == "" or answer == " ":
            fReload()

    elif answer == "not consciously":
            print "Yes life is a sacrifice, regardless of whether done consciously or not."
            print "fill me in plz"
            time.sleep(1)

    elif answer == 'no' or answer == 'not really' or answer == 'not really...': 
            anum = 0; result()
    elif answer == 'i dont think so' or answer == 'idts': 
            anum = 0; result()

    elif answer == 'not sure' or answer == 'maybe' or answer == "i dont know" or answer == "idk":
        print "if you are not sure then maybe it is best to think it over and answer later"; 
        questionKnowOrDo()
        
    elif answer == 'a little' or answer == "kinda": 
            anum = 2; result()
    elif answer == 'yes': 
            anum = 5; result()
    elif answer == 'a lot':
        anum = 7; result()
    elif answer == 'absolutely': 
        anum = 9; result()

    elif answer == 'x' or answer == 'exit': exit ()
    elif answer == 'e': edit()

    else: 
        print "unfortunately I dont understand that response. try again.";
    
        on()
        fReload()

def response2 ():
        response2 = raw_input (">>> ")
        if response2 == "x" or response2 == "exit" or response2 == "": exit()

        elif response2 == "e": edit()
           
        elif response2 == "can i?" or response2 == "how can i?":
            print "for now if you are willing that is enough.  So the question returns.."
            question2()

        elif response2 == "i dont know if i can":
            print "He who chooses the Infinite has been chosen by the Infinite."

            print """   He has received the divine touch without which there is no awakening,
                        no opening of the spirit; but once it is received, attainment is sure, 
                        whether conquered swiftly in the course of one human life or pursued 
                        patiently through many stadia of the cycle of existence in the manifested 
                        universe."""
            #print "he has received the divine touch"
            #print "and all can be done if the god-touch is there"
            #print "you can, it is God's Will, and God's Will will triumph eventually. it is written"
            print "it is the mother who is the sadhak and the sadhana"
            
            print "Would you choose?"
            question3()

        elif response2 == "yes":
            print "how?"
            whichQuestion() 
        elif response2 == "im trying" or response2 == "i am trying":
            print "fill this in2"
        elif response2 == "i want to":
            print "okay. but... As I asked, "
            question2()
        else:
            print "elsemsg"


def result ():
    
    if anum == -1:
                print "Does that mean that you will make an offering to God today?"
                fBinary()
                answerYes()

    elif anum == 0:
        print "are you sure? could you really waste a day so? if so, then perhaps it is best to make amends?"
        fBinary()
        
    elif 0 < anum < 3:
        print "that is better than nothing. for sure. yet... do you wish only to circle slowly towards the far off light? "
        fBinary()
    
    elif 4 < anum < 8 :
        print "good. how much did you move towards God?"
        addAnum()

    elif anum > 8:
        print "excellent"
        print "today was well spent then"

    elif anum == "e": edit()
    elif anum == "x" or anum == "": exit()

    else:
        print "fill this in3"
        time.sleep(1)





def howMuchLogAnum(whichaction):
    howManyMuch()
    addDivineLog(whichaction)
    addAnum()

def howManyMuch ():
    global howmanymuch
    print "How many/much?"
    howmanymuch = raw_input (">>> ")
    print "If item name is captured, then put into divine log"

def whichAction():
    global whichaction
    print "Which action?"
    whichaction = raw_input (">>> ")

# BINARY
def fBinary():
    binary = raw_input (">> ")
    if binary == "x": fReload()
    elif binary == "kinda": print "0"
    elif binary == "yes" or binary == "y" or binary == "Yes" or binary == "yes i will": print "1"
    elif binary == "sure" or binary == "ok" or binary == "i think so" or binary == "yes please": print "2" 
    elif binary == "d20": 
        global RANDOM202
        os.environ['RAND'] = str(RANDOM202+5)
        subprocess.call(['sed -n "$RAND"p d20'], shell=True)
        reloadPass()
    elif binary == "e": edit()
    else: 
        answerNo()

def reloadPass():
    reloadpass = raw_input ("Press any key to reload:  ")
    fReload()

def answerYes():
    #print "Would you be willing to do it now?"; fBinary()
    whichAction()
    #print "Good on you"
    #print "Did you do it?"; fBinary()
    howManyMuch()
    print "In what spirit did you make the offering?"
    print " <add quality of offering function> "
    print "Were you sober when you did it?"
    print " <add some function for recordin this> "
    print "Noted in the Divine Log."; addDivineLog(whichaction)
    #addAnum()
    slp1()

def answerNo():
    print "That is too bad,"
    #sleep(1)
    ANUM = anum
    lowerAnumStandard(ANUM) # set anumStandard to current anum.  (copping out)
    off()
    fReload()

def slp1(): time.sleep(1)
def slp3(): time.sleep(3)
def slp5(): time.sleep(5)
def slp10(): time.sleep(10)
def sleep(x): time.sleep(x)

def addDivineLog(whichaction):
    os.environ["howmanymuch"] = howmanymuch
    os.environ["whichaction"] = whichaction
    print "upgrade this so that it checked if there is some for the day already? see edit-sav.sh?"
    subprocess.call(['echo $(date "+%Y-%m-%d %T") = $whichaction = $howmanymuch >> ~/Documents/Notes/chatbotdivinelog'], shell=True)
    sleep(.5)

def addAnum():
    #print "anum is a number representing how much effort you put towards find God, moving towards God or how much of your day you offered to God"
    print "Add how much to anum?"
    global anum
    print "current anum =", anum
    addanum = input (">>> ")
    if addanum == 0:
        off()
        fReload()
    anum = anum + addanum
    os.environ["anum"] = str(anum)
    subprocess.call(['sed -i "12s/=.*/=\"$anum\"/" ~/Documents/Notes/chatbot.py'], shell=True)          

def lowerAnumStandard(LAS):
    os.environ["ANUM"] = str(LAS)
    subprocess.call(['sed -i "14s/=.*/=\"$ANUM\"/" ~/Documents/Notes/chatbot.py'], shell=True)          

def setAnumStandard():
    print "To what would you like to set your anum standard?"
    global dailyanumstandard
    dailyanumstandard = raw_input (">>> ")
    os.environ["anum"] = dailyanumstandard
    subprocess.call(['sed -i "14s/=.*/=\"$anum\"/" ~/Documents/Notes/chatbot.py'], shell=True)          
    fReload()























clear()
secondsTimeStamp()


programStart()

#whichQuestion()








 # print "BPAT[", 0, "] =", BPAT[0]
    # print "BPAT[", 1, "] =", BPAT[1]


#for num, line in enumerate(keys, 1):

   # for line in keys:
    #    for i in range (0, paras):
     #       BPAT = bcolors.BOLD + PAT + bcolors.ENDC
   #         if sPAT[i] not in line:
    #            return False
 #           print line


    #for line in keys: 
    #    re.sub(PAT, BPAT, line, re.I)
             
   # for line in keys: 
        #if re.search ("\\b.*"+PAT+".*\\$", line):
        #    for i in range(0, paras):
       #         boldline = re.sub(sPAT[i], BPAT[i], line)
      #          print boldline
             
        #if re.search (PAT, line, re.I):
        #if re.search ("\\b.*"+PAT+".*\\$", line):
         #   print re.sub(PAT, BPAT, line)
            #print boldPat

     #   if re.search(PAT, line):
      #      boldPat = re.sub(PAT, BPAT, line, re.I)
       #     print boldPat

 #       for line in keys:
  ##          for i in range (0, paras):
   #             if all(sPAT[i]):
    #                print line

#        for line in keys:
 #           if re.finditer(sPAT, line):
  #              print line
            
            #for i in range (0,paras):   
                #sBPAT = bcolors.BOLD + sPAT[i] + bcolors.ENDC
                #if sPAT[i] in line:    
                 #   print line
                    #boldPat[i] = re.sub(sPAT[i], sBPAT[i], line, re.I)
                    #print boldPat[i]
#
   #     for line in keys:
    #        if sPAT[0] in line:
     #           boldPat = re.sub(sPAT[0], sBPAT, line, re.I)
      #          print boldPat

            #if re.search(sPAT[0:paras], line):
             #   print line
                #print boldPat
             #   print line

    #for line in keys:
    #    line = line.rstrip()

     #   if re.search(PAT, line):
      #      boldPat = re.sub(PAT, BPAT, line, re.I)
       #     print boldPat

        # if re.search(PAT, line):
        #     patlen = len(PAT)
        #     patIndex = line.find(PAT)
        #     patIndex2 = line.find(PAT)
        #     patIndex2 = patIndex + patlen
        #     print patIndex
        #     print line[:patIndex] + bcolors.BOLD + PAT + bcolors.ENDC + line[patIndex2:] 
        #print line

#s = "Your number is <b>123</b>"
    #m = re.search(r"\d+", s)
    #print m.group()

#    SLOG = raw_input (">>> ")
#    os.environ ["SLOG"] = SLOG
#    subprocess.call(['grep --color=auto -n $SLOG chatbotlog'], shell=True)
