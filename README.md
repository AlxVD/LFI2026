# Для пользователей Visual Studio

В первый раз - при запуске выбираете пункт "Clone a repository".
В поле "Repository location" указываете https://github.com/AlxVD/LFI2026

При последующих запусках этого делать не надо - сразу открываете решение (solution) LFI2026.

### Реализация и тестирование решений

Когда садитесь дописывать задачу:
1. В окне "Git Changes" (можно открыть через меню *View*) находите кнопку "Commit All", на ней нажимаете на стрелку вниз (выпадающий список), в списке выбираете "Stash All" (появится строчка в разделе "Stashes"). После этого выполняете команду git pull (вверху окна стрелка "вниз" - наведите мышку чтобы увидеть название). По окончании синхронизации репозитория - нажимаете правой кнопкой на строчку в разделе "Stashes" и выбираете "Pop -> Pop All as Unstaged".
2. Добавляете в нужный проект требуемые файлы (cpp/h/hpp), дописываете код.
3. Выбираете требуемый проект (когда их будет несколько) как основной (правой кнопокой мыши на имя проекта -> "Set as Startup Project".
4. Привычным образом компилируете/собираете/запускаете/отлаживаете.

# Для пользователей Linux (или работающих из командной строки)

В первый раз потребуется:
1. Клонировать данный репозиторий на свой компьютер (`git clone https://github.com/AlxVD/LFI2026.git`). В его
корне - создать каталог `build` (`mkdir build`).
2. `apt install clang-format clang-tidy` (команда для Ubuntu/Debian; в других дистрибутивах - по аналогии).

### Реализация и тестирование решений

При последующих запусках:
1. Убедитесь, что вы используете последнюю доступную версию заданий. Для этого выполните:
```
git stash
git pull
git stash pop
```
P.S. Разберитесь, что делают эти команды.

2. Реализуйте всё, что требуется в задаче.

3. После этого перейдите в директорию `build` (`cd build`) и скомпилируйте ваше решение и тесты:

```
cmake ..
make <название задачи>_test (либо make <название задачи>_public_test - в зависимости от наличия cpp-файла в каталоге)
```

В случае успеха вы увидите примерно следующее:

```
-- The C compiler identification is GNU 9.3.0
-- The CXX compiler identification is GNU 9.3.0
...
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: /home/LFI2025/public_testing/sum/build
Scanning dependencies of target sum_public_test
[ 33%] Building CXX object CMakeFiles/sum_public_test.dir/home/LFI2025/sum/sum.cpp.o
[ 66%] Building CXX object CMakeFiles/sum_public_test.dir/sum_public_test.cpp.o
[100%] Linking CXX executable sum_public_test
[100%] Built target sum_public_test
```
Решение собралось под всеми флагами, это уже что-то.

4. Далее запускаем тестирование (из папки `build`).

```
./<название задачи>_test (либо ./<название задачи>_public_test - в зависимости от того что собирали)
```

```
===============================================================================
All tests passed (18 assertions in 6 test cases)
``` 

Все тесты пройдены, ого. Вы что, задачу решили?

5. Начинаем проверку стиля кода.

```
cd .. (возвращаемся в корневую папку репозитория)
./codestyle_checker.sh <название задачи/папки с задачей>
```

```
81 warnings generated.
47141 warnings generated.
Suppressed 47141 warnings (47141 in non-user code).
Use -header-filter=.* to display errors from all non-system headers. Use -system-headers to display errors from system headers as well.
```

Если видим только какие-то предупреждения, то не обращаем на них внимания. Если же есть ошибки стиля - вы увидите строки `error`. Их
надо будет исправить.
