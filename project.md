# Project goals

The primary goal for this project is to complete development of a web site that will be used by participants in a Duke of Edinburgh project.  The DofE project will involve the creation of pages by DofE students that describe various locations associated with Kent and the display of "then and now" images for each location.  The "then" images have been obtained from digitized historical postcards.

A basic infrastructure for the site has been created using a beta version of the [Juncture](https://juncture-digital.org/) framework, currently under development by JSTOR Labs.  Juncture is a generalization of the code base used for the [Kent Maps Online](https://kent-maps.online/) and [Plant Humanities Lab](https://lab.plant-humanities.org/) web sites.

Using Juncture, all site content is developed using simple text files annotated with [Markdown](https://www.markdownguide.org/) (for text formatting) and simple HTML tags for augmenting the text with visualizations that are displayed when the page is rendered by Juncture.

The development work to be performed for the project is defined in the following sections.

## Completion of a site home page

The site home page will provide text describing the project and site and visual components that link to the "then and now" pages from a tile grid or map.  The user will be able to toggle between the tile and map views.  All content for the home page is defined in the top-level site `README.md` markdown file.

The tile (or card) and map viewer components are minimally working but require refinement and additional functionality, including:

1. Replacing the simple pin markers on the map with thumbnail images for the location and an info box that is displayed on hover.
2. Refining the tile grid.  This includes refining the display of the individual tiles/cards as well as making the grid more responsive to different display resolutions.

## Completion of the Then and Now page

Each Then and Now location included in the site will have a separate page that includes some basic textual inforamtion about the location and an image viewer that displays the current and historical images enabling interactive comparison.  Each of the location pages are defined in separate markdown files that contain the description text and the URLs and metadata for the images used.

# Implementation background, links, and notes

- The site infrastructure uses the Juncture framework being developed by JSTOR Labs.  Documentation for Juncture can be found at https://juncture-digital.org/docs/.
- Juncture is based on two key technologies and services.  [Github](https://github.com/) is used for content management and site hosting.  The site is implemented as a Single Page Application (SPA) using the [Vue.js](https://vuejs.org/) javascript framework.
- The Then and Now image viewer uses the code from the Github repo at https://cuberis.github.io/openseadragon-curtain-sync/.  This is an extension for the OpenSeadragon IIIF viewer used by Juncture.
- The map on the home page uses the open source [Leaflet](https://leafletjs.com/) library.  A number of [Leaflet plugins](https://leafletjs.com/plugins.html) have been developed for the core library and are generally easy to add/use with the core library.
- The Juncture framework was designed for extensibility.  Extensions to the Juncture core functionality are implemented in components that are added to the `/components` folder located at the project root.  Each component is implemented as a standard Vue [Single File Component](https://vuejs.org/v2/guide/single-file-components.html) that is dynamically loaded when the app/site is launched.  Code bundling using Webpack or other module bundlers is not used, simplifying development and deployment of code extensions and updates.

## Local development and testing

While it is technically possible to develop Juncture extensions only using the Github text editor a local development environment is typically needed for any non-trivial development work.  The `README.md` file in the ['/utils/dev-server'](/dofe/utils/dev-server) folder provides basic instructions for setting up and using a simple server that can be used for local development and testing.
