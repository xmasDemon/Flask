# Flask
# app.py

```
from flask import Flask, render_template, request

app = Flask(__name__)

@app.route('/', methods=['GET', 'POST'])
def index():
    if request.method == 'POST':
        # Получаем данные из формы
        user_data = request.form.get('user_data')
        # Обрабатываем данные (просто делаем их заглавными буквами)
        processed_data = user_data.upper() if user_data else "Вы не ввели данные"
        return render_template('index.html', result=processed_data)
    return render_template('index.html', result=None)

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

# index.html

```
<!DOCTYPE html>
<html>
<head>
    <title>Flask Docker App</title>
</head>
<body>
    <h1>Приветственное сообщение</h1>
    <p>Добро пожаловать в наше Flask-приложение!</p>
    
    <form method="POST">
        <label for="user_data">Введите текст:</label>
        <input type="text" id="user_data" name="user_data">
        <button type="submit">Отправить</button>
    </form>
    
    {% if result %}
    <h2>Результат обработки:</h2>
    <p>{{ result }}</p>
    {% endif %}
</body>
</html>
```

# requirements.txt

```
flask==2.1.0
werkzeug==2.0.3
```

# Dockerfile

```
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```
![image](https://github.com/user-attachments/assets/2ee88940-e1c3-487c-9795-61c3918c5e8e)
![image](https://github.com/user-attachments/assets/273691c9-7889-4621-b43f-c5ef73f9deed)
