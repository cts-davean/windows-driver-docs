---
title: Bug Check 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION
description: The DRIVER_VERIFIER_DETECTED_VIOLATION bug check has a value of 0x000000C4. This is the general bug check code for fatal errors found by Driver Verifier. 
keywords: ["Bug Check 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION", "DRIVER_VERIFIER_DETECTED_VIOLATION"]
ms.date: 04/10/2020
topic_type:
- apiref
api_name:
- DRIVER_VERIFIER_DETECTED_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
---

# Bug Check 0xC4: DRIVER\_VERIFIER\_DETECTED\_VIOLATION

The DRIVER\_VERIFIER\_DETECTED\_VIOLATION bug check has a value of 0x000000C4. This is the general bug check code for fatal errors found by Driver Verifier. For more information, see [Handling a Bug Check When Driver Verifier is Enabled](handling-a-bug-check-when-driver-verifier-is-enabled.md).

> [!IMPORTANT]
> This topic is for programmers. If you are a customer who has received a blue screen error code while using your computer, see [Troubleshoot blue screen errors](https://www.windows.com/stopcode).

## DRIVER\_VERIFIER\_DETECTED\_VIOLATION Parameters

Parameter 1 identifies the type of violation. The meaning of the remaining parameters varies with the value of Parameter 1. The parameter values are described in the following table.

**Note**  If you have trouble viewing all 5 columns in this table, try the following:
- Expand your browser window to full size.
- Place the cursor in the table and use the arrow keys to scroll left and right.

### 0x00 to 0x70

|Parameter 1|Parameter 2|Parameter 3|Parameter 4|Cause of Error|
|--- |--- |--- |--- |--- |
|0x00|Current IRQL|Pool type|Number of bytes|The driver requested a zero-byte pool allocation.|
|0x01|Current IRQL|Pool type|Size of allocation, in bytes|The driver attempted to allocate paged memory with IRQL > APC_LEVEL.|
|0x02|Current IRQL|Pool type|Size of allocation, in bytes|The driver attempted to allocate nonpaged memory with IRQL > DISPATCH_LEVEL.|
|0x03| | | |The caller is trying to allocate more than one page of must succeed pool, but one page is the maximum allowed by this API. |
|0x10|Bad Address| 0 | 0 |The driver attempted to free an address that was not returned from an allocate call.|
|0x11|Current IRQL|Pool type|Address of pool|The driver attempted to free paged pool with IRQL > APC_LEVEL.|
|0x12|Current IRQL|Pool type|Address of pool|The driver attempted to free nonpaged pool with IRQL > DISPATCH_LEVEL.|
|0x13 or 0x14|Reserved|Pointer to pool header|Pool header contents|The driver attempted to free memory pool which was already freed.|
|0x15|Timer entry|Pool type|Pool address being freed|The pool the caller is trying to free contains an active timer.|
|0x16|Reserved|Pool address|0|The driver attempted to free pool at a bad address, or the driver passed invalid parameters to a memory routine.|
|0X17|Resource entry | Pool type |Pool address being freed |The pool the caller is trying to free contains an active ERESOURCE. |
|0x30|Current IRQL|Requested IRQL|0|The driver passed an invalid parameter to [KeRaiseIrql](/windows-hardware/drivers/ddi/wdm/nf-wdm-keraiseirql). (The parameter was either a value lower than the current IRQL, or a value higher than HIGH_LEVEL. This may be the result of using an uninitialized parameter.)|
|0x31|Current IRQL|Requested IRQL|0: New IRQL is bad 1: New IRQL is invalid inside a DPC routine|The driver passed an invalid parameter to [KeLowerIrql](/windows-hardware/drivers/ddi/wdm/nf-wdm-kelowerirql~r1). (The parameter was either a value higher than the current IRQL, or a value higher than HIGH_LEVEL. This may be the result of using an uninitialized parameter.)|
|0x32|Current IRQL|Spin lock address|0|The driver called [KeReleaseSpinLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock) at an IRQL other than DISPATCH_LEVEL. (This may be due to a double-release of a spin lock.)|
|0x33|Current IRQL|Fast mutex address|0|The driver attempted to acquire fast mutex with IRQL > APC_LEVEL.|
|0x34|Current IRQL|Thread APC disable count|Fast mutex address|The driver attempted to release fast mutex at an IRQL other than APC_LEVEL.|
|0x35|Current IRQL|Spin lock address|Old IRQL|The kernel released a spin lock with IRQL not equal to DISPATCH_LEVEL.|
|0x36|Current IRQL|Spin lock number|Old IRQL|The kernel released a queued spin lock with IRQL not equal to DISPATCH_LEVEL.|
|0x37|Current IRQL|Thread APC disable count|Resource|The driver tried to acquire a resource, but APCs are not disabled.|
|0x38|Current IRQL|Thread APC disable count|Resource|The driver tried to release a resource, but APCs are not disabled.|
|0x39|Current IRQL|Thread APC disable count|Mutex|The driver tried to acquire a mutex "unsafe" with IRQL not equal to APC_LEVEL on entry.|
|0x3A|Current IRQL|Thread APC disable count|Mutex|The driver tried to release a mutex "unsafe" with IRQL not equal to APC_LEVEL on entry.|
|0x3B|Current IRQL|Object to wait on|Time out parameter|KeWaitXxx routine is being called at DISPATCH_LEVEL or higher.|
|0x3C|Handle passed to routine|Object type|0|The driver called [ObReferenceObjectByHandle](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle) with a bad handle.|
|0x3D| 0 | 0 |Address of the bad resource|The driver passed a bad (unaligned) resource to [ExAcquireResourceExclusive](../kernel/mmcreatemdl.md).|
|0x3E| 0 | 0 |0|The driver called [KeLeaveCriticalRegion](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion) for a thread that is not currently in a critical region.|
|0x3F|Object address|New object reference count. -1: dereference case  1: reference case|0|The driver applied [ObReferenceObject](/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject) to an object that has a reference count of zero, or the driver applied [ObDereferenceObject](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject) to an object that has a reference count of zero.|
|0x40|Current IRQL|Spin lock address|0|The driver called [KeAcquireSpinLockAtDpcLevel](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel) with IRQL < DISPATCH_LEVEL.|
|0x41|Current IRQL|Spin lock address|0|The driver called [KeReleaseSpinLockFromDpcLevel](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel) with IRQL < DISPATCH_LEVEL.|
|0x42|Current IRQL|Spin lock address|0|The driver called [KeAcquireSpinLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) with IRQL > DISPATCH_LEVEL.|
|0x51|Base address of allocation|Address of the reference beyond the allocation|Number of charged bytes|The driver attempted to free memory after having written past the end of the allocation. A bug check with this parameter occurs only when the Pool Tracking option of Driver Verifier is active.|
|0x52|Base address of allocation|Hash entry|Number of charged bytes|The driver attempted to free memory after having written past the end of the allocation. A bug check with this parameter occurs only when the Pool Tracking option of Driver Verifier is active.|
|0x53|Base address of allocation|Header|Reserved|The driver attempted to free memory after having written past the end of the allocation. A bug check with this parameter occurs only when the Pool Tracking option of Driver Verifier is active.|
|0x54|Base address of allocation|Reserved|Pool hash size|The driver attempted to free memory after having written past the end of the allocation. A bug check with this parameter occurs only when the Pool Tracking option of Driver Verifier is active.|
|0x59|Base address of allocation|Listindex|Reserved|The driver attempted to free memory after having written past the end of the allocation. A bug check with this parameter occurs only when the Pool Tracking option of Driver Verifier is active.|
|0x60|Bytes allocated from paged pool|Bytes allocated from nonpaged pool|Total number of allocations that were not freed|The driver is unloading without first freeing its pool allocations. A bug check with this parameter occurs only when the Pool Tracking option of Driver Verifier is active.|
|0x61|Bytes allocated from paged pool|Bytes allocated from nonpaged pool|Total number of allocations that were not freed|A driver thread is attempting to allocate pool memory while the driver is unloading. A bug check with this parameter occurs only when the Pool Tracking option of Driver Verifier is active.|
|0x62|Name of the driver|Reserved|Total number of allocations that were not freed, including both paged and nonpaged pool|The driver is unloading without first freeing its pool allocations. A bug check with this parameter occurs only when the Pool Tracking option of Driver Verifier is active. Type !verifier 3 drivername.sys for info on the allocations that were leaked that caused the bugcheck.|
|0x6F|MDL address|Physical page being locked|Highest physical page in the system|MmProbeAndLockPages called on pages not in PFN database. This is typically a driver calling this routine to lock its own private dualport RAM.  Not only is this not needed, it can also corrupt memory on machines with noncontiguous physical RAM.|

### 0x70 to 0x91

|Parameter 1|Parameter 2|Parameter 3|Parameter 4|Cause of Error|
|--- |--- |--- |--- |--- |
|0x70|Current IRQL|MDL address|Access mode|The driver called [MmProbeAndLockPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) with IRQL > DISPATCH_LEVEL.|
|0x71|Current IRQL|MDL address|Process address|The driver called MmProbeAndLockProcessPages with IRQL > DISPATCH_LEVEL.|
|0x72|Current IRQL|MDL address|Process address|The driver called MmProbeAndLockSelectedPages with IRQL > DISPATCH_LEVEL.|
|0x73|Current IRQL|In 32-bit Windows: Low 32 bits of the physical address In 64-bit Windows: the 64-bit physical address|Number of bytes|The driver called [MmMapIoSpace](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace) with IRQL > DISPATCH_LEVEL.|
|0x74|Current IRQL|MDL address|Access mode|The driver called [MmMapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages) in kernel mode with IRQL > DISPATCH_LEVEL.|
|0x75|Current IRQL|MDL address|Access mode|The driver called [MmMapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages) in user mode with IRQL > APC_LEVEL.|
|0x76|Current IRQL|MDL address|Access mode|The driver called [MmMapLockedPagesSpecifyCache](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache) in kernel mode with IRQL > DISPATCH_LEVEL.|
|0x77|Current IRQL|MDL address|Access mode|The driver called [MmMapLockedPagesSpecifyCache](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache) in user mode with IRQL > APC_LEVEL.|
|0x78|Current IRQL|MDL address|0|The driver called [MmUnlockPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages) with IRQL > DISPATCH_LEVEL.|
|0x79|Current IRQL|Virtual address being unmapped|MDL address|The driver called [MmUnmapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmaplockedpages) in kernel mode with IRQL > DISPATCH_LEVEL.|
|0x7A|Current IRQL|Virtual address being unmapped|MDL address|The driver called [MmUnmapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmaplockedpages) in user mode with IRQL > APC_LEVEL.|
|0x7B|Current IRQL|Virtual address being unmapped|Number of bytes|The driver called [MmUnmapIoSpace](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace) with IRQL > APC_LEVEL.|
|0x7C|MDL address|MDL flags|0|The driver called [MmUnlockPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages), and passed an MDL whose pages were never successfully locked.|
|0x7D|MDL address|MDL flags|0|The driver called [MmUnlockPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages), and passed an MDL whose pages are from nonpaged pool. (These should never be unlocked.)|
|0x7E|Current IRQL|DISPATCH_LEVEL|0|The driver called [MmAllocatePagesForMdl](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdl), [MmAllocatePagesForMdlEx](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdlex), or [MmFreePagesFromMdl](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreepagesfrommdl) with IRQL > DISPATCH_LEVEL.|
|0x7F|Current IRQL|MDL address|MDL flags|The driver called [BuildMdlForNonPagedPool](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool) and passed an MDL whose pages are from paged pool.|
|0x80|Current IRQL|Event address|0|The driver called [KeSetEvent](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent) with IRQL > DISPATCH_LEVEL.|
|0x81|MDL address|MDL flags|0|The driver called [MmMapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages). (You should use [MmMapLockedPagesSpecifyCache](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache) instead, with the BugCheckOnFailure parameter set to FALSE.)|
|0x82|MDL address|MDL flags|0|The driver called [MmMapLockedPagesSpecifyCache](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache) with the BugCheckOnFailure parameter equal to TRUE. (This parameter should be set to FALSE.)|
|0x83|Start of physical address range to map|Number of bytes to map|First page frame number that isn't locked down|The driver called [MmMapIoSpace](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace) without having locked down the MDL pages. The physical pages represented by the physical address range being mapped must have been locked down prior to making this call.|
|0x85|MDL address|Number of pages to map|First page frame number that isn't locked down|The driver called [MmMapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages) without having locked down the MDL pages.|
|0x89|MDL address|Pointer to the non-memory page in the MDL|The non-memory page number in the MDL|An MDL is not marked as "I/O", but it contains non-memory page addresses.|
|0x91|Reserved|Reserved|Reserved|The driver switched stacks using a method that is not supported by the operating system. The only supported way to extend a kernel mode stack is by using [KeExpandKernelStackAndCallout](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keexpandkernelstackandcallout).|

### 0xA0 to 0x140

|Parameter 1|Parameter 2|Parameter 3|Parameter 4|Cause of Error|
|--- |--- |--- |--- |--- |
|0xA0|Pointer to the IRP making the read or write request|Device object of the lower device|Number of the sector in which the error was detected|A cyclic redundancy check (CRC) error was detected on a hard disk. A bug check with this parameter occurs only when the Disk Integrity Checking option of Driver Verifier is active.|
|0xA1|Copy of the IRP making the read or write request. (The actual IRP has been completed.)|Device object of the lower device|Number of the sector in which the error was detected|A CRC error was detected on a sector (asynchronously). A bug check with this parameter occurs only when the Disk Integrity Checking option of Driver Verifier is active.|
|0xA2|IRP making the read or write request, or a copy of this IRP|Device object of the lower device|Number of the sector in which the error was detected|The CRCDISK checksum copies don't match. This could be a paging error. A bug check with this parameter occurs only when the Disk Integrity Checking option of Driver Verifier is active.|
|0xB0 |MDL address|MDL flags|Incorrect MDL flags|The driver called [MmProbeAndLockPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages) for an MDL with incorrect flags. For example, the driver passed an MDL created by [MmBuildMdlForNonPagedPool](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool) to MmProbeAndLockPages.|
|0xB1 |MDL address|MDL flags|Incorrect MDL flags|The driver called MmProbeAndLockProcessPages for an MDL with incorrect flags. For example, the driver passed an MDL created by [MmBuildMdlForNonPagedPool](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmbuildmdlfornonpagedpool) to MmProbeAndLockProcessPages.|
|0xB2 |MDL address|MDL flags|Incorrect MDL flags|The driver called [MmMapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages) for an MDL with incorrect flags. For example, the driver passed an MDL that is already mapped to a system address or that was not locked to MmMapLockedPages.|
|0xB3 |MDL address|MDL flags|Missing MDL flags (at least one was expected)|The driver called [MmMapLockedPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpages) for an MDL with incorrect flags. For example, the driver passed an MDL that is not locked to MmMapLockedPages.|
|0xB4 |MDL address|MDL flags|Unexpected partial MDL flag|The driver called [MmUnlockPages](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages) for a partial MDL. A partial MDL is one that was created by [IoBuildPartialMdl](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl).|
|0xB5|MDL address|MDL flags|Unexpected partial MDL flag|MmUnmapLockedPages called on a partial MDL (created with [IoBuildPartialMdl](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildpartialmdl)).|
|0xB6|MDL address|MDL flags|Missing MDL flag|MmUnmapLockedPages called on an MDL that is not mapped to a system address.|
|0xB7|Number of physical pages corrupted.|First corrupted physical page.|Last corrupted physical page.|The system BIOS has corrupted low physical memory during a sleep transition.|
|0xB8 |MDL address|MDL flags|Reserved|The pages that are described by the MDL are still mapped. The driver must unmap the pages before calling IoFreeMdl.|
|0xB9 |Address being unmapped.|MDL address.|Reserved|MmUnmapLockedPages called with a bad user space address.|
|0xC0 |Address of the IRP|0|Reserved|The driver called [IoCallDriver](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) with interrupts disabled.|
|0xC1 |Address of the driver dispatch routine|Reserved|Reserved|A driver dispatch routine was returned with interrupts disabled.|
|0xC2 | 0 | 0 |0|The driver called a Fast I/O dispatch routine after interrupts were disabled.|
|0xC3 |Address of the driver Fast I/O dispatch routine|Reserved|Reserved|A driver Fast I/O dispatch routine was returned with interrupts disabled.|
|0xC5 |Address of the driver dispatch routine|The current thread's APC disable count|The thread's APC disable count prior to calling the driver dispatch routine|A driver dispatch routine has changed the thread's APC disable count. The APC disable count is decremented each time a driver calls [KeEnterCriticalRegion](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion), [FsRtlEnterFileSystem](../ifs/fsrtlenterfilesystem.md), or acquires a mutex. The APC disable count is incremented each time a driver calls [KeLeaveCriticalRegion](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion), [KeReleaseMutex](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex), or [FsRtlExitFileSystem](../ifs/fsrtlexitfilesystem.md). Because these calls should always be in pairs, the APC disable count should be zero whenever a thread is exited. A negative value indicates that a driver has disabled APC calls without re-enabling them. A positive value indicates that the reverse is true.|
|0xC6 |Address of the driver Fast I/O dispatch routine|Current thread's APC disable count|The thread's APC disable count prior to calling the Fast I/O driver dispatch routine|A driver Fast I/O dispatch routine has changed the thread's APC disable count. The APC disable count is decremented each time a driver calls [KeEnterCriticalRegion](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion), [FsRtlEnterFileSystem](../ifs/fsrtlenterfilesystem.md), or acquires a mutex. The APC disable count is incremented each time a driver calls [KeLeaveCriticalRegion](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion), [KeReleaseMutex](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex), or [FsRtlExitFileSystem](../ifs/fsrtlexitfilesystem.md). Because these calls should always be in pairs, the APC disable count should be zero whenever a thread is exited. A negative value indicates that a driver has disabled APC calls without re-enabling them. A positive value indicates that the reverse is true.|
|0xCA |Address of the lookaside list|Reserved|Reserved|The driver has attempted to re-initialize a lookaside list.|
|0xCB |Address of the lookaside list|Reserved|Reserved|The driver has attempted to delete an uninitialized lookaside list.|
|0xCC |Address of the lookaside list|Starting address of the pool allocation|Size of the pool allocation|The driver has attempted to free a pool allocation that contains an active lookaside list.|
|0xCD |Address of the lookaside list|Block size specified by the caller|Minimum supported block size|The driver has attempted to create a lookaside list with an allocation block size that is too small.|
|0xD0 |Address of the ERESOURCE structure|Reserved|Reserved|The driver has attempted to re-initialize an ERESOURCE structure.|
|0xD1 |Address of the ERESOURCE structure|Reserved|Reserved|The driver has attempted to delete an uninitialized ERESOURCE structure.|
|0xD2 |Address of the ERESOURCE structure|Starting address of the pool allocation|Size of the pool allocation|The driver has attempted to free a pool allocation that contains an active ERESOURCE structure.|
|0xD5 |Address of the IO_REMOVE_LOCK structure created by the checked build version of the driver|Current [IoReleaseRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) tag|Reserved|The current [IoReleaseRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) tag does not match the previous [IoAcquireRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) tag. If the driver calling IoReleaseRemoveLock is not in a checked build, Parameter 2 is the address of the shadow IO_REMOVE_LOCK structure created by Driver Verifier on behalf of the driver. In this case, the address of the IO_REMOVE_LOCK structure used by the driver is not used at all, because Driver Verifier is replacing the lock address for all the remove lock APIs. A bug check with this parameter occurs only when the I/O Verification option of Driver Verifier is active.|
|0xD6 |Address of the IO_REMOVE_LOCK structure created by the checked build version of the driver|Tag that does not match previous [IoAcquireRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) tag|Previous [IoAcquireRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) tag|The current [IoReleaseRemoveLockAndWait](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait) tag does not match the previous [IoAcquireRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock) tag. If the driver calling [IoReleaseRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock) is not a checked build, Parameter 2 is the address of the shadow IO_REMOVE_LOCK structure created by Driver Verifier on behalf of the driver. In this case, the address of the IO_REMOVE_LOCK structure used by the driver is not used at all, because Driver Verifier is replacing the lock address for all the remove lock APIs. A bug check with this parameter occurs only when the I/O Verification option of Driver Verifier is active.|
|0xD7|Address of the checked build Remove Lock structure that is used internally by Driver Verifier|Address of the Remove Lock structure that is specified by the driver|Reserved|A Remove Lock cannot be re-initialized, even after it calls [IoReleaseRemoveLockAndWait](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait), because other threads might still be using that lock (by calling [IoAcquireRemoveLock](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)). The driver should allocate the Remove Lock inside its device extension, and initialize it a single time. The lock will be deleted together with the device extension.|
|0xDA |Starting address of the driver|WMI callback address inside the driver|Reserved|An attempt was made to unload a driver that has not deregistered its WMI callback function.|
|0xDB |Address of the device object|Reserved|Reserved|An attempt was made to delete a device object that was not deregistered from WMI.|
|0xDC |Reserved|Reserved|Reserved|An invalid RegHandle value was specified as a parameter of the function [EtwUnregister](/windows-hardware/drivers/ddi/wdm/nf-wdm-etwunregister).|
|0xDD |Address of the call to EtwRegister|Starting address of the unloading driver|For Windows 8 and later versions, this parameter is the ETW RegHandle value.|An attempt was made to unload a driver without calling [EtwUnregister](/windows-hardware/drivers/ddi/wdm/nf-wdm-etwunregister).|
|0xDF |Synchronization object address| 0 | 0 |The synchronization object is in session address space. Synchronization objects are not allowed in session address space because they can be manipulated from another session or from system threads that have no session virtual address space.|
|0xE0 |User-mode address that is used as a parameter|Size ,in bytes, of the address range that is used as a parameter|Reserved|A call was made to an operating system kernel function that specified a user-mode address as a parameter.|
|0xE1 |Address of the synchronization object|Reserved|Reserved|A synchronization object was found to have an address that was either invalid or pageable.|
|0xE2 |Address of the IRP|User-mode address present in the IRP|Reserved|An IRP with Irp->RequestorMode set to KernelMode was found to have a user-mode address as one of its members.|
|0xE3 |Address of the call to the API|User-mode address used as a parameter in the API|Reserved|A driver has made a call to a kernel-mode ZwXxx routine with a user-mode address as a parameter.|
|0xE4 |Address of the call to the API|Address of the malformed UNICODE_STRING structure|Reserved|A driver has made a call to a kernel-mode ZwXxx routine with a malformed UNICODE_STRING structure as a parameter.|
|0xE5 |Current IRQL|Reserved|Reserved|A call was made to a Kernel API at the incorrect IRQL.|
|0xE6 |Address inside the driver making the Zw API call|Current IRQL|Special kernel APCs.|Kernel Zw API was not called at IRQL = PASSIVE_LEVEL and with special kernel APCs enabled.|
|0xEA |Current IRQL|The thread's APC disable count|Address of the pushlock|A driver has attempted to acquire a pushlock while APCs are enabled.|
|0xEB |Current IRQL|The thread's APC disable count|Address of the pushlock|A driver has attempted to release a pushlock while APCs are enabled.|
|0xF0 |Address of the destination buffer|Address of the source buffer|Number of bytes to copy|A driver called the memcpy function with overlapping source and destination buffers.|
|0xF5 |Address of the NULL handle|Object type|Reserved|A driver passed a NULL handle to [ObReferenceObjectByHandle](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle).|
|0xF6 |Handle value being referenced|Address of the current process|Address inside the driver that performs the incorrect reference|A driver references a user-mode handle as kernel mode.|
|0xF7 |Handle value specified by the caller|Object type specified by the caller|AccessMode specified by the caller|A driver is attempting a user-mode reference for a kernel handle in the context of the system process.|
|0xFA |Completion routine address.|IRQL value before it calls the completion routine|Current IRQL value, after it calls the completion routine|The IRP completion routine returned at an IRQL that was different from the IRQL the routine was called at.|
|0xFB |Completion routine address|Current thread's APC disable count|The thread's APC disable count before it calls the IRP completion routine|The thread's APC disable count was changed by the driver's IRP completion routine. The APC disable count is decremented each time a driver calls [KeEnterCriticalRegion](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion), [FsRtlEnterFileSystem](../ifs/fsrtlenterfilesystem.md), or acquires a mutex. The APC disable count is incremented each time a driver calls [KeLeaveCriticalRegion](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion), [KeReleaseMutex](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasemutex), or [FsRtlExitFileSystem](../ifs/fsrtlexitfilesystem.md). Because these calls should always be in pairs, the APC disable count should be zero whenever a thread is exited. A negative value indicates that a driver has disabled APC calls without re-enabling them. A positive value indicates that the reverse is true.|
|0xFC |Address inside the driver making the incorrect API call.|Provided ApcContext value.|Reserved|Calling ZwNotifyChangeKey (from kernel mode) with unsupported ApcContext value.|

### 0x105 to 0x140

| Parameter 1 | Parameter 2        | Parameter 3 | Parameter 4 | Cause of Error                                                      |
|-------------|--------------------|-------------|-------------|---------------------------------------------------------------------|
| 0x105       | Address of the IRP | 0           | 0           | The driver uses ExFreePool instead of IoFreeIrp to release the IRP. |
| 0x10A       | 0                  | 0           | 0           | The driver attempts to charge pool quota to the Idle process.       |
|0x10B        | 0                  | 0           |0            |The driver attempts to charge pool quota from a DPC routine. This is incorrect because the current process context is undefined.|
|0x110 | 0| 0| 0| Address of the Interrupt Service Routine|Address of the extended context that was saved before it executed the ISR|Address of the extended context was saved after it executed the ISR|The interrupt service routine (ISR) for the driver has corrupted the extended thread context.|
|0x111 | Address of the Interrupt Service Routine|IRQL before executing ISR|IRQL after executing ISR|The interrupt Service Routine returned a changed IRQL.|
|0x115 | The address of the thread responsible for the shutdown, that might be deadlocked.| 0 | 0 |Driver Verifier detected that the system has taken longer than 20 minutes and shutdown is not complete.|
|0x11A | Current IRQL| 0| 0| The driver calls KeEnterCriticalRegion at IRQL > APC_LEVEL.|
|0x11B | Current IRQL| 0| 0|The driver calls KeLeaveCriticalRegion at IRQL > APC_LEVEL.|
|0x120 |Address of the IRQL value|Address of the Object to wait on|Address of Timeout value|The thread waits at IRQL > DISPATCH_LEVEL. Callers of KeWaitForSingleObject or KeWaitForMultipleObjects must run at IRQL <= DISPATCH_LEVEL.|
|0x121 |Address of the IRQL value|Address of the Object to wait on|Address of Timeout value|The thread waits at IRQL equals DISPATCH_LEVEL and the Timeout is NULL. Callers of KeWaitForSingleObject or KeWaitForMultipleObjects can run at IRQL <= DISPATCH_LEVEL. If a NULL pointer is supplied for Timeout, the calling thread remains in a wait state until the Object is signaled.|
|0x122 |Address of the IRQL value|Address of the Object to wait on|Address of the Timeout value|The thread waits at DISPATCH_LEVEL and Timeout value is not equal to zero (0). If the Timeout != 0, the callers of KeWaitForSingleObject or KeWaitForMultipleObjects must run at IRQL <= APC_LEVEL.|
|0x123 |Address of the Object to wait on| 0 | 0 |The caller of KeWaitForSingleObject or KeWaitForMultipleObjects specified the wait as UserMode, but the Object is on the kernel stack.|
|0x130 |Address of work item| 0 | 0 |The work item is in session address space. Work items are not allowed in session address space because they can be manipulated from another session or from system threads that have no session virtual address space.|
|0x131 |Address of work item| 0 | 0 |The work item is in pageable memory. Work items have to be in nonpageable memory because the kernel uses them at DISPATCH_LEVEL.|
|0x135 |Address of IRP|Number of milliseconds allowed between the [IoCancelIrp](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp) call and the completion for this IRP|0|The canceled IRP did not completed in the expected time The driver took longer than expected to complete the canceled IRP.|
|0x13A |Address of the pool block being freed|Incorrect value|Address of the incorrect value|The driver has called [ExFreePool](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) and Driver Verifier detects an error in one of the internal values that is used to track pool usage.|
|0x13B |Address of the pool block being freed|Address of the incorrect value|Address of a pointer to the incorrect memory page|The driver has called [ExFreePool](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) and Driver Verifier detects an error in one of the internal values that is used to track pool usage.|
|0x13C |Address of the pool block being freed|Incorrect value|Address of the incorrect value|The driver has called [ExFreePool](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) and Driver Verifier detects an error in one of the internal values that is used to track pool usage.|
|0x13D |Address of the pool block being freed|Address of the incorrect value|Correct value that was expected|The driver has called [ExFreePool](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) and Driver Verifier detects an error in one of the internal values that is used to track pool usage.|
|0x13E |Pool block address specified by the caller|Pool block address tracked by Driver Verifier|Pointer to the pool block address that is tracked by Driver Verifier|The pool block address specified by the caller of [ExFreePool](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) is different from the address tracked by Driver Verifier.|
|0x13F|Address of the pool block being freed|Number of bytes being freed|Pointer to the number of bytes tracked by Driver Verifier|The number of bytes of memory being freed in the call to [ExFreePool](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) is different from the number of bytes tracked by Driver Verifier.|
|0x140 |Current IRQL|MDL address|Associated virtual address with this MDL|A non-locked MDL was constructed from either pageable or tradable memory.|
|0x141 |Highest physical address the driver requested for allocation|Number of bytes to allocate|0|The driver is explicitly requesting physical memory under 4GB.|

### 0x1000 to 0x100B - Deadlocks

| Parameter 1 | Parameter 2 | Parameter 3 | Parameter 4 | Cause of Error |
|-------------|-------------|-------------|-------------|----------------|
|0x1000 | Address of the resource| Reserved | Reserved | Self-deadlock: The current thread has tried to recursively and exclusively acquire a resource which it only owns shared. A bug check with this parameter occurs only when the Deadlock Detection option of Driver Verifier is active.|
|0x1001 | Address of the resource that was the final cause of the deadlock|Reserved|Reserved|Deadlock: A lock hierarchy violation has been found. A bug check with this parameter occurs only when the Deadlock Detection option of Driver Verifier is active. (Use the [!deadlock](-deadlock.md) extension for further information.)|
|0x1002 | Address of the resource|Reserved|Reserved|Uninitialized resource: A resource has been acquired without having been initialized first. A bug check with this parameter occurs only when the Deadlock Detection option of Driver Verifier is active.|
|0x1003 | Address of the resource that is being released deadlocked|Address of the resource that should have been released first|Reserved|Unexpected release: A resource has been released in an incorrect order. A bug check with this parameter occurs only when the Deadlock Detection option of Driver Verifier is active.|
|0x1004 | Address of the resource|Address of the thread that acquired the resource|Address of the current thread|Unexpected thread: The wrong thread releases a resource. A bug check with this parameter occurs only when the Deadlock Detection option of Driver Verifier is active.|
|0x1005 | Address of the resource|Reserved|Reserved|Multiple initialization: A resource is initialized more than one time. A bug check with this parameter occurs only when the Deadlock Detection option of Driver Verifier is active.|
|0x1007 | Address of the resource|Reserved|Reserved|Unacquired resource: A resource is released before it has been acquired. A bug check with this parameter occurs only when the Deadlock Detection option of Driver Verifier is active.|
|0x1008 | Lock address|Reserved|Reserved|The driver tried to acquire a lock by using an API that is mismatched for this lock type.|
|0x1009 | Lock address|Reserved|Reserved|The driver tried to release a lock by using an API that is mismatched for this lock type.|
|0x100A | Owner thread address|Reserved|The terminated thread owns the lock.|
|0x100B | Lock address|Owner thread address|Reserved|The deleted lock is still owned by a thread.|
|0x1010 | Device object to which the Write IRP was issued.|The address of the IRP.|System-Space Virtual Address for the buffer that the MDL describes.|Invariant MDL buffer contents for Write Irp were modified.|
|0x1011 | Device object to which the Write IRP was issued.|The address of the IRP.|System-Space Virtual Address for the buffer that the MDL describes.|Invariant MDL buffer contents for Read Irp were modified during dispatch or buffer backed by dummy pages.|
|0x1012 | A pointer to the string describing the violation.|Data that is involved in this corruption (0 if not used).|Data that is involved in this corruption (0 if not used).|Verifier extension state storage detected corruption.|
|0x1013 | A pointer to the driver object.|A pointer to the captured original I/O callbacks.|Reserved (unused).|Verifier detected internal corruption in the captured original I/O callbacks.|

### 0x2000 to 0x2005 - Code Integrity Issues

| Parameter 1 | Parameter 2 | Parameter 3 | Parameter 4 | Cause of Error |
|-------------|-------------|-------------|-------------|----------------|
|0x2000 |The address in the driver's code where the error was detected. |Pool Type. | Pool Tag (if provided).|Code Integrity Issue: The caller specified an executable pool type. (Expected: NonPagedPoolNx) |
|0x2001 |The address in the driver's code where the error was detected. |Page Protection (WIN32_PROTECTION_MASK). | 0 |Code Integrity Issue: The caller specified an executable page protection. (Expected: cleared PAGE_EXECUTE* bits) |
|0x2002 |The address in the driver's code where the error was detected. |Page Priority (MM_PAGE_PRIORITY logically OR'd with MdlMapping*). |0|Code Integrity Issue: The caller specified an executable MDL mapping. (Expected: MdlMappingNoExecute) |
|0x2003 |The image file name (Unicode string). | The address of the section header.|The section name (UTF-8 encoded string). |Code Integrity Issue: The image contains an executable and writable section. |
|0x2004 |The image file name (Unicode string). |The address of the section header. |The section name (UTF-8 encoded string). |Code Integrity Issue: The image contains a section that is not page aligned. |
|0x2005 |The image file name (Unicode string). | IAT Directory.|The section name (UTF-8 encoded string). |Code Integrity Issue: The image contains an IAT located in an executable section. |

