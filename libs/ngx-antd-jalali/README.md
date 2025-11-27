<p align="center">
  <a href="http://ng.ant.design">
    <img width="230" src="https://img.alicdn.com/tfs/TB1TFFaHAvoK1RjSZFwXXciCFXa-106-120.svg">
  </a>
</p>

<h1 align="center">
ngx-antd-jalali <br>
Jalali Date Adapter
</h1>

<div align="center">

Angular DatePicker component library based on Ant Design with Jalali (Persian) calendar support.

[![npm package](https://img.shields.io/npm/v/ngx-antd-jalali.svg?style=flat-square)](https://www.npmjs.com/package/ngx-antd-jalali)
[![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg?style=flat-square)](https://github.com/prettier/prettier)

</div>

## [Demo](https://stackblitz.com/edit/ng-met-antd-datepicker)

View DatePickerJalali in action at [Stackblitz Demo](https://stackblitz.com/edit/ng-met-antd-datepicker)

<img src="https://user-images.githubusercontent.com/42533472/171279996-75478af5-7977-4845-bf56-846c448308ae.gif" alt="jalali-date-picker" style="max-width: 100%; display: inline-block;" data-target="animated-image.originalImage">

## 🖥 Environment Support

- Angular `^20.0.0`
- ng-zorro-antd `^20.0.0`
- Server-side Rendering
- Modern browsers including the following [specific versions](https://angular.io/guide/browser-support)

## 📦 Installation

```bash
npm install ng-zorro-antd@^20.0.0
npm install ngx-antd-jalali jalali-moment
```

## 🔧 Usage in Angular Workspace

### Step 1: Install Dependencies

In your Angular project, install the required packages:

```bash
npm install ng-zorro-antd@^20.0.0 ngx-antd-jalali jalali-moment
```

### Step 2: Import Styles

Add the ng-zorro-antd styles to your `angular.json`:

```json
{
  "styles": [
    "node_modules/ng-zorro-antd/ng-zorro-antd.min.css"
  ]
}
```

Or import in your global styles file:

```less
@import "ng-zorro-antd/ng-zorro-antd.min.css";
```

### Step 3: Configure the Module

#### Standalone Components (Recommended for Angular 20+)

```typescript
import { Component } from '@angular/core';
import { FormsModule, ReactiveFormsModule } from '@angular/forms';
import { NzDatePickerModule } from 'ngx-antd-jalali/date-picker';
import { NzCalendarModule } from 'ngx-antd-jalali/calendar';
import { NZ_I18N, fa_IR, NZ_DATE_CONFIG, NZ_DATE_FORMATS } from 'ngx-antd-jalali/i18n';
import { NzDateAdapter, JalaliMomentDateAdapter } from 'ngx-antd-jalali/core';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [
    FormsModule,
    ReactiveFormsModule,
    NzDatePickerModule,
    NzCalendarModule
  ],
  providers: [
    { provide: NZ_I18N, useValue: fa_IR },
    { provide: NzDateAdapter, useClass: JalaliMomentDateAdapter },
    {
      provide: NZ_DATE_CONFIG,
      useValue: {
        firstDayOfWeek: 6, // Saturday
      }
    }
  ],
  template: `
    <nz-date-picker [(ngModel)]="date"></nz-date-picker>
    <nz-range-picker [(ngModel)]="dateRange"></nz-range-picker>
  `
})
export class AppComponent {
  date: Date | null = null;
  dateRange: [Date, Date] | null = null;
}
```

#### NgModule-based Application

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule, ReactiveFormsModule } from '@angular/forms';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';

import { NzDatePickerModule } from 'ngx-antd-jalali/date-picker';
import { NzCalendarModule } from 'ngx-antd-jalali/calendar';
import { NzTimePickerModule } from 'ngx-antd-jalali/time-picker';
import { NZ_I18N, fa_IR, NZ_DATE_CONFIG } from 'ngx-antd-jalali/i18n';
import { NzDateAdapter, JalaliMomentDateAdapter } from 'ngx-antd-jalali/core';

@NgModule({
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
    FormsModule,
    ReactiveFormsModule,
    NzDatePickerModule,
    NzCalendarModule,
    NzTimePickerModule
  ],
  providers: [
    { provide: NZ_I18N, useValue: fa_IR },
    { provide: NzDateAdapter, useClass: JalaliMomentDateAdapter },
    {
      provide: NZ_DATE_CONFIG,
      useValue: {
        firstDayOfWeek: 6, // Saturday
      }
    }
  ],
  // ...
})
export class AppModule {}
```

### Step 4: Use Components in Templates

#### Date Picker

```html
<!-- Basic date picker -->
<nz-date-picker [(ngModel)]="date"></nz-date-picker>

<!-- Date picker with time -->
<nz-date-picker nzShowTime [(ngModel)]="dateTime"></nz-date-picker>

<!-- Month picker -->
<nz-month-picker [(ngModel)]="month"></nz-month-picker>

<!-- Year picker -->
<nz-year-picker [(ngModel)]="year"></nz-year-picker>

<!-- Week picker -->
<nz-week-picker [(ngModel)]="week"></nz-week-picker>
```

#### Range Picker

```html
<!-- Basic range picker -->
<nz-range-picker [(ngModel)]="dateRange"></nz-range-picker>

<!-- Range picker with time -->
<nz-range-picker nzShowTime [(ngModel)]="dateTimeRange"></nz-range-picker>
```

#### Calendar

```html
<!-- Full calendar -->
<nz-calendar [(ngModel)]="selectedDate"></nz-calendar>

<!-- Calendar card mode -->
<nz-calendar nzMode="year" [(ngModel)]="selectedDate"></nz-calendar>
```

#### Time Picker

```html
<!-- Basic time picker -->
<nz-time-picker [(ngModel)]="time"></nz-time-picker>

<!-- 12-hour format -->
<nz-time-picker [(ngModel)]="time" [nzUse12Hours]="true"></nz-time-picker>
```

## 🌐 Internationalization (i18n)

The library supports Persian (Farsi) locale out of the box:

```typescript
import { NZ_I18N, fa_IR } from 'ngx-antd-jalali/i18n';

@NgModule({
  providers: [
    { provide: NZ_I18N, useValue: fa_IR }
  ]
})
export class AppModule {}
```

## 📅 Custom Date Adapter

If you need to present another calendar like [Jalali](https://en.wikipedia.org/wiki/Jalali_calendar) or [Hijri](https://en.wikipedia.org/wiki/Islamic_calendar), you can provide a custom NzDateAdapter which implements required methods to deal with native date object.

### Creating a Custom Date Adapter

```typescript
import { NzDateAdapter } from 'ngx-antd-jalali/core';

export class CustomDateAdapter extends NzDateAdapter<any> {
  // Implement all abstract methods
  today(): Date { /* ... */ }
  parse(text: string, formatStr: string): Date { /* ... */ }
  format(date: Date, displayFormat: string): string { /* ... */ }
  // ... other methods
}

@NgModule({
  providers: [
    { provide: NzDateAdapter, useClass: CustomDateAdapter }
  ],
})
export class AppModule {}
```

### Sample Jalali-Moment Date Adapter

[Jalali-Moment date adapter](https://gist.github.com/psychomet/22798ab7552b38751ac44a665fe1c512)

## 📖 API Reference

### NzDatePickerComponent

| Property | Description | Type | Default |
| --- | --- | --- | --- |
| `[(ngModel)]` | Date value | `Date` | - |
| `[nzDisabled]` | Disabled state | `boolean` | `false` |
| `[nzFormat]` | Date format | `string` | `'yyyy/MM/dd'` |
| `[nzShowTime]` | Show time picker | `boolean \| SupportTimeOptions` | `false` |
| `[nzPlaceHolder]` | Placeholder text | `string` | - |

### NzRangePickerComponent

| Property | Description | Type | Default |
| --- | --- | --- | --- |
| `[(ngModel)]` | Date range value | `[Date, Date]` | - |
| `[nzDisabled]` | Disabled state | `boolean` | `false` |
| `[nzFormat]` | Date format | `string` | `'yyyy/MM/dd'` |
| `[nzShowTime]` | Show time picker | `boolean \| SupportTimeOptions` | `false` |

## 🤝 Contributing

We welcome contributions! Please see the main repository for contribution guidelines.

## 📄 License

MIT License - see the [LICENSE](LICENSE) file for details.
