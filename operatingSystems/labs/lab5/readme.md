# Потоковая передача информации между процессом и файлом
**Цель работы:** изучение методов программирования по работе с файлами через системные вызовы и стандартную библиотеку ввода-вывода для языка C.

## **Выполнение:**
С помощью компилятора C создать и выполнить программы, исходный текст которой приведен в примере 1. Модифицировать эту программу для вывода на экран информации о результате создания файла.
1. Прочитать методический материал.
2. Изучить характеристики и синтаксис функций и системных вызовов.
3. Набрать код примера 1 в текстовый файл и произвести компиляцию программы.
```C
#include <sys/types.h>
#include <fcntl.h>
#include <stdio.h>

int main()
{
  int fd;
  size_t size;
  char string[] = "Hello, world!";
  (void)unmask(0);
  if((fd=open("myfile",O_WRONLY | O_CREAT, 0666)) < 0)
  {
    printf("Can't open file\n");
    exit(-1);
  }
  size = write(fd, string, 14);
  if (size != 14)
  {
    printf("Can't write all string\n");
    exit(-1);
  }
  if (close(fd) < 0)
  {
    printf("Can't close file\n");
  }
  return 0;
}
```
4. Проверить работоспособность программы.
5. Модифицировать программу для вывода на экран сообщение о результате создания файла.
```C
#include <sys/types.h>
#include <fcntl.h>
#include <stdio.h>

int main()
{
  int fd;
  size_t size;
  char string[] = "Hello, world!";
  (void)unmask(0);
  if((fd=open("myfile",O_WRONLY | O_CREAT, 0666)) < 0)
  {
    printf("Can't open file\n");
    exit(-1);
  }
  size = write(fd, string, 14);
  if (size != 14)
  {
    printf("Can't write all string\n");
    exit(-1);
  }
  if (close(fd) < 0)
  {
    printf("Can't close file\n");
  }
  if (close(fd) = 0)
  {
    printf("File created!\n");
  }
  return 0;
}
```
6. Проверить работоспособность модифицированной программы.