### 0xA001 to 0xA00D - VM Switch Issues

|Parameter 1|Parameter 2|Parameter 3|Parameter 4|Cause of Error|
|--- |--- |--- |--- |--- |
|0xA001 |A pointer to the NetBufferList object|A pointer to the virtual switch object (if NON-NULL)|Reserved (unused)|VM Switch: The SourceHandle for the caller-supplied NetBufferList must be set. See the [AllocateNetBufferListForwardingContext](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context) routine.|
|0xA002 |A pointer to the NetBufferList object|A pointer to the virtual switch object (if NON-NULL).|Reserved (unused)|VM Switch: The caller supplied NetBufferList's forwarding detail is not zero. See the [AllocateNetBufferListForwardingContext](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_allocate_net_buffer_list_forwarding_context) routine.|
|0xA003 |A pointer to the NetBufferList object|A pointer to the virtual switch object (if NON-NULL).|Reserved (unused)|VM Switch: The caller supplied a NetBufferList with packet header or routing context that is NULL. See [Packet Management Guidelines for the Extensible Switch Data Path](../network/packet-management-guidelines-for-the-extensible-switch-data-path.md).|
|0xA004 |ID of invalid port|NIC Index|A pointer to the virtual switch object (if NON-NULL).|VM Switch: The caller specified an invalid Port and NIC index combination. See [Hyper-V Extensible Switch Port and Network Adapter States](../network/hyper-v-extensible-switch-port-and-network-adapter-states.md).|
|0xA005 |A pointer to the NetBufferList object|A pointer to the Destination list.|A pointer to the virtual switch object (if NON-NULL).|VM Switch: The caller supplied an invalid destination. See [AddNetBufferListDestination](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination) and [UpdateNetBufferListDestinations](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations).|
|0xA006 |A pointer to the NetBufferList object|A pointer to the virtual switch object (if NON-NULL).|Reserved (unused)|VM Switch: The caller supplied an invalid source NIC or Port object. See [Hyper-V Extensible Switch Port and Network Adapter States](../network/hyper-v-extensible-switch-port-and-network-adapter-states.md).|
|0xA007 |A pointer to the NetBufferList object|A pointer to the virtual switch object (if NON-NULL).|Reserved (unused)|VM Switch: The caller supplied an invalid destination list. See [AddNetBufferListDestination](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination) and [UpdateNetBufferListDestinations](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations).|
|0xA008 |Parent NIC object|NIC index|A pointer to the virtual switch object (if NON-NULL).|VM Switch: Attempting to reference a NIC when not allowed. See [Hyper-V Extensible Switch Port and Network Adapter States](../network/hyper-v-extensible-switch-port-and-network-adapter-states.md).|
|0xA009 |Port being referenced|A pointer to the virtual switch object (if NON-NULL)|Reserved (unused)|VM Switch: Attempt to reference a port when not allowed. See [Hyper-V Extensible Switch Port and Network Adapter States](../network/hyper-v-extensible-switch-port-and-network-adapter-states.md).|
|0xA00A |A pointer to the NetBufferList object|ContextTypeInfo object|Reserved (unused)|VM Switch: Failure context is already set. See [SetNetBufferListSwitchContext](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_set_net_buffer_list_switch_context).|
|0xA00B |A pointer to the NetBufferList object|NDIS_SWITCH_REPORT_FILTERED_NBL_FLAGS_*|A pointer to the virtual switch object (if NON-NULL)|VM Switch: Invalid direction provided for dropped NetBufferList. See [ReportFilteredNetBufferLists](/windows-hardware/drivers/ddi/ndis/nc-ndis-ndis_switch_report_filtered_net_buffer_lists).|
|0xA00C |A pointer to the NetBufferList object|Send Flags value|A pointer to the virtual switch object (if NON-NULL)|VM Switch: NetBufferList chain has multiple source ports when NDIS_SEND_FLAGS_SWITCH_SINGLE_SOURCE flag is set. See [Hyper-V Extensible Switch Send and Receive Flags](../network/hyper-v-extensible-switch-send-and-receive-flags.md).|
|0xA00D |A pointer to the NetBufferList object|A pointer to the virtual switch context|A pointer to the virtual switch object (if NON-NULL)|VM Switch: One or more NetBufferLists in chain have invalid destination when NDIS_RECEIVE_FLAGS_SWITCH_DESTINATION_GROUP flag is set. See [Hyper-V Extensible Switch Send and Receive Flags](../network/hyper-v-extensible-switch-send-and-receive-flags.md).|
|0xA00E|A pointer to the NetBufferLists object. |A pointer to the virtual switch context. |A pointer to the virtual switch object (if NON-NULL). |VM Switch: Attempting to complete NetBufferList through WNV when VMS_NBL_ROUTING_CONTEXT_FLAG_NO_WNV_PROCESSING flag is set.|

