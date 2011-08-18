A small jQuery plugin which acts as a simplification of the [Geolocation API](http://dev.w3.org/geo/api/spec-source.html).

Instead of using navigator.geolocation.getCurrentPosition you can now just use the jQuery methods `$.geolocation.get()` or `$.geolocation.watch()`.

Contrary to the standard API the only parameter the functions expect is a JSON object with three properties in no particular order: success, error, options. For success and error you can also use their alias properties "win" and "fail": `$.geolocation.get({win: function() {}, fail: function() {}, options);`

You can also use `$.geolocation.getCurrentPosition(success, error, options)` to get native API feeling if this makes you happier. In conjunction with my Geolocation API polyfill script this also works with some non-standard Geolocation APIs like Google Gears or Blackberry Location.

## Usage

### $.geolocation.clearWatch(integer watchID)
Stops tracking of the user for the according watchID.

### $.geolocation.get(object config)
Get the current position of the user

#### Config properties

<ul>
	<li>
		<strong>error</strong><br />
		Function to call if geolocation request failed
	</li>
	<li>
		<strong>fail</strong><br />
		Alias for error
	</li>
	<li>
		<strong>options</strong>
		Options for the geolocation request
		<ul>
			<li>enableHighAccuracy</li>
			<li>maximumAge</li>
			<li>timeout</li>
		</ul>
	</li>
	<li>
		<strong>success</strong><br />
		Function to call if geolocation request was successful
	</li>
	<li>
		<strong>win</strong><br />
		Alias for success
	</li>
</ul>


### $.geolocation.getCurrentPosition(callback success, callback error, object settings)
Get the current position of the user (API standard behavior)

#### Parameters

<strong>success</strong> Function to call if geolocation request was successful
<strong>error</strong> Function to call if geolocation request failed
<strong>options</strong> Options for the geolocation request
<ul>
	<li>enableHighAccuracy</li>
	<li>maximumAge</li>
	<li>timeout</li>
</ul>

### $.geolocation.stop(integer watchID)

Stops tracking of the user for the according watchID.

### $.geolocation.stopAll()

Stops all running watchPosition callbacks.

### $.geolocation.watch(object config)

Track the movement of the user
Returns: watchID (Integer)

#### Config properties

<ul>
	<li>
		<strong>error</strong><br />
		Function to call if geolocation request failed
	</li>
	<li>
		<strong>fail</strong><br />
		Alias for error
	</li>
	<li>
		<strong>settings</strong>
		Options for the geolocation request
		<ul>
			<li>enableHighAccuracy</li>
			<li>maximumAge</li>
			<li>timeout</li>
		</ul>
	</li>
	<li>
		<strong>success</strong><br />
		Function to call if geolocation request was successful
	</li>
	<li>
		<strong>win</strong><br />
		Alias for success
	</li>
</ul>


### $.geolocation.watchPosition(callback success, callback error, object settings)

Track the movement of the user (API standard behavior)
Returns: watchID (Integer)

#### Parameters

<strong>success</strong> Function to call if geolocation request was successful
<strong>error</strong> Function to call if geolocation request failed
<strong>options</strong> Options for the geolocation request
<ul>
	<li>enableHighAccuracy</li>
	<li>maximumAge</li>
	<li>timeout</li>
</ul>


### Examples
<pre>function alertMyPosition(position) {
	alert("Your position is " + position.coords.latitude + ", " + position.coords.longitude);
}

function noLocation(error) {
	alert("No location info available. Error code: " + error.code);
}

$('#getPositionButton').bind('click', function() {
	$.geolocation.get({win: alertMyPosition, fail: noLocation});
});

$('#watchPositionButton').bind('click', function() {
	// alertMyPosition is called each time the user's position changes
	myPosition = $.geolocation.watch({win: alertMyPosition}); 
});

$('#stopButton').bind('click', function() {
	$.geolocation.stop(myPosition);
});</pre>

<h3>Demo</h3>
[You can find a demo here](http://manuel-bieh.de/publikationen/scripts/jquery/geolocation/)