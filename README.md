bootstrap-datepicker
====================

Our own fork of eternicode's bootstrap datepicker that includes time selection.

## Changes

We've made some major changes to this fork of bootstrap datepicker. The main change is the ability to select time in a simple and easy way. Below we document some of these changes. For the original usage, see the [eternicode's docs](http://bootstrap-datepicker.readthedocs.org/)

## Options

One of the big changes in this fork is the ability to select time. So we have a few more options when you initialize the datepicker.

### showTime

showTime by default is true. If you pass in 'false' it will not show the time selection menu. It will thus revert to the old style datepicker.

### startTime

startTime is a parameter that takes a digital 24-hour time string as the start time when you open the datepicker. The default is 12:00. It also automatically converts 24h time to AM/PM. So for example "16:00" would display as "4:00" PM in the datepicker.

### startDateThreshold

The startDateThreshold parameter is a way to set how strict the startDate parameter should be in disabling previous days to be selectable. The default is 'time'. This means that if you are beyond the startDate parameter in terms of the time in the day, then the datepicker will disable that day. Because the startDate parameter doesn't take time into account, the default time is around noon of that day. So if you're using the datepicker in the afternoon, the current day will be disabled.

To solve this there is another variable for the startDateThreshold called, 'day'. This sets the threshold to disable any days before the startDate and doesn't take the time into account. It ignores it. The startDate parameter is then more consistent on disabling the days before it.

## Events

We've added an extra event.

### setButton

This event gets triggered when you press the "Set" button. At present we don't have a method enabled to store the time as variable, so you'll have to grab the data from the DOM. Here is how our setButton listener looks like.

```javascript
.on('setButton', function(ev){
	// Makes sure that the datepicker is still there in case something happened.
	if($('.datepicker-time select[name=hour]').length) {
		// Grab the hours
		var hour = parseInt($('.datepicker-time select[name=hour]').val());
		// Grab the minutes
		var minute = parseInt($('.datepicker-time select[name=minute]').val());
		// Grab the meridiem
		var meridiem = $('.datepicker-time select[name=ampm]').val();

		// Logic for adjusting for meridiem
		if(meridiem == 'pm' && hour != 12) hour += 12;
		else if(meridiem == 'am' && hour == 12) hour = 0;

		// Create date object
		// Grabs the date from the datepicker
		var date = new Date(ev.date);
		// Sets the hours
		date.setHours(hour);
		// Sets the minutes
		date.setMinutes(minute);
	}
})
```

The listener above is definitely a good idea for us to simplify in the future.

## Some missing changes

Unfortunately, our fork of the bootstrap datepicker is a bit out of date from [eternicode's fork](https://github.com/eternicode/bootstrap-datepicker). For example we don't have the multidate selectors & orientation parameters present among some other changes. We've decided to release our version as is. We can update it if users are keen to see of the eternicode's features added back in.

## Contributing

When you've made your changes, feel free to submit pull requests. We're also open to suggestions to make some of the changes for you as well.

## Thanks

Thanks to [@eternicode](https://github.com/eternicode) for the fork and Stefan for the [original version](http://www.eyecon.ro/bootstrap-datepicker/). Also thanks goes out to [@joelg](https://github.com/joelg), who's done most of the work on this fork.