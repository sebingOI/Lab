# Child process

The child_process module provides the ability to spawn subprocesses in a manner that is similar, but not identical, to popen(3).

child_process 모듈은 popen(3)과 유사하지만 동일하지는 않은 방식으로 하위 프로세스를 생성하는 기능을 제공한다.

 This capability is primarily provided by the child_process.spawn() function:

 이 기능은 주로 child_process.spawn() 함수에 의해 제공됩니다.

By default, pipes for `stdin`, `stdout`, and `stderr` are established between the parent Node.js process and the spawned subprocess. 

기본적으로 stdin, stdout 및 stderr용 파이프는 상위 Node.js 프로세스와 생성된 하위 프로세스 사이에 설정됩니다.

These pipes have limited (and platform-specific) capacity.

이러한 파이프는 제한된 용량(플랫폼별)을 가지고 있습니다.

 If the subprocess writes to stdout in excess of that limit without the output being captured, the subprocess blocks waiting for the pipe buffer to accept more data.

  출력이 캡처되지 않은 상태에서 하위 프로세스가 해당 제한을 초과하여 stdout에 쓸 경우 하위 프로세스는 파이프 버퍼가 더 많은 데이터를 수락할 때까지 대기하는 블록이 됩니다.

 This is identical to the behavior of pipes in the shell. Use the `{ stdio: 'ignore' }` option if the output will not be consumed.

 이것은 쉘에 있는 파이프의 작동과 동일합니다. 출력이 안될  경우 { stdio: 'ignore' } 옵션을 사용하십시오.

 

The command lookup is performed using the `options.env.PATH` environment variable if it is in the `options` object. Otherwise, `process.env.PATH` is used.

명령 검색(호출,찾다) 는 options.env를 사용하여 수행됩니다.옵션 개체에 있는 경우 PATH 환경 변수입니다. 그렇지 않으면 process.env.PATH가 사용됩니다.

On Windows, environment variables are case-insensitive.

Windows에서 환경 변수는 대소문자를 구분하지 않습니다.

 Node.js lexicographically sorts the `env` keys and uses the first one that case-insensitively matches. 

 Node.js는 사전적으로 환경 키를 정렬하고 대소문자를 구분하지 않고 일치하는 첫 번째 키를 사용한다.

Only first (in lexicographic order) entry will be passed to the subprocess. 

 첫 번째 항목(사전순으로)만 하위 프로세스에 전달됩니다. 

This might lead to issues on Windows when passing objects to the `env` option that have multiple variants of the same key, such as `PATH` and `Path`.

이로 인해 PATH 및 PATH와 같이 동일한 키의 여러 변형이 있는 env 옵션으로 개체를 전달할 때 윈도우즈에서 문제가 발생할 수 있습니다.

The `[child_process.spawn()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_spawn_command_args_options)` method spawns the child process asynchronously, without blocking the Node.js event loop. 

child_process.spawn() 메소드는 Node.js 이벤트 루프를 차단하지 않고 차일드 프로세스를 비동기식으로 생성합니다. 

The `[child_process.spawnSync()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_spawnsync_command_args_options)` function provides equivalent functionality in a synchronous manner that blocks the event loop until the spawned process either exits or is terminated.

child_process.spaunSync() 함수는 동기식으로 동일한 기능을 제공하여 생성된 프로세스가 종료되거나 종료될 때까지 이벤트 루프를 차단합니다.

For convenience, the child_process module provides a handful of synchronous and asynchronous alternatives to child_process.spawn() and child_process.spawnSync(). 

편의를 위해 child_process 모듈은 child_process.spawn() 및 child_process.spawnSync()에 대한 몇 가지 동기식 및 비동기식 대체 기능을 제공합니다. 

Each of these alternatives are implemented on top of child_process.spawn() or child_process.spawnSync().

이러한 각 대안들은 child_process.spawn() 또는 child_process.spawnSync() 위에 구현된다.

[부가적 ](https://www.notion.so/9b724a923ddb413084ed6f583a91eea2)