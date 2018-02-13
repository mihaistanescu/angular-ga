# googleanalytics-angular [![Build Status](https://travis-ci.org/mihaistanescu/googleanalytics-angular.svg?branch=PublishBranch)](https://travis-ci.org/mihaistanescu/googleanalytics-angular)

> Google Analytics for your Angular application


## Install

```
$ npm install --save googleanalytics-angular
```


## Usage

### Configuration

The Google Analytics tracking script is not included in this module. Make sure to add it to your page.

```js
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { GoogleAnalyticsModule, GA_TOKEN } from 'googleanalytics-angular';

import { AppComponent } from './app.component';

@NgModule({
	imports: [
		BrowserModule,
		GoogleAnalyticsModule.forRoot()
	],
	declarations: [
		AppComponent
	],
	bootstrap: [AppComponent],
	providers: [
		{ provide: GA_TOKEN, useValue: 'UA-TOKEN-1' }
	]
})
export class AppModule { }
```

It's also possible to leave the configuration empty and configure the library later on through the service.

```js
@NgModule({
	imports: [
		BrowserModule,
		GoogleAnalyticsModule.forRoot()
	],
	declarations: [
		AppComponent
	],
	bootstrap: [AppComponent]
})
export class AppModule { }
```

### Service

Inject the `GoogleAnalyticsService` into your components or services.

```js
import { Component, OnInit } from '@angular/core';
import { GoogleAnalyticsService } from 'googleanalytics-angular';

@Component({
	templateUrl: 'app.component.html'
})
export class AppComponent implements OnInit {

	constructor(
		private gaService: GoogleAnalyticsService
	) { }

	ngOnInit() {
		this.gaService.event.emit({
			category: 'app',
			action: 'bootstrap'
		});
	}
}
```

#### Configuration

```js
import { Component, OnInit } from '@angular/core';
import { GoogleAnalyticsService } from 'googleanalytics-angular';

@Component({
	templateUrl: 'app.component.html'
})
export class AppComponent implements OnInit {

	constructor(
		private gaService: GoogleAnalyticsService
	) { }

	ngOnInit() {
		this.gaService.configure('UA-TOKEN-1');
	}
}
```

#### Named Tracker 

More information about named trackers can be found [`here`](https://developers.google.com/analytics/devguides/collection/analyticsjs/command-queue-reference).

```js
import { Component, OnInit } from '@angular/core';
import { GoogleAnalyticsService } from 'googleanalytics-angular';

@Component({
	templateUrl: 'app.component.html'
})
export class AppComponent implements OnInit {

	constructor(
		private gaService: GoogleAnalyticsService
	) { }

	ngOnInit() {
		var options = { 
			clientId: 'clientId',
			cookieDomain: 'auto',
			name: 'trackerName',
			namedTracker: true
		}

		this.gaService.configure('UA-TOKEN-1', options);
	}
}
```



## API

### service.configure(trackingId, [options])

#### trackingId

Type: `string`

Tracking Id.

#### options

Type: `Object` `string`<br>
Default: `auto`

Any of the [`Create Only Fields`](https://developers.google.com/analytics/devguides/collection/analyticsjs/field-reference#create).

The ability to send to named tracker with option `namedTracker`<br>
Type: `boolean`<br>
Default: `false`


### service.event.emit(event: Event)

Emit a Google Analytics event.

#### event

##### category

Type: `string`

Typically the object that was interacted with (e.g. `Video`)

##### action

Type: `string`

The type of interaction (e.g. `play`)

##### label

*Optional*<br>
Type: `string`

Useful for categorizing events (e.g. `Fall Campaign`)

##### value

*Optional*<br>
Type: `number`

A numeric value associated with the event (e.g. `42`)

### service.pageview.emit(pageview: PageView)

Emit a Google Analytics page view.

#### pageview

##### page

Type: `string`

The path portion of a URL. This value should start with a slash (/) character.

##### title

*Optional*<br>
Type: `string`

The title of the page (e.g. homepage)

##Original Author

Thanks to Sam Verschueren for the original implementation.

## License

MIT © [Mihai Stanescu](https://github.com/mihaistanescu)
