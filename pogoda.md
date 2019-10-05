

```python
import urllib.request
import urllib.error
import re


def downloading_page():
    user_agent = 'Mozilla/5.0 (Windows NT 6.1; Win64; x64)'
    try:
        req = urllib.request.Request('https://yandex.ru/pogoda/moscow/', headers={'User-Agent': user_agent})
        with urllib.request.urlopen(req) as response:
            html = response.read().decode('utf-8')
            return html
    except urllib.error.URLError as e:
        print(e.reason)


def temp_and_cloud(html):
    # The part about the temperature
    final_temp = []
    regtemp = re.compile('Сегодня</div>.*?</a></div>', re.DOTALL)
    temp = regtemp.findall(html)
    regtag = re.compile('<.*?>', re.DOTALL)
    regword = re.compile(r'[^\x00-\x7F\x80-\xFF\u0100-\u017F\u0180-\u024F\u1E00-\u1EFF]')  # nothing except Latin
    regdate = re.compile(r'\d.*?[.]', re.DOTALL)
    # Actually, i could just slice the important part, but i practiced re.
    for i in temp:
        clean_temp = regtag.sub('', i)
        clean_temp = regword.sub('', clean_temp)
        clean_temp = regdate.sub('', clean_temp)
        final_temp.append(clean_temp)

    # \u00b0 = ° in unicode. All this trouble with the degree sign is that it's the same as russian "о" for python.
    # the part of code here finds out where to slice the info about the temperature so it fits nicely for day and night
    # parts.
    degree_sign1 = '\u00b0\+'
    degree1 = re.search(degree_sign1, str(final_temp))
    degree1 = str(degree1)
    # Now we need to find where re.search span ends and this number is the place to slice.
    degree1 = re.findall(' \d+', degree1)
    slice_temp = int(degree1[0][1:]) - 1
    # The first two and the last two elements are brackets of the list, which was converted to string.
    print('Температура днём: ' + str(final_temp)[2:slice_temp] + '\n'
          + 'Температура ночью: ' + str(final_temp)[slice_temp:-2])

    # The part about the clouds
    final_cloud = []
    cloud = regtemp.findall(html)
    for i in cloud:
        clean_cloud = regtag.sub('', i)
        final_cloud.append(clean_cloud)
    degree_sign2 = 'ночью.*?\u00b0'
    degree2 = re.search(degree_sign2, str(final_cloud))
    degree2 = str(degree2)
    # Now we need to find where re.search span ends and this number is the place to slice.
    degree2 = re.findall(' \d+', degree2)
    slice_cloud = int(degree2[0][1:])
    # Here the second degree symbol is found and the rest of the text after it is shown
    print('Облачность: ' + str(final_cloud)[slice_cloud:-2])


temp_and_cloud(downloading_page())

```

    Температура днём: 5 +11°
    Температура ночью: +4°
    Облачность: Пасмурно
    


```python
def sunrise_sunset(html):
    # Sunrise part
    final_sunrise = []
    regsunrise = re.compile('Восход</span>.*?</dl>', re.DOTALL)
    sunrise = regsunrise.findall(html)
    regtag = re.compile('<.*?>', re.DOTALL)
    for i in sunrise:
        clean_sunrise = regtag.sub('', i)
        final_sunrise.append(clean_sunrise)
        print(str(final_sunrise[0][0:6]) + ' сегодня в ' + str(final_sunrise[0][6:]))

    # Sunset part
    final_sunset = []
    regsunset = re.compile('Закат</span>.*?</dl>', re.DOTALL)
    sunset = regsunset.findall(html)
    regtag = re.compile('<.*?>', re.DOTALL)
    for i in sunset:
        clean_sunset = regtag.sub('', i)
        final_sunset.append(clean_sunset)
        print(str(final_sunset[0][0:5]) + ' сегодня в ' + str(final_sunset[0][5:]))
sunrise_sunset(downloading_page())
```

    Восход сегодня в 06:39
    Закат сегодня в 17:55
    
