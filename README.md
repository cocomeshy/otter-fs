# otter-fs

Filesystem access over raw syscalls (read, write, stat, mkdir).

Part of the Otter standard library. Otter is a compiled systems language with no garbage collector and no libc dependency (pthread for threading is the one exception); everything else goes through raw syscalls and DLL imports.

## Install

In your `otter.nest`:

```nest
deps {
  use "fs" want "1.0.0"
}
```

Then:

```sh
otter pkg pull
```

## API reference

### `fs.open(path:str, flags:int, mode:int) -> int`

Opens a file, returning a file descriptor (>= 0) or a negative error. `flags` uses the host platform's open() flag values; prefer the convenience helpers read_file/write_file for the common cases.

### `fs.read(fd:int, buf:rawptr, count:int) -> int`

Reads up to `count` bytes into `buf`. Returns bytes read, or negative on error.

### `fs.write(fd:int, buf:str, count:int) -> int`

Writes `count` bytes from `buf`. Returns bytes written, or negative on error.

### `fs.close(fd:int) -> int`

Closes a file descriptor.

### `fs.seek(fd:int, offset:int, whence:int) -> int`

Repositions the file offset. whence: 0=SET, 1=CUR, 2=END.

### `fs.delete(path:str) -> int`

Deletes a file. Returns 0 on success.

### `fs.mkdir(path:str, mode:int) -> int`

Creates a directory with the given octal mode. Returns 0 on success.

### `fs.exists(path:str) -> bool`

Returns true if the path can be opened for reading.

### `fs.read_file(path:str) -> str`

Reads an entire file into a null-terminated string. Returns "" on error.

### `fs.write_file(path:str, content:str) -> int`

Writes `content` to `path`, creating/truncating it. Returns bytes written or negative on error. Uses platform-correct O_WRONLY|O_CREAT|O_TRUNC flags.

---

## Dependencies

memory.

## License

MIT.
