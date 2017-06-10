# Hakyll: синтаксическая подсветка

В этой заметке я расскажу как добавить синтаксическую подсветку в Ваши файлы
на _Markdown_ в _Hakyll_.

## Включение синтаксической подсветки

Поддержка синтаксической подсветки поставляется вместе с _Hakyll_, и, чтобы её
включить, потребуется произвести несколько простейших действий.

- загрузите репозиторий _Hakyll_:

``` bash
git clone https://github.com/jaspervdj/hakyll.git
```

- скопируйте в каталог `css` Вашего проекта файл из загруженного репозитория:

```
web/css/syntax.css
```

- добавьте соответствующий тег `link` в шаблон
    `templates/default.html` (или в какой другой на Ваше усмотрение):

``` xml
<link rel="stylesheet" type="text/css" href="/css/syntax.css" />
```

- оформите примеры исходных текстов в следующем формате:

\`\`\` язык<br />
исходный код<br />
\`\`\`

## Примеры подсветки

Ниже я привёл примеры работы синтаксической подсветки на разных языках. В
скобках для каждого из языков указано его обозначение.

- Haskell (haskell)

``` haskell
main = print "Hello!"
```

- C++ (cpp)

``` cpp
#include <cstdio>

int main() {
    puts("Hello!");
    return 0;
}
```

- Bash (bash)

``` bash
echo "Hello!"
```

- Pascal (pascal)

``` pascal
begin
  WriteLn "Hello!";
end.
```

- Ruby (ruby)

``` ruby
puts "Hello!"
```

- Perl (perl)

``` perl
print "Hello!\n";
```

## Настройка подсветки

Вы можете изменять тему оформления исходников просто редактируя 
файл стилей `css/syntax.css`. Если Вы хотите получить такое же обрамление 
как у меня добавьте в этот файл стилей следующие строчки и подкорректируйте 
стиль на свой вкус:

``` css
pre.sourceCode {
    background-color: #F6F6F6;
    box-shadow: inset 0 1pt 1pt #999999;
    padding: 3pt;
    border-radius: 3pt;
    display: inline-block;
}
```

Пока всё!
