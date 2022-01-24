# Child process 2

- `[child_process.exec()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_exec_command_options_callback)`: spawns a shell and runs a command within that shell, passing the `stdout` and `stderr` to a callback function when complete.

child_process.exe: 셸을 생성하고 해당 셸 내에서 명령을 실행하여 stdout과 stderr을 완료 시 콜백 함수에 전달합니다.

- `[child_process.execFile()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_execfile_file_args_options_callback)`: similar to `[child_process.exec()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_exec_command_options_callback)` except that it spawns the command directly without first spawning a shell by default.

child_process.execFile(): 기본적으로 셸을 먼저 생성하지 않고 직접 명령을 생성한다는 점을 제외하면 child_process.exec()와 유사합니다.

- `[child_process.fork()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_fork_modulepath_args_options)`: spawns a new Node.js process and invokes a specified module with an IPC communication channel established that allows sending messages between parent and child.

child_process.fork(): 새 Node.js 프로세스를 생성하고 부모 및 자식 간에 메시지를 보낼 수 있는 IPC 통신 채널이 설정된 지정된 모듈을 호출합니다.

- `[child_process.execSync()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_execsync_command_options)`: a synchronous version of `[child_process.exec()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_exec_command_options_callback)` that will block the Node.js event loop.

child_process.execSync(): Node.js 이벤트 루프를 차단할 동기화된 버전의 child_process.exec()입니다.

- `[child_process.execFileSync()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_execfilesync_file_args_options)`: a synchronous version of `[child_process.execFile()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_execfile_file_args_options_callback)` that will block the Node.js event loop.

child_process.execFileSync(): child_process의 동기화된 버전입니다.Node.js 이벤트 루프를 차단할 execFile()입니다.

For certain use cases, such as automating shell scripts, the [synchronous counterparts](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_synchronous_process_creation) may be more convenient. 

셸 스크립트 자동화와 같은 특정 사용 사례의 경우 동기식 스크립트가 더 편리할 수 있습니다.

In many cases, however, the synchronous methods can have significant impact on performance due to stalling the event loop while spawned processes complete.

그러나 많은 경우 동기식 메소드는 생성된 프로세스가 완료되는 동안 이벤트 루프를 지연시키기 때문에 성능에 상당한 영향을 미칠 수 있다.

### **Asynchronous process creation**

비동기 프로세스 생성

The `[child_process.spawn()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_spawn_command_args_options)`, `[child_process.fork()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_fork_modulepath_args_options)`, `[child_process.exec()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_exec_command_options_callback)`, and `[child_process.execFile()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_execfile_file_args_options_callback)` methods all follow the idiomatic asynchronous programming pattern typical of other Node.js APIs.

child_process.spawn(), child_process.fork(), child_process.exec() 및 child_process입니다.execFile() 메소드는 모두 다른 Node.js API의 전형적인 관용적 비동기 프로그래밍 패턴을 따릅니다.

Each of the methods returns a `[ChildProcess](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_class_childprocess)` instance. These objects implement the Node.js `[EventEmitter](https://nodejs.org/docs/latest-v15.x/api/events.html#events_class_eventemitter)` API, allowing the parent process to register listener functions that are called when certain events occur during the life cycle of the child process.

각 메서드는 ChildProcess 인스턴스를 반환합니다. 이러한 개체들은 Node.js EventEmitter API를 구현하여 상위 프로세스가 하위 프로세스의 수명 주기 동안 특정 이벤트가 발생할 때 호출되는 수신기 함수를 등록할 수 있게 합니다.

The `[child_process.exec()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_exec_command_options_callback)` and `[child_process.execFile()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_execfile_file_args_options_callback)` methods additionally allow for an optional `callback` function to be specified that is invoked when the child process terminates.

child_process.exec() 및 child_process입니다.execFile() 메서드는 하위 프로세스가 종료될 때 호출되는 선택적 콜백 함수를 추가로 지정할 수 있습니다.

### **Spawning `.bat` and `.cmd` files on Windows**

윈도우즈에서 .bat 및 .cmd 파일 생성

The importance of the distinction between `[child_process.exec()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_exec_command_options_callback)` and

 `[child_process.execFile()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_execfile_file_args_options_callback)` can vary based on platform. 

child_process.exec()와 child_process 간의 구별의 중요도입니다.execFile()은 플랫폼에 따라 다를 수 있습니다.

On Unix-type operating systems (Unix, Linux, macOS) `[child_process.execFile()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_execfile_file_args_options_callback)` can be more efficient because it does not spawn a shell by default. 

Unix 유형 운영 체제(유닉스, 리눅스, macOS) child_process.execFile()은 기본적으로 셸을 생성하지 않으므로 더 효율적일 수 있습니다.

On Windows, however, `.bat` and `.cmd` files are not executable on their own without a terminal, and therefore cannot be launched using `[child_process.execFile()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_execfile_file_args_options_callback)`. 

그러나 Windows에서 .bat와 .cmd 파일은 터미널 없이 자체적으로 실행할 수 없으므로 child_process를 사용하여 시작할 수 없습니다.execFile()입니다.

When running on Windows, `.bat` and `.cmd` files can be invoked using `[child_process.spawn()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_spawn_command_args_options)` with the `shell` option set, with `[child_process.exec()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_exec_command_options_callback)`, or by spawning `cmd.exe` and passing the `.bat` or `.cmd` file as an argument (which is what the `shell` option and `[child_process.exec()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_exec_command_options_callback)` do). 

윈도우즈에서 실행할 때 .bat 및 .cmd 파일은 셸 옵션이 설정된 child_process.exec()을 사용하거나 cmd.exe를 생성하고 .bat 또는 .cmd 파일을 인수로 전달(쉘 옵션 및 child_process.exec())하여 호출할 수 있습니다.

In any case, if the script filename contains spaces it needs to be quoted.

스크립트 파일 이름에 공백이 포함되어 있으면 따옴표로 묶어야 합니다.

[부가적 ](https://www.notion.so/cb9f01fa2b4e480aad3123f645187085)