### 0x00020002 to 0x00020022 - DDI Compliance Rule Violations

|Parameter 1|Parameter 2|Parameter 3|Parameter 4|Cause of Error|
|--- |--- |--- |--- |--- |
|0x00020002 |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlApcLte](../devtest/wdm-irqlapclte.md). The rule specifies that the driver must call [ObGetObjectSecurity](/windows-hardware/drivers/ddi/wdm/nf-wdm-obgetobjectsecurity) and [ObReleaseObjectSecurity](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreleaseobjectsecurity) only when IRQL <= APC_LEVEL.|
|0x00020003 |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlDispatch](../devtest/wdm-irqldispatch.md). The IrqlDispatch rule specifies that the driver must call certain routines only when IRQL = DISPATCH_LEVEL|
|0x00020004 |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlExAllocatePool](../devtest/wdm-irqlexallocatepool.md). The IrqlExAllocatePool rule specifies that the driver calls [ExAllocatePoolWithTag](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) and [ExAllocatePoolWithTagPriority](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority) only when at IRQL<=DISPATCH_LEVEL.|
|0x00020005 |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlExApcLte1](../devtest/wdm-irqlexapclte1.md). The IrqlExApcLte1 rule specifies that the driver calls ExAcquireFastMutex and ExTryToAcquireFastMutex only at IRQL <= APC_LEVEL.|
|0x00020006 |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlExApcLte2](../devtest/wdm-irqlexapclte2.md). The IrqlExApcLte2 rule specifies that the driver calls certain routines only when IRQL <= APC_LEVEL.|
|0x00020007 |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlExApcLte3](../devtest/wdm-irqlexapclte3.md). The IrqlExApcLte3 rule specifies that the driver must call certain executive support routines only when IRQL <= APC_LEVEL.|
|0x00020008 |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlExPassive](../devtest/wdm-irqlexpassive.md). The IrqlExPassive rule specifies that the driver must call certain executive support routines only when IRQL = PASSIVE_LEVEL.|
|0x00020009 |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlIoApcLte](../devtest/wdm-irqlioapclte.md). The IrqlIoApcLte rule specifies that the driver must call certain I/O manager routines only when IRQL <= APC_LEVEL.|
|0x0002000A |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlIoPassive1](../devtest/wdm-irqliopassive1.md). The IrqlIoPassive1 rule specifies that the driver must call certain I/O manager routines only when IRQL = PASSIVE_LEVEL.|
|0x0002000B |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlIoPassive2](../devtest/wdm-irqliopassive2.md). The IrqlIoPassive2 rule specifies that the driver must call certain I/O manager routines only when IRQL = PASSIVE_LEVEL.|
|0x0002000C |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlIoPassive3](../devtest/wdm-irqliopassive3.md). The IrqlIoPassive3 rule specifies that the driver must call certain I/O manager routines only when IRQL = PASSIVE_LEVEL.|
|0x0002000D |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlIoPassive4](../devtest/wdm-irqliopassive4.md). The IrqlIoPassive4 rule specifies that the driver must call certain I/O manager routines only when IRQL = PASSIVE_LEVEL.|
|0x0002000E |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlIoPassive5](../devtest/wdm-irqliopassive5.md). The IrqlIoPassive5 rule specifies that the driver must call certain I/O manager routines only when IRQL = PASSIVE_LEVEL.|
|0x0002000F |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlKeApcLte1](../devtest/wdm-irqlkeapclte1.md). The IrqlKeApcLte1 rule specifies that the driver must call certain kernel routines only when IRQL <= APC_LEVEL.|
|0x00020010 |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlKeApcLte2](../devtest/wdm-irqlkeapclte2.md). The IrqlKeApcLte2 rule specifies that the driver must call certain kernel routines only when IRQL <= APC_LEVEL.|
|0x00020011 |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlKeDispatchLte](../devtest/wdm-irqlkedispatchlte.md). The IrqlKeDispatchLte rule specifies that the driver must call certain kernel routines only when IRQL <= DISPATCH_LEVEL.|
|0x00020015 |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlKeReleaseSpinLock](../devtest/wdm-irqlkereleasespinlock.md). The IrqlKeReleaseSpinLock rule specifies that the driver must call KeReleaseSpinLock only when IRQL = DISPATCH_LEVEL.|
|0x00020016 |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlKeSetEvent](../devtest/wdm-irqlkesetevent.md). The IrqlKeSetEvent rule specifies that the [KeSetEvent](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent) routine is only called at IRQL <= DISPATCH_LEVEL when Wait is set to FALSE, and at IRQL <= APC_LEVEL when Wait is set to TRUE.|
|0x00020019 |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlMmApcLte](../devtest/wdm-irqlmmapclte.md). The IrqlMmApcLte rule specifies that the driver must call certain memory manager routines only when IRQL <= APC_LEVEL.|
|0x0002001A |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlMmDispatch](../devtest/wdm-irqlmmdispatch.md). The IrqlMmDispatch rule specifies that the driver must call [MmFreeContiguousMemory](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmfreecontiguousmemory) only when IRQL = DISPATCH_LEVEL.|
|0x0002001B |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlObPassive](../devtest/wdm-irqlobpassive.md). The IrqlObPassive rule specifies that the driver must call [ObReferenceObjectByHandle](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle) only when IRQL = PASSIVE_LEVEL.|
|0x0002001C |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlPsPassive](../devtest/wdm-irqlpspassive.md). The IrqlPsPassive rule specifies that the driver must call certain process and thread manager routines only when IRQL = PASSIVE_LEVEL.|
|0x0002001D |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [IrqlReturn](../devtest/wdm-irqlreturn.md).|
|0x0002001E |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlRtlPassive](../devtest/wdm-irqlrtlpassive.md). The IrqlRtlPassive rule specifies that the driver must call [RtlDeleteRegistryValue](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtldeleteregistryvalue) only when IRQL = PASSIVE_LEVEL.|
|0x0002001F |Pointer to the string that describes the violated rule condition.|Optional pointer to the rule state variable(s).|Reserved|The driver violated the DDI compliance rule [IrqlZwPassive](../devtest/wdm-irqlzwpassive.md). The IrqlZwPassive rule specifies that the driver must call [ZwClose](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose) only when IRQL = PASSIVE_LEVEL.|
|0x00020022 |Pointer to the string that describes the violated rule condition.|Reserved (unused)|Reserved (unused)|The driver violated the DDI compliance rule [IrqlIoDispatch](../devtest/wdm-irqliodispatch.md).|
|0x00020023 |A pointer to the string describing the violated rule condition. |Reserved (unused). |Reserved (unused). |The driver violated the DDI compliance rule  [IrqlIoRtlZwPassive](../devtest/wdm-irqliortlzwpassive.md). The IrqlIoRtlZwPassive rule specifies that the driver calls the DDIs listed in the rule only when it is executing at IRQL = PASSIVE_LEVEL.|
|0x00020024 |A pointer to the string describing the violated rule condition. |Reserved (unused). |Reserved (unused). |The driver violated the DDI compliance rule [IrqlNtifsApcPassive](../devtest/wdm-irqlntifsapcpassive.md). The IrqlNtifsApcPassive rule specifies that the driver calls the DDIs listed in the rule only when it is executing either at IRQL = PASSIVE_LEVEL or at IRQL <= APC_LEVEL.|
|0x00020025 |A pointer to the string describing the violated rule condition. |Reserved (unused). |Reserved (unused). |The driver violated the Microsoft internal DDI compliance rule IrqlKeMore. |

