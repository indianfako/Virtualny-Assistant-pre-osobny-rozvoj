import nltk
from datetime import datetime
import speech_recognition as sr
import matplotlib.pyplot as plt

# Inicializácia knižnice nltk
nltk.download('punkt')

class PersonalDevelopmentAssistant:
    def __init__(self, user_name):
        self.user_name = user_name
        self.goals = []
        self.progress = {}
        self.community_members = []

    def greet_user(self):
        current_hour = datetime.now().hour
        if current_hour < 12:
            return f"Dobré ráno, {self.user_name}!"
        elif 12 <= current_hour < 18:
            return f"Dobrý deň, {self.user_name}!"
        else:
            return f"Dobrý večer, {self.user_name}!"

    def add_goal(self, goal):
        self.goals.append(goal)
        self.progress[goal] = 0
        return f"Cieľ '{goal}' bol pridaný."

    def update_progress(self, goal, progress):
        if goal in self.goals:
            self.progress[goal] = progress
            return f"Pokrok pre cieľ '{goal}' bol aktualizovaný na {progress}%."
        else:
            return f"Cieľ '{goal}' neexistuje."

    def personal_development_tips(self):
        tips = [
            "Stanovte si jasné a dosiahnuteľné ciele.",
            "Pravidelne si robte sebareflexiu.",
            "Investujte do svojho vzdelania a zručností.",
            "Udržujte si pozitívny prístup.",
            "Nájdite si čas na oddych a regeneráciu."
        ]
        return tips

    def virtual_coaching_session(self):
        return "Virtuálne koučingové sedenie je naplánované na budúci týždeň."

    def community_support(self):
        return "Pripojte sa k našej komunite na adrese: www.communitysupport.com"

    def motivate_user(self):
        return f"Pokračujte v skvelej práci, {self.user_name}! Ste na správnej ceste."

    def add_community_member(self, member_name):
        self.community_members.append(member_name)
        return f"{member_name} bol pridaný do komunity."

    def list_goals(self):
        return f"Vaše ciele sú: {', '.join(self.goals)}"

    def list_progress(self):
        progress_list = [f"{goal}: {progress}%" for goal, progress in self.progress.items()]
        return f"Pokrok: {', '.join(progress_list)}"

    def voice_detection(self):
        recognizer = sr.Recognizer()
        with sr.Microphone() as source:
            print("Počúvam...")
            audio = recognizer.listen(source)
            try:
                text = recognizer.recognize_google(audio, language="sk-SK")
                print(f"Rozpoznaný text: {text}")
                return text
            except sr.UnknownValueError:
                return "Nerozumiem, prosím skúste znova."
            except sr.RequestError:
                return "Služba rozpoznávania hlasu nie je dostupná."

    def visualize_progress(self):
        goals = list(self.progress.keys())
        progress_values = list(self.progress.values())

        plt.figure(figsize=(10, 5))
        plt.bar(goals, progress_values, color='blue')
        plt.xlabel('Ciele')
        plt.ylabel('Pokrok (%)')
        plt.title('Vizualizácia pokroku')
        plt.show()

def main():
    assistant = PersonalDevelopmentAssistant("Johan Fako")
    print(assistant.greet_user())
    print(assistant.add_goal("Naučiť sa nový programovací jazyk"))
    print(assistant.update_progress("Naučiť sa nový programovací jazyk", 50))
    print("Tu sú niektoré tipy na osobný rozvoj:")
    for tip in assistant.personal_development_tips():
        print(f"- {tip}")
    print(assistant.virtual_coaching_session())
    print(assistant.community_support())
    print(assistant.motivate_user())
    print(assistant.add_community_member("Nový člen"))
    print(assistant.list_goals())
    print(assistant.list_progress())
    print(assistant.voice_detection())
    assistant.visualize_progress()

if __name__ == "__main__":
    main()
