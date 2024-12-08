# 💞 AI 코딩 활용 영어수업 과제 만들기 
## 오은지, 정하은, 윤세희
### 2024년 12월 11일

## Lesson Plan 수정 완료 (로미오와 줄리엣 Listening & Speaking) - 어떻게 넣어야하고 수정해야하는지 모르겠어요 내일 다시 해볼께요......
![image](https://github.com/user-attachments/assets/2cf43f8c-980e-4033-9eb8-c7792889c923)


    {
      "cell_type": "markdown",
      "source": [
        "# **While-Listening Activity: Learning New Words**\n",
        "## 2. Gradio TTS App"
      ],
      "metadata": {
        "id": "ALOfAcx5Mho_"
      }
    },
    {
      "cell_type": "code",
      "source": [
        "!pip install gradio\n",
        "!pip install gtts\n",
        "!pip install SpeechRecognition\n",
        "\n",
        "import gradio as gr\n",
        "from gtts import gTTS\n",
        "import speech_recognition as sr\n",
        "from difflib import SequenceMatcher\n",
        "import tempfile\n",
        "import os\n",
        "\n",
        "# Define your sentences here\n",
        "sents = [\n",
        "    \"Romeo and Juliet - A Cruel Twist of Fate.\",\n",
        "    \"Welcome, everyone! Tonight, we are going to perform Shakespeare’s play, Romeo and Juliet. Romeo and Juliet, which was written in the mid-16th century, around 1595, is one of the four great tragedies written by Shakespeare. This was a time when Shakespeare was actively writing, and many of his famous works were created during this period. Before we begin, I’d like to tell you the storyline of Romeo and Juliet. Knowing the story will help you enjoy the play even more. Many years ago, in the city of Verona, Italy, there were two families, the Montagues and the Capulets. These two families were always battling and did not like each other.\",\n",
        "    \"One day, when Romeo Montague, who was a member of the Montague family, secretly went to a Capulet party. There, he saw Juliet Capulet, whose family was one of the most influential families in Verona. As soon as they saw each other, they fell in love. But their love was in danger because of the strong hate between their families. After the Montagues left the party, Romeo went back to the Capulet house and hid outside Juliet’s window. Juliet stood at her window, whispering".\",\n",
        "    \"Oh Romeo, Romeo! Where are you Romeo? Give up your family name, or if you won't, just promise to love me, and I'll give up being a Capulet. Below Juliet's window, Romeo stood in the shadows of a wall. He looked up at her, his heart beating fast. Romeo and Juliet promised to marry in secret and expressed their love for each other. However, their secret was soon discovered, and the battling between the two families got worse. Would Romeo and Juliet be able to keep their love? Let’s watch the play and find out!\"\n",
        "]\n",
        "\n",
        "def text_to_speech(selected_sentence, language):\n",
        "    tld = 'co.uk' if language == \"British English\" else 'com'\n",
        "\n",
        "    sn = int(selected_sentence.split(\".\")[0])  # Extract the sentence number\n",
        "    mytext = sents[sn - 1]  # Get the selected sentence\n",
        "\n",
        "    tts = gTTS(text=mytext, lang='en', tld=tld, slow=False)\n",
        "    filename = 'output.mp3'\n",
        "    tts.save(filename)\n",
        "    return filename\n",
        "\n",
        "def recognize_speech_from_microphone(audio_path):\n",
        "    recognizer = sr.Recognizer()\n",
        "    try:\n",
        "        with sr.AudioFile(audio_path) as source:\n",
        "            audio_data = recognizer.record(source)\n",
        "            text = recognizer.recognize_google(audio_data)\n",
        "            return text\n",
        "    except sr.UnknownValueError:\n",
        "        return \"Could not understand the audio\"\n",
        "    except sr.RequestError as e:\n",
        "        return f\"Could not request results from Google Speech Recognition service; {e}\"\n",
        "    except Exception as e:\n",
        "        return str(e)\n",
        "\n",
        "def calculate_similarity(original_text, recognized_text):\n",
        "    return SequenceMatcher(None, original_text.lower(), recognized_text.lower()).ratio() * 100\n",
        "\n",
        "def process_audio(selected_sentence, audio_path):\n",
        "    sn = int(selected_sentence.split(\".\")[0])  # Extract the sentence number\n",
        "    original_text = sents[sn - 1]  # Get the selected sentence\n",
        "    recognized_text = recognize_speech_from_microphone(audio_path)\n",
        "    if \"Error\" in recognized_text or \"Could not\" in recognized_text:\n",
        "        return recognized_text, 0.0\n",
        "    similarity = calculate_similarity(original_text, recognized_text)\n",
        "    return recognized_text, similarity\n",
        "\n",
        "def display_sentence(selected_sentence):\n",
        "    sn = int(selected_sentence.split(\".\")[0])\n",
        "    return sents[sn - 1]\n",
        "\n",
        "with gr.Blocks() as demo:\n",
        "    with gr.Row():\n",
        "        with gr.Column():\n",
        "            gr.Markdown(\"### Text-to-Speech Converter\")\n",
        "            dropdown_sentences = gr.Dropdown(choices=[f\"{i}. {sents[i-1]}\" for i in range(1, len(sents) + 1)], label=\"Select Sentence\")\n",
        "            radio_language = gr.Radio(choices=['American English', 'British English'], label=\"Language\")\n",
        "            generate_tts_button = gr.Button(\"Generate Speech\")\n",
        "            tts_audio_output = gr.Audio(type=\"filepath\", label=\"Output Audio\")\n",
        "            generate_tts_button.click(text_to_speech, inputs=[dropdown_sentences, radio_language], outputs=tts_audio_output)\n",
        "            selected_sentence_display = gr.Textbox(label=\"Selected Sentence\", interactive=False)\n",
        "            dropdown_sentences.change(display_sentence, inputs=dropdown_sentences, outputs=selected_sentence_display)\n",
        "\n",
        "    with gr.Row():\n",
        "        with gr.Column():\n",
        "            gr.Markdown(\"### Pronunciation Evaluator\")\n",
        "            mic_input = gr.Audio(label=\"Your Pronunciation\", type=\"filepath\")\n",
        "            result_button = gr.Button(\"Evaluate Pronunciation\")\n",
        "            recognized_text = gr.Textbox(label=\"Recognized Text\")\n",
        "            similarity_score = gr.Number(label=\"Similarity (%)\")\n",
        "\n",
        "            result_button.click(process_audio, inputs=[dropdown_sentences, mic_input], outputs=[recognized_text, similarity_score])\n",
        "\n",
        "demo.launch()\n"
      ]

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

## Lesson Materials

### Story Title: Oh, Romeo Romeo! 
+ [text link](https://github.com/5eunji/Final-project-G3/blob/main/Oh%2C%20Romeo%20Romeo_text!.txt)
+ [image link](https://github.com/5eunji/Final-project-G3/blob/main/%EB%A1%9C%EB%AF%B8%EC%98%A4%EC%99%80%20%EC%A4%84%EB%A6%AC%EC%97%A3_combined.png)

#### :blush::blue_book:We made a picturing book to help get the story quickly! Click the link below!:)📙  -> 이미지북 만들었는데 선생님들 화면에서 열리는지 확인 한번 해주세요!
+ [picture book link](https://app.bookcreator.com/read/library/-ODbVVRFt1qwc8vjZI2_/VBDaDwoLP7bd4s7WpgalRoIC3jt2/anvSLBo-QSuYBfBNvbacAA/EAzHAfCXRr-h4-lf0EKb_g)

**<Synopsis>**
In Verona, an Italian city torn apart by the feud between two powerful families, the Montagues and the Capulets, young Romeo and Juliet's love story unfolds as a timeless tale of passion and tragedy. While attending a masquerade ball hosted by the Capulets, Romeo Montague secretly infiltrates the event and encounters Juliet Capulet. Instantly captivated by each other, their love blossoms despite the fierce hatred between their families. Underneath Juliet's window, the two confess their love and vow to marry in secret. They pledge to defy the boundaries set by their families, driven by their devotion to one another. However, their secret union sets off a chain of events that deepens the animosity between the Montagues and the Capulets. As the story progresses, misunderstandings and cruel twists of fate lead to heartbreak and loss, solidifying their love as a symbol of enduring passion and the devastating cost of division. Their story, one of Shakespeare’s greatest tragedies, continues to captivate audiences as a powerful reminder of love’s triumph and the dangers of hatred.


## Huggingface  각각 링크 삽입 필요
   
| Gradio Wordcloud App | Gradio TTS Listening App(1) | Gradio TTS Listening App(2) | Gradio Recorder App(?)
|:--:|:--:|:--:|:--:|:--:|
<a href="https://huggingface.co/spaces/teatwots/wordcloud"> <img src="https://github.com/5eunji/Final-project-G3/blob/main/%EB%A1%9C%EB%AF%B8%EC%98%A4%EC%99%80%20%EC%A4%84%EB%A6%AC%EC%97%A3%201.png" alt="wordcloud"> </a>|<a href="https://huggingface.co/spaces/englissi/gstesolfinallistening"> <img src="https://github.com/ShieldEdu/G4-finalproject/blob/main/Images/2.png" alt="tts_app"> 
</div>
