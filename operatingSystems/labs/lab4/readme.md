# Функции для создания процессов
**Цель работы:** изучение методов программирования по созданию пользовательских процессов в ОС Linux.

## **Выполнение:**
С помощью компилятора C создать и выполнить программы, исходный текст которых приведен в примерах 1 - 4.
1. Прочитан методический материал.
2. Изучены характеристики и синтаксис функций и системных вызовов.
3. Набран код програм в текстовые файлы и произведена их компиляция.
Пример 1:
```shell
#include <stdio.h>
#include <unistd.h>

int main()
{
  printf("Номер процесса: %d\n", (int) getpid() );
  printf("Номер родительского процесса: %d\n", (int) getppid() );
  return 0;
}
```
Пример 2:
```shell
#include <stdlib.h>
int main()
{
  int return_value;
  return_value = system(“ls –l /”);
  return return_value;
}
```
_P.S. У меня глаза выкатываются от этих различий в стайлинге программ_


Пример 3:
```shell
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
int main()
{
  pid_t child_pid;
  printf("ID процесса основной программы: %d\n", (int) getpid() );
  child_pid = fork();
  if (child_pid)
  {
    printf("Это родительский процесс, с ID %d\n", (int) getpid() );
    printf("Дочерний процесс, с ID %d\n", (int) child_pid);
  }
  else
  {
    printf("Дочерний процесс c ID %d\n", (int) getpid() );
    return 0;
  }
}
```
Пример 4:
```shell
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>

int spawn(char* program, char** arg_list)
{
  pid_t child_pid;
  child_pid = fork();
  if (child_pid)
  return child_pid;
  else
  {
    execvp(program, arg_list);
    fprintf(stderr, "an error процесс in execvp\n");
    abort();
  }
}

int main()
{
  int child_status;
  char* arg_list[] = {"ls","-l","/",NULL};
  spawn("ls", arg_list);
  wait(&child_status);
  printf("done\n");
  return 0;
}
```
4.Проверена работоспособность программ.