### 0x00040003 to 0x00043006 - DDI Compliance Rule Violations

|Parameter 1|Parameter 2|Parameter 3|Parameter 4|Cause of Error|
|--- |--- |--- |--- |--- |
|0x00040003 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [CriticalRegions](../devtest/wdm-criticalregions.md).|
|0x00040006 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [QueuedSpinLock](../devtest/wdm-queuedspinlock.md).|
|0x00040007 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [QueuedSpinLockRelease](../devtest/wdm-queuedspinlockrelease.md).|
|0x00040009 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [SpinLock](../devtest/wdm-spinlock.md).|
|0x0004000A | Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo)|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [SpinlockRelease](../devtest/wdm-spinlockrelease.md).|
|0x0004000E |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [GuardedRegions](../devtest/wdm-guardedregions.md).|
|0x0004100B |Pointer to the string that describes the violated rule condition.|Reserved (unused)|Reserved (unused)|The driver violated the DDI compliance rule [RequestedPowerIrp](../devtest/wdm-requestedpowerirp.md).|
|0x0004100F |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [IoSetCompletionExCompleteIrp](../devtest/wdm-iosetcompletionexcompleteirp.md).|
|0x00043006 |Pointer to the string that describes the violated rule condition.|Reserved (unused)|Reserved (unused)|The driver violated the DDI compliance rule [PnpRemove](../devtest/wdm-pnpremove.md).|

