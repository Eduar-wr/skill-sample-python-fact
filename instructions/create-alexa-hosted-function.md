import openai
import logging
import json
from ask_sdk_core.skill_builder import SkillBuilder
from ask_sdk_core.dispatch_components import AbstractRequestHandler
from ask_sdk_core.handler_input import HandlerInput
from ask_sdk_model import Response

logger = logging.getLogger(__name__)
logger.setLevel(logging.INFO)

api_key = "YOUR_API_KEY"

class GptQueryHandler(AbstractRequestHandler):
    def can_handle(self, handler_input):
        return handler_input.request_envelope.request.intent.name == "GptQueryIntent"

    def handle(self, handler_input):
        query = handler_input.request_envelope.request.intent.slots["query"].value
        response = openai.Completion.create(
            engine="text-davinci-003",
            prompt=query,
            max_tokens=50
        )
        speech_text = response.choices[0].text.strip()
        return handler_input.response_builder.speak(speech_text).response

sb = SkillBuilder()
sb.add_request_handler(GptQueryHandler())
lambda_handler = sb.lambda_handler()
Código generado por IA. Revisar y usar cuidadosamente. Más información sobre preguntas frecuentes.
