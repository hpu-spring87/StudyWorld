### 判断是否在MainThread

```Java

private boolean _isCurrentlyOnMainThread() {
      return Looper.myLooper() == Looper.getMainLooper();
}

引用Looper方法：
/**
   * Return the Looper object associated with the current thread.  Returns
   * null if the calling thread is not associated with a Looper.
   */
  public static @Nullable Looper myLooper() {
      return sThreadLocal.get();
  }

/**
  * Returns the application's main looper, which lives in the main thread of the application.
  */
   public static Looper getMainLooper() {
       synchronized (Looper.class) {
           return sMainLooper;
       }
   }

```

###
