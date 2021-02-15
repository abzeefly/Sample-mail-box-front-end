## Report

- I started off by choosing a framework to finish the challenge. As I have previous experience using Vue to make single page applications, I decided to use **Vue JS** with **Bootstrap** to achieve mission 1.

- I started by working on the desktop view for the app. For my search bar I tried to use an existing date range picker but all the available Vue date picker libraries either had problems with customisation or just did not have a range feature, so I just went with a b-input box which has two dates separated by a "-" as per the document.

- Next, I created the email data and functions to return results with the correctly formatted datetime. I used moments js for this task.

- After my results were working correctly, I decided to use b-table to create a table of my results and used templates to customise data, labels and rows.

- Once my desktop table component was working and looking as required I created my mobile component using stacked divs inside a v-for loop of results. This gave freedom to make the section to look as required.

- After finishing Mission 1 for Mission 2 I **row-details** scoped slot with an onClick event to create cards under my rows of the table to make an accordion table. So every row when clicked show the mail with all information making the application more usable and easy to use.

- I repeated a similar process for the mobile view and added the body of the email under the email information so when clicked/tapped you could see all the relevant information there, without disturbing the view of the app too much.

- This is how I finished Mission 2.
