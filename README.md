# 💞 AI 코딩 활용 영어수업 과제 만들기 
## 오은지, 정하은, 윤세희
### 2024년 12월 11일

## Lesson Plan 수정 완료 (로미오와 줄리엣 Listening & Speaking) - 활동에 파이썬 코드만 넣으면 될거같아요 (교수님꺼 넣기, 본문 통 tts)
![image](https://github.com/user-attachments/assets/2cf43f8c-980e-4033-9eb8-c7792889c923)

!pip install gradio
!pip install gtts
!pip install SpeechRecognition

import gradio as gr
from gtts import gTTS
import speech_recognition as sr
from difflib import SequenceMatcher
import tempfile
import os

# Define your sentences here
sents = [
    "In the small mountain village of Echo Ridge, adventure was a part of everyday life. Nestled among towering peaks, the village was said to be protected by the 'Guardian of the Glen,' a massive eagle that supposedly watched over the villagers from its perch high in the mountains. The legend inspired many adventurous tales among the villagers, especially the children.",
    "Among these children was a bright-eyed eighth grader named Alex. Alex was known for his daring spirit and his love for exploring the rugged landscapes around Echo Ridge. He had a particular fascination with old maps and tales of hidden treasures that had been lost in the mountains centuries ago.",
    "One day, while exploring the local library, Alex stumbled upon an ancient map tucked inside a forgotten book on village lore. The map hinted at the location of a lost treasure, hidden deep within a cave known as Whispering Hollow. Excited by the prospect of a real adventure, Alex decided to seek out the treasure.",
    "Knowing the journey would be risky, he enlisted the help of his best friends, Mia and Sam. Together, they prepared for the expedition, gathering supplies and studying the map extensively. They planned their route, took note of landmarks, and readied themselves for any challenges they might face.",
    "Their journey began at dawn. They trekked through dense forests, crossed rushing streams, and climbed steep cliffs. Along the way, they encountered various wildlife and navigated through tricky terrain, their map guiding them every step of the way.",
    "After hours of hiking, they finally reached Whispering Hollow. The cave was more magnificent than they had imagined, filled with intricate stalactites and echoes of dripping water. Using their flashlights, they ventured deeper into the cave, guided by the markings on the map.",
    "As they reached the heart of the cave, they discovered an ancient chest hidden behind a fallen boulder. With hearts pounding, they moved the boulder and opened the chest. Inside, instead of gold or jewels, they found a collection of old artifacts: pottery, coins, and a beautifully carved statuette of an eagle — the Guardian of the Glen.",
    "Realizing the historical significance of their find, they decided to donate the artifacts to the local museum. The village celebrated their discovery, and the children were hailed as heroes. Their adventure brought the community together, sparking a renewed interest in the history and legends of Echo Ridge. Alex, Mia, and Sam became local legends, known not only for their daring but also for their spirit of discovery and respect for heritage. They continued to explore the mountains, each adventure strengthening their friendship and deepening their connection to their village.",
    "The legend of the Guardian of the Glen lived on, not just as a protector but as a symbol of adventure and discovery, inspiring future generations to explore the mysteries of Echo Ridge."
]

def text_to_speech(selected_sentence, language):
    tld = 'co.uk' if language == "British English" else 'com'

    sn = int(selected_sentence.split(".")[0])  # Extract the sentence number
    mytext = sents[sn - 1]  # Get the selected sentence

    tts = gTTS(text=mytext, lang='en', tld=tld, slow=False)
    filename = 'output.mp3'
    tts.save(filename)
    return filename

def recognize_speech_from_microphone(audio_path):
    recognizer = sr.Recognizer()
    try:
        with sr.AudioFile(audio_path) as source:
            audio_data = recognizer.record(source)
            text = recognizer.recognize_google(audio_data)
            return text
    except sr.UnknownValueError:
        return "Could not understand the audio"
    except sr.RequestError as e:
        return f"Could not request results from Google Speech Recognition service; {e}"
    except Exception as e:
        return str(e)

def calculate_similarity(original_text, recognized_text):
    return SequenceMatcher(None, original_text.lower(), recognized_text.lower()).ratio() * 100

def process_audio(selected_sentence, audio_path):
    sn = int(selected_sentence.split(".")[0])  # Extract the sentence number
    original_text = sents[sn - 1]  # Get the selected sentence
    recognized_text = recognize_speech_from_microphone(audio_path)
    if "Error" in recognized_text or "Could not" in recognized_text:
        return recognized_text, 0.0
    similarity = calculate_similarity(original_text, recognized_text)
    return recognized_text, similarity

def display_sentence(selected_sentence):
    sn = int(selected_sentence.split(".")[0])
    return sents[sn - 1]

with gr.Blocks() as demo:
    with gr.Row():
        with gr.Column():
            gr.Markdown("### Text-to-Speech Converter")
            dropdown_sentences = gr.Dropdown(choices=[f"{i}. {sents[i-1]}" for i in range(1, len(sents) + 1)], label="Select Sentence")
            radio_language = gr.Radio(choices=['American English', 'British English'], label="Language")
            generate_tts_button = gr.Button("Generate Speech")
            tts_audio_output = gr.Audio(type="filepath", label="Output Audio")
            generate_tts_button.click(text_to_speech, inputs=[dropdown_sentences, radio_language], outputs=tts_audio_output)
            selected_sentence_display = gr.Textbox(label="Selected Sentence", interactive=False)
            dropdown_sentences.change(display_sentence, inputs=dropdown_sentences, outputs=selected_sentence_display)

    with gr.Row():
        with gr.Column():
            gr.Markdown("### Pronunciation Evaluator")
            mic_input = gr.Audio(label="Your Pronunciation", type="filepath")
            result_button = gr.Button("Evaluate Pronunciation")
            recognized_text = gr.Textbox(label="Recognized Text")
            similarity_score = gr.Number(label="Similarity (%)")

            result_button.click(process_audio, inputs=[dropdown_sentences, mic_input], outputs=[recognized_text, similarity_score])

demo.launch()


## Overview 
This lesson plan is designed for middle school students and focuses on enhancing Listening and speaking skills through interactive activities using Gradio and Python coding. The lesson is based on the story "Romeo and Juliet."

## Objectives

📚 Introduce and discuss key vocabulary from the story to enhance students’ understanding of the text.

🧠 Develop listening comprehension skills through TTS-generated narration and character dialogues.

✅ Improve speaking and pronunciation skills by practicing and recording role-play dialogues.

🎙️ Foster students’ ability to express emotions and intonation through character-based speaking activities



## Teaching Procedure (55 minutes in total)

1. 🎧 Listening Activity (35 minutes)

(1) Pre-Listening Activity: Learning New Words (10 minutes)

🎯 Objective: Introduce and discuss new vocabulary from the story.


📱 Activity:

Use the Gradio Wordcloud App to generate a word cloud of key vocabulary from the story.

Students analyze the word cloud to predict the story's content.


👨‍🏫 Teacher's Role:

Project the word cloud and guide a discussion on the words.

Explain meanings, use examples, and answer questions.

Encourage students to share their thoughts on how the words might relate to the story's theme.

Highlight any challenging or unusual words and explain their significance in the context of the story.



👦👧 Students' Role:

Discuss predictions based on the word cloud.

Take notes and ask about unfamiliar vocabulary.

Share personal ideas or examples related to the words during the discussion.

Work together in pairs or small groups to explore possible connections between the words.



(2) Main Listening Activity: TTS Listening (15 minutes)

🎯 Objective: Improve listening comprehension and engagement.


📱 Activity:

Play a TTS-generated narration of the story using pyttsx3 or an external TTS library.

Provide a handout with comprehension questions for students to answer as they listen.

👨‍🏫 Teacher's Role:

Play the TTS narration.

Pause after each section to ask comprehension questions and ensure understanding.

👦👧 Students' Role:

Listen actively and complete the comprehension questions.



(3) Pair Listening: TTS Dialogues (10 minutes)

🎯 Objective: Understand the dialogue between Romeo and Juliet through TTS.


📱 Activity:

Use TTS to play dialogue between Romeo and Juliet.
Focus on tone, intonation, and expression.


👨‍🏫 Teacher's Role:

Play the TTS dialogues.

[Romeo & Juliet dialogue]

Juliet: Oh, Romeo, Romeo! Where are you, Romeo?

Romeo: Juliet, I am here, standing below your window.

Juliet: Why must our families hate each other? Why can’t we be together?

Romeo: I don’t care about my family’s name. I only care about you, Juliet.

Juliet: If you truly love me, promise to stay with me forever.

Romeo: I promise, my love. I will always be with you, no matter what.

Juliet: Then let’s marry in secret and prove that love can conquer anything.

Discuss how the characters’ emotions are conveyed through tone and intonation.


👦👧 Students' Role:

Listen carefully and discuss the emotions of the characters.



2. 🎙 Speaking Activity (20 minutes)
   
(1) Role-Playing Activity: Recreate the Scene (10 minutes

🎯 Objective: Enhance speaking skills and practice expression through role-playing.

📱 Activity:

Students use a recording app (e.g., Gradio Audio Recorder) to record their own dialogue as Romeo and Juliet.

Encourage them to mimic the tone and emotion from the TTS examples.


👨‍🏫 Teacher's Role:

Assign roles and help students practice lines.

Provide constructive feedback on pronunciation and intonation.

Encourage students to act out the scene with expression and emotion.

Offer guidance on body language and facial expressions to enhance the performance.


👦👧 Students' Role:

Practice and record their role-play.

Listen to their recordings and refine their delivery.

Focus on improving fluency and confidence while speaking.

Collaborate with peers to give and receive feedback on each other's performances.


(2) Feedback and Sharing (10 minutes)

🎯 Objective: Reflect on speaking performance and improve further.

📱 Activity:

Play back the recorded dialogues in class.
Discuss areas for improvement and celebrate strong performances.

👨‍🏫 Teacher's Role:

Facilitate discussion and provide specific feedback.
Highlight good examples of expression and clarity.

👦👧 Students' Role:

Share recordings and reflect on feedback.
Set goals for future speaking improvement.

### Notes for Teachers

- ✅ Ensure all Gradio apps are set up and tested before the lesson.
- 🛠️ Be prepared to assist students with any technical issues that may arise while using the apps.
- 💬 Encourage students to actively participate and ask questions throughout the lesson.
- ⚙️ Adapt the activities as needed based on the students' proficiency levels and engagement.

## Lesson Materials 로미오와 줄리엣에 맞게 하면 되는데 자료는 있지만 삽입은 어떻게 하지?(텍스트 이미지 삽입 완료 했습니다 -하은)

### Story Title: Oh, Romeo Romeo! 
+ [text link](https://github.com/5eunji/Final-project-G3/blob/main/Oh%2C%20Romeo%20Romeo_text!.txt)
+ [image link](https://github.com/5eunji/Final-project-G3/blob/main/%EB%A1%9C%EB%AF%B8%EC%98%A4%EC%99%80%20%EC%A4%84%EB%A6%AC%EC%97%A3_combined.png)

#### :blush::blue_book:We made a picturing book to help get the story quickly! Click the link below!:)📙 text 이미지 사진북 만들어야함 -> 하은 토요일 오전까지 해놓겠습니다 
+ [picture book link](https://www.childbook.ai/book/s/the-guardians-secret-spgd)

**<Synopsis>** 수정 완료했습니다 - 하은
In Verona, an Italian city torn apart by the feud between two powerful families, the Montagues and the Capulets, young Romeo and Juliet's love story unfolds as a timeless tale of passion and tragedy. While attending a masquerade ball hosted by the Capulets, Romeo Montague secretly infiltrates the event and encounters Juliet Capulet. Instantly captivated by each other, their love blossoms despite the fierce hatred between their families. Underneath Juliet's window, the two confess their love and vow to marry in secret. They pledge to defy the boundaries set by their families, driven by their devotion to one another. However, their secret union sets off a chain of events that deepens the animosity between the Montagues and the Capulets. As the story progresses, misunderstandings and cruel twists of fate lead to heartbreak and loss, solidifying their love as a symbol of enduring passion and the devastating cost of division. Their story, one of Shakespeare’s greatest tragedies, continues to captivate audiences as a powerful reminder of love’s triumph and the dangers of hatred.


## Huggingface  각각 링크 삽입 필요

<div align=center>
   
| Gradio Wordcloud App | Gradio TTS Listening App | Gradio Cloze Question App | Gradio Image Sequencing App | Gradio Writing Checker App |
|:--:|:--:|:--:|:--:|:--:|
|<a href="https://huggingface.co/spaces/teatwots/wordcloud"> <img src="https://github.com/ShieldEdu/G4-finalproject/blob/main/Images/1.png" alt="wordcloud"> </a>|<a href="https://huggingface.co/spaces/englissi/gstesolfinallistening"> <img src="https://github.com/ShieldEdu/G4-finalproject/blob/main/Images/2.png" alt="tts_app"> </a>|<a href="https://huggingface.co/spaces/englissi/gstesolclozetest"> <img src="https://github.com/ShieldEdu/G4-finalproject/blob/main/Images/3-1.png" alt="cloze_question_app"> </a>|<a href="https://huggingface.co/spaces/teatwots/sequencing"> <img src="https://github.com/ShieldEdu/G4-finalproject/blob/main/Images/4-1.png" alt="image_sequencing_app"> </a>|<a href="https://huggingface.co/spaces/teatwots/grammarchecking"> <img src="https://github.com/ShieldEdu/G4-finalproject/blob/main/Images/5-1.png" alt="writing_checker_app"> </a>|
</div>
