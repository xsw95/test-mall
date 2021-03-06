# async和await
## 同步
如果在函数返回的时候，调用者就能够得到预期结果(即拿到了预期的返回值或者看到了预期的效果)，那么这个函数就是同步的。
如果函数是同步的，即使调用函数执行的任务比较耗时，也会一直等待直到得到预期结果。

## 异步
如果在函数返回的时候，调用者还不能够得到预期结果，而是需要在将来通过一定的手段得到，那么这个函数就是异步的。
如果函数是异步的，发出调用之后，马上返回，但是不会马上返回预期结果。调用者不必主动等待，当被调用者得到结果之后会通过回调函数主动通知调用者。

## async，await用法
ES2017中的新增特性async，await来实现异步，要使用await，包含它的最近的一级函数必须是async的，例：
```
handleAddNewOne () {
   // 先检验表单合法性
   this.$refs.form.validate(async valid => {
     if (!valid) return;

     const content = this.isSourceTab
          ? '该 Campid 记录已经存在，请不要重复添加！'
          : 'Pubid + Campid + isMannual 作为 Key 的记录已经存在，请检查！';
     if (!this.canAddNewForPublisher() || !this.canAddNewForDemand()) {
       this.$Message.warning({ content });
       return;
     }

     const isCampidBelongToSource = await this.isCampidBelongToSource();
       if (!isCampidBelongToSource) return;
       this.loading.addNew = true;
       this.isSourceTab ? this.addNewforDemand() : this.addNewForPublisher();
     });
},
```
如果async写在handleAddNewOne之前，await就找不到。

async函数声明定义了一个异步函数，它返回一个AsyncFunction对象。异步函数是一个通过事件循环异步操作的函数，使用隐式Promise返回其结果。
但是使用异步函数的代码的语法和结构更像是使用标准同步函数。


