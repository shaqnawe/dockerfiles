# Last modified: 2024-10-27T08:38:08.714749+00:00
FROM demisto/python3:3.11.10.113941

COPY requirements.txt .

RUN apk --update add --no-cache --virtual .build-dependencies python3-dev build-base wget git \
  && pip install --no-cache-dir -r requirements.txt \
  && apk del .build-dependencies
