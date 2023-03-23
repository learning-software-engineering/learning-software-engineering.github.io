# Google Maps Javascript API

## Table of contents
### [Introduction](#introduction-1)
### [Requirements](#requirements-1)
### [Basic Google Map Integration](#basic-google-map-integration-1)
### [Embedding a Google Map on a React Website](#embedding-a-google-map-on-a-react-website-1)
### [Common Issues](#common-issues-1)

## Introduction

The following is a simple introduction to utilizing Google Maps Javascript API to embed custom maps on a website. This article assumes some basic knowledge of HTML, CSS, JavaScript, and Node.js


## Requirements

To use this API, the user should have Node.js installed and configured correctly. Additionally, users need to sign up for a Google Developer account, and set up their Google Maps Javascript API key, by adding a payment method to their account and following this guide. 

https://developers.google.com/maps/documentation/embed/get-api-key

In their project, users must make sure to load the Google API script correctly, by specifying their unique Google Map API Key or else their map will not load correctly. For example,

`src="https://maps.googleapis.com/maps/api/js?key=AIzaSyB41DRUbKWJHPxaFjMAwdrzWzbVKartNGg&callback=initMap&v=weekly"`

In this example, `AIzaSyB41DRUbKWJHPxaFjMAwdrzWzbVKartNGg` is the unique key id.


## Basic Google Map Integration

Google has an introductory guide on their developers website that details the process to integrate a simple Google Map with custom markers on a website.

https://developers.google.com/maps/documentation/javascript/adding-a-google-map#maps_add_map-javascript

Note that this guide DOES NOT work for a React website, users working in a react environment must follow the "Embedding a Google Map on a React Website" section.

Users must make sure to edit the `<script>` tag that loads the Google Map API to add their unique API key.


## Embedding a Google Map on a React Website

Embedding a Google Map on a React website is different as it requires importing a different package and following a different guide. The guide can be found here:

https://www.npmjs.com/package/@react-google-maps/api

A full documentation of the React Google Maps API package can be found here:

https://react-google-maps-api-docs.netlify.app

Users utilizing this package must make sure to run `npm install @react-google-maps/api` or add the package to their dependencies before running the website.

The individual compenents that the user wishes to use must also be included in the imports at the beginning of whichever files they are used in. A full list of the package components and their properties can be found in the "react-google-maps-api-docs" guide link of this section. For example, a user creating a custom map and adding markers to it would perform the following at the beginning of their JavaScript file:

`import { GoogleMap, Marker} from '@react-google-maps/api';`


## Common Issues

Here a few common issues that may arise when working with the Google Maps API and their likely solutions.

1. The package components are not being imported correctly<br />
    Ensure that you are importing the Google Maps API script correctly in your HTML file with your unique key, or running `npm install @react-google-maps/api` if you are working within a React project.
2. The package is loading, but the map is not displaying <br />
    Make sure you are dedicating a specific `<div>` to the map section and attaching it there.
3. The map only displays sometimes <br />
    Add `async` and `defer` to your script tag in your HTML file, as your API script may not be loading before your JavaScript files are run.