### 0x00081001 to 0x00082005 - AVStream Driver Compliance Rule Violations

|Parameter 1|Parameter 2|Parameter 3|Parameter 4|Cause of Error|
|--- |--- |--- |--- |--- |
|0x00081001 |Pointer to the string that describes the violated rule condition. |Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [KsDeviceMutex](../devtest/ks-ksdevicemutex.md).|
|0x00081002 |Pointer to the string that describes the violated rule condition. |Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [KsStreamPointerClone](../devtest/ks-ksstreampointerclone.md).|
|0x00081003 |Pointer to the string that describes the violated rule condition. |Reserved (unused)|Reserved (unused)|The driver violated the DDI compliance rule [KsStreamPointerLock](../devtest/ks-ksstreampointerlock.md).|
|0x00081004 |Pointer to the string that describes the violated rule condition. |Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [KsStreamPointerUnlock](../devtest/ks-ksstreampointerunlock.md).|
|0x00081005 |Pointer to the string that describes the violated rule condition. |Reserved (unused)|Reserved (unused)|The driver violated the DDI compliance rule [KsCallbackReturn](../devtest/ks-kscallbackreturn.md).|
|0x00081006 |Pointer to the string that describes the violated rule condition. |Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [KsIrqlDeviceCallbacks](../devtest/ks-ksirqldevicecallbacks.md).|
|0x00081007 |Pointer to the string that describes the violated rule condition. |Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [KsIrqlFilterCallbacks](../devtest/ks-ksirqlfiltercallbacks.md).|
|0x00081008 |Pointer to the string that describes the violated rule condition. |Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [KsIrqlPinCallbacks](../devtest/ks-ksirqlpincallbacks.md).|
|0x00081009 |Pointer to the string that describes the violated rule condition. |Reserved (unused)|Reserved (unused)|The driver violated the DDI compliance rule  [KsIrqlDDIs](../devtest/ks-ksirqlddis.md).|
|0x0008100A |Pointer to the string that describes the violated rule condition. |Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [KsFilterMutex](../devtest/ks-ksfiltermutex.md).|
|0x0008100B |Pointer to the string that describes the violated rule condition. |Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [KsProcessingMutex](../devtest/ks-ksprocessingmutex.md).|
|0x0008100C |Pointer to the string that describes the violated rule condition. |Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [KsInvalidStreamPointer](../devtest/ks-ksinvalidstreampointer.md).|
|0x00082001 |Pointer to the string that describes the violated rule condition. |Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [KsTimedPinSetDeviceState](../devtest/ks-kstimedpinsetdevicestate.md).|
|0x00082002 |Pointer to the string that describes the violated rule condition. |Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [KsTimedDeviceCallbacks](../devtest/ks-kstimeddevicecallbacks.md).|
|0x00082003 |Pointer to the string that describes the violated rule condition. |Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [KsTimedFilterCallbacks](../devtest/ks-kstimedfiltercallbacks.md).|
|0x00082004 |Pointer to the string that describes the violated rule condition. |Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [KsTimedPinCallbacks](../devtest/ks-kstimedpincallbacks.md).|
|0x00082005 |Pointer to the string that describes the violated rule condition. |Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [KsTimedProcessingMutex](../devtest/ks-kstimedprocessingmutex.md).|


