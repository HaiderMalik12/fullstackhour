---
layout: dark-post
title: "Bootstraping Angular2 Application"
description: "How Angular2 Bootstraps an Application"
tags: [Angular2]
comments: true
image:
    feature: Angular2-logo.png
categories: [Angular2]
share: true
---




### File Structure

*app/app.component.ts*

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template:`<h1>Bootstraping Angular2 Application</h1>`
})
export class AppComponent {
  
}
```

[View Example](https://embed.plnkr.co/zWfNfr/)

*index.html*

```html
<body>
    <app-root>Loading...</app-root>
</body>
```

*app/app.module.ts*

```typescript
import { BrowserModule }  from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component'
@NgModule({
  imports: [BrowserModule],
  declarations: [AppComponent],
  bootstrap: [AppComponent]
})
export class AppModule {
}
 
```


*app/main.ts*

```typescript
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic'; import { AppModule } from './app.module';
platformBrowserDynamic().bootstrapModule(AppModule);
```

The bootstrap process loads main.ts which is the entry point of the application.
The `AppModule` operats as the root module of our application. This root module
is configured to use `AppComponent` as the component to bootstrap, and will be
rendered on any `app-root` HTML element.

### Bootstraping Providers

This bootstrap process also starts with dependency injection in Angular2.


*app/app.module.ts*

```typescript
import { BrowserModule }  from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component'
import { AuthService } from './auth.service';
@NgModule({
  imports: [BrowserModule],
  providers: [AuthService],
  declarations: [AppComponent],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

[View Example](https://embed.plnkr.co/zWfNfr/)

 {% include disqus.html %}
