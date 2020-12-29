# CHANGELOG try-gatsby-cloud

## purposes of this instance

Connect Gatsby and Drupal; get quick insights into the requirements and opportunities for other decoupled Drupal projects

## progress toward reaching stated purposes

[x] create an uncustomized gatsby site
  - try with instance on Gatsby Cloud per 

[x] create a Drupal instance per https://www.drupal.org/project/gatsby [note001]
  - try on a merge request for PASK 8.x
    [x] push modules with basic config
    [x] update PSH PHP

[ ] serve content from Drupal to Gatsby
  - start with JSON-API, which might be better supported
    [x] npm install gatsby-source-drupal

---

[note001] - Installation

  [x] Download and install the module as you would any other Drupal 8 module. Using composer is the preferred method.
  [x] Make sure to turn on the Gatsby Refresh endpoint by enabling the environment variable 'ENABLE_GATSBY_REFRESH_ENDPOINT' in your Gatsby environment file as documented in https://www.gatsbyjs.org/docs/environment-variables
  [x] It's easiest to test this by signing up for Gatsby cloud preview at https://www.gatsbyjs.com/. There is a free tier that will work for most development and small production sites. This is needed for incremental builds to work. You can also configure this to run against a local Gatsby development server. You need to make sure your Drupal site can communicate with your Gatsby development server over port 8000. Using a tool such as ngrok can be helpful for testing this locally.
  [ ] Install the gatsby-source-drupal plugin on your Gatsby site if using JSON:API
    or gatsby-source-graphql if you are using the Drupal GraphQL module. There are
    no additional configuration options needed for the plugin to work (besides
    enabling the __refresh endpoing as documented above). However, you
    can add the optional secret key (JSON:API only) to match your Drupal
    configuration's secret key.

    module.exports = {
      plugins: [
        {
          resolve: `gatsby-source-drupal`,
          options: {
            baseUrl: `...`,
            secret: `any-value-here`
          }
        }
      ]
    };

    Enable the Gatsby module. If you are using JSON:API it's recomended to
    enable the Gatsby JSON:API Instant Preview & Incremental Builds module for a faster preview experience and incremental builds support.
    Navigate to the configuration page for the Gatsby Drupal module.
    Copy the URL to your Gatsby preview server (either Gatsby cloud or a locally
    running instance). Once you have that, the Gatsby side is set up to receive
    updates.
    Add an optional secret key to match the configuration added to your
    gatsby-config.js file as documented above.
    Optionally add the callback webhook from Gatsby Cloud to trigger your
    incremental builds (JSON:API only). You can also check the box which will only
    trigger incremental builds when you publish content. You can also enter a
    build callback URL in this box (which can be used to trigger build services
    such as Netlify).
    If you are updating the Gatsby Drupal module and are still using an old
    version of gatsby-source-drupal, you can select to use the legacy callback.
    Note: this will eventually be removed and it's recommended to upgrade your
    gatsby-source-drupal plugin on your Gatsby site.
    Select the entity types that should be sent to the Gatsby Preview server.
    At minimum you typically will need to check `Content` but may need other entity
    types such as Files, Media, Paragraphs, etc.
    Save the configuration form.
    If you want to enable the Gatsby Preview button or Preview Iframe, go to the
    Content Type edit page and check the boxes for the features you would like to
    enable for that specific content type.
