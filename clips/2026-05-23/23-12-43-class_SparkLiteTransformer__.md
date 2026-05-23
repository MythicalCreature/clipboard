---
date: 2026-05-23T23:12:43+08:00
source: clipboard
chars: 496
---

class SparkLiteTransformer {
  name = 'spark-lite-transformer';
  endPoint = '/v1/chat/completions';
  async transformRequestIn(request, provider) {
    if (Array.isArray(request.messages)) {
      request.messages = request.messages.map(message => {
        if (message.content && typeof message.content !== "string") {
          message.content = JSON.stringify(message.content);
        }
        return message;
      });
    }
    return request;
  }
}
module.exports = SparkLiteTransformer;