### 0x00091001 to 0x0009400C - NDIS DDI Compliance Rule Violations

|Parameter 1|Parameter 2|Parameter 3|Parameter 4|Cause of Error|
|--- |--- |--- |--- |--- |
|0x00091001 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [NdisOidComplete](../devtest/ndis-ndisoidcomplete.md).|
|0x00091002 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [NdisOidDoubleComplete](../devtest/ndis-ndisoiddoublecomplete.md).|
|0x0009100E |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the DDI compliance rule [NdisOidDoubleRequest](../devtest/ndis-ndisoiddoublerequest.md).|
|0x00092003 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the NDIS/WIFI verification rule [NdisTimedOidComplete](../devtest/ndis-ndistimedoidcomplete.md).|
|0x0009200D |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the NDIS/WIFI verification rule [NdisTimedDataSend](../devtest/ndis-ndistimeddatasend.md).|
|0x0009200F |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the NDIS/WIFI verification rule [NdisTimedDataHang](../devtest/ndis-ndistimeddatahang.md).|
|0x00092010 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo). |The driver violated the NDIS/WIFI verification rule [NdisFilterTimedPauseComplete](../devtest/ndisfiltertimedpausecomplete-.md).|
|0x00092011 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo). |The driver violated the NDIS/WIFI verification rule [NdisFilterTimedDataSend](../devtest/ndisfiltertimeddatasend.md).|
|0x00092012 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo). |The driver violated the NDIS/WIFI verification rule [NdisFilterTimedDataReceive](../devtest/ndisfiltertimeddatareceive.md).|
|0x00093004 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the NDIS/WIFI verification rule [WlanAssociation](../devtest/ndis-wlanassociation.md).|
|0x00093005 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the NDIS/WIFI verification rule [WlanConnectionRoaming](../devtest/ndis-wlanconnectionroaming.md).|
|0x00093006 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the NDIS/WIFI verification rule [WlanDisassociation](../devtest/ndis-wlandisassociation.md).|
|0x00093101|Pointer to the string describing the violated rule condition. |Reserved (unused)|Reserved (unused)|The driver violated the NDIS/WIFI verification rule [WlanAssert](../devtest/ndis-wlanassert.md).|
|0x00094007 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the NDIS/WIFI verification rule [WlanTimedAssociation](../devtest/ndis-wlantimedassociation.md).|
|0x00094008 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the NDIS/WIFI verification rule [WlanTimedConnectionRoaming](../devtest/ndis-wlantimedconnectionroaming.md).|
|0x00094009 |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the NDIS/WIFI verification rule [WlanTimedConnectRequest](../devtest/ndis-wlantimedconnectrequest.md).|
|0x0009400B |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the NDIS/WIFI verification rule [WlanTimedLinkQuality](../devtest/ndis-wlantimedlinkquality.md).|
|0x0009400C |Pointer to the string that describes the violated rule condition.|Address of internal rule state (second argument to !ruleinfo).|Address of supplemental states (third argument to !ruleinfo).|The driver violated the NDIS/WIFI verification rule [WlanTimedScan](../devtest/ndis-wlantimedscan.md).|

Cause
-----

See the description of each code in the Parameters section for a description of the cause. Further information can be obtained by using the [**!analyze -v**](-analyze.md) extension.

Resolution
----------

This bug check can only occur when Driver Verifier has been instructed to monitor one or more drivers. If you did not intend to use Driver Verifier, you should deactivate it. You might also consider removing the driver that caused this problem.

If you are the driver writer, use the information obtained through this bug check to fix the bugs in your code.

For full details on Driver Verifier, see [Driver Verifier](../devtest/driver-verifier.md).

Remarks
-------

The \_POOL\_TYPE codes are enumerated in Ntddk.h. In particular, **0** (zero) indicates nonpaged pool and **1** (one) indicates paged pool.

*(Windows 8 and later versions of Windows)* If [DDI compliance checking](../devtest/ddi-compliance-checking.md) causes a bug check, run [Static Driver Verifier](../devtest/static-driver-verifier.md) on the driver source code and specify the DDI compliance rule (identified by the parameter 1 value) that caused the bug check. Static Driver Verifier can help you locate the cause of the problem in your source code.

## <span id="see_also"></span>See also

[Handling a Bug Check When Driver Verifier is Enabled](handling-a-bug-check-when-driver-verifier-is-enabled.md)