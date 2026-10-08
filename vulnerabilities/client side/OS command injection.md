## Ways of injecting OS commands

You can use a number of shell metacharacters to perform OS command injection attacks.

A number of characters function as command separators, allowing commands to be chained together. The following command separators work on both Windows and Unix-based systems:

- `&`
- `&&`
- `|`
- `||`

The following command separators work only on Unix-based systems:

- `;`
- Newline (`0x0a` or `\n`)

On Unix-based systems, you can also use backticks or the dollar character to perform inline execution of an injected command within the original command:

- `` ` ``injected command `` ` ``
- `$(`injected command `)`

The different shell metacharacters have subtly different behaviors that might change whether they work in certain situations. This could impact whether they allow in-band retrieval of command output or are useful only for blind exploitation.

Sometimes, the input that you control appears within quotation marks in the original command. In this situation, you need to terminate the quoted context (using `"` or `'`) before using suitable shell metacharacters to inject a new command.

## How to prevent OS command injection attacks

Найефективніший спосіб запобігти вразливостям інʼєкції команд операційної системи — **ніколи не викликати OS-команди з коду прикладного рівня**. Майже в усіх випадках існують інші способи реалізувати потрібну функціональність, використовуючи **безпечніші API платформи**.

Якщо ж вам **обовʼязково потрібно викликати команди ОС із використанням даних, наданих користувачем**, тоді необхідно виконувати **сувору валідацію введення**. Прикладами ефективної валідації є:

- перевірка за **білим списком** дозволених значень;
    
- перевірка, що введене значення є **числом**;
    
- перевірка, що введення містить **лише буквено-цифрові символи**, без будь-якого іншого синтаксису або пробілів.
    

**Ніколи не намагайтеся санітизувати введення шляхом екранування shell-метасимволів.** На практиці це надто схильне до помилок і може бути обійдене досвідченим зловмисником.