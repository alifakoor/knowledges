Run levels in Linux refer to different modes of operation that the operating system can run in. Each run level represents a specific state of the machine, indicating what services and processes are running. Traditional Unix and Linux systems use run levels to define different states of the machine from fully operational to completely shut down.

Here is a brief overview of the common run levels:

1. **Runlevel 0**: Halt
   - This run level is used to shut down the system. When the system enters runlevel 0, it halts all processes and turns off the machine.

2. **Runlevel 1**: Single-user mode
   - Also known as maintenance or rescue mode, this run level is used for system maintenance tasks. Only the root user is logged in, and no network services are started. It's used for tasks that require exclusive access to the system, such as filesystem repairs.

3. **Runlevel 2**: Multi-user mode without networking
   - In this mode, multiple users can log in, but networking services are not started. It's typically used in environments where networking is not required or for troubleshooting purposes.

4. **Runlevel 3**: Multi-user mode with networking
   - This is a common run level for text-based or console-only server environments. Multiple users can log in, and networking services are started. It is a full multi-user mode with network capabilities but without a graphical user interface (GUI).

5. **Runlevel 4**: Undefined
   - This run level is not defined by default and can be customized by the system administrator for specific purposes.

6. **Runlevel 5**: Multi-user mode with networking and GUI
   - This is the standard run level for desktop environments. It includes all the features of runlevel 3, plus a graphical user interface. It is the default mode for most desktop installations.

7. **Runlevel 6**: Reboot
   - This run level is used to reboot the system. When the system enters runlevel 6, it shuts down all processes and reboots the machine.

Modern Linux systems, particularly those using systemd, have largely replaced traditional run levels with "targets." These targets provide more flexibility and finer control over system states. For example, common systemd targets include:

- **poweroff.target**: Equivalent to runlevel 0 (halt).
- **rescue.target**: Equivalent to runlevel 1 (single-user mode).
- **multi-user.target**: Equivalent to runlevel 3 (multi-user mode with networking).
- **graphical.target**: Equivalent to runlevel 5 (multi-user mode with networking and GUI).
- **reboot.target**: Equivalent to runlevel 6 (reboot).

Despite this shift, understanding traditional run levels remains important for working with older systems and for understanding the evolution of Linux system management.

show the current run level:
`who -r`
