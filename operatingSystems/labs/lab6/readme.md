# Передача информации между процессами. Системный вызов pipe
**Цель работы:** изучение методов программирования по взаимодействию процессов через системные вызовы и стандартную библиотеку ввода-вывода.

## **Выполнение:**
1. Прочитан методический материал.
2. Изучены характеристики и синтаксис функций системных вызовов.
3. Набраны коды примеров в текстовые файлы и произведена их компиляция.

Пример 1

```C
#include <sys/types.h>
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>

int main()
{
  int fd[2];
  size_t size;
  char string[] = "Hello, world!";
  char resstring[14];
  if (pipe(fd) < 0)
  {
    printf("Can't create pipe\n");
    exit(-1);
  }
  size = write(fd[1], string, 14);
  if (size != 14)
  {
    printf("Can't write all string\n");
    exit(-1);
  }
  size = read(fd[0], resstring, 14);
  if (size < 0)
  {
    printf("Can't read string\n);
    exit(-1);
  }
  printf("%s\n", resstring);
  if (close(fd[0]) < 0)
  {
    printf("Can't close input stream\n");
  }
  if (close(fd[1]) < 0)
  {
    printf("Can't close output stream\n");
  }
  return 0;
}
```

Пример 2

```C
#include <sys/types.h>
#include <unistd.h>
#include <stdio.h>
#include <stdlib.h>

int main()
{
  int fd[0], result;
  size_t size;
  char resstring[14];
  if (pipe(fd) < 0)
  {
    printf("Can't create pipe\n");
    exit(-1);
  }
  result = fork();
  if (result < 0)
  {
    printf("Can't fork child\n");
    exit(-1);
  }
  else if (result > 0)
  {
    close(fd[0]);
    size = write(fd[1], "Hello, world!", 14);
    if (size != 14)
    {
      printf("Can't write all string\n");
      exit(-1);
    }
    close(fd[1]);
    printf("Parent exit\n");
  }
  else
  {
    close(fd[1]);
    size = read(fd[0], resstring, 14);
    if (size < 0)
    {
      printf("Can't read string\n");
      exit(-1);
    }
    printf("%s\n", resstring);
    close(fd[0]);
  }
  return 0;
}
```

Компиляция программ

```bash
gcc -o <имя создаваемой программы> <имя файла с кодом.c>
```

4. Проверена работоспособность программ.

Запуск программ

```bash
./<имя созданной программы>
```
