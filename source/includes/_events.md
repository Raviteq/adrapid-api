# Events

Events are generated through Server Sent Events (SSE:s). This enable tracking orders in real time
and display them on the browser as they are completed.


## Watching order events

> item_complete event:

```json
{
    "id": "1234",
    "type": "asft",
    "format": "300x300"
}
```

> order_complete event:

```json
{
    "id": "123"
}
```

```javascript
//
// Vanilla javascript example
//

function watch_order(order_id, api_key)
{
  //
  // setup & initialize the EventSource
  //
  var base_url    = 'http://api.adrapid.com/events/order',
      token       = generate_token(api_key),
      evt_url     = base_url + order_id + '/' + token,
      evtSource   = new EventSource(evt_url);

  //
  // listen to eventsource events
  //

  //
  // show items as they are completed
  //
  evtSource.addEventListener("item_complete", function(e) {
      var data = JSON.parse(e.data); // parse json data to array
      show_banner(data.id); // show result using a custom function
  }, false);

  //
  // show an message when all order items have been completed
  //
  evtSource.addEventListener('order_complete', function(e) {
      var order = JSON.parse(e.data);
      alert('Successfully completed order #' + order.id + '!');
  }, false);
}
```

Use the following endpoint to watch for order events. The endpoint emits two events: *item_complete* and *order_complete*.

### SSE Endpoint

`http://api.adrapid.com/events/order/:id/:token`

