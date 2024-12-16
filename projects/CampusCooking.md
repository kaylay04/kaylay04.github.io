---
layout: project
type: project
image: img/CampusCooking/CampusCookingLogo.jpg
title: "CampusCooking"
date: 2024
published: true
labels:
  - HTML
  - CSS
  - React
  - Typescript
  - Next.js
summary: "Campus Cooking is an application that helps campus students make affordable, healthy, and accessible meals. It provides students with recipes that respect common constraints such as limited kitchen resources, limited cooking skills, limited time, and limited access to grocery stores."
---
## Table of contents

* [Overview](#overview)
* [User Guide](#user-guide)
* [Milestones](#milestones)
* [Deployment](#deployment)
* [Community Feedback](#community-feedback)
* [Team](#team)

## Overview

Campus Cooking is an application that helps campus students make affordable, healthy, and accessible meals. It provides students with recipes that respect common constraints such as limited kitchen resources, limited cooking skills, limited time, and limited access to grocery stores.

### Key Features

* Recipes designed for basic kitchen setups, primarily using a toaster oven or microwave.
* Ingredients that are easy to find within walking distance of campus.
* Customizable filters for dietary preferences (e.g., vegan, gluten-free).
* Estimated cost and serving size for each recipe.
* Estimated preparation time for each recipe.

### Purpose

Many campus students resort to fast food or vending machine snacks due to limited resources, which impacts both their health and budget. Campus Cooking aims to improve student nutrition and support a healthier lifestyle by making cooking accessible and affordable.

## User Guide

This section provides an overview of Campus Cooking's main features and how students, vendors, and admins can interact with the system.

### Landing Page

The landing page introduces new users to Campus Cooking, with easy navigation to sign up or sign in.
This page will also include a place to browse recipes and posts via the grid view.

![](img/CampusCooking/landing-page-1.jpg)
![](img/CampusCooking/landing-page-2.jpg)
![](img/CampusCooking/landing-page-3.jpg)
![](img/CampusCooking/landing-page-4.jpg)


### Recipe Search and Filters

The recipe search page allows students to explore a variety of meals and snacks, with filters for dietary restrictions and ingredient availability. Each recipe page includes:
- Step-by-step instructions
- A list of ingredients, prices, and sources
- Dietary tags (e.g., vegan, gluten-free)
- Estimated preparation time and servings
User are also able to add their own recipes to the database via the add recipe page, which will be accessible only to logged in users, and the posts will be reviewed by admins when added to the database.
![](img/CampusCooking/add-recipe-page.jpg)
![](img/CampusCooking/search-recipe-page-1.jpg)
![](img/CampusCooking/search-recipe-page-2.jpg)

### Login Page 
Users can sign up or sign in to the application using their existing account, or create an account with their email and password.
![](img/CampusCooking/login-signup-page.jpg)

### Contact Us Page
Users can contact us as developers through the form, with suggestions for improvement, questions, or ideas for other appliances/filters the application could include.
![](img/CampusCooking/contact-us-page.jpg)

### About Us Page
Users can learn more about the developers and the purpose of the application.
![](img/CampusCooking/about-us-page.jpg)

### Admin Dashboard

Admins have additional privileges. They get an overview over every recipes and can monitor them by deleting not appropriate recipes or editing them. 
![](img/CampusCooking/admin_monitor_page.jpg)

![](img/CampusCooking/admin_delete_recipe.jpg)

![](img/CampusCooking/admin_edit_recipe.jpg)


### Github Organization

Here is a link to our GitHub [organization](https://github.com/Campus-Cooking) associated with this project and inside it, the repositories

## Milestones

### Milestone 1 

For Milestone 1, we delivered the initial version of our system be deploying it to [Vercel](https://campus-cooking.vercel.app/), creating a landing page with clear purpose, login area, and mockups for additional pages. We managed development using GitHub Issues and a "M1" project board, adhering to Issue Driven Project Management (IDPM) practices.

You can watch our Milestone 1 project board [here](https://github.com/orgs/Campus-Cooking/projects/1/views/6).



### Milestone 2

For Milestone 2, we will significantly enhance our system's functionality and quality by implementing at least four fully functional pages, including database integration for reading and writing data. We will gaian use GitHub Issues and a "M2" project board. 

You can watch our Milestone 2 project board [here](https://github.com/orgs/Campus-Cooking/projects/5/views/6).

For Milestone 2 we have implemented these pages in our system:
* Home Page
* Log in and Sign up Page
* View Recipe Page
* Add Recipe Page (only accessible for logged in users)
* Contact Page


### Milestone 3 

The purpose of Milestone 3 is to polish the codebase, address any remaining UI issues, and ensure a smooth user experience. This final pass involved debugging, enhancing styling, and improving overall functionality.

You can watch our Milestone 3 project board [here](https://github.com/orgs/Campus-Cooking/projects/8).

# Developer Guide

## Overview

This Developer Guide provides instructions for developers to set up, run, and modify the Campus Cooking application. Follow these steps to clone the repository, configure dependencies, and customize the system as needed.

## Prerequisites

Before setting up the project, ensure you have the following installed on your system:

- **Node.js** (version 16 or above)
- **npm** (Node Package Manager, bundled with Node.js)
- **Git** (for version control)
- **Vercel CLI** (optional, for deployment)

## Setup Instructions

### 1. Clone the Repository

1. Open your terminal or command prompt.
2. Run the following command to clone the repository:

   ```
   git clone https://github.com/Campus-Cooking/campus-cooking.git
    ```
   
### 2. Install dependencies
1. Open your terminal or command prompt.
2. Run the following command to clone the repository:

   ```
   npm install
   ```

### 3. Start the development server:

   ```
   npm run dev
   ```
 
This will launch the application at http://localhost:3000.

### GitHub Hosting Guidlines
We are committed to adhering to GitHub's hosting guidelines by ensuring our repository complies with all terms of service and community standards. This includes using GitHub responsibly to store and share code, respecting intellectual property rights, maintaining appropriate content, and avoiding prohibited uses such as illegal, malicious, or harmful activities. By following these guidelines, we aim to foster a safe, collaborative, and professional environment for our project and the broader GitHub community.

## Deployment
Our system has been deployed on Vercel, you can access it by clicking [here](https://campus-cooking.vercel.app/).

The app in production is successfully writing to database when signing up and adding recipes. It is successfully reading from database when logging in users.

## Community Feedback

Users appreciate the clean, modern design and student-friendly approach, highlighting the focus on simple recipes that use basic kitchen appliances like microwaves and toaster ovens. Features like dietary filters, estimated costs, serving sizes, and step-by-step instructions make cooking approachable and affordable for students with limited time and resources.

Users would like to see new features added in the future, like a "quick meals" or "5-ingredient recipes" section, difficulty ratings, nutritional information, and a way to save or favorite recipes. Adding community-driven elements like comments, reviews, and ratings could enhance engagement, while streamlined recipe submission and consistency in page layouts would improve usability.

Overall, the feedback suggests that the site effectively solves a major problem for students by making cooking accessible and affordable. While there’s room for added functionality and community-building features, the core concept resonates well, making it a valuable resource for those new to cooking.

## Team

Campus Cooking is designed, created and built by [Anaya Cole](https://anayaemily.github.io/), [Lindsey Clement](https://lindseynclement.github.io/), [Christina Holthe](https://chrshol.github.io/) and [Kayla Young](https://kaylay04.github.io/). 

#### Team Contract
You can watch our team contract [here](https://docs.google.com/document/d/1IeZ3gzcvCw6sXPzIBjEe9HSV4btgJgGbPfj0qyVp7VA/edit?tab=t.0#heading=h.ahjfca2rpk54).




