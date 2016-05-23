#wait()与notify()/notifyAll()

只能在同步控制方法或同步块中调用wait()、notify()和notifyAll()。如果在非同步的方法里调用这些方法，在运行时会抛出IllegalMonitorStateException异常。

