# Child_process 5

****`child_process.spawn(command[, args][, options])`****

The `child_process.spawn()` method spawns a new process using the given `command`, with command-line arguments in `args`. If omitted, `args` defaults to an empty array.

**If the `shell` option is enabled, do not pass unsanitized user input to this function. Any input containing shell metacharacters may be used to trigger arbitrary command execution.**

A third argument may be used to specify additional options, with these defaults:

Use `cwd` to specify the working directory from which the process is spawned. If not given, the default is to inherit the current working directory. If given, but the path does not exist, the child process emits an `ENOENT` error and exits immediately. `ENOENT` is also emitted when the command does not exist.

Use `env` to specify environment variables that will be visible to the new process, the default is `[process.env](https://nodejs.org/docs/latest-v15.x/api/process.html#process_process_env)`.

`undefined` values in `env` will be ignored.

Example of running `ls -lh /usr`, capturing `stdout`, `stderr`, and the exit code:

Certain platforms (macOS, Linux) will use the value of `argv[0]` for the process title while others (Windows, SunOS) will use `command`.

Node.js currently overwrites `argv[0]` with `process.execPath` on startup, so `process.argv[0]` in a Node.js child process will not match the `argv0` parameter passed to `spawn` from the parent, retrieve it with the `process.argv0` property instead.

If the `signal` option is enabled, calling `.abort()` on the corresponding `AbortController` is similar to calling `.kill()` on the child process except the error passed to the callback will be an `AbortError`:

### **`options.detached`**

Added in: v0.7.10

On Windows, setting `options.detached` to `true` makes it possible for the child process to continue running after the parent exits. The child will have its own console window. Once enabled for a child process, it cannot be disabled.

On non-Windows platforms, if `options.detached` is set to `true`, the child process will be made the leader of a new process group and session. Child processes may continue running after the parent exits regardless of whether they are detached or not. See `[setsid(2)](http://man7.org/linux/man-pages/man2/setsid.2.html)` for more information.

By default, the parent will wait for the detached child to exit. To prevent the parent from waiting for a given `subprocess` to exit, use the `subprocess.unref()` method. Doing so will cause the parent's event loop to not include the child in its reference count, allowing the parent to exit independently of the child, unless there is an established IPC channel between the child and the parent.

When using the `detached` option to start a long-running process, the process will not stay running in the background after the parent exits unless it is provided with a `stdio` configuration that is not connected to the parent. If the parent's `stdio` is inherited, the child will remain attached to the controlling terminal.

Example of a long-running process, by detaching and also ignoring its parent `stdio` file descriptors, in order to ignore the parent's termination: