# pythonquiz
from random import sample
from usernp import user
score=0
def menu():
    print("1.Add questions")
    print("2.Take the assesment")
    print("3.Get the score")
    print("4.exit")

def takeQuiz(L):
    global score
    score=0
    for e in L:
        #print(e[0])
        i=1
        print(e[0][0])
        opl=e[0]
        opl=opl[1:]
        for s in opl:
            print(i,":",s)
            i=i+1
        a=input("Enter the correct option:")
        if a==e[1]:
            score=score+1
        else:
            score=score-0.25
    return score

def addQuestions():
    print("1.Add through console")
    print("2.Throgh file")
    ip=int(input("Choose UR option:"))
    if ip==1:
        while True:
            print("Adding questions throgh console...")
            QBF=open("QBank.txt","a")
            Q=input("Enter the question:")
            op1=input("OP1:")
            op2=input("OP2:")
            op3=input("OP3:")
            op4=input("OP4:")
            ans=input("Answer:")
            QBF.write(Q)
            QBF.write("#")
            QBF.write(op1)
            QBF.write("#")
            QBF.write(op2)
            QBF.write("#")
            QBF.write(op3)
            QBF.write("#")
            QBF.write(op4)
            QBF.write("#")
            QBF.write(ans)
            QBF.write("\n")
            yn=input("Would you like to add one more question?...")
            if yn=="no":
                break
        QBF.close()
    else:
        print("Adding qustions throgh file copy...")
        source=input("Enter the file name:")
        fp=open(source,"r")
        QBF=open("QBank.txt","a")
        s=fp.read()
        QBF.write(s)
        fp.close()
        QBF.close()


while True:
    name=input("Enter the user name:")
    pword=input("Enter the password:")
    if user.get(name,None)==pword:
        pass
    else:
        exit()
    menu()
    ch=int(input("Enter your choice:"))
    if ch==1:
        addQuestions()
    elif ch==2:
        QL=[]
        n=int(input("How many questions would you like to have"))
        QBF=open("QBank.txt","r")
        for q in QBF:
            q=q.strip()
            q=q.split("#")
            qop=q[:-1]
            ans=q[-1]
            QL.append([qop,ans])
        #print(QL)
        #print(len(QL))
        QNL=sample(range(len(QL)),n)
        #print(QNL)
        QList=[]
        for i in QNL:
            q=QL[i]
            QList.append(q)
        takeQuiz(QList)
        QBF.close()
        print("You got:",score)
    elif ch==3:
        print("Score is:",score)
    elif ch==4:
        print("Exiting from application....")
        exit()
