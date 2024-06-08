# Создание и выполнение командных файлов в среде ОС Linux
**Цель работы:** изучение методов создания и выполнения командных файлов на языке Shell - интерпретатора.

## **Выполнение:**
Создайте и выполните Shell - программы, включающей следующие действия:
Создание Shell - программы
```bash
vi <имя.sh>
```
1. Создать каталог DIR и в нем создать файл Myfile.txt, записать в файл свою фамилию и текущее время.
Содержимое Shell - программы.
```vi
echo -n <"промпт для ввода названия">
read dirname
mkdir $dirname
cd $dirname
echo <"Фамилия"> > Myfile.txt
date +%T >> Myfile.txt
```
```bash
sh shell1.sh
```
2. Переименовать файл Myfile.txt в Old_Myfile.txt и установить у него атрибут ReadOnly.
Содержимое Shell - программы
```vi
mv Myfile.txt Old_Myfile.txt
chmod 444 Old_Myfile.txt
ls -l
```
```bash
cd DIR
sh shell2.sh
```
3. Вычислить омическое сопротивление двух параллельное соединенных резисторов. Значения сопротивлений резисторов в диапазоне от 0,1 ом до 1000 Мом вводить с клавиатуры.
Содержимое Shell - программы
```vi
echo -n "Введите первое сопротивление: "
read firstOm
echo -n "Введите второе сопротивление: "
read secondOm
if [$firstOm -le 100000000 ] && (( $(echo "$firstOm > 0.1" | bc -l) )) && [ $secondOm -le 100000000 ] && (( $(echo "$secondOm > 0.1" | bc -l) )); then
    echo "R = " `echo "scale=2; $firstOm*$secondOm/($firstOm+$secondOm)"|bc`;
else
    echo "Неверное число";
fi
```
```bash
sh shell2.sh
cat shell2.sh
```
```bash
cat <имя файла>
```
4. Перевести заданное десятичное число в шестнадцатеричную форму. Ввод десятичного числа с клавиатуры в диапазоне от 0 до 4096.
```vi
echo "Введите число от 0 до 4096:"
read number
if [[ $number -ge 0]] && [[ $number -le 4096]];
then
echo "Answer: " `echo "ibase=10;obase=16;$number"|bc`;
else
echo "Неверное число";
fi
```
5. Запрос и ввод имени пользователя, сравнение с текущим логическим именем пользователя и вывод сообщения: верно/неверно.
```vi
echo "Введите имя пользователя: "
read userName
if [ "$userName" = "$USER" ];
then
echo "Верно";
else
echo "Неверно";
fi
```
6. Запрос и ввод имени файла в текущем каталоге и вывод сообщения о типе файла.
```bash
echo "Введите имя файла: "
read fileName
if test -a $fileName
then
  if test -d $fileName
  then
    echo "Это директория"
  else
    echo "Это файл"
  fi
else
    echo "Файл не существует"
fi
```
7. Циклическое чтение системного времени и очистка экрана в заданный момент.
```bash
echo -n "Введите время: "
read Time
while [ $(date +%S) != $Time ] ;
do
  sleep 1
done
clear
```
8. Циклический просмотр списка файлов и выдача сообщения при появлении заданного имени в списке.
```bash
name=$1

until [ 'ls -R | grep $name' ]; do
  sleep 1
done
echo "Файл найден!"
```
