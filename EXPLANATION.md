## Navbar Component

The Navbar component provides a navigation menu and search functionality for the application. Its functionalities includes:

#### **Navigation Links:**
>The Navbar displays navigation links to different pages. In this case, it includes links to the "Cats" page and the "Add Cat" page. These links allow users to easily navigate between these pages.

#### **Search Input:** 
>The Navbar includes a search input field that allows users to search for cats. When the user enters a search query, the input value is emitted to the parent component, triggering a search action.

## Index Page

The Index Page serves as the main page for displaying a list of cats. Its functionalities includes:

#### **Displaying Cats:** 
> The component retrieves a list of cats from an API and displays them in a responsive grid layout. Each cat is represented by a card containing information such as the cat's name, breed, and age. Clicking on a cat's image opens a detailed view of the cat.

#### **Infinite Loading:** 
> To provide a smooth scrolling experience, the component implements an infinite loading mechanism. As the user scrolls to the bottom of the page, additional cat data is loaded from the API and appended to the existing list of cats. This ensures that more cats are displayed as the user continues scrolling.

#### **Search Functionality:** 
>The component allows users to search for cats by entering a search query. When the search query is updated in the Navbar component, the IndexPage component receives the updated value and performs a search action. This triggers the retrieval of cats matching the search query from the API.

#### **Spinner**:
> While cats are being loaded or searched, a spinner component is displayed to indicate that the application is fetching data.

#### **Cat Detail Pop-up:** 
> Clicking on a cat's image opens a pop-up window that displays detailed information about the selected cat. This pop-up component provides a carousel for exploring cat images details.

## Add Cat Page

The Add Cat page is designed to enable users to add new cats to the application. Its features include:

#### **Form Validation:** 
> The Add Cat page includes a form for users to enter details about the new cat, such as its name, age, breed, and color. The form includes validation to ensure that all required fields are filled out before the cat can be saved.

#### **Image Upload:** 
> The form allows users to upload images of the cat. It supports multiple image uploads, in this case, two images. These images are sent to the API along with the cat details when the form is submitted.

#### **Error Handling:** 
> If there are any errors during the process of creating a new cat, such as network issues or validation errors, an error message is displayed to alert the user. This ensures that users receive feedback about the success or failure of their actions.
