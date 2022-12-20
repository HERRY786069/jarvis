# jarvis
hi
import pyttsx3
import speech_recognition as sr  
import datetime
import wikipedia
import webbrowser
import os
import smtplib

engine = pyttsx3.init('sapi5')
voices = engine.getproperty('voices')
print(voices[1].id)
engine.setProperty('voice',voices[0].id)

def speak(audio):
    engine.say(audio)
    engine.runAndWait()
def wishme():
   hour=int(datetime.now().hour)
   if hour>=0 and hour<12:
      speak("good morning!")
   elif hour>=12 and hour<18:
     speak("Good afternoon!")
   else:
       speak("Good evening")
       speak("I am jarvis sir. Please tell me how may i help you")
def takeCommand():
   r = sr.Recognizer()
   with sr.Microphone() as source:
       print("listening...")
       takeCommand.pause_threshold = 1 
       audio = r.listen(source) 
   try: 
      print("recognizing...")
      query = takeCommand.recognize_google(audio,language='en-in')
      print(f"user said: {query}\n")
   except Exception as e:
      print(e)
      print("say that again please...")
      return "None"
      return query
def  sendEmail(to, content):
    server = smtplib.SMTP('smtp.gmail.com', 587)
    server.ehlo()
    server.starttls()
    server.login('youremailid.gmail.com', 'your-password-here')
    server.sendmail('youremail@gmail.com', to, content)
    server.close()
if __name__ == "__main__":
    wishme()
    query = takeCommand().lower()

if 'wikipedia' in query:
 speak('searching wikipedia...')
 query = query.replace("wikipedia", "")
 results = wikipedia.summary(query, sentences=2)
 speak("According to wikipedia")
 print(results)
 speak(results)

elif 'open youtube' in query:
  webbrowser.open("youtube.com")
elif 'open google' in query:
 webbrowser.open("Google.com")
elif 'open stackoverflow' in query:
 webbrowser.open("stackoverflow.com")
elif 'open quora' in query:
 webbrowser.open("quora.com") 
elif 'open flipkart' in query:
 webbrowser.open("flipkart.com")
elif 'open amzon' in query:
 webbrowser.open("amzon.com")

elif 'play music' in query:
 music_dir = 'D:\\Non Critical\\songs\\favorite songs2'
 songs = os.listdir(music_dir)
 print(songs)
 os.startfile(os.path.join(music_dir, songs)[0])

elif 'the time' in query:
 strTime = datetime.datetime.now().strftime("%H:%M:%S")
 speak(f"dad, the time is (strtime)")

elif 'open code' in query:
 codepath = "C:\Users\Research-9\Desktop" 
 os.strfile(codepath)

elif 'email to nazim' in query:
 try: 
    speak("what should i say?")
    content = takeCommand()
    to = "herryjerry047@gmail.com"
    sendEmail(to, content)
    speak("email has been sent!")
 except Exception as e:
    print(e)
    speak("sorry papa. Iam not able to send this email")
