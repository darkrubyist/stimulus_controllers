# Copy Controller

Copies text from `input` and `textarea` elements to the clipboard.

## Quick Start

#### `app/javascript/controllers/index.js`

```js
import { Application } from 'stimulus'
import { definitionsFromContext } from 'stimulus/webpack-helpers'
import CopyController from '@hopsoft/copy-controller'

const application = Application.start()
const context = require.context('./controllers', true, /\.js$/)
application.load(definitionsFromContext(context))
application.register('copy', CopyController)
```

#### `app/views/demos/copy.html.erb`

```html
<div data-controller="copy" data-copied-content='Copied...' data-copied-duration='2'>
  <textarea data-target='copy.source'></textarea>
  <button type="button" data-target='copy.button' data-action='click->copy#copy'>Copy</button>
</div>
```

## Usage

The root element is a container that holds holds all other elements and is configured by setting

```
data-controller="copy"
```

### Configuration

| Attribute              |          | Default   | Description                                                                                        |
| ---------------------  | -------- | --------- | -------------------------------------------------------------------------------------------------- |
| `data-copied-content`  | optional | Copied... | Content to show in the button after a copy has been performed                                      |
| `data-copied-duration` | optional | 2         | How many seconds to show the copied content in the button before reverting to the original content |

Copied content can be disabled by setting `data-copied-content=""` or `data-copied-duration="0"`

### Targets

Targets are child elements identified by setting

```
data-target="copy.TARGET_NAME"
```

| Name     |          | Description                                              |
| -------- | -------- | -------------------------------------------------------- |
| `source` | required | An input or textarea that holds the content to be copied |
| `button` | required | The button used to perform the copy                      |

### Actions

Actions are behaviors that can be triggered and are identified by setting

```
data-action="copy#ACTION_NAME"
```

| Name     |          | Description                                                         |
| -------- | -------- | ------------------------------------------------------------------- |
| `copy`   | required | Performs the copy action (typically defined on the `button` target) |
