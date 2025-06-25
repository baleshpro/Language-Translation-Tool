from flask import Flask, render_template, request
from googletrans import Translator
from gtts import gTTS
import os



# now Iam going to create a simple Flask application that translates text and generates audio from the translated text.

app = Flask(__name__)
translator = Translator()

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/translate', methods=['POST'])
def translate():
    text = request.form['text']
    source_lang = request.form['source_lang']
    target_lang = request.form['target_lang']

    # Translate text
    translated = translator.translate(text, src=source_lang, dest=target_lang)
    translated_text = translated.text

    # Generate audio with gTTS
    tts = gTTS(text=translated_text, lang=target_lang)
    audio_path = "static/output.mp3"
    tts.save(audio_path)

    return render_template('index.html', translated_text=translated_text, audio_path=audio_path, original_text=text)

if __name__ == '__main__':
    app.run(debug=True)
