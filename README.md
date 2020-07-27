# Android rxjava实现倒计时功能

### 1. 导入rxjava框架
```java
//rxjava rxandroid
api 'io.reactivex.rxjava2:rxjava:2.2.19'
api 'io.reactivex.rxjava2:rxandroid:2.1.1'
api 'com.trello.rxlifecycle2:rxlifecycle-android-lifecycle:2.2.2'
```

### 2. 代码实现
```java
        //intervalRange四个参数分别为：从0开始、到60结束、延时0开始，单位时间（NANOSECONDS,MICROSECONDS,MILLISECONDS,SECONDS,MINUTES,HOURS,DAYS）。
        Disposable countdownDisposable = Flowable.intervalRange(0, 60, 0, 1, TimeUnit.SECONDS)
                .observeOn(AndroidSchedulers.mainThread())
                .doOnNext(new Consumer<Long>() {
                    @Override
                    public void accept(Long aLong) throws Exception {
                        countdownTimeTextView.setText((60 - aLong) + "秒" + "后结束");
                    }
                })
                .doOnComplete(new Action() {
                    @Override
                    public void run() throws Exception {
                        //倒计时完毕事件处理
                        finish();
                    }
                })
                .subscribe();
```

>如果本篇文章对您有帮助 麻烦点个赞支持一下

[回到顶部](#readme)
