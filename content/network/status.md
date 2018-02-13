---
layout: single
title: Status
menu:
    main:
        parent: network
---

<script type="view" id="status-view">
<div class="statoid">
<span class="service">{service}</span>
<span class="status">{status}</span>
</div>
</script>

<script type="view" id="message-view">
<div class="message">
<h3>{title}</h3>
<p>{description}</p>
<span class="created">{created}</span>
<span class="updated">{updated}</span>
</div>
</script>

<div id="statuses"></div>
<div id="messages"></div>

<script>
	var status_view = document.getElementById('status-view').innerHTML;
    var message_view = document.getElementById('message-view').innerHTML;
	
	function renderView(data, view)
	{
		var newView = ''+view;
		for (let attr in data){
			newView = newView.replace('{'+attr+'}', data[attr]);
		}
		return newView;
	}

	
	var data = {
		"services":
		[
			{
				"service": "Gateways",
				"status": "Operational"
			},
			{
				"service": "Things Network Infrastructure",
				"status" :"Operational"
			},
			{
				"service": "Kent Network API",
				"status" : "Operational"
			},
			{
				"service": "Databases",
				"status" : "Operational"
			},
			{
				"service": "Web Servers",
				"status" : "Operational"
			},
			{
				"service": "Kent Network Apps",
				"status" : "Operational"
			}
		],
		"messages":
		[
			{
				"title": "Planned maintenance",
				"created": "2015-05-22T14:56:29.000Z",
				"updated": "2015-05-22T14:56:28.000Z",
				"description": "hoovering the insides of gateway 1"
			}
		]
	};
	
	for (var i = 0; i < data['services'].length; i++) {
		var elem = renderView(data['services'][i], status_view);
		document.getElementById("statuses").innerHTML += elem;
	}

	for (var i = 0; i < data['messages'].length; i++) {
		var elem = renderView(data['messages'][i], message_view);
		document.getElementById("messages").innerHTML += elem;
	}

</script>
