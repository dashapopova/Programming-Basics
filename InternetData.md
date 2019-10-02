
## Internet data

To download a page from the Internet you can use the `urllib.request` module. (Here are some alternative modules: https://stackoverflow.com/questions/7191337/python-better-network-api-than-urllib)

When we try to open a webpage, our browser sends a request to the server ("Hi server! I would like to get the code of the page with the following address!"), and the server sends its answer ("Hi! Here is the requested code: ..."). To get a webpage using python, you need to formulate your request to the server:


```python
import urllib.request #importing module
import re
req = urllib.request.Request('https://habr.com/')
with urllib.request.urlopen(req) as response:
   html = response.read().decode('utf-8')
```

The variable `req` contains our request. The function `urlopen` gets the answer from the server and downloads the page the has the link https://habr.com/ into the `response` variable. The `response` variable acts as a file: for example, we can read its content into a new variable with the function `.read()`. In our example we ended up saving the contents of the web page into the variable `html`. Let's make sure that we have the html-code stored in this variable:


```python
print(html[:210])
```

    <!DOCTYPE html>
    <html lang="ru" class="no-js">
      <head>
        <meta http-equiv="content-type" content="text/html; charset=utf-8" />
    <meta content='width=1024' name='viewport'>
    <title>Лучшие публикации за сутки / 
    

Sometimes the server blocks unfriendly (in its opinion) requests. Instead of saying to the server 'Hi! I am Python-urllib/3.5' your program can pretend to be a well-respected browser:


```python
url = 'https://habr.com/'
user_agent = 'Mozilla/5.0 (Windows NT 6.1; Win64; x64)' 
req = urllib.request.Request(url, headers={'User-Agent':user_agent})  

with urllib.request.urlopen(req) as response:
   html = response.read().decode('utf-8')
```

Imagine that we want to extract specific information from the code we've got, e.g., to extract all the article titles. We can view the source code of the page we've downloaded <view-source:https://habr.com/> and notice that the article titles are tagged **h2** with the **post__title** class. The article title looks like that:

<h2 class="post__title">
    <a href="https://habr.com/company/google/blog/425279/" class="post__title_link">Как собеседует Google: чему быть, чего не миновать</a>
  </h2>

To extract all the article titles, let's use a regular expression.


```python
regPostTitle = re.compile('<h2 class="post__title">.*?</h2>', flags= re.DOTALL)
titles = regPostTitle.findall(html)
```

Let's see how many titles there are and let's print the first three titles.


```python
print(len(titles))
```

    20
    


```python
print(titles[:3])
```

    ['<h2 class="post__title">\n    <a href="https://habr.com/ru/post/469659/" class="post__title_link">RC Машинки: Введение</a>\n  </h2>', '<h2 class="post__title">\n    <a href="https://habr.com/ru/post/469667/" class="post__title_link">Права в Linux (chown, chmod, SUID, GUID, sticky bit, ACL, umask)</a>\n  </h2>', '<h2 class="post__title">\n    <a href="https://habr.com/ru/company/jetinfosystems/blog/469651/" class="post__title_link">WIBAttack. Так ли страшна новая уязвимость SIM-карт</a>\n  </h2>']
    

Now let's clean the titles and delete all the line breaks and tags and print the prettified version.


```python
new_titles = []
regTag = re.compile('<.*?>', re.DOTALL)
regSpace = re.compile('\s{2,}', re.DOTALL)
for t in titles:
    clean_t = regSpace.sub("", t)
    clean_t = regTag.sub("", clean_t)
    new_titles.append(clean_t)
for t in new_titles:
    print(t)
```

    RC Машинки: Введение
    Права в Linux (chown, chmod, SUID, GUID, sticky bit, ACL, umask)
    WIBAttack. Так ли страшна новая уязвимость SIM-карт
    Управление распределенной командой в режиме многопроектности (обзор и видео доклада)
    Как накормить миллионы китайцев за полчаса
    Справочная: подробно об iPhone 11, 11 Pro и новых Apple Watch после двух недель тестирования
    Исследование: если покупатель понимает, что говорит с чат-ботом, то покупка не состоится вовсе
    Путеводитель по Солнечной системе для автостопщиков
    Курение, ЗОЖ, мотивация и скорость разработки ПО
    Зачем вам служба поддержки, которая не поддерживает?
    9 лучших опенсорс находок за сентябрь 2019
    Celestia: приключения багов в космосе
    Как мы в Parallels покоряли Sign In with Apple
    Охладить вино быстро! Российское изобретение
    Регулярная Авалония
    В 90-х рэпер MC Hammer разрабатывал игру, но сегодня U Can't Touch This
    Настройка VSCode для работы с Scala
    Человеческое сознание. Перенести нельзя скопировать?
    Деревянные игрушки, часть пятая — 1991
    Опубликован список из 25 самых опасных уязвимостей ПО
    

Now let's replace html-sequences nbsp and rarr with an arrow:


```python
for t in new_titles:
    print(t.replace("&nbsp;&rarr;", " -> "))
```

    RC Машинки: Введение
    Права в Linux (chown, chmod, SUID, GUID, sticky bit, ACL, umask)
    WIBAttack. Так ли страшна новая уязвимость SIM-карт
    Управление распределенной командой в режиме многопроектности (обзор и видео доклада)
    Как накормить миллионы китайцев за полчаса
    Справочная: подробно об iPhone 11, 11 Pro и новых Apple Watch после двух недель тестирования
    Исследование: если покупатель понимает, что говорит с чат-ботом, то покупка не состоится вовсе
    Путеводитель по Солнечной системе для автостопщиков
    Курение, ЗОЖ, мотивация и скорость разработки ПО
    Зачем вам служба поддержки, которая не поддерживает?
    9 лучших опенсорс находок за сентябрь 2019
    Celestia: приключения багов в космосе
    Как мы в Parallels покоряли Sign In with Apple
    Охладить вино быстро! Российское изобретение
    Регулярная Авалония
    В 90-х рэпер MC Hammer разрабатывал игру, но сегодня U Can't Touch This
    Настройка VSCode для работы с Scala
    Человеческое сознание. Перенести нельзя скопировать?
    Деревянные игрушки, часть пятая — 1991
    Опубликован список из 25 самых опасных уязвимостей ПО
    

+ What does `re.compile` do?

Roughly speaking, `compile()` let's us compile the regular expression (turn a regular expression string into a special object) and use it multiple times. `re.search(..., ...)` first compiles the regular expression and then searches for the matching sequences -- great if we search just once. 


```python
text = 'our text'
regName = re.compile('our regular expression') # compiling our regular expression
toSearch = regName.search(text) 
toFindAll = regName.findall(text)  
toSub = regName.sub('replacement', text) 
```

+ What does `regName.sub(..., ...)` do?

`regName.sub('replacement', text)` means: take the compiled regular expression from the `regName` variable, and replace everything that corresponds to this regular expression in the variable `text` with 'replacement'. 

+ What is `re.DOTALL`?

A dot in a regular expression means any symbol except for the new line symbol.  By adding `flags = re.DOTALL` we ensure that the dot will mean any symbol including the new line symbol.
