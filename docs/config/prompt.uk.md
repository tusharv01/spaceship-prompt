# Налаштування командного рядка

Ця сторінка описує опції командного рядка Spaceship.

## Термінологія

Командний рядок складається з **секцій**. Всі секції поєднуються в [**послідовність командного рядка**](#Послідовність-командного-рядка).

Під час процесу відображення командний рядок проходить по послідовності та викликає кожну секцію. Якщо ви хочете додати власну секцію – додайте її в послідовність. Ви можете додавати чи вилучати секціїї з послідовності командного рядка в будь-який час.

Типова секція складається з **префіксу**, **символу**, **змісту** та **суфіксу**. Символ та зміст виділяються **кольором**. Ось приклад для секції `package`:

```
is 📦 3.16.5
```

У наведеному вище, `is` є префіксом, `📦` символом, `3.16.5` змістом, а `` (пробіл) суфіксом.

Кожна складова секції може бути налаштована за допомогою відповідних **опцій**. Опції це звичайні змінні середовища з такою сигнатурою: `SPACESHIP_<SECTION>_<OPTION>`:

```zsh
# SPACESHIP_<SECTION>_<OPTION>
  SPACESHIP_PACKAGE_PREFIX="via·"
  SPACESHIP_PACKAGE_SUFFIX=" "
  SPACESHIP_PACKAGE_COLOR="green"
```

У прикладі вище `PACKAGE` це **секція**, а `PREFIX`, `SUFFIX` та `COLOR` це **опції** для префіксу, суфіксу та кольору відповідно.

!!! info
    Допускається використання [базових кольорів](https://wiki.archlinux.org/index.php/zsh#Colors) або [кольорових кодів](https://upload.wikimedia.org/wikipedia/commons/1/15/Xterm_256color_chart.svg).

## Послідовність командного рядка

**Послідовність командного рядка** визначає порядок, в якому секції виконуються і відображаються. Порядок секцій у командному рядку контролюється опцією `SPACESHIP_PROMPT_ORDER`.

За замовчуванням, порядок секцій наступний:

```zsh
SPACESHIP_PROMPT_ORDER=(
  time           # Time stamps section
  user           # Username section
  dir            # Current directory section
  host           # Hostname section
  git            # Git section (git_branch + git_status)
  hg             # Mercurial section (hg_branch  + hg_status)
  package        # Package version
  node           # Node.js section
  bun            # Bun section
  deno           # Deno section
  ruby           # Ruby section
  python         # Python section
  elm            # Elm section
  elixir         # Elixir section
  xcode          # Xcode section
  swift          # Swift section
  golang         # Go section
  perl           # Perl section
  php            # PHP section
  rust           # Rust section
  haskell        # Haskell Stack section
  scala          # Scala section
  kotlin         # Kotlin section
  java           # Java section
  lua            # Lua section
  dart           # Dart section
  julia          # Julia section
  crystal        # Crystal section
  docker         # Docker section
  docker_compose # Docker section
  aws            # Amazon Web Services section
  gcloud         # Google Cloud Platform section
  azure          # Azure section
  venv           # virtualenv section
  conda          # conda virtualenv section
  dotnet         # .NET section
  ocaml          # OCaml section
  vlang          # V section
  zig            # Zig section
  purescript     # PureScript section
  erlang         # Erlang section
  kubectl        # Kubectl context section
  ansible        # Ansible section
  terraform      # Terraform workspace section
  pulumi         # Pulumi stack section
  ibmcloud       # IBM Cloud section
  nix_shell      # Nix shell
  gnu_screen     # GNU Screen section
  exec_time      # Execution time
  async          # Async jobs indicator
  line_sep       # Line break
  battery        # Battery level and status
  jobs           # Background jobs indicator
  exit_code      # Exit code section
  sudo           # Sudo indicator
  char           # Prompt character
)
```

Ви можете додавати та видаляти секції за допомогою команд `spaceship add` та `spaceship remove` таким чином:

```zsh
# Видаляє секцію git з командного рядка
spaceship remove git

# Додає секцію git до командного рядка
spaceship add git
```

### Послідовність правого командного рядка

Також ви можете додавати секції праворуч від командного рядка, вказуючи їх у опції `SPACESHIP_RPROMPT_ORDER`. За замовчуванням, `SPACESHIP_RPROMPT_ORDER` – порожній масив.

## Налаштування секцій

Ви можете налаштовувати кожну секцію командного рядка за допомогою опцій секції. Подивіться документацію секцій для отримання додаткової інформації.

Крім використання вбудованих секцій, ви можете додавати сторонні секції або створити власні.

[Подивитися вбудовані секції](/uk/sections ""){.md-button} [Подивитися всі секції](/uk/registry ""){.md-button}

## Налаштування командного рядка

Ця група налаштувань визначає поведінку командного рядка і стандартні параметри відображення секцій.

| Змінна                               | За замовчуванням | Пояснення                                         |
|:------------------------------------ |:----------------:| ------------------------------------------------- |
| `SPACESHIP_PROMPT_ASYNC`             |      `true`      | Чи відображати командний рядок асинхронно         |
| `SPACESHIP_PROMPT_ADD_NEWLINE`       |      `true`      | Додає символ нового рядка перед кожним запитом    |
| `SPACESHIP_PROMPT_SEPARATE_LINE`     |      `true`      | Розтягнути командний рядок на два рядки           |
| `SPACESHIP_PROMPT_FIRST_PREFIX_SHOW` |     `false`      | Показати префікс першої секції в командному рядку |
| `SPACESHIP_PROMPT_PREFIXES_SHOW`     |      `true`      | Чи показувати префікси секцій                     |
| `SPACESHIP_PROMPT_SUFFIXES_SHOW`     |      `true`      | Чи показувати суфікси секцій                      |
| `SPACESHIP_PROMPT_DEFAULT_PREFIX`    |      `via·`      | Префікс за замовчуванням для секцій               |
| `SPACESHIP_PROMPT_DEFAULT_SUFFIX`    |        ``        | Суфікс за замовчуванням для секцій                |

Трохи більше про ці налаштування:

### Асинхронне відображення

Опція `SPACESHIP_PROMPT_ASYNC` визначає, чи має командний рядок відображатися асинхронно, чи ні. За замовчуванням, він відображається асинхронно.

Синхронні секції показуються миттєво. Асинхронні секції обробляються у фоні та показуються коли інформація готова до відображення.

[Cекція `async`](/uk/sections/async) заміняє асинхронні секції, поки вони завантажуються.

### Відступи командного рядка

Spaceship додає порожній рядок між запитами. Ви можете вимкнути цю поведінку, змінивши значення опції `SPACESHIP_PROMPT_ADD_NEWLINE` на `false`.

Командний рядок також виділяється новим рядком якщо `SPACESHIP_PROMPT_SEPARATE_LINE` має значення `true`.

### Відображення префіксу першої секції

Spaceship приховує префікс першої секції командного рядка. Ви можете увімкнути цю поведінку, встановивши `SPACESHIP_PROMPT_FIRST_PREFIX_SHOW` у `true`.

### Відображення префіксів та суфіксів

Ви можете вимкнути відображення префіксів та суфіксів, встановивши `SPACESHIP_PROMPT_PREFIXES_SHOW` та `SPACESHIP_PROMPT_SUFFIXES_SHOW` у `false`.

Додатково ви можете змінити префікс та суфікс за замовчуванням за допомогою опцій `SPACESHIP_PROMPT_DEFAULT_PREFIX` та `SPACESHIP_PROMPT_DEFAULT_SUFFIX`. Ці значення будуть використані для відображення префіксів або суфіксів, якщо не встановлено відповідні опції секції.
