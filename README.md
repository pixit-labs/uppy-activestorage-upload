# uppy-activestorage-upload

<img src="https://uppy.io/images/logos/uppy-dog-head-arrow.svg" width="120" alt="Uppy logo: a superman puppy in a pink suit" align="right">

The ActiveStorage Upload plugin handles Ruby on Rails ActiveStorage direct uploads with Uppy.

## Example
Let's suppose we have a user model with a has_one_attached :image

```ruby
class User < ApplicationRecord
  has_one_attached :image
end
```

We have to insert somewhere a form that defines an input for the user resource with a file_field input for the image, with data attribute direct_upload: true
With this data_attribute defined, activestorage will automagically generate an input with some data attributes(data-direct-upload-url,  data-direct-upload-token, data-direct-upload-attachment-name)
```erb
<%- simple_form_for User.new do %>
  <%= f.file_field :image, as: :hidden, data: { direct_upload: true} %
<%- end %>
```

Then use `ActiveStorageUpload` as an Uppy plugin in your Javascript pack and pass this file input as an option.
The plugin will use this input and its data attributes in order to make an authenticated DirectUpload.
More information about it Rails 7.0 breaking changes with DirectUpload api [here](https://edgeguides.rubyonrails.org/active_storage_overview.html#integrating-with-libraries-or-frameworks)

```js
const Uppy = require('@uppy/core')
const ActiveStorageUpload = require('uppy-activestorage-upload')

const uppy = new Uppy()
uppy.use(ActiveStorageUpload, {
  activestorageInput: document.querySelector("input[name='user[image]']")
})
```

## Installation

```bash
yarn add @rails/activestorage
yarn add https://github.com/pixit-labs/uppy-activestorage-upload
or
npm install @rails/activestorage
npm install https://github.com/pixit-labs/uppy-activestorage-upload --save
```

We recommend installing from npm and then using a module bundler such as [Webpack](http://webpack.github.io/), [Browserify](http://browserify.org/) or [Rollup.js](http://rollupjs.org/).

## License

[The MIT License](./LICENSE).
