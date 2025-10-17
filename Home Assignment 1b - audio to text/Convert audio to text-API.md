Audio to text convertor using 

model : whisper-large-v3
API : https://api.groq.com/openai/v1/audio/transcriptions

curl --location 'https://api.groq.com/openai/v1/audio/transcriptions' \
--header 'Content-Type: multipart/form-data' \
--header 'Authorization: Bearer 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' \
--header 'Cookie: __cf_bm=pXy5Tb6zctwT5EZYdii_5YGGEwyPEd0zNHyHRO0EavI-1760631607-1.0.1.1-MninyjxP6cOOQQiwNg0rPE_mnIKY7fd.uUj78ZWeGyJAW2zWeDYPi3fHLh.4BzaWfxNUb_92tTjxIGPuHplgqQRrnXMHtZnY4lVTa.d2w74' \
--form 'model="whisper-large-v3"' \
--form 'file=@"/C:/Users/Admin/Documents/AI Training TestLeaf/Week2Day2-12-Oct-2025/sample-0.mp3"'

--------------------------------
Ouput JSON response : 
200k

{
    "text": " \"'He doesn't belong to you, and I don't see how you have anything to do with what is be his power yet. \"'He's heaps only that from this stage to you.'",
    "x_groq": {
        "id": "req_01k7px4knxe0x81ndya0gbzdme"
    }
}

