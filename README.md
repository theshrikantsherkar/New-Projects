# New-Projects
This repository consists of the latest new projects coded by me.

print("\t\t\t\tWelcome here!!!\n \t\t\t\ti am J.A.R.V.I.S")

import os
import pyttsx3
import datetime
import speech_recognition as sr
import pyaudio
import wikipedia
import webbrowser
import smtplib
import random

num = random.randint(0, 80)


lst = ["sir, you are looking great.", "i like your hairstyle sir.", "boss you are looking cute today.", "boss you look so charming", "wow sir i can't wink my eyes from you", "may you always stay blessed by your such good looks"]
looks = random.choice(lst)



engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')


engine.setProperty('voice', voices[1].id)


def speak(audio):
    engine.say(audio)
    engine.runAndWait()


def wishme():
    hour = int(datetime.datetime.now().hour)
    if hour >= 00 and hour < 12:
        speak(f"good morning boss!!!")
    elif hour >= 12 and hour < 16:
        speak(f"good afternoon boss!!!")
    elif hour >= 16 and hour < 19:
        speak(f"good evening boss!!!")
    else:
        speak(f"good night sir!!!")
    speak(f"i am jarvis, how may i help you?")

def sendEmail(to, content):
    server = smtplib.SMTP('smtp.@gmail.com', 587)
    server.ehlo()
    server.starttls()
    server.login('email id', 'your password ')
    server.sendmail('email id', to, content)
    server.close()

def takecommand():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("\n\nlistening....")
        r.pause_threshold = 1
        audio = r.listen(source)

    try:
        print("recognizing....")
        query = r.recognize_google(audio, language='en-in')
        print("user said:", query)

    except Exception as e:
        # print(e)
        print("\nsay that again please.....")
        # speak('say that again please.....')
        return "none"

    return query


if __name__ == "__main__":
    wishme()  # functions from where we start the actual assistant tasks
    while True:

        query = takecommand().lower()
        if 'what is' in query:
            speak('searching in wikipedia....')
            query = query.replace("what is", "")
            result = wikipedia.summary(query, sentences=2)
            print("According to wikipedia...", result)
            speak("According to wikipedia...")
            speak(result)

        elif 'who is' in query:
            speak('searching in wikipedia....')
            query = query.replace("what is", "")
            result = wikipedia.summary(query, sentences=3)
            print("According to wikipedia...", result)
            speak("According to wikipedia...")
            speak(result)

        elif 'open youtube' in query:
            speak('i hope the internet works fast so that you can enjoy your moment')
            webbrowser.open("youtube.com")

        elif 'open google' in query:
            speak('i hope the internet works fast so that you can enjoy your moment')
            webbrowser.open("google.com")

        elif 'play music' in query or 'play songs' in query:
            music_dir = 'E:\\12th study material\\songs'
            speak('opening some of your favourite songs, i hope you love them')
            songs = os.listdir(music_dir)
            os.startfile(music_dir)
            # print(songs)
            os.startfile(os.path.join(music_dir, songs[num]))

        elif 'time' in query:
            strtime = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"Sir, the time is {strtime}")
            speak('i think you should do what you are supposed to now!')
            print(strtime)

        elif 'code' in query:
            pathCode = "C:\\Users\\Shrikant_Sherkar\\AppData\\Roaming\\Microsoft\\Windows\\Start Menu\\Programs\\Visual Studio Code"
            speak('sir, i guess you are working on a new project')
            os.startfile(pathCode)

        elif 'pycharm' in query:
            speak('sir, i guess you are planning an upgrade for me! ')
            pathPy = "C:\\ProgramData\\Microsoft\\Windows\\Start Menu\\Programs\\JetBrains"
            os.startfile(pathPy)


        elif 'open game' in query:
            speak('sir i think you need some rest or probably a break')
            NfsPath = "E:\\R.G. Catalyst\\Need for Speed - Most Wanted"
            os.startfile(NfsPath)

        elif 'email for me' in query:
            try:
                speak('what should i say?')
                content = takecommand()
                to = "receivers email id"
                sendEmail(to, content)
                speak('email has been sent')
            except Exception as e:
                print(e)
                speak('I am sorry sir, this could not be done now...')

        elif 'hello' in query:
            speak('hello sir! i am jarvis. how are you?')

        elif 'you there' in query:
            speak('always there for you sir!')

        elif 'quit' in query:
            speak('as you say sir,\n i hope i was worth your time!')
            break

        elif 'looking' in query or 'look' in query:
            speak(looks)

        elif 'introduce' in query:
            speak('hi, my name is JARVIS. i am a virtual assistant program designed and coded by Mr. Prashant. My name stands for '
                  'Just AnotheR Very Intelligent System. i can help you completing your daily tasks. what do you want me to do sir?')
            print("hi, my name is J.A.R.V.I.S. i am a virtual assistant program designed and coded by Mr. Prashant. My name stands for "
                  "Just AnotheR Very Intelligent System. i can help you completing your daily tasks. what do you want me to do?")











