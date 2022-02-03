# Child process 3

**`child_process.exec(command[, options][, callback])`**

- `command` [<string>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) The command to run, with space-separated arguments.
- 명령 <string> 공백으로 구분된 인수가 있는 실행할 명령입니다.
- `options` [<Object>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
    - `cwd` [<string>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) Current working directory of the child process. **Default:** `process.cwd()`.
    - cwd <string> 자식 프로세스의 현재 작업 디렉터리입니다. 기본값: process.cwd().
    - `env` [<Object>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) Environment key-value pairs. **Default:** `process.env`.
    - env <Object> 환경 키-값 쌍. 기본값: process.env.
    - `encoding` [<string>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) **Default:** `'utf8'`
    - 인코딩 <string> 기본값: 'utf8’
    - `shell` [<string>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) Shell to execute the command with. See [Shell requirements](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_shell_requirements) and [Default Windows shell](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_default_windows_shell). **Default:** `'/bin/sh'` on Unix, `process.env.ComSpec` on Windows.
    - shell <string> 명령을 실행할 셸입니다. 셸 요구 사항 및 기본 윈도우즈 셸을 참조하십시오. 기본값: Unix의 '/bin/sh', process.env.Windows의 ComSpec.
    - `signal` [<AbortSignal>](https://nodejs.org/docs/latest-v15.x/api/globals.html#globals_class_abortsignal) allows aborting the child process using an AbortSignal.
    - 신호 <AbortSignal>을 사용하면 AbortSignal을 사용하여 자식 프로세스를 중단할 수 있습니다.
    - `timeout` [<number>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type) **Default:** `0`
    - `maxBuffer` [<number>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type) Largest amount of data in bytes allowed on stdout or stderr. If exceeded, the child process is terminated and any output is truncated. See caveat at `[maxBuffer` and Unicode](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_maxbuffer_and_unicode). **Default:** `1024 * 1024`.
    - `killSignal` [<string>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) | [<integer>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type) **Default:** `'SIGTERM'`
    - `uid` [<number>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type) Sets the user identity of the process (see `[setuid(2)](http://man7.org/linux/man-pages/man2/setuid.2.html)`).
    - `gid` [<number>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Number_type) Sets the group identity of the process (see `[setgid(2)](http://man7.org/linux/man-pages/man2/setgid.2.html)`).
    - `windowsHide` [<boolean>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#Boolean_type) Hide the subprocess console window that would normally be created on Windows systems. **Default:** `false`.
- `callback` [<Function>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function) called with the output when process terminates.
    - `error` [<Error>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)
    - `stdout` [<string>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) | [<Buffer>](https://nodejs.org/docs/latest-v15.x/api/buffer.html#buffer_class_buffer)
    - `stderr` [<string>](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures#String_type) | [<Buffer>](https://nodejs.org/docs/latest-v15.x/api/buffer.html#buffer_class_buffer)
- Returns: [<ChildProcess>](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_class_childprocess)

Spawns a shell then executes the `command` within that shell, buffering any generated output. 

그런 다음 셸을 생성하며 생성된 출력을 버퍼링하여 해당 셸 내에서 명령을 실행합니다.

The `command` string passed to the exec function is processed directly by the shell and special characters (vary based on [shell](https://en.wikipedia.org/wiki/List_of_command-line_interpreters)) need to be dealt with accordingly:

Exec 함수에 전달된 명령 문자열은 셸에 의해 직접 처리되며 특수 문자(쉘 기반 변수)는 이에 따라 처리되어야 합니다.

```jsx
const { exec } = require('child_process');

exec('"/path/to/test file/test.sh" arg1 arg2');
// Double quotes are used so that the space in the path is not interpreted as
// a delimiter of multiple arguments.

exec('echo "The \\$HOME variable is $HOME"');
// The $HOME variable is escaped in the first instance, but not in the second.
```

**Never pass unsanitized user input to this function. Any input containing shell metacharacters may be used to trigger arbitrary command execution.**

표준화되지 않은 사용자 입력을 이 함수에 전달하지 마십시오. 셸 메타캐릭터를 포함하는 모든 입력은 임의 명령 실행을 트리거하는 데 사용될 수 있습니다

If a `callback` function is provided, it is called with the arguments `(error, stdout, stderr)`. On success, `error` will be `null`. 

'callback' 함수가 제공되는 경우 '(error, stdout, stderr)' 인수와 함께 호출된다. 성공하면 에러는 널이 된다.

On error, `error` will be an instance of `[Error](https://nodejs.org/docs/latest-v15.x/api/errors.html#errors_class_error)`. 

오류가 발생하면 오류가 오류의 인스턴스가 됩니다.

The `error.code` property will be the exit code of the process. 

'error.code' 속성은 프로세스의 종료 코드가 됩니다.

By convention, any exit code other than `0` indicates an error. 

일반적으로 0이 아닌 종료 코드는 오류를 나타냅니다.

`error.signal` will be the signal that terminated the process.

'error.signal'은 프로세스를 종료한 신호입니다.

The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. 

콜백에 전달된 stdout 및 stderr 인수는 하위 프로세스의 stdout 및 stderr 출력을 포함합니다.

By default, Node.js will decode the output as UTF-8 and pass strings to the callback.

기본적으로 Node.js는 출력을 UTF-8로 디코딩하고 문자열을 콜백으로 전달합니다.

 The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output. 

'인코딩' 옵션은 stdout 및 stderr 출력을 디코딩하는 데 사용되는 문자 인코딩을 지정하는 데 사용할 수 있습니다.

If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

'인코딩'이 '버퍼'인 경우 또는 인식할 수 없는 문자 인코딩인 경우 '버퍼' 개체가 콜백에 대신 전달됩니다.

If `timeout` is greater than `0`, the parent will send the signal identified by the `killSignal` property (the default is `'SIGTERM'`) if the child runs longer than `timeout` milliseconds.

시간 초과가 0보다 클 경우 하위 항목이 시간 초과 밀리초보다 오래 실행되면 부모에서 killSignal 속성(기본값 'SIGTERM')으로 식별되는 신호를 보냅니다.

Unlike the `[exec(3)](http://man7.org/linux/man-pages/man3/exec.3.html)` POSIX system call, `child_process.exec()` does not replace the existing process and uses a shell to execute the command.

exec(3) POSIX 시스템 호출과 달리 child_process.exec()은 기존 프로세스를 대체하지 않고 셸을 사용하여 명령을 실행합니다.

If this method is invoked as its `[util.promisify()](https://nodejs.org/docs/latest-v15.x/api/util.html#util_util_promisify_original)`ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties.

이 메서드가 유틸리티로 호출되는 경우.promy()ed 버전은 stdout 및 stderr 속성을 가진 개체에 대한 Promise를 반환합니다.

 The returned `ChildProcess` instance is attached to the `Promise` as a `child` property.

반환된 ChildProcess 인스턴스는 Promise에 Child Process 속성으로 첨부됩니다

 In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

에러가 발생하면(0이 아닌 종료 코드를 초래하는 에러를 포함) 거부된 약속은 콜백에 동일한 에러 객체와 함께 반환되지만 stdout과 stderr의 두 가지 추가 속성으로 반환된다.

[부가적 ](https://www.notion.so/7ddad7b87e554a4caed7b2cb8f16f413)