# BMML Filters

On top of Angular.js built-in filters, we have added some custom filters that you can use in your custom code.

To read about Angular.js built-in filters, please visit [Angular.js documentation](https://code.angularjs.org/1.8.0/docs/api/ng/filter/filter)

## Introduction

Filters are used to format the data in the view. They can be used in the following way:

```html
{{ expression | filter }}
```

Where `expression` is the data to be formatted and `filter` is the name of the filter.



## BMML Time
For a time string, this filter will format the time to the following format: `H:mm A`
By default the format is `H:mm a`, but you can specify a different format by passing it as a parameter to the filter.
For example:
```html
{{ '12:00:00' | bmmlTime }}
```
Or with a different format:
```html
{{ '12:00:00' | bmmlTime: 'HH:mm' }}
```

Read more about the [Format tokens](https://momentjs.com/docs/#/displaying/format/) for the format options.

## Hebrew Date
> Supported from **v3.1.305** and on.

Converts a date into a Hebrew (Jewish) calendar date string.
The input can be a `Date`, an ISO date string (e.g. `'2025-03-30'`) or a timestamp.
An invalid or empty input returns an empty string.

By default the day and year are rendered as Hebrew numerals (gematria), e.g. `א׳ ניסן תשפ״ה`:
```html
{{ '2025-03-30' | hebrewDate }}
```

You can pass an options object to control the output:
```html
{{ record.due_date | hebrewDate: { dayName: true } }}
```

### Options
- `dayName` (boolean) - prefix the Hebrew weekday name (e.g. `ראשון`). Default: `false`.
- `day` (boolean) - include the day of the month. Default: `true`.
- `month` (boolean) - include the month name. Default: `true`.
- `year` (boolean) - include the year. Default: `true`.
- `numerals` (boolean) - use Hebrew numerals (gematria). When `false`, arabic digits are used. Default: `true`.
- `separator` (string) - the token separator. Default: `' '` (a single space).

### Examples
```html
{{ '2025-03-30' | hebrewDate }}                       <!-- א׳ ניסן תשפ״ה -->
{{ '2025-03-30' | hebrewDate: { dayName: true } }}    <!-- ראשון א׳ ניסן תשפ״ה -->
{{ '2025-03-30' | hebrewDate: { numerals: false } }}  <!-- 1 ניסן 5785 -->
{{ '2025-03-30' | hebrewDate: { year: false } }}      <!-- א׳ ניסן -->
{{ '2025-03-30' | hebrewDate: { separator: '-' } }}   <!-- א׳-ניסן-תשפ״ה -->
```