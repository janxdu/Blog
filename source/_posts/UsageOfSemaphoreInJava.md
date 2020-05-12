---
title: Usage of Semaphore in Java
categories: Back-End
date: 2017-11-28 00:00:00
---

Recently I needed to prepare a presentation about Java thread at the weekly meeting. I intended to present the usage of Semaphore, which is a way of mutual exclusion to guarantee concurrency correction. In early version of JDK, the Synchronize symbol is the only way that provides data synchronization at function and block level. However, it provides a package named `java.utils,concurrent.locks` since JDK1.6, which contains senior features for the same intention, including interruptible at waiting and fair lock and etc. In it, `AbstractQueuedSynchronizer` provides a framework for implementing blocking locks and related synchronizers (semaphores, events, etc) that rely on first-in-first-out (FIFO) wait queues. We will see an implement of `AbstractQueuedSynchronizer`--`Semaphore` to analysis the essential idea of it and its usage.
The simplest usage of `Semaphore` are:
- acquire(): Acquires a permit from this semaphore, blocking until one is available, or the thread is interrupted.
- release(): Releases a permit, returning it to the semaphore.
We will mainly discuss  the two process by an example of imitating a situation of depositing into bank. Supposes there are two bank tellers in the bank, six customers want to deposit, so they need to line up.

```java
 /**
     * Bank account Entity
 **/
 public class BankAccount {

    private int amount = 0;

    private String id = null;

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public int getAmount() {
        return amount;
    }

    public void save(int money) {
        amount += money;
    }
}
```

```
public class SemaphoreTest {

    /**
     * deposit
     */
    class NewThread implements Runnable {
        private BankAccount bankAccount;
        private Semaphore   semaphore;

        public NewThread(BankAccount bankAccount, Semaphore semaphore) {
            this.bankAccount = bankAccount;
            this.semaphore = semaphore;
        }

        public void run() {
            if (semaphore.availablePermits() > 0) {
                System.out.println("Thread " + bankAccount.getId() + " is starting. Entering into the bank, a teller is available.");
            } else {
                System.out.println("Thread " + bankAccount.getId() + " is starting，Entering into the bank, every teller is busy，line up. ");
            }
            try {
                semaphore.acquire();

                if(!Thread.currentThread().isInterrupted()){
                    bankAccount.save((int) Math.round(Math.random()*1000));
                    Thread.sleep(Math.round(Math.random()*1000));
                    System.out.println("Thread "+bankAccount.getId() + " deposit：" + bankAccount.getAmount());
                    System.out.println("Thread " + bankAccount.getId() + "has deposited，leave the bank.");
                }
                semaphore.release();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    /**
     * thread handler
     */
    public void threadHandler() throws InterruptedException {
        Semaphore semaphore = new Semaphore(2);
        ExecutorService es = Executors.newCachedThreadPool();
        for (int i = 0; i < 6; i++) {
            BankAccount bankAccount = new BankAccount();
            bankAccount.setId("account"+i);
            es.submit(new Thread(new NewThread(bankAccount, semaphore)));
        }
        es.shutdown();

    }

    public static void main(String[] args) throws InterruptedException {
        SemaphoreTest test = new SemaphoreTest();
        test.threadHandler();
    }
}
```
Result:
```java
Thread account0 is starting. Entering into the bank, a teller is available.
Thread account1 is starting. Entering into the bank, a teller is available.
Thread account2 is starting，Entering into the bank, every teller is busy，line up. 
Thread account3 is starting，Entering into the bank, every teller is busy，line up. 
Thread account4 is starting，Entering into the bank, every teller is busy，line up. 
Thread account5 is starting，Entering into the bank, every teller is busy，line up. 
Thread account0 deposit：258
Thread account0has deposited，leave the bank.
Thread account1 deposit：55
Thread account1has deposited，leave the bank.
Thread account2 deposit：902
Thread account2has deposited，leave the bank.
Thread account4 deposit：336
Thread account4has deposited，leave the bank.
Thread account3 deposit：610
Thread account3has deposited，leave the bank.
Thread account5 deposit：717
Thread account5has deposited，leave the bank.
```
The `Semaphore` initiator confines total amount of tellers. Let‘s check the implement of `acquire()` in `Semaphore`, parameter `1` stands for acquiring  one permit from the semaphore.
```
public void acquire() throws InterruptedException {
        sync.acquireSharedInterruptibly(1);
    }
```
Then we look into `acquireSharedInterruptibly()`, at first it checks if the thread is interrupted, next it does two things: 
-   Try to acquire assigned permits from the semaphore.
-  If acquire failed, says the semaphore is lower than 0, then stay and wait in a chain.
```
public final void acquireSharedInterruptibly(int arg)
            throws InterruptedException {
        if (Thread.interrupted())
            throw new InterruptedException();
        if (tryAcquireShared(arg) < 0)
            doAcquireSharedInterruptibly(arg);
    }
```
The `tryAcquireShared()` is implemented in `Semaphore`,`AbstractQueuedSynchronizer` only provide interface, because the rule of an acquirement's success and failure depends on specific business. `Semaphore` default uses a unfair strategy, which means it is possible for one thread to invoke acquire before another but reach the ordering point after the other. Generally, the throughput advantages of non-fair ordering often outweigh fairness considerations. The unfair way of `tryAcquireShared()` is shown below, it calculates remaining state and break if the amount of state has been drained or acquires successfully. `compareAndSetState()` in it, acronym as `CAS`, is a common way of guaranteeing a state is updated atomically.
```java
final int nonfairTryAcquireShared(int acquires) {
            for (;;) {
                int available = getState();
                int remaining = available - acquires;
                if (remaining < 0 ||
                    compareAndSetState(available, remaining))
                    return remaining;
            }
        }
```
Then we analysis `doAcquireSharedInterruptibly()` , when the thread's acquirement is failed, it has to wait in a FIFO chain through `addWaiter()`. If it becomes the header in chain, trying to acquire again. If acquires successes, then sets head of queue to be the node and try to signal next queued node. If it fails, checks and updates status for a node that failed to acquire, while parks and checks interrupt at the same time. If some problem happened on the whole process, it will cancel the node's acquire.
```
private void doAcquireSharedInterruptibly(int arg)
        throws InterruptedException {
        final Node node = addWaiter(Node.SHARED);
        boolean failed = true;
        try {
            for (;;) {
                final Node p = node.predecessor();
                if (p == head) {
                    int r = tryAcquireShared(arg);
                    if (r >= 0) {
                        setHeadAndPropagate(node, r);
                        p.next = null; // help GC
                        failed = false;
                        return;
                    }
                }
                if (shouldParkAfterFailedAcquire(p, node) &&
                    parkAndCheckInterrupt())
                    throw new InterruptedException();
            }
        } finally {
            if (failed)
                cancelAcquire(node);
        }
    }
```

`release()` in `Semaphore`:
```
 public void release() {
        sync.releaseShared(1);
    }
```
It invokes `releaseShared()` of a class derived from `AbstractQueuedSynchronizer`.

