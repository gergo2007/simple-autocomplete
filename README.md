# simple-autocomplete

A simple Vue autocomplete component using axios to get data from Laravel based API. 

## Installation

```js
npm i --save-dev simple-autocomplete
```

### Browser

Include the script file, then install the component with `Vue.use(SimpleAutocomplete);` e.g.:

```html
<script type="text/javascript" src="node_modules/vuejs/dist/vue.min.js"></script>
<script type="text/javascript" src="node_modules/simple-autocomplete/dist/simple-autocomplete.min.js"></script>
<script type="text/javascript">
  Vue.use(SimpleAutocomplete);
</script>
```

### Module

```js
import SimpleAutocomplete from 'simple-autocomplete';
```

## Usage

Once installed, it can be used in a template as simply as:

```html
<simple-autocomplete></simple-autocomplete>
```

Example:

```html
 <simple-autocomplete id="location" route={{route('api.locations.list')}} search_for="name" placeholder="Location" min-length="3" @selected-result="setLocationID"></simple-autocomplete>
```

ID: The autocomplete input's id

Route: API route to send the query to

Search For: The key to search for

Placeholder: Input's placeholder

Min Length: Input's minimum lenght to query

The component emits a selected-result event, containing the selected result (the full object).

Query example


```html

"query": {	
    "name": "London"
}

