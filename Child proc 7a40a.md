# Child process 4

****`child_process.execFile(file[, args][, options][, callback])`****

The `child_process.execFile()` function is similar to `[child_process.exec()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_exec_command_options_callback)` except that it does not spawn a shell by default. Rather, the specified executable `file` is spawned directly as a new process making it slightly more efficient than `[child_process.exec()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_exec_command_options_callback)`.

child_process입니다.execFile() 함수는 기본적으로 셸을 생성하지 않는다는 점을 제외하고는 child_process.exec()와 유사합니다. 오히려, 지정된 실행 파일이 새로운 프로세스로 직접 생성되어 하위_process.exec()보다 약간 더 효율적입니다.

The same options as `[child_process.exec()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_exec_command_options_callback)` are supported. 

child_process.exec()와 동일한 옵션이 지원됩니다.

Since a shell is not spawned, behaviors such as I/O redirection and file globbing are not supported.

셸이 생성되지 않기 때문에 I/O 리디렉션 및 파일 전역과 같은 동작은 지원되지 않습니다. 

The `stdout` and `stderr` arguments passed to the callback will contain the stdout and stderr output of the child process. 

콜백에 전달된 stdout 및 stderr 인수는 하위 프로세스의 stdout 및 stderr 출력을 포함합니다.

By default, Node.js will decode the output as UTF-8 and pass strings to the callback. 

기본적으로 Node.js는 출력을 UTF-8로 디코딩하고 문자열을 콜백으로 전달합니다.

The `encoding` option can be used to specify the character encoding used to decode the stdout and stderr output.

인코딩 옵션은 stdout 및 stderr 출력을 디코딩하는 데 사용되는 문자 인코딩을 지정하는 데 사용할 수 있습니다.

 If `encoding` is `'buffer'`, or an unrecognized character encoding, `Buffer` objects will be passed to the callback instead.

인코딩이 '버퍼'이거나 인식할 수 없는 문자 인코딩인 경우 버퍼 객체가 콜백에 대신 전달됩니다.

If this method is invoked as its `[util.promisify()](https://nodejs.org/docs/latest-v15.x/api/util.html#util_util_promisify_original)`ed version, it returns a `Promise` for an `Object` with `stdout` and `stderr` properties.

이 메서드가 util.promisify()ed 버전으로 호출 된 경우 stdout 및 stderr 속성을 가진 객체에 대한 promise를 반환합니다.

 The returned `ChildProcess` instance is attached to the `Promise` as a `child` property. In case of an error (including any error resulting in an exit code other than 0), a rejected promise is returned, with the same `error` object given in the callback, but with two additional properties `stdout` and `stderr`.

반환된 ChildProcess(자식 프로세스) 인스턴스가 하위 항목으로 Promise 속성에 첨부됩니다. 에러가 발생하면(0이 아닌 종료 코드를 초래하는 에러를 포함) 거부된 Promise는 콜백에 동일한 에러 객체와 함께 반환되지만 stdout과 stderr의 두 가지 추가 속성으로 반환 됩니다.

If the `shell` option is enabled, do not pass unsanitized user input to this function. Any input containing shell metacharacters may be used to trigger arbitrary command execution.

셸 옵션이 활성화된 경우 이 함수에 표준화되지 않은 사용자 입력을 전달하지 마십시오. 셸 특수문자를 포함하는 모든 입력은 임의 명령 실행을 트리거하는 데 사용될 수 있습니다.

If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

신호 옵션이 활성화된 경우 콜백에 전달된 오류를 제외하고 해당 Abort()를 호출하는 것은 하위 프로세스에서 .kill()을 호출하는 것과 유사합니다.

****`child_process.fork(modulePath[, args][, options])`****

The `child_process.fork()` method is a special case of `[child_process.spawn()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_spawn_command_args_options)` used specifically to spawn new Node.js processes.

child_process.fork() 메소드는 새로운 Node.js 프로세스를 생성하기 위해 특별히 사용되는 child_process.spawn()의 특별한 경우이다.

 Like `[child_process.spawn()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_spawn_command_args_options)`, a `[ChildProcess](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_class_childprocess)` object is returned.

Child_process.spawn()과 마찬가지로 ChildProcess 개체가 반환됩니다.

 The returned `[ChildProcess](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_class_childprocess)` will have an additional communication channel built-in that allows messages to be passed back and forth between the parent and child.

반환된 ChildProcess에는 부모와 자식 간에 메시지를 주고받을 수 있는 추가 통신 채널이 내장되어 있습니다.

 See `[subprocess.send()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_subprocess_send_message_sendhandle_options_callback)` for details.

자세한 내용은 하위 프로세스.send()를 참조하십시오.

Keep in mind that spawned Node.js child processes are independent of the parent with exception of the IPC communication channel that is established between the two.

생성된 Node.js 하위 프로세스는 둘 사이에 설정된 IPC 통신 채널을 제외하고 상위 프로세스와 독립적입니다.

 Each process has its own memory, with their own V8 instances.

각 프로세스에는 자체 V8 인스턴스가 있는 자체 메모리가 있습니다.

 Because of the additional resource allocations required, spawning a large number of child Node.js processes is not recommended.

추가 리소스 할당이 필요하므로 많은 수의 하위 Node.js 프로세스를 생성하지 않는 것이 좋습니다.

By default, `child_process.fork()` will spawn new Node.js instances using the `[process.execPath](https://nodejs.org/docs/latest-v15.x/api/process.html#process_process_execpath)` of the parent process.

기본적으로 child_process.fork()는 프로세스를 사용하여 새 Node.js 인스턴스를 생성합니다.상위 프로세스의 execPath입니다.

 The `execPath` property in the `options` object allows for an alternative execution path to be used.

옵션 개체의 execPath 속성을 사용하면 대체 실행 경로를 사용할 수 있습니다.

Node.js processes launched with a custom `execPath` will communicate with the parent process using the file descriptor (fd) identified using the environment variable `NODE_CHANNEL_FD` on the child process.

사용자 지정 execPath로 시작된 Node.js 프로세스는 하위 프로세스에서 환경 변수 NODE_CHANNEL_FD를 사용하여 식별된 파일 설명자(fD)를 사용하여 상위 프로세스와 통신합니다.

Unlike the `[fork(2)](http://man7.org/linux/man-pages/man2/fork.2.html)` POSIX system call, `child_process.fork()` does not clone the current process.

fork(2) POSIX 시스템 호출과 달리 child_process.fork()는 현재 프로세스를 복제하지 않습니다.

The `shell` option available in `[child_process.spawn()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_spawn_command_args_options)` is not supported by `child_process.fork()` and will be ignored if set.

child_process.spawn()에서 사용할 수 있는 셸 옵션은 child_process.fork()에서 지원되지 않으므로 설정된 경우 무시됩니다.

If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

신호 옵션이 활성화된 경우 콜백에 전달된 오류를 제외하고 해당 Abort()를 호출하는 것은 하위 프로세스에서 .kill()을 호출하는 것과 유사합니다.

[부가적](https://www.notion.so/217b517178884c978aa9498b29650fa2)