# italian-consulate-website-automation
Originally forked from https://github.com/drewhershey/italian-consulate-website-automation

This fork:
Supports SMS notifications via Twilio
Autofills the booking form
Auto traverses the calendar to find an open appointment
Restarts the script if it fails/crashes

This project uses Puppeteer to script browser interactions to automate the apppointment booking process on the Italian Consulate webiste.

The process for obtaining an appointment for citizenship recognition is notoriously difficult and time consuming. This project hopes to simplify it somewhat, while adding its own hurdles in the form of: booking forms that may deviate from the form this script expects, requiring some hand-tooling of the CSS selectors and adding selectors for form fields that may exist in the form you encounter during the booking process.

## What this script does:

- Assumes your booking page works similarly to the Italian Consulate form for San Francisco.
- Allows for attempting to book an appointment for multiple links (there are two citizenship appointment links for the SF consulate).
- Logs into the Prenot@mi website using the credentials you provide.
- Attempts to navigate to the booking page every `n` seconds. This is customizable.
- If it succeeds in reaching the booking page, it will automatically fill in the form fields with the information you provide.
- Once the calendar page loads, it will close any other tabs that have not reached the calendar page. Then it will automatically click through the months until it finds an available appointment.
- If it finds an available appointment, the script can send you an alert (SMS via Twilio and/or email via SendGrid). Once it finds an available appointment,
it clicks on that appointment and the stops the script, allowing you to manually continue and finish the apppointment booking process.
- If you are logged out - the session expires every 30 minutes - the script will log you back in and continue attempting to find an open appointment.
- If the script or the browser exits unexpectedly, `forever` will restart the script so that the booking attempts can continue indefinitely.

To start the script:
`npm run start`

To stop the script:
`npm run stop`

To view the logs:
`npm run logs`
