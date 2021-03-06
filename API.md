If you don't know how to define types with tcomb you may want to take a look at its [README](https://github.com/gcanti/tcomb/blob/master/README.md) file.

# createForm

```js
createForm(type, [opts])
```

Returns a React.js component handling the form fields defined by the `type` struct.

- `type`: a `struct` or a `subtype` of a `struct`
- `opts`: a hash containing directives on how you want render the form

Example

```js
var Person = struct({
  name: Str,
  surname: Str
});

var Form = createForm(Person);
```

## getValue()

Returns an instance of `type` if the validation succeded, `null` otherwise.

## opts.value: maybe(Obj)

A hash containing the default values of the form fields.

Example

```js
var Person = struct({
  name: Str,
  surname: Str
});

var Form = createForm(Person, {
  value: {
    name: 'Giulio',
    surname: 'Canti'
  }
});
```

## opts.label: Any

Adds a label above the form.

Example

```js
var Person = struct({
  name: Str,
  surname: Str
});

var Form = createForm(Person, {
  label: 'Insert your data'
});
```

## opts.auto

One of `placeholders` (default), `labels`, `none`. Adds automatically generated placeholders or labels
to the form. Set `auto` to `none` if you don't want neither.

Example

```js
var Person = struct({
  name: Str,
  surname: Str
});

var Form = createForm(Person, {
  auto: 'labels'
});
```

## opts.order: maybe(list(Str))

Renders the form fields in the specified order

Example

```js
var Person = struct({
  name: Str,
  surname: Str
});

var Form = createForm(Person, {
  order: ['surname', 'name'] // `surname` field first, then `name` field
});
```

## opts.fields: maybe(Obj)

A hash containing the options for every fields. See the section `opts` of the inputs types
for details.

```js
var Person = struct({
  name: Str,
  surname: Str
});

var Form = createForm(Person, {
  fields: {
    name: { label: 'Your name' },       // override default placeholder / label
    surname: { label: 'Your surname' }  // override default placeholder / label
  }
});
```

# createList

```js
createList(type, [opts])
```

Returns a React.js component handling the items defined by the `type` list.

- `type`: a `list` or a `subtype` of a `list`
- `opts`: a hash containing directives on how you want render the list

Example

```js
var Tags = list(Str);

var Form = createList(Tags);
```

## getValue()

Returns an instance of `type` if the validation succeded, `null` otherwise.

## opts.value: maybe(Arr)

A hash containing the default values of the form fields.

Example

```js
var Tags = list(Str);

var Form = createList(Tags, {
  value: ['domain', 'driven', 'forms']
});
```

## opts.label: Any

Adds a label above the form.

Example

```js
var Tags = list(Str);

var Form = createList(Tags, {
  label: 'Insert your tags'
});
```

## opts.disableAdd: maybe(Bool)

If set to `true` removes the possibility to add an item to the list.

## opts.disableRemove: maybe(Bool)

If set to `true` removes the possibility to remove the items from the list.

## opts.disableOrder: maybe(Bool)

If set to `true` removes the possibility to sort the items in the list.

## opts.item: maybe(Obj)

A hash containing the options for every item in the list. See the section `opts` of the inputs types
for details.

```js
var Colors = list(Str);

var Form = createList(Colors, {
  item: {
    type: 'color' // use HTML5 color textbox
  }
});
```

# textbox

```js
textbox(type, [opts])
```

- `type`: every type that it makes sense to render in a textbox / textarea
- `opts`: a hash containing directives on how you want render the textbox / textarea

## opts.type: maybe(Str)

One of

- `text`
- `textarea`
- `password`
- `color`
- `date`
- `datetime`
- `datetime-local`
- `email`
- `month`
- `number`
- `range`
- `search`,
- `tel`
- `time`
- `url`
- `week`

## opts.value: Any

The default value of the textbox / textarea.

## opts.label: Any

Adds a label above the textbox / textarea.

## opts.help: Any

Adds a label below the textbox / textarea.

## opts.groupClasses: maybe(Obj)

Customize the `className` of the containing `div`.

## opts.placeholder: maybe(Str)

Overrrides the default placeholder.

## opts.i17n: maybe(I17n)

i17n support

Example

```js
var Person = struct({
  name: Str,
  age: Num // a number property
});

var Form = createForm(Person, {
  fields: {
    age: {
      i17n: {
        // this is used from the model to the UI
        format: function (value) {
          return value;
        },
        // this is used from the UI to the model
        parse: function (s) {
          return parseFloat(s, 10);
        }
      }
    }
  }
});
```

# select

```js
textbox(type, [opts])
```

- `type`: an `enums` or a `subtype` of an `enums`
- `opts`: a hash containing directives on how you want render the select

## opts.value: maybe(type)

The default value of the select.

## opts.label: Any

Adds a label above the select.

## opts.help: Any 

Adds a label below the select.

## opts.groupClasses: maybe(Obj)

Customize the `className` of the containing `div`.

## opts.emptyOption: maybe(Option)

Adds a first option to the select representing a "no choice".
Overrides the default one.

Example

```js
var Country = enums({ IT: 'Italy', US: 'United States' });

var Person = struct({
  name: Str,
  country: Country
});

var Form = createForm(Person, {
  fields: {
    country: {
      emptyOption: {value: '', text: '-'}
    }
  }
});
```

## opts.order: maybe(Order)

Sorts the options `asc` or `desc`.

# radio

```js
textbox(type, [opts])
```

- `type`: an `enums` or a `subtype` of an `enums`
- `opts`: a hash containing directives on how you want render the radio

## opts.value: Any

The default value of the radio.

## opts.label: Any

Adds a label above the radio.

## opts.help: Any

Adds a label below the radio.

## opts.groupClasses: maybe(Obj)

Customize the `className` of the containing `div`.

## opts.order: maybe(Order)

# checkbox

```js
checkbox(type, [opts])
```

- `type`: a `Bool` or a `subtype` of a `Bool`
- `opts`: a hash containing directives on how you want render the checkbox

## opts.value: maybe(type)

The default value of the checkbox.

## opts.label: Any

Adds a label above the checkbox.

## opts.help: Any

Adds a label below the checkbox.

## opts.groupClasses: maybe(Obj)

Customize the `className` of the containing `div`.

