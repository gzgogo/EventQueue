
# 用javascript实现一个事件队列

详见[github](https://github.com/gzgogo/EventQueue)，使用方法参考`index.html`
```
function EventQueue(delayTime) {
  this._delayTime = delayTime || 20;
  this._queue = [];
}

EventQueue.prototype = {
  add: function (excute, params) {
    this._queue.push({
      excute: excute,
      params: params
    });

    this.start();
  },

  start: function () {
    if (this._delayTime <= 0) {
      this.process();
    } else {
      var self = this;
      setTimeout(function () {
        self.process();
      }, self._delayTime);
    }
  },

  process: function () {
    var item = this._queue.shift();

    if (item) {
      var self = this;
      item.excute(item.params, function () {
        self.process();
      });
    }
  }
};
```