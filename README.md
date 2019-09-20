Restricted Input
================

Allow restricted character sets in `input` elements.

## Demo

Try the latest version of Restricted Input [here](https://braintree.github.io/restricted-input/).

## Features

- Disallow arbitrary characters based on patterns
- Maintains caret position
- Format/Update on paste
- Works in IE11+

## Development

**Install dependencies**

```bash
nvm use # if you have node version manager installed
npm i
```

**Watch files and run demo server**

```bash
npm run development
```

This will start a server on port `3099` which can be overridden with the `PORT` env var.

**Unit tests**

The following command will run the linting task and the unit tests.

```sh
npm test
```

**Integration tests**

First, [sign up for a free open source Browserstack account](https://www.browserstack.com/open-source?ref=pricing).

Copy the `.env.example` file to `.env`

```sh
cp .env.example .env
```

Fill in the SAUCE_USERNAME and SAUCE_ACCESS_KEY environmental variables with your credentials:

```sh
BROWSERSTACK_USERNAME=username
BROWSERSTACK_ACCESS_KEY=access_key
```

To run the integration tests in Safari, Google Chrome, Firefox, IE11 and Microsoft Edge:

```sh
npm run development # in another terminal window
npm run test:integration
```

To run tests in only one browser, prefix the test command with an `ONLY_BROWSER` env variable:

```sh
# run only in edge browser
ONLY_BROWSER=edge npm run test:integration

# run only in chrome browser
ONLY_BROWSER=chrome npm run test:integration

# run only in ie 11 browser
ONLY_BROWSER=ie npm run test:integration

# run only in safari browser
ONLY_BROWSER=safari npm run test:integration

# run only in firefox browser
ONLY_BROWSER=firefox npm run test:integration
```


To run only certain tests, add the `.only` property before running the test:

```js
it.only('does something', function () {
```

## Usage

```javascript
import RestrictedInput from 'restricted-input';

const formattedCreditCardInput = new RestrictedInput({
  element: document.querySelector('#credit-card'),
  pattern: '{{9999}} {{9999}} {{9999}} {{9999}}'
});
```

## Patterns

Patterns are a mixture of [`Placeholder`](#placeholder)s and [`PermaChar`](#permachar)s.

### Placeholder

A `Placeholder` is the part of the pattern that accepts user input based on some restrictions. A placeholder is defined in the pattern using two open curly brackets, the placeholder, followed by two closing curly brackets e.g. `{{Abc123}}`.

The patterns a `Placeholder` can be are:
 - a single alpha character that matches the alpha regex `/[A-Za-z]/`. e.g. `{{C}}` will match one alpha character.
 - a single digit that matches the digit regex `/[0-9]/`. e.g. `{{3}}` will match one digit.
 - a `*` character that matches `/./`. e.g. `{{*}}` will match the next character.

### PermaChar

A `PermaChar` is the part of the pattern that is automatically inserted. `PermaChar`s are defined in the pattern as any characters other than `Placeholder`s.

### Example patterns

Some example patterns with behavior are listed:
 - `12{{3}}`
   - Inserts `12`.
   - Waits for a single digit from the user.
 - `{{A}}BC`
   - Waits for a single alpha from the user.
   - Inserts `BC`.
 - `${{*2L}}E`
   - Inserts `$`.
   - Waits for any single character input from the user.
   - Waits for a single digit from the user.
   - Waits for a single alpha from the user.
   - Inserts `E`.

## API

### options

| Key | Type | Description |
| --- | ---- | ----------- |
| element | `HTMLInputElement` or `HTMLTextAreaElement` | A valid reference to an `input` or `textarea` DOM node |
| pattern | `String` | Pattern describing the allowed character set you wish for entry into corresponding field. See [Patterns](#patterns).|

## Browser Support

**Desktop**

- Chrome (latest)
- Firefox (17+)
- Safari (8+)
- IE11 (desktop/metro)
- IE10 (desktop/metro)
- IE9

## Browsers Where Formatting is Turned Off Automatically

Old versions of Samsung Android browsers are incompatible with formatting. These will not attempt to intercept the values and format the input.

## TODO

- [ ] Improve jsdoc
- [ ] Add example guides/pages
