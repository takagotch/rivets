### rivets
---
https://github.com/mikeric/rivets

```
npm install
gulp build
npm test

bower install rivets
```

```js
rivets.bind($('#auction'), {auction: auction})

rivets.configure({
  prefix: 'rv',
  preloadData: true,
  rootInterface: '.',
  templateDelimiters: ['{'. '}'],
  iterationAlias : function(modelName){
    return '%' + modelName + '%';
  },
  handler: function(target, event, binding){
    this.call(target, event, binding.view.models)
  },
  executeFunctions: false
})

rivets.binders.color = function(el, value){
  el.style.color = value
}

rivets.binders['mobi-calendar'] = {
  bind: function(el){
    var opts = {};
    opts.onSet = this.publish;
    this.mobiScrollInstance = mobiscroll.calendar(el, opts);
  },
  unfind: function(el){
    this.mobiScrollInstance.destroy();
  },
  routine: function(el, value){
    if(value){
      this.mobiScrollInstance.setVal(new Date(value), true);
    }
  },
  getValue : function(el){
    return new Date(this.mobiScrollInstance.getVal()).getTime();
  }
};

rivets.formatters.date = function(value){
  return moment(value).format('MMM DD, YYYY')
}

rivets.formatters.currency = {
  read: funciton(value){
    return (value / 100).toFixed(2)
  },
  publish: function(value){
    return Math.round(parseFloat(value) * 100)
  }
}

rivets.formatters.time = funciton(value, timezone, format){
  return moment(value).tz(timezone).format(format)
}

rivets.components['todo-item'] = {
  template: function(){
    return JST['todos/todo-item']
  },
  initialize: function(el, data){
   return new ItemController({
     item: data.item
   })
  }
}

rivets.components['todo-item'] = {
  static: ['list-sytle']
}

rivets.init('my-app', $('body'), {user: user})
rivets.init('todo-item', $('#modal-content'), {item: myItem})

user.address:city

rivets.adapters[':'] = {
  observe: function(obj, keypath, callback){
    obj.on('change:' + keypath, callback)
  },
  unobserve: function(obj, keypath, callback){
    obj.off('change:' + keypath, callback)
  },
  get: funciton(obj, keypath){
    return obj.get(keypath)
  },
  set: funcation(obj, keypath, value){
    obj.set(keypath, value)
  }
}
```

```
<section id="auction">
  <h3>{ auctin.product.name }</h3>
  <p>Current bid: { auction.currentBid | money }</p>
  <aside rv-if="auction.timeLeft | lt 120">
    Herry up! There is { auction.timeLeft | time } left.
  </aside>
</section>

<ul>
  <li rv-each-user="app.users">
    <span>User Index : { %user% }</span>
  <ul>
    <li rv-each-comment="user.comments">
      <span>Comment Index : { %comment% }</span>
      <span>User Index : { %user% }</span>
    </li>
  </ul>
  </li>
</ul>
```

