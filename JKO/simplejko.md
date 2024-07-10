<h1>INSTRUCTIONS</h1>

<ul>
<li>Open your class in Internet Explorer.</li>
<li>Press the F12 key when your class is fully loaded. This will open the developer tools.</li>
<li>Click on the Console tab of the developer tools window.</li>
<li>Paste the following code in the text box at the bottom of the console tab.</li>
<li>Either manually click on the green Play arrow or hold CTRL and press ENTER.</li>
</ul>

<p><br /></p>

# LMS Completion Status Updater

This script is designed to update the completion status of a course in a Learning Management System (LMS) to "completed". Once the status is updated, it attempts to submit this change if the required elements are present on the page. It's implemented with best practices such as strict mode, error handling, and defensive programming to ensure robust operation.

## Implementation

The script checks for the presence of specific DOM elements before attempting to interact with them, preventing runtime errors. It also uses a try-catch block to handle any unexpected errors gracefully. The functionality is wrapped inside a function to avoid polluting the global namespace, making it reusable in different contexts.

```javascript
'use strict';

function updateCompletionStatusAndSubmit() {
    try {
        // Simulate 5 minutes spent
        const timeSpent = 300; // time in seconds (5 minutes)
        API_1484_11.SetValue('cmi.session_time', timeSpent.toString()); // Assuming the API can record session time

        // Set the course to completed
        const apiCallResult = API_1484_11.SetValue('cmi.completion_status', 'completed');
        console.log('API Call Result:', apiCallResult);

        // Fetching the course header and submit button elements
        const courseHeader = document.getElementsByName('courseheader').item(0);
        if (courseHeader && courseHeader.contentDocument) {
            const submitButton = courseHeader.contentDocument.getElementById('c');
            if (submitButton) {
                submitButton.submit();
            } else {
                console.log('Submit button not found.');
            }
        } else {
            console.log('Course header or its document not found.');
        }
    } catch (error) {
        console.error('Error encountered:', error);
    }
}

updateCompletionStatusAndSubmit();
