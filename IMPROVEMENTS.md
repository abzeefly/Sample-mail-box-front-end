## IMPROVEMENTS

- Using a **Date Range Picker** instead of typing in the date would be a better experience for the user. We can use libraries like **vue2-daterange-picker** to accomplish or use bootstrap vues **b-form-datepicker** to select start and end date separately as well.

- Make the table labels functional. We can use bootstraps **b-table** and allowing fields to be sortable when defining the fields. For the mobile view we can create **OnClick** functions to select and set the sorting field for the result array and change the CSS and image. The OnClick function will take in the field and a Boolean (true : asc, false: desc) and return the sorted set of results on click.

- On the Mobile view, tapping the **right arrow icon** can show the full-page view of the email with all the information and a way to download the attachments.

- The **To Badge** can have a popover card which is trigger on hover which could show all the **From, To, CC, BCC** information for quick preview of sender and receiver info.

- The **Attachment Clips** can have a popover card which is triggered on hover which show the files that are attached to the email.
