import speech_recognition as sr

def listen():
    recognizer = sr.Recognizer()

    with sr.Microphone() as source:
        print("Listening...")
        recognizer.adjust_for_ambient_noise(source)
        audio = recognizer.listen(source, timeout=5)

    return audio

def recognize_speech(audio):
    recognizer = sr.Recognizer()

    try:
        print("Recognizing...")
        text = recognizer.recognize_google(audio)
        print(f"You said: {text}")
        return text.lower()
    except sr.UnknownValueError:
        print("Sorry, I could not understand what you said.")
        return ""
    except sr.RequestError as e:
        print(f"Error connecting to Google Speech Recognition service: {e}")
        return ""

def assistant():
    while True:
        print("Say something or type 'exit' to end:")
        audio = listen()

        if "exit" in recognize_speech(audio):
            print("Exiting...")
            break

if __name__ == "__main__":
    assistant()
