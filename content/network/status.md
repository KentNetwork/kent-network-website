---
layout: single
title: Status
menu:
    main:
        parent: network
---

<script type="view" id="status-view">
<div class="statoid">
<span class="fas fa-circle" style="color: {lightcolor}"></span>
<span class="service">{service}</span>
<span class="status">{status}</span>
</div>
</script>

<script type="view" id="message-view">
<div class="message">
<h3>{title}</h3>
<span class="created">{created}</span>
<span class="updated">{LastUpdated}</span>
</div>
</script>

<h1 id="api-status"><span id="api-traffic-light"></span>API: </h1>
<div id="statuses"></div>

<h1>Messages</h1>

<div id="messages"></div>

<script>
	var status_view = document.getElementById('status-view').innerHTML;
    var message_view = document.getElementById('message-view').innerHTML;
	
	function statusToColor(status) {
		switch(status) {
		  case "ok": 
			  return "green";
          case "error": 
		      return "red";
		  default: 
		    return "#ff9800";
		}
	
	}
	
	function renderView(data, view)
	{
	    console.log(data);
		var newView = ''+view;
		for (let attr in data){
			newView = newView.replace('{'+attr+'}', data[attr]);
		}
		newView = newView.replace('{lightcolor}', statusToColor(data['status']));
		return newView;
	}
	
	var endpoint = "https://api.kent.network/status";
	var xhttp = new XMLHttpRequest();	
	xhttp.onreadystatechange = function () {
		if (this.readyState == 4 && this.status == 200) {
			let data = JSON.parse(this.responseText);
			
			document.getElementById("api-status").innerHTML += data['status'];
			tl = document.getElementById("api-traffic-light");
			tl.className = "fas fa-circle";
			tl.style = "color: " + statusToColor(data['status']);
			
			for (var i = 0; i < data['services'].length; i++) {
				var elem = renderView(data['services'][i], status_view);
				document.getElementById("statuses").innerHTML += elem;
			}

            for (var i = 0; i < data['messages'].length; i++) {
				data['messages'][i]['created'] = (new Date(data['messages'][i]['created'])).toDateString()
				data['messages'][i]['LastUpdated'] = (new Date(data['messages'][i]['LastUpdated'])).toDateString()
				var elem = renderView(data['messages'][i], message_view);
				document.getElementById("messages").innerHTML += elem;
			}
		} else if (this.readyState == 4) {
			
		}
	}
	xhttp.open("GET", endpoint, true);
	xhttp.send();
</script>
