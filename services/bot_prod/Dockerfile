FROM python:3.9-slim-bullseye
WORKDIR /app
ENV APP_PATH=services/bot_prod
COPY . .
RUN pip install -r $APP_PATH/requirements.txt

CMD ["python3", "services/bot_prod/app.py"]