## Windows Defender Emulator Bypasses

- Some Defender Emulator bypasses
- All code examples are in c++, I don't care for any other language.

### Credits / Resources

- https://github.com/hfiref0x/WDExtract
- https://www.youtube.com/watch?v=wDNQ-8aWLO0


### GetUserName

The emulated version of GetUserName returns a static string of "JohnDoe".

You can bypass it with:
```c++
CHAR user[MAX_USERNAME_SIZE];
GetUserNameA((LPSTR)user, MAX_USERNAME_SIZE);

if(user == "JohnDoe"){
    ExitProcess(-1);// Emulated, unless actual username is JohnDoe
}
```
Since the username could actually be JohnDoe, it might be worth adding an extra check.


### GetComputerName

The emulated version of GetUserName returns a static string of "HAL9TH".

```c++
CHAR user[MAX_USERNAME_SIZE];
GetComputerName((LPSTR)user, MAX_USERNAME_SIZE);

if(user == "JohnDoe"){
    ExitProcess(-1);
}
```

### GetConsoleProcessList

The emulated version of GetConsoleProcessList simply returns 0, 
https://docs.microsoft.com/en-us/windows/console/getconsoleprocesslist states that "If the return value is zero, the function has failed, because every console has at least one process associated with it.".

```c++
if(GetConsoleProcessList(5, 5) == 0){
    // could be emulated.
}
```