# Process启动流程-基于安卓13

com.android.server.am.ProcessList有ProcessMap<AppZygote>集合和ArrayMap<AppZygote, ArrayList<ProcessRecord>>进程的记录

ProcessList的startProcess方法可以通过AppZygote启动，也可以通过android.os.Process的start静态方法启动

com.android.server.am.ProcessRecord有ActivityManagerService、ApplicationInfo、UidRecord、PackageList、ActiveInstrumentation、各种Record、成员变量

android.os.AppZygote包含android.os.ChildZygoteProcess和android.content.pm.ApplicationInfo

ChildZygoteProcess继承android.os.ZygoteProcess

ZygoteProcess有LocalSocketAddress信息，通过socket建立连接，通过startViaZygote方法启动

ActivityManagerService里面有ActivityManagerInternal对象

public final ActivityManagerInternal mInternal

public final class LocalService extends ActivityManagerInternal implements ActivityManagerLocal {

com.android.server.am.ActivityManagerService的LocalService内部类#startIsolatedProcess或者startSdkSandboxProcessLocked或者startProcessLocked或者attachApplicationLocked或者finishBooting或者addAppLocked或者cleanUpApplicationRecordLocked或者bindBackupAgent或者startProcess

ProcessList的startProcessLocked、handleProcessStart方法调用startProcess

com.android.server.am.ProcessList#startProcess--

    通过appZygote.getProcess().start(--Process.start

android.os.Process.start--

android.os.ZygoteProcess.start--

ZygoteProcess有LocalSocketAddress信息

android.os.ZygoteProcess的子类有ChildZygoteProcess，ChildZygoteProcess是AppZygote的成员变量