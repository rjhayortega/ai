
### An AI Chatbot framework built in Python



Building a chatbot can sound daunting, but it’s totally doable. IKY is an AI powered conversational dialog interface built in Python. With IKY it’s easy to create Natural Language conversational scenarios with no coding efforts whatsoever. The smooth UI makes it effortless to create and train conversations to the bot and it continuously gets smarter as it learns from conversations it has with people. IKY can live on any channel of your choice (such as Messenger, Slack etc.) by integrating it’s API with that platform.

You don’t need to be an expert at artificial intelligence to create an awesome chatbot that has artificial intelligence. With this basic project you can create an artificial intelligence powered chatting machine in no time.There may be scores of bugs. So feel free to contribute  via pull requests.

![](https://media.giphy.com/media/3o84TXUIPsp6GRn4re/source.gif)

### Installation
After any of next methods, you will need to [import db](#restore), and navigate to http://localhost:8001.

### Docker Compose
```sh
docker-compose build
docker-compose up
```

### Docker
```sh
docker build -t "ai-chat-bot" .
docker run --name=chabot-node-1  -e="APPLICATION_ENV=Production" -v ./:/usr/src/app -p 8001:8080 -it ai-chat-bot gunicorn --bind 0.0.0.0:8080 run:app
docker exec -it chabot-node-1 python /usr/src/app/setup.py
```

### without docker

* Then use pip to install all required python packages
```sh
pip install -r requirements.txt
```
* Run setup script for setting up some default intents
```sh
$ python setup.py
```

* Development
```sh
$ python run.py
```
* Production
```sh
$ APPLICATION_ENV="Production" gunicorn -k gevent --bind 0.0.0.0:8001 run:app
```

### Heroku
[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

* add your dev/production configurations in config.py

```python
class Production(Config):
    # MongoDB Database Details
    DB_HOST = "mongodb://127.0.0.1:27017/"
    DB_USERNAME = ""
    DB_PASSWORD = ""

    # Web Server details
    WEB_SERVER_PORT = 80

class Development(Config):
    DEBUG = True
```

### DB
#### Backup
```
docker-compose exec mongodb bash
cd data/
mongodump
exit
docker cp aichatbotframework_mongodb_1:/data/dump .
```

#### Restore
```
docker cp dump aichatbotframework_mongodb_1:/data/
docker-compose exec mongodb bash
cd data
mongorestore --drop --db=iky-ai --dir=dump/iky-ai/
exit
```

