

## 实现Runnable接口

### 继承Thread类

- 子类继承Thread类具备多线程能力
- 启动线程：子类对象.start()
- ==不建议使用：避免OOP单继承局限性==

### 继承Runnable接口

- 实现接口Runnable具有多线程能力
- 启动线程：传入对象+Thread对象.start()
- ==推荐使用：避免单继承局限性，灵活，方便同一个对象被多个线程使用==



## 并发问题









