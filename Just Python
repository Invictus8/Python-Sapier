import os
import random

#очистка экрана
def cls():
    os.system('cls' if os.name=='nt' else 'clear')

def poisk(y , x): #узнать есть ли вокруг клетки мины
  poisk_yx = 0
  if pole[y - 1][x - 1] == 2:
    poisk_yx += 1
  if pole[y - 1][x] == 2:
    poisk_yx += 1
  if pole[y - 1][x + 1] == 2:
    poisk_yx += 1
  if pole[y][x - 1] == 2:
    poisk_yx += 1
  if pole[y][x + 1] == 2:
    poisk_yx += 1
  if pole[y + 1][x - 1] == 2:
    poisk_yx += 1
  if pole[y + 1][x] == 2:
    poisk_yx += 1
  if pole[y + 1][x + 1] == 2:
    poisk_yx += 1
  return poisk_yx

def poisk_pustoti(y , x): #узнать свободные клетки вокруг
  global pole
  pole[y][x] = 0
  if poisk(y , x) == 0:
    if pole[y - 1][x - 1] == 1:
      poisk_pustoti(y - 1, x - 1)
    if pole[y - 1][x] == 1:
      poisk_pustoti(y - 1, x)
    if pole[y - 1][x + 1] == 1:
      poisk_pustoti(y - 1, x + 1)
    if pole[y][x - 1] == 1:
      poisk_pustoti(y , x - 1)
    if pole[y][x + 1] == 1:
      poisk_pustoti(y , x + 1)
    if pole[y + 1][x - 1] == 1:
      poisk_pustoti(y + 1, x- 1)
    if pole[y + 1][x] == 1:
      poisk_pustoti(y + 1, x)
    if pole[y + 1][x + 1] == 1:
      poisk_pustoti(y + 1, x + 1)
      


