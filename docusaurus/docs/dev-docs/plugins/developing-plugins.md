---
title: Developing plugins
# description: todo
displayed_sidebar: devDocsSidebar
pagination_prev: dev-docs/plugins
pagination_next: dev-docs/api/plugins/admin-panel-api
---

# Developing Strapi plugins

:::info
This section is about developing Strapi plugins to use them as local plugins or to submit them to the Marketplace. Not what you're looking for? Read the [plugins introduction](/dev-docs/plugins) and find your use case and recommended section to read from there.
:::

Strapi allows the development of plugins that work exactly like the built-in plugins or 3rd-party plugins available from the Marketplace. Once created, your plugin can be:

- used as a local plugin, working only with a specific Strapi project,
- or submitted to the [Marketplace](https://market.strapi.io) to be shared with the community.

The first step to developing a Strapi plugin is to create it using the CLI-based generator. Then you'll be able to leverage the [plugin APIs](#plugin-apis) to add features to your plugin.

## Plugin creation

Strapi provides a [command line interface (CLI)](/dev-docs/cli) for creating plugins. To create a plugin:

1. Navigate to the root of a Strapi project.
2. Run `yarn strapi generate` or `npm run strapi generate` in a terminal window to start the interactive CLI.
3. Choose "plugin" from the list, press Enter, and give the plugin a name in kebab-case (e.g. `my-plugin`)
4. Choose either `JavaScript` or `TypeScript` for the plugin language.
5. Create a plugins configuration file if one does not already exist: `./config/plugins.js` or `./config/plugins.ts` for TypeScript projects.
6. Enable the plugin by adding it to the [plugins configurations](/dev-docs/configurations/plugins) file:

<Tabs>
<TabItem value="js" label="JavaScript">

```js title="./config/plugins.js"
module.exports = {
  // ...
  "my-plugin": {
    enabled: true,
    resolve: "./src/plugins/my-plugin", // path to plugin folder
  },
  // ...
};
```

</TabItem>

<TabItem value="ts" label="TypeScript">

```js title=./config/plugins.ts
export default {
  // ...
  "my-plugin": {
    enabled: true,
    resolve: "./src/plugins/my-plugin", // path to plugin folder
  },
  // ...
};
```

</TabItem>
</Tabs>

7. Run `npm install` or `yarn` in the newly-created plugin directory.
8. (_TypeScript-specific_) Run `yarn build` or `npm run build` in the plugin directory. This step transpiles the TypeScript files and outputs the JavaScript files to a `dist` directory that is unique to the plugin.
9. Run `yarn build` or `npm run build` at the project root.
10. Run `yarn develop` or `npm run develop` at the project root.

Plugins created using the preceding directions are located in the `plugins` directory of the application (see [project structure](/dev-docs/project-structure)).

:::note
During plugin development it is helpful to use the `--watch-admin` flag to toggle hot reloading of the admin panel. See the [Admin panel customization](/dev-docs/admin-panel-customization) documentation for more details. (TypeScript specific) While developing your plugin, you can run `yarn develop --watch-admin` or `npm run develop -- --watch-admin` in the plugin directory to watch the changes to the TypeScript server files. From 4.15.1 this is no longer required.
:::

## Plugin APIs

Strapi provides the following programmatic APIs for plugins to hook into some of Strapi's features:

<CustomDocCardsWrapper>
<CustomDocCard emoji="" title="Server API" description="Use the Server API to have your plugin interact with the backend server of Strapi." link="/dev-docs/api/plugins/server-api" />
<CustomDocCard emoji="" title="Admin Panel API" description="Use the Admin Panel API to have your plugin interact with the admin panel of Strapi." link="/dev-docs/api/plugins/admin-panel-api" />
</CustomDocCardsWrapper>

:::strapi Custom fields plugins
Plugins can also be used to add [custom fields](/dev-docs/custom-fields) to Strapi.
:::
