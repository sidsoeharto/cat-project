# Cat Project Documentation

This documentation provides an overview of the Cat Project, including its features, components, and usage instructions.

## Build Setup

```bash
# install dependencies
$ yarn install

# serve with hot reload at localhost:3000
$ yarn dev

# build for production and launch server
$ yarn build
$ yarn start
```

## Table of Contents

1. [Introduction](#introduction)
2. [Features](#features)
3. [Components](#components)
   - [Navbar](#navbar)
   - [IndexPage](#indexpage)
   - [CreateCatPage](#createcatpage)
   - [InputField](#inputfield)
   - [InputFile](#inputfile)
4. [Installation](#installation)
5. [Usage](#usage)
6. [Contributing](#contributing)
7. [License](#license)

## Introduction

The Cat Project is a web application that allows users to manage cat data. It provides features for viewing a list of cats, searching for cats by their name and breed, creating new cat data, and displaying detailed information about individual cats.

## Features

- View a list of cats with their basic details
- Search for cats by name and breed
- Create new cat data with name, age, breed, color, and images
- Validate form inputs
- Implement infinite scrolling for loading more cat data

## Components

### Navbar

The `Navbar` provides links to navigate between the Cats page and the Add Cat page. It also includes a search input field to search for cats.

Props:

- `searhQuery` (String): The value of the search field.
- `showSearch` (Boolean, default: `true`): Determines whether to show the search input field.

### IndexPage

The `IndexPage` component displays a grid of cat cards, showing their images, names, breeds, and ages. It fetches cat data from an API and supports infinite scrolling to load more cats as the user scrolls down. Clicking on a cat card opens a popup with detailed information about the cat.

Props:

- None

### CreateCatPage

The `CreateCatPage` component provides a form for creating new cat data. It includes input fields for name, age, breed, color, and images. It validates the form inputs and displays error messages if any fields are missing or if the images exceed the maximum file size.

Props:

- None

### InputField

The `InputField` component is a reusable input field component that displays a label and an input element. It supports validation and displays error messages for required fields.

Props:

- `name` (String, required): The name attribute of the input field.
- `label` (String, required): The label to display for the input field.
- `value` (Any, required): The value of the input field.
- `submitted` (Boolean, default: `false`): Indicates whether the form containing the input field has been submitted.
- `requiredMessage` (String, default: "This field is required"): The error message to display if the field is required.
- `type` (String, default: "text"): The type of the input field.
- `isRequired` (Boolean, default: `false`): Determines whether the field is required for validation.

### InputFile

The `InputFile` component is a specialized version of the `InputField` component specifically for file inputs. It handles file selection and displays error messages if the file is required or exceeds the maximum file size.

Props:

- `name` (String, required): The name attribute of the input file field.
- `label` (String, required): The label to display for the input file field.
- `value` (Any, required): The value of the input file field.
- `submitted` (Boolean, default: `false`): Indicates whether the form containing the input file field has been submitted.
- `requiredMessage` (String, default: "This field is required"): The error message to display if the field is required.
- `index` (Number, required): The index of the input file field (used for error messages).
- `isRequired` (Boolean, default: `false`): Determines whether the field is required for validation.

## Installation

To install and run the Cat Project locally, follow these steps:

1. Clone the repository: `git clone https://github.com/sidsoeharto/cat-project.git`
2. Navigate to the project directory: `cd cat-project`
3. Install the dependencies: `yarn install`
4. Start the development server: `yarn dev`
5. Access the application at `http://localhost:3000`

## Usage

The Cat Project provides a user-friendly interface for managing cat data. Here are the main steps to use the application:

1. View the List of Cats:
   - Open the application in your web browser.
   - The home page will display a list of cats with their basic details.
   - Use the search bar to search for cats by name and breed.

2. Create a New Cat:
   - Click on the "Add Cat" link in the navigation bar.
   - Fill out the form with the cat's name, age, breed, color, and upload two images.
   - Submit the form to create the new cat.
   - If the form validation fails, error messages will be displayed indicating the required fields and any other validation errors.

3. View Cat Details:
   - Click on a cat card from the list to view detailed information about the cat.
   - A popup will display the cat's images, name, breed, and age.

