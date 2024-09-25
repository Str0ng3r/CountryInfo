Nuxt Holiday Application -

This project is a holiday listing application built using Nuxt 3, Vue 3, and Axios. It displays public holidays for different countries and provides detailed holiday information for specific countries.

Table of Contents -
Features
Technologies Used
Installation
Running the Application
Building the Application
Application Structure

Features -
Fetches and displays a list of countries from the Nager.Date API.
Displays a filtered list of countries based on search input.
Selects random countries to display upcoming public holidays.
Provides detailed information for a specific country, including its region, country code, and public holidays.
Allows users to select a specific year to view holidays in that year.
Responsive design using SCSS for styling.

Technologies Used -
Nuxt 3: A Vue 3-based framework for building server-side rendered and static applications.
Vue 3: Progressive JavaScript framework for building user interfaces.
Axios: Promise-based HTTP client for making requests to the Nager.Date API.
Sass (SCSS): A CSS preprocessor that helps in writing modular and reusable styles.

Dependencies
The following dependencies are used in this project:

"dependencies": {
"axios": "^1.7.7",
"nuxt": "^3.13.0",
"nuxt-icons": "^3.2.1",
"vue": "latest",
"vue-router": "latest"
},
"devDependencies": {
"sass": "^1.79.3"
}

Installation -
npm install

Running the Application
To start the application in development mode, run the following command:
npm run dev
This will start the development server, and you can access the application by navigating to http://localhost:3000 in your browser.

Building the Application for Host and another
To build the application for production, use the following command:
npm run build
This command will create a production-ready version of the application in the .output directory.

Application Structure
Here's a high-level overview of the project's structure:

components/: Contains reusable Vue components like CountryCard.vue, RandomCountry.vue, and HolidayCard.vue for displaying country and holiday information.
pages/: Contains the main pages of the application:
index.vue: The homepage that displays a list of countries and random public holidays.
[countryCode].vue: A dynamic route page that displays detailed information about a country's public holidays.
assets/: Contains stylesheets, images, or other static assets.
app.vue: The root Vue component.
nuxt.config.ts: Nuxt configuration file where global settings are managed.
Key Files
index.vue (Homepage):
Displays a searchable list of countries and random long weekends for selected countries.
Allows filtering countries by name.
Fetches data using Axios from the Nager.Date API.
[countryCode].vue (Country-specific page):
Displays detailed holiday data for a specific country.
Allows switching between years to view holidays in a selected year.
API Endpoints Used
Available Countries: Fetches the list of available countries.
GET https://date.nager.at/api/v3/AvailableCountries
Next Public Holidays: Fetches the next public holidays for a country.
GET https://date.nager.at/api/v3/NextPublicHolidays/{countryCode}
Public Holidays by Year: Fetches public holidays for a country in a specific year.
GET https://date.nager.at/api/v3/PublicHolidays/{year}/{countryCode}
Country Information: Fetches additional information for a specific country.
GET https://date.nager.at/api/v3/CountryInfo/{countryCode}
SCSS Styling
The project uses SCSS for styling. SCSS files are located in the assets directory, and each component has scoped styles for modularity.

Additional Libraries/Frameworks
Nuxt Icons: A Nuxt module that provides access to a wide range of icons for easy integration in the UI.
