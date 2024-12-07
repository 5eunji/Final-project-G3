# 💞 AI 코딩 활용 영어수업 과제 만들기 
## 오은지, 정하은, 윤세희
### 2024년 12월 11일

## Useful Links 삭제 예정 참고용 
|💠[Emoji](https://gist.github.com/rxaviers/7360908) | 💠[ProjectGuide](https://github.com/MK316/Spring2024/blob/main/DLTESOL/project/README.md) | 💠[Reading material](https://raw.githubusercontent.com/MK316/Spring2024/main/DLTESOL/project/story02.txt) | 💠[CodePage](https://github.com/ShieldEdu/G4-finalproject/blob/main/FPG04.ipynb) | 💠 [APP#1-Wordcloud](https://huggingface.co/spaces/teatwots/wordcloud) | 💠 [APP#2-TTS-listening](https://huggingface.co/spaces/englissi/gstesolfinallistening) | 💠 [APP#3-Cloze test](https://huggingface.co/spaces/englissi/gstesolclozetest) | 💠 [APP#4-Sequencing app](https://huggingface.co/spaces/teatwots/sequencing) | 💠 [APP#5-Grammar Checker](https://huggingface.co/spaces/teatwots/grammarchecking)  | 

## Lesson Plan 로미오와 줄리엣 구문 이용해서 리스닝, 스피킹 위주, 학생:대화문 직접 듣고 앱 이용해서 녹음해보고 롤플레이형식 직접하기
![Final Banner](https://github.com/5eunji/Final-project-G3/blob/main/Oh%2C%20Romeo%20Romeo!.png)

## Overview
This lesson plan is designed for middle school students and focuses on enhancing writing and grammar skills through interactive activities using Gradio and Python coding. The lesson is based on the story "Romeo and Juliet."

## Objectives 우리꺼에 맞게 수정완료 
📚 Introduce and discuss key vocabulary from the story to enhance students’ understanding of the text.
🧠 Develop listening comprehension skills through TTS-generated narration and character dialogues.
✅ Improve speaking and pronunciation skills by practicing and recording role-play dialogues.
🎙️ Foster students’ ability to express emotions and intonation through character-based speaking activities



##Teaching Procedure (55 minutes in total)

1. 🎧 Listening Activity (35 minutes)
2. 
(1) Pre-Listening Activity: Learning New Words (10 minutes)

🎯 Objective: Introduce and discuss new vocabulary from the story.

📱 Activity:

Use the Gradio Wordcloud App to generate a word cloud of key vocabulary from the story.
Students analyze the word cloud to predict the story's content.

👨‍🏫 Teacher's Role:

Project the word cloud and guide a discussion on the words.
Explain meanings, use examples, and answer questions.

👦👧 Students' Role:

Discuss predictions based on the word cloud.
Take notes and ask about unfamiliar vocabulary.

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
Discuss how the characters’ emotions are conveyed through tone and intonation.

👦👧 Students' Role:
Listen carefully and discuss the emotions of the characters.

2. 🎙 Speaking Activity (20 minutes)
(1) Role-Playing Activity: Recreate the Scene (10 minutes)
🎯 Objective: Enhance speaking skills and practice expression through role-playing.

📱 Activity:
Students use a recording app (e.g., Gradio Audio Recorder) to record their own dialogue as Romeo and Juliet.
Encourage them to mimic the tone and emotion from the TTS examples.

👨‍🏫 Teacher's Role:
Assign roles and help students practice lines.
Provide constructive feedback on pronunciation and intonation.

👦👧 Students' Role:
Practice and record their role-play.
Listen to their recordings and refine their delivery.

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

### 기타 이건 지워도 되는건가?
+ [App Link](https://huggingface.co/spaces/ejun123/ReadAloud)
+ [App Link2](https://ejun123-ReadAloud.hf.space)
+ [QR code](https://mrkim21.github.io/appfolder/qrcode.html)
+ [Emoji](https://gist.github.com/rxaviers/7360908)

|a|b|c|
|--|--|--|
|1|2|3|

![Image](https://github.com/junkyuhufs/HUFSworkshop/raw/main/data/tiger.jpg)
