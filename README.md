# vision-api-ocr
We managed to run the code with one image where the image return a text value.....but when we try to run the code with 10 images it does not work...is there any possible way to the run 10 images at the same time?
import os, io
from google.cloud import vision
from google.cloud.vision import types
import pandas as pd

os.environ['GOOGLE_APPLICATION_CREDENTIALS'] = r'anjir.json'

client = vision.ImageAnnotatorClient()

FILE_NAME = 'receipttest4.jpg'
filenamez = 'receipttest5.jpg'
FOLDER_PATH = r'C:\Users\Fadhlan\Desktop\Python venv\image\text'

with io.open(os.path.join(FOLDER_PATH, FILE_NAME), 'rb') as image_file:
    content = image_file.read()


with io.open(os.path.join(FOLDER_PATH, filename), 'rb') as image_file:
    content = image_file.read()

image = vision.types.Image(content=content)
response = client.text_detection(image=image)
texts = response.text_annotations


df = pd.DataFrame(columns=['locale', 'description'])
for text in texts:
    df = df.append(
        dict(
            locale=text.locale,
            description=text.description
        ),
        ignore_index=True
    )
print(df['description'][0])
