# ember-cli-honeybadger-io [![CircleCI](https://circleci.com/gh/Fatsoma/ember-cli-honeybadger-io.svg?style=svg)](https://circleci.com/gh/Fatsoma/ember-cli-honeybadger-io)

Javascript error tracking with <https://www.honeybadger.io>

honeybadger.js docs <https://github.com/honeybadger-io/honeybadger-js>

Install the addon:

```sh
ember install ember-cli-honeybadger-io
```

## Configuration

For more options see honeybadger.js docs.

`config/environment.js`

```js
ENV.honeybadger = {
  apiKey: 'project api key'
}
```

```sh
ember g instance-initializer honeybadger
```

`instance-initializers/honeybadger.js`

```js
import Ember from 'ember';

const { RSVP, set } = Ember;

export function initialize(appInstance) {
  let service = appInstance.lookup('service:honeybadger');

  Ember.onerror = function(error) {
    service.notify(error);
  };

  RSVP.on('error', function(error) {
    service.notify(error);
  });

  // optional extras/ideas
  /* let session = appInstance.lookup('service:session');

  set(service, 'beforeNotify', (notice) => {
    notice.context = {
      userId: session.userId
    };

    notice.cookies = document.cookies
  }); */
}

export default {
  name: 'honeybadger',
  initialize
};

```

## Notes

honeybadger.js is lazy loaded via `service.notify`.

Addon by [Fatsoma](http://www.fatsoma.com)
