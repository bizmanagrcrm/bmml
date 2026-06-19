# `<bmml-heb-datepicker>`
> Supported from **v3.1.305** and on.

This element renders a Hebrew (Jewish) calendar datepicker. It behaves like a native date input: clicking a day selects it immediately. It binds through `ng-model`, which holds the selected date as a JavaScript `Date` (like a native date input's `valueAsDate`), while the read-only input displays the date in Hebrew.

example:
```<bmml-heb-datepicker ng-model="$data.due_date"></bmml-heb-datepicker>```

- `ng-model` - the model that holds the selected date as a `Date` object (required).
- `settings` - an optional configuration object. Supported keys:
    - `israel` (boolean) - use the Israel holiday schedule (single festival day). When `false`, the Diaspora schedule is used. Default: `true`.
    - `requireApply` (boolean) - when `true`, a day click only highlights the day and the user must press the OK button to confirm. When `false` (default), a day click selects immediately, like a native date picker.
    - `showWeekday` (boolean) - include the Hebrew weekday name in the input text (when the picker is closed), e.g. `ראשון א ניסן תשפה` instead of `א ניסן תשפה`. Default: `false`.
    - `hideHeader` (boolean) - hide the picker header that shows the selected date. Default: `false`.
    - `gershayim` (boolean) - show geresh/gershayim punctuation on the Hebrew day and year, e.g. `י״א` / `תשפ״ה` instead of `יא` / `תשפה`. Default: `false`.
    - `lang` (string) - language of the footer buttons (Today / Clear / OK): `'en'` (default) or `'he'` for Hebrew (היום / נקה / אישור).
    - `labels` (object) - override individual button labels, e.g. `{ today: 'Today', clear: 'Clear', apply: 'Save' }`. Takes precedence over `lang`. (The `apply` label only appears when `requireApply` is set.)
    - `color` (string) - an accent color (CSS color) applied to the picker via the `--main-color` CSS variable.
    - `initDate` (Date | string) - an initial date to seed the picker with when the model is empty.
    - `noStyles` (boolean) - skip the built-in stylesheet entirely so you style the picker yourself. Default: `false`.

example with settings:
```<bmml-heb-datepicker ng-model="$data.due_date" settings="{ israel: false, showWeekday: true, color: '#3b82f6' }"></bmml-heb-datepicker>```

## Styling / overriding
The element comes with a minimal built-in style so it renders like a native calendar out of the box. It is designed to be easy to override, in increasing order of power:

1. **Recolor / resize with CSS variables** - every color and size is a `--he-dp-*` token, so you can re-theme without fighting specificity. Set them on the element (or any ancestor):
    ```css
    bmml-heb-datepicker {
      --he-dp-accent: #16a34a;   /* selected day / today / primary button */
      --he-dp-radius: 10px;
      --he-dp-day-size: 36px;
      --he-dp-width: 300px;
    }
    ```
    Available tokens: `--he-dp-accent`, `--he-dp-on-accent`, `--he-dp-bg`, `--he-dp-text`, `--he-dp-subtle`, `--he-dp-muted`, `--he-dp-border`, `--he-dp-control-border`, `--he-dp-hover`, `--he-dp-radius`, `--he-dp-popup-radius`, `--he-dp-day-size`, `--he-dp-width`, `--he-dp-z`, `--he-dp-shadow`. (The `color` setting is a shortcut for `--he-dp-accent`.)

2. **Override the classes** - the root carries the `he-dp` class and every part has a stable class: `he-dp__input`, `he-dp__popup`, `he-dp__title`, `he-dp__nav`, `he-dp__navbtn`, `he-dp__select`, `he-dp__weekday`, `he-dp__day` (with the modifiers `he-dp__day--today`, `he-dp__day--selected`, `he-dp__day--holiday`, `he-dp__day--empty`), `he-dp__footer`, `he-dp__btn` / `he-dp__btn--primary`. The defaults are single-class selectors injected at the top of `<head>`, so your own stylesheet wins. You can also add a class on the element (e.g. `<bmml-heb-datepicker class="my-dp">`) to scope your rules.

3. **Opt out completely** - pass `settings="{ noStyles: true }"` to skip the built-in stylesheet and style the `he-dp__*` classes from scratch.

The companion [`hebrewDate` filter](../filters/README.md) can be used to display the selected date elsewhere, for example: `{{ $data.due_date | hebrewDate }}`.
