# SwaggerEngine

Include [swagger-ui](https://github.com/swagger-api/swagger-ui) as rails engine.

## Swagger specifications

https://github.com/swagger-api/swagger-spec/blob/master/versions/2.0.md

## Install

Add to Gemfile

```gem 'swagger_engine'```

Add to your config/routes.rb

```mount SwaggerEngine::Engine, at: "/api-docs"```

### Protect your route

#### Devise

```
authenticate :user do
  mount SwaggerEngine::Engine, at: "/api-docs"
end
```

or

```
authenticate :user, lambda { |u| u.admin? } do
  mount SwaggerEngine::Engine, at: "/api-docs"
end
```

#### Basic http auth

Set username and password in `config/initializers/swagger_engine.rb`:

```
SwaggerEngine.configure do |config|
  config.admin_username = ENV['ADMIN_USERNAME']
  config.admin_password = ENV['ADMIN_PASSWORD']
end
```

## Configure

### Json files

Set the path of your json files in a initializer, you can specify relative paths
if your json files are dynamically served:

```
#config/initializers/swagger_engine.rb

SwaggerEngine.configure do |config|
  config.json_files = {
    default: "api/swagger.json",
    v1:      "lib/swagger/swagger_v1.json",
    v2:      "lib/swagger/swagger_v2.json"
  }
end
```
`lib/swagger/` is a good place to place them..

### Edit your json files

Use [Swagger editor](https://github.com/swagger-api/swagger-editor).

## Upgrade Swagger UI

- [Download](https://github.com/swagger-api/swagger-ui/releases) latest release source code.
- Fetch styles, images, js from `source_code/dist` and update files in `swagger_engine/app/assets`.
- Don't add style.css/style.scss file
- Change in styles `url` to `asset-url` and change path to images:
    `url('../images/throbber.gif')` -> `asset-url('throbber.gif')`
- Check if libs updated/added in  `source_code/dist/lib` compare with `swagger_engine/app/assets/javascripts/wagger_engine/lib` and update/add this libs require in `swagger_engine/app/assets/javascripts/wagger_engine/application.js`

## License

This project rocks and uses MIT-LICENSE.
