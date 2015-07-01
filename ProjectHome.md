This plug-in is used to send and receive the JSON object directly with Web Sockets API.
## Usage ##
### Connection ###
```
var ws = $.websocket("ws://127.0.0.1:8080/");
```

### Sending Message ###
```
ws.send('hello');  // sending message is '{type:'hello'}'.
ws.send('say', {name:'foo', text:'baa'});  // sending message is '{type:'say', data:{name:'foo', text:'baa'}}'
```

### Event Handling ###
```
var ws = $.websocket("ws://127.0.0.1:8080/", {
	open: function() { ... },
	close: function() { ... },
	events: {
		say: function(e) {
			alert(e.data.name); // 'foo'
			alert(e.data.text); // 'baa'
		}
	}
});
```


## Example ##
```
<!doctype html>
<html>
<head>
<meta charset="UTF-8">
<title>WebSocket Chat</title>
</head>
<body>
<h1>WebSocket Chat</h1>
<section id="content"></section>
<input id="message" type="text"/>
<script src="http://www.google.com/jsapi"></script>
<script>google.load("jquery", "1.3")</script>
<script src="http://jquery-json.googlecode.com/files/jquery.json-2.2.min.js"></script>
<script src="http://jquery-websocket.googlecode.com/files/jquery.websocket-0.0.1.js"></script>
<script>
var ws = $.websocket("ws://127.0.0.1:8080/", {
	events: {
		message: function(e) { $('#content').append(e.data + '<br>') }
	}
});
$('#message').change(function(){
  ws.send('message', this.value);
  this.value = '';
});
</script>
</body>
</html>
```