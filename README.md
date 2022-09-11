- 👋 Hi, I’m @devansh0331
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
devansh0331/devansh0331 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import pyttsx3
import datetime
import speech_recognition as sr
import pyaudio
import wikipedia
import webbrowser
import os
from PIL import Image , ImageGrab




engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')

engine.setProperty('voice' , voices[1].id)

def speak(audio):
    engine.say(audio)
    engine.runAndWait()

def greeting():
    hour = int(datetime.datetime.now().hour)

    if hour>=4 and hour<12:
        speak("Good Morning Sir!")
    
    elif hour>=12 and hour<16:
        speak("Good Afternoon Sir!")
    
    else:
        speak("Good Evening Sir!")
    
    speak("I'm Zira! An Artificial Intelligence Bot")

def takeScreenshot():
    image = ImageGrab.grab()
    image.show()


def takeInput():
    #Takes microphone input from the user and returns string output

    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)

    try:
        print("Recognizing...")
        query = r.recognize_google(audio , language='en-in')
        print(f"User said: {query}\n")

    except Exception as e:
        print(e)
        print("Please speak again...")
        return "None"

    return query

if __name__ == "__main__":
    greeting()
    x = True
    while x:
        query = takeInput().lower()

        if 'wikipedia' in query:
            speak("Searcing Wikipedia")
            query = query.replace("wikipeida" , "")
            query = query.replace("tell me about" , "")

            results = wikipedia.summary(query, sentences=2) 
            speak("According to wikipedia")
            print(results)
            speak(results)
            
        elif 'open youtube' in query:
            webbrowser.open("youtube.com")
        
        elif 'play song' in query:
            music_dir = 'D:\\music'
            songs = os.listdir(music_dir)
            
            os.startfile(os.path.join(music_dir , songs[0]))

        elif 'time now' in query:
            timeNow = datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"Time is : {timeNow}")

        elif 'search' and 'on youtube' in query:
            query = query.replace('search' , '')
            query = query.replace('on youtube' , '')

            webbrowser.open(f"https://www.youtube.com/results?search_query={query}")

        elif 'search' and 'on google' in query:
            query = query.replace('search' , '')
            query = query.replace('on google' , '')

            webbrowser.open(f"https://www.google.com/search?q={query}&oq=gwimkiper&aqs=chrome.1.69i57j0i546l3j0i30i546.6562j0j7&sourceid=chrome&ie=UTF-8")

        
        elif 'open code' in query:
            codePath = "C:\\Microsoft VS Code\\Code.exe"
            os.startfile(codePath)

        elif 'take screenshot' in query:
            speak("Taking Sreenshot")
            takeScreenshot()

        elif 'stop listening' in query:
            speak("Ok sir! It was nice to talk to you")
            hour = int(datetime.datetime.now().hour)
            if hour > 7 and hour < 20:
                speak("Have a nice day ahead")
            else:
                speak("Good night")
            x = False


        


