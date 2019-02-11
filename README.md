### rivets
---
https://github.com/mikeric/rivets

```
npm install
gulp build
npm test
```

```js
rivets.bind($('#auction'), {auction: auction})
```

```
<section id="auction">
  <h3>{ auctin.product.name }</h3>
  <p>Current bid: { auction.currentBid | money }</p>
  <aside rv-if="auction.timeLeft | lt 120">
    Herry up! There is { auction.timeLeft | time } left.
  </aside>
</section>
```

