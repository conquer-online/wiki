# Timestamps

Some messages sent by the client include a time or timestamp.

## Local Time

☑️ Assumed (Soul)

Messages such as [MsgTalk](messages/msgtalk.md) use a time calculated using the following formula:

```cpp
DWORD SysTimeGet(void)
{
    time_t long_time;
    time(&long_time); /* Get time as long integer. */

    struct tm* pTime;
    pTime = localtime(&long_time); /* Convert to local time. */

    DWORD dwTime = pTime->tm_hour * 100 + pTime->tm_min;
    return dwTime;
}
```

Considering that Conquer Online is a global game across multiple timezones, the local time being sent to the server cannot be used for any sort of visual element for observing players. However, it can be used for general spam detection or idempotency checks.

## System Time

☑️ Assumed (Soul)

Messages such as [MsgInteract](messages/msginteract.md) use the system time, which is the [timeGetTime](https://learn.microsoft.com/en-us/windows/win32/api/timeapi/nf-timeapi-timegettime) function in the Windows API. The precision for these time fields can be five milliseconds or more, depending on the machine; therefore, it's unreasonable to use these timestamps to check for attack timing.

> ⚠️ __WARNING__
>
> This is a 32-bit timestamp, meaning a possible range of 0 to 2^32 milliseconds (about 49.71 days). Do not use these timestamps to validate timing on the server unless the wrap around is taken into consideration.