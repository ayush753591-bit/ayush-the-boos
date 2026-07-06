# ayush-the-boos
import os
import webbrowser
impot speech_recognition as sr

sites = [
    ["youtube", "https://youtube.com"],
    ["wikipedia", "https://wikipedia.com"],
    ["google", "https://google.com"],
    ["github", "https://github.com"],
]

def say(text):
    os.system(f'say "{text}"')


def takeCommand():
    r = sr.Recognizer()
    with sr.Microphone() as source:
        print("Listening...")
        r.pause_threshold = 1
        audio = r.listen(source)
        try:
            query = r.recognize_google(audio, language='en-in')
            print(f"User said: {query}")
            return query
        except Exception as e:
            print(f"Error: {e}")
            return ""


if __name__ == '__main__':
    print('PyCharm')
    say("I am Jarvis A.I, How can I help you sir?")
    while True:
        print("Listening...")
        query = takeCommand()

        # Open sites
        for site in sites:
            if f"open {site[0]}" in query.lower():
                say(f"Opening {site[0]} sir...")
                webbrowser.open(site[1])
                print (f"Opening {site[0]} sir...")
            if "close {site[0]}" in query.lower():
                say(f"Closing {site[0]} sir...")
                os.system(f"pkill -f {site[0]}")
                print (f"Closing {site[0]} sir...")
                if "exity" in query.lower():
                    say("Exiting sir...")
                    print("Exiting sir...")
                    exit()
