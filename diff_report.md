# Code Modification

## - Makefile  

l. 3
```c
CS333_PROJECT ?= 1
```
l. 4
```c
PRINT_SYSCALLS ?= 1
```
l. 16
```c
CS333_UPROGS += _date
```

## - syscall.c

l. 109 - 111
```c
#ifdef CS333_P1
// internally, the function prototype must be ’int’ not ’uint’ for sys_date()
extern int sys_date(void);
#endif
```
l. 138 - 140
```c
#ifdef CS333_P1
[SYS_date]    sys_date,
#endif
```
l. 169 - 171
```c
#ifdef CS333_P1
  [SYS_date]    "date",
#endif
```
l. 184 - 186
```c
    #ifdef PRINT_SYSCALLS
    cprintf("%s -> %d\n",
            syscallnames[num], curproc->tf->eax);
    #endif
```

## - user.h

l. 28 - 30
```c
#ifdef CS333_P1
int date(struct rtcdate*);
#endif
```

## - usys.S

l. 33
```c
SYSCALL(date)
```

## - syscall.h

l. 25
```c
#define SYS_date    SYS_halt+1
```

## - sysproc.c

l. 101 - 112
```c
#ifdef CS333_P1
int
sys_date(void)
{
  struct rtcdate *d;

  if(argptr(0, (void*)&d, sizeof(struct rtcdate)) < 0)
    return -1;
  cmostime(d);
  return 0;
}
#endif
```

## - proc.h

l. 52
```c
  uint start_ticks;
```

## - proc.c

l. 151
```c
  p->start_ticks = ticks;
```

l. 566 - 572
```c
  #ifdef CS333_P1
  int elapsed_ms = ticks - p->start_ticks;
  int elapsed_s = elapsed_ms / 1000;
  int mod_elapsed = elapsed_ms % 1000;
  cprintf("%d\t%s\t\t%d.%d\t%s\t%d\t", p->pid, p->name, elapsed_s, mod_elapsed, state_string, p->sz);
  return;
  #endif // CS333_P1
```
