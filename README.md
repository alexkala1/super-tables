# SUPER TABLES

This is a PoC (Proof-of-Concept) app that will showcase the features of a Datatable. The app serves the purpose of evaluating the skills of Web Developers and their competency with specific tools and technologies.

_Note about the Datatable:_ The core component of this PoC is the Datatable. You are free to use either a publicly available Datatable component or build one on your own. 🤔

## Toolbox

The PoC project should be developed using the following tools:

1. Nuxt 3 (already set up with a git repo)
2. Vue 3 with [Script Setup](https://vuejs.org/api/sfc-script-setup.html#basic-syntax) syntax
3. Typescript
4. [TailwindCSS](https://tailwindcss.com/) framework

## Routes

1. **Home page** - main app page with Menu and other Lorem Ipsum (fictional) content
2. **List View page** - page with Datatable
3. **Item View page** - page with item details, this is where users land when clicking on a row

## Must-Have Datatable Features

1. **Sorting** - Rows get sorted based on the column header that was clicked.
2. **Paging** - User can navigate back and forward between pages.
3. **Expanding row** - Clicking on a chevron-down icon at the left edge of a row, reveals a section for extra row information. The section collapses if the icon is clicked again.
4. **Navigating to item** - When users click on a row, they will be navigated to the Item View page.

## Nice-to-Have Datatable Features

1. **Smart back to list** - When users are in List View page and click on a row, they navigate to the Item Page. There, by clicking the browser's back button, they should return to the same List View page they started from, and the app should briefly highlight the table row that was clicked initially. Hence, if the List View has many rows users will know which one they clicked last. 😊

## Must-Have Scoring Factors

1. **Excellency in responsiveness** - the app should be functional and well rendered in all screen sizes.
2. **Excellency in UX** - you are asked to apply element positioning and English texts that help the users learn quickly the app functions and enjoy using them.
3. **Excellency in coding** - you are asked to deliver Vue components written with Typescript code that is well-formatted, bug free, performs efficiently and has no tslint errors or warnings.

## Nice-to-Have Scoring Factors

1. **Design coolness** - making the app look nice with icons, animations, page transitions and other cool-looking features will give you extra credit.
2. **Nuxt 3 competencies** - the more Nuxt features you can demonstrate the more credit you get.

## Acquiring the sample the Data

The data required to implement the PoC should be acquired using the Nuxt's [data fetching](https://nuxt.com/docs/getting-started/data-fetching) APIs.

However, their form and origination is up to you. For example, you could tap in to an online public dataset or create and serve the data via [Nuxt's server directory](https://nuxt.com/docs/guide/directory-structure/server).

## Handing in your assignment

After receiving your assignment you will have 3 days to complete it. To hand in your assignment you are expected to:

1. commit all your files into git
2. fill in the Completion form in Appendix 1
3. delete the `node_modules` and `.nuxt` directories
4. zip the project folder as `super-tables.zip`
5. email the `super-tables.zip` back to us

We will unzip the project folder and run `yarn` to install it and then `yarn dev` to run it.

## Appendix 1: Completion form

You are expected to **score yourself** by filling in the following form. You should score each feature separately using a 5 scale score, with 0 being `"I have not implemented the feature"` and 5 being `"I am totally satisfied with my feature implementation"`.

| Feature            | Score (0-5)     |
| ------------------ | --------------- |
| Sorting            | type your score |
| Paging             | type your score |
| Expanding row      | type your score |
| Navigating to item | type your score |
| Smart back to list | type your score |

---

Should you have any questions feel free to contact us.

Good luck! 💪
