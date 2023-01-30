# Personal Assistant Chat Application Using OpenAI's GPT-3

Are you looking for a personal assistant that can understand and respond to your natural language commands and queries? Look no further! This project uses OpenAI's GPT-3 model to create a personal assistant that can interact with you via speech or text.

The project includes both Speech-to-Text and Text-to-Speech capabilities, allowing you to interact with the assistant in a natural, conversational way. The user interface is similar to a chat application, with typing animations and the ability to replay messages.

## Getting Started

Before you can start using the personal assistant, there are a few requirements and prerequisites that you'll need to take care of:

1. Obtain API/entitlement keys from [OpenAI](https://beta.openai.com/account/api-keys) and [IBM](https://myibm.ibm.com/products-services/containerlibrary).
2. Deploy the TTS and STT models separately.
3. Update the `base_url` values (in `script.js` and `worker.py`) to use the associated links from the deployed TTS, STT models, and localhost.
4. Start up the server (Using the Personal Assistant section)

Once you have your API keys and the models deployed, you can begin bringing up the TTS and STT models by following the below.

## Locally deploying the TTS and STT models

These images take a long time to load, especially on the first load. Note only the building process takes a long time, afterwards the containers will run quickly and smoothly. Please be patient while the images are building. If you wish to speed up the building process, you can remove any models in the `tts` or `stt` files that you do not want.

### Starting the TTS container

Remember to be in the correct directory - always be in the directory for the associated Dockerfile.

In a new terminal run the following commands. If you wish to run the image in the background you can add the `-d` option after `docker run`. Running the image in the background, allows you to continue using this terminal and does not show the logs of the container in the terminal.

```sh
cd models/tts # assuming you are in the root directory of this repository
docker build . -t tts-standalone # this will take a while, you can do other things outside of this terminal while you wait
docker run --rm -it --env ACCEPT_LICENSE=true --publish 1081:1080 tts-standalone # this runs the image in the foreground
```

Now update the `base_url` value in the `workey.py` file for the `text_to_speech` function to `http://localhost:1081`

### Starting the STT container

Remember to be in the correct directory - always be in the directory for the associated Dockerfile.

In a new terminal run the following commands. If you wish to run the image in the background you can add the `-d` option after `docker run`. Running the image in the background, allows you to continue using this terminal and does not show the logs of the container in the terminal.

```sh
cd models/stt # assuming you are in the root directory of this repository
docker build . -t stt-standalone # this will take a while, you can do other things outside of this terminal while you wait
docker run --rm -it --env ACCEPT_LICENSE=true --publish 1080:1080 stt-standalone # this runs the image in the foreground
```

Now update the `base_url` value in the `workey.py` file for the `speech_to_text` function to `http://localhost:1080`

### Deploying these images globally

If you deploy these TTS and STT images globally, you'll need to update the `base_url` values in the `workey.py` file to be correctly configured to the new URL values. Please do not forget this when deploying globally.

## Using the Personal Assistant

### Using Docker

If build and run the application using Docker, you will not have to worry about setting up your environment. The only downside is if you make any changes to the files, you will need to rebuild and run the service each time. To run the application in a Docker container, run the following commands:

```bash
docker build -t chatapp-with-voice-and-openai .
docker run -d -p 8000:8000 chatapp-with-voice-and-openai
```

Then open up your browser and go to `http://localhost:8000`. You can then speak or type your command or query by clicking on the microphone or typing into the message bar. The assistant will then respond with a message and read the message outloud.

### Without Docker

*These commands assumes `python` and `python3`, as well as, `pip` and `pip3` are synonymous/linked*

If you're not using Docker, you will need to set up your environment to allow for the application to run. You can do this within a virtual environment or not. This section assumes you have `python version 3.10+` installed along with its associated `pip` version. Install the required packages with the following command:

```bash
pip install -r requirements.txt
```

Then just run:
```bash
python server.py
```

Then open up your browser and go to `http://localhost:8000`. You can then speak or type your command or query by clicking on the microphone or typing into the message bar. The assistant will then respond with a message and read the message outloud.

## Note

* Make sure to keep your API keys secure and not to share them with anyone.
* Make sure the URLs are working and are correctly used in the code

## Additional Resources

- [OpenAI API documentation](https://beta.openai.com/docs/api-reference/introduction)
- [IBM Watson Text-to-Speech documentation](https://cloud.ibm.com/docs/services/text-to-speech)
- [IBM Watson Speech-to-Text documentation](https://cloud.ibm.com/docs/services/speech-to-text)
- [IBM Watson Speech GitHub](https://github.com/ibm-build-lab/Watson-Speech)


## Demo

Heres a quick video of planning a trip to Portugal with the Assistant. Audio output is not recorded but is there.

[demo-video](demo/demo.mov)


Here is a screenshot of the application in action in dark mode

![visiting-Toronto](demo/visit-toronto-dark.png)


## Conclusion

With the Personal Assistant, you can now interact with your computer in a natural and conversational way. We hope you find this project useful and enjoy using it as much as we enjoyed building it. Learn to build your own on [CognitiveClass.ai](https://cognitiveclass.ai/courses/chatapp-powered-by-openai)