while True:
  itog = 0
  #0 - поле не закрашено, 1 - поле закрашено, 2 - поле с миной, 9 - граница, не сканируется
  #поле больше на одну клетку в каждую сторону чтобы не вводить
  #проверку на то крайняя ли клетка на поле
   pole = []
  
  vybor = input('1 - Новичок\n2 - Любитель\n3 - Профессионал\n4 - Особый\nВыберите режим (1 - 4):\n')
  cls()
  if not vybor.isdigit():
      cls()
      continue
  if int(vybor) > 4 or int(vybor) < 1:
      cls()
      continue

  if int(vybor) == 1:
    size_pole = [9 , 9]
    miny = 10
    cls()
  elif int(vybor) == 2:
    size_pole = [16 , 16]
    miny = 40
    cls()
  elif int(vybor) == 3:
    size_pole = [26 , 18]
    miny = 99
    cls()
  else:
    size_pole = input('Введите размер поля x (2 - 26) и y (2 - 26) через пробел:\n').split()
    if len(size_pole) != 2:
        cls()
        continue
    if not size_pole[0].isdigit() or not size_pole[1].isdigit():
        cls()
        continue
    size_pole[0] = int(size_pole[0])
    size_pole[1] = int(size_pole[1])
    if int(size_pole[0]) > 26 or int(size_pole[0]) < 2 or int(size_pole[1]) > 26 or int(size_pole[1]) < 2:
        cls()
        continue
    print('Максимальное количество мин:')
    print(size_pole[0] * size_pole[1] - 1)
    miny = input('Введите количество мин:\n')
    if not miny.isdigit():
        cls()
        continue
    if int(miny) > size_pole[0] * size_pole[1] - 1 or int(miny) < 1:
        cls()
        continue
    miny = int(miny)
    cls()
  
  for i in range(size_pole[1] + 2): #строка
      pole.append([])
      for j in range(size_pole[0] + 2): #символ
        if i == 0 or i == size_pole[1] + 1 or j == 0 or j == size_pole[0] + 1:
          pole[i].append(9)
        else:
          pole[i].append(1)
          
          #расстаение мин
  xminy = 0
 
  while xminy < miny:
    xminy_y = random.randint(1 , size_pole[1])
    xminy_x = random.randint(1 , size_pole[0])
    if pole[xminy_y][xminy_x] != 2:
      pole[xminy_y][xminy_x] = 2
      xminy += 1
  
  probely_y_str = '     '
  verh_str = ''
  niz_str = ''
  for i in range(1 , size_pole[0] + 1):
    verh_str += chr(i + 64) + ' '
    niz_str += chr(i + 64) + ' '
    probely_y_str += '  '
  verh_str = '  x ' + verh_str + 'x\ny' + probely_y_str + 'y\n'
  niz_str = 'y' + probely_y_str + 'y\n  x ' + niz_str + 'x\n'



  while True:
    win = 0
    #вывод поля на экран
    print('Количество мин:' , miny)
    image_pole = verh_str
    for i in range(1 , size_pole[1] + 1): #строка
      image_pole += chr(i + 64) + '  '
      for r in range(1 , size_pole[0] + 1): #символ
        if pole[i][r] == 1 or pole[i][r] == 2:
          image_pole += "|■"
        else:
          win += 1
          stroka_p = poisk(i , r)
          if stroka_p == 0:
            image_pole += "| "
          else:
            image_pole += "|" + str(stroka_p)
      image_pole += "|  " + chr(i + 64) + '\n'
    image_pole += niz_str

    if win == size_pole[0] * size_pole[1] - miny: #победа 
      itog = 2
      cls()
      break
      
    print(image_pole)
    
    xy = input('Введите xy:\n')
    if len(xy) != 2:
      cls()
      continue
      
       xy_osh = False
    for i in xy:
      i = ord(i)
      if (i < 65 or i > 90) and (i < 97 or i > 122):
        xy_osh = True
    if xy_osh:
      cls()
      continue

    y = xy[1].lower()
    x = xy[0].lower()

    y = ord(y) - 96
    x = ord(x) - 96

    if y > size_pole[1] or x > size_pole[0]:
      cls()
      continue

    if pole[y][x] == 0:
      cls()
      continue

    if pole[y][x] == 1:
      poisk_pustoti(y , x)
      cls()
      continue

    if pole[y][x] == 2:
      cls()
      itog = 1
      break

    cls()



  if itog == 1:

    print('Количество мин:' , miny)
    image_pole = verh_str
    for i in range(1 , size_pole[1] + 1): #строка
      image_pole += chr(i + 64) + '  '
      for r in range(1 , size_pole[0] + 1): #символ
        if y == i and x == r:
          image_pole += "|X"
        elif pole[i][r] == 1:
          image_pole += "|■"
        elif pole[i][r] == 2:
          image_pole += "|ʘ"
        else:
          stroka_p = poisk(i , r)
          if stroka_p == 0:
            image_pole += "| "
          else:
            image_pole += "|" + str(stroka_p)
      image_pole += "|  " + chr(i + 64) + '\n'
    image_pole += niz_str

    print(image_pole)
    print('!!!\nВЫ ПРОИГРАЛИ\n!!!')
    input()
    cls()
    
     if itog == 2:

    print('Количество мин:' , miny)
    image_pole = verh_str
    for i in range(1 , size_pole[1] + 1): #строка
      image_pole += chr(i + 64) + '  '
      for r in range(1 , size_pole[0] + 1): #символ
        if pole[i][r] == 1:
          image_pole += "|■"
        elif pole[i][r] == 2:
          image_pole += "|ʘ"
        else:
          stroka_p = poisk(i , r)
          if stroka_p == 0:
            image_pole += "| "
          else:
            image_pole += "|" + str(stroka_p)
      image_pole += "|  " + chr(i + 64) + '\n'
    image_pole += niz_str

    print(image_pole)
    print('!!!\nПОЗДРАВЛЯЮ, ВЫ ВЫИГРАЛИ :)\n!!!')
    input()
    cls()