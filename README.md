# Voice-Assistant
A voice assistant created on Python, which can speak the time, find information or speak user entered input.

    import subprocess
    import sys

    import wolframalpha
    import pyttsx3
    import tkinter
    import json
    import random
    import operator
    import speech_recognition as sr
    import datetime
    import wikipedia
    import webbrowser
    import os

    import smtplib
    import ctypes
    import time
    import shutil

    from pyttsx3 import voice
    def text_to_speech():
        engine = pyttsx3.init()

        if 'darwin' in sys.platform:
            voices = engine.getProperty('voices')
            for voice in voices:
                if 'Samantha' in voice.name:  # Change 'Samantha' to the desired voice
                    engine.setProperty('voice', voice.id)
                    break

        else:
            voices = engine.getProperty('voices')
            engine.setProperty('voice', voices[1].id)

        return engine

    def speak(audio, engine=None):
        if engine is None:
            engine = text_to_speech()
        engine.say(audio)
        engine.runAndWait()

    def speak_time():
        engine = pyttsx3.init()

        current_time = datetime.datetime.now()

        time_string = current_time.strftime("%I:%M %p")

        engine.say("The time is " + time_string)
        engine.runAndWait()

    def switch_case_example(case):
        if case == 'time':
            speak_time()
        elif case == 'search':
            speak('Enter topic followed by space in space wikipedia')
            search_input = input("Enter topic: ")

            query = search_input.lower()

            if 'wikipedia' in query:
                speak('Searching Wikipedia...')
                query = query.replace("wikipedia", "")
                results = wikipedia.summary(query, sentences = 3)
                speak("According to Wikipedia")
                print(results)
                speak(results)
            else:
                speak('I apologize but I cannot find it.')
                
        elif case == 'speak':
            speak('Enter what you want me to say')
            speech = input("Enter speech: ")
            speak(speech)

        else:
            speak('I am sorry, but my abilities are limited to finding the time and searching information.')


    if __name__ == '__main__':

        speak('How may I help you?')
        speak('I can find the time, search information, or speak your input.')
        print("Tasks : \n1.time \n2.search \n3.speak")
        user_input = input("Enter task: ")
        switch_case_example(user_input)

