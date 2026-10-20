# UBC Student Experience Quest

A browser-based prototype of a student feedback survey for UBC Student Health and Wellbeing. The survey presents six questions as a short campus-themed “quest,” tracks progress, and unlocks a prize-wheel animation when the survey is complete.

> **Demo only:** This project is a standalone front-end prototype. It does not submit, transmit, or persist survey responses, and the prize names are placeholders. Do not enter real or sensitive health information.

## What it does

The page guides a participant through the following flow:

1. **Start the quest.** An introductory screen explains the survey and offers a button to begin.
2. **Answer six questions.** The participant can move backward and forward through the survey. Required questions must have a response before continuing; the final two questions are optional and can be skipped.
3. **View progress.** A progress bar, percentage, question count, status message, and Thunderbird label update as the participant advances.
4. **Complete the quest.** The page displays a thank-you message and a “+25 XP” completion reward.
5. **Spin the prize wheel.** The participant can spin once per completed survey and see one of five placeholder prize names selected at random.
6. **Start again.** The restart button clears the in-memory answers and returns to the introduction.

### Survey questions

| #   | Topic                                                             | Response type                               | Required? |
| --- | ----------------------------------------------------------------- | ------------------------------------------- | --------- |
| 1   | Whether the visit fell short of expectations                      | Yes / No                                    | Yes       |
| 2   | Appointment wait time                                             | One of four time ranges                     | Yes       |
| 3   | Experience with the health care provider                          | Five-point quality scale                    | Yes       |
| 4   | Likelihood of recommending UBC Student Health and Wellbeing       | Agreement scale, including “Not Applicable” | Yes       |
| 5   | Health conditions or disabilities the participant identifies with | Select all that apply                       | No        |
| 6   | Compliment or opportunity for improvement                         | Free-text response                          | No        |

## Run it locally

There is no build step, package installation, backend, or configuration required. The app is contained in a single HTML file.

### Option 1: Open the file directly

1. Download or clone this repository.
2. Open `final_draft.html` in a current web browser, such as Chrome, Edge, or Firefox.
   - On Windows, you can double-click the file in File Explorer.
   - Or right-click it and choose **Open with** to select a browser.

### Option 2: Serve it locally

If Python is installed, open PowerShell in the project directory and run:

```powershell
py -m http.server 8000
```

Then visit <http://localhost:8000/> and open `final_draft.html`. Stop the server with **Ctrl+C** in PowerShell when finished.

Serving the file locally is optional; it does not add a backend or enable response submission.

## Project contents

```text
.
├── README.md
└── final_draft.html
```

`final_draft.html` contains the page markup, styles, JavaScript, and embedded image data. It has no external runtime dependencies.

## How the prototype works

- Survey questions and response options are defined in a JavaScript array in `final_draft.html`.
- Answers are held in a JavaScript object while the page is open. They are not written to local storage, cookies, a database, or a server.
- The prize wheel is drawn as inline SVG. Its selection is made randomly in the browser; the five current prize labels are sample text.
- Styling and responsive layout are included in the HTML file, along with the campus map and Thunderbird artwork.

## UI update (October 19, 2026)

This update changes only how the survey looks and moves. The six questions, their wording, answer options and order are exactly the same as before. The UBC wordmark, the Thunderbird artwork, the campus map background, the colour palette and the window-style layout are also unchanged.

### Loading

- **New loading screen:** while the page opens, a cream screen shows the UBC wordmark, a navy loading bar and the text "LOADING SURVEY...". It fades out after about one second.
- **Entrance animation:** after the loading screen, the header and the two windows slide up into place.
- **Question transitions:** each question, the start screen and the completion screen fade in when they appear.

### Progress bar

- **Smooth fill:** the bar now glides to its new width. Before, it jumped in blocky steps.
- **New look:** the fill is a navy gradient with moving gold diagonal stripes, a light sheen on top and a gold leading edge. The track has a soft inset shadow.
- **Checkpoints:** diamond markers sit on the bar between questions. Each one turns gold with a small "pop" when the student passes it.
- **Counting percentage:** the percentage counts up to its new value instead of jumping.

### Answer choices and buttons

- **Checkboxes:** each answer has a square checkbox on the right. A selected answer shows a gold check on navy, plus a gold bar on its left edge. This replaces the old `[X]` text marks.
- **No flicker:** picking an answer updates it in place. The whole question card no longer redraws on every click.
- **Buttons:** buttons lift slightly on hover and press in when clicked.
- **Keyboard focus:** answers and buttons show a clear gold outline when reached with the keyboard.
- **Required-answer message:** pressing Continue without answering a required question now shows a message inside the page, which shakes once. Before, it was a browser pop-up.

### Prize wheel

- **Redesign:** the wheel has navy, gold and cream slices. Around it are a thick navy rim with 24 lights, pegs between the slices, a navy-and-gold centre hub with "UBC", and a new teardrop pointer.
- **Spin:** the wheel makes six full turns over about 5.5 seconds and slows down gradually. The pointer flicks each time a peg passes it, and the rim lights chase while it spins.
- **Win:** the winning slice flashes with a gold outline and the lights blink. The prize appears in a gold "You won" card, and confetti bursts from the wheel.
- **Readable labels:** labels on the left half of the wheel are flipped so none read upside down. Prize names longer than 14 characters wrap onto two lines.
- **Fair result:** the prize is chosen first, and the wheel is then aimed so that slice stops under the pointer. The prize shown always matches the slice the pointer lands on.
- **One spin:** the spin button is disabled after one spin, as before.

### Accessibility

- If the student's device is set to reduce motion, the page skips the confetti and the loading delay, and the wheel stops after a short spin.
- The spin result is announced to screen readers when it appears.

## Editing the demo

To customize the prototype, edit `final_draft.html`:

- **Survey content and choices:** Update the `questions` array in the script. Each question defines its prompt, options (where applicable), response type, and whether it is optional.
- **Prize labels:** Replace the entries in the `prizes` array with the desired demo labels.
- **Appearance and layout:** Adjust the CSS in the page’s `<style>` block.
- **Images:** The current artwork is embedded in the HTML as image data, rather than loaded from separate image files.

Keep the question response types consistent with the rendering logic: `single`, `multi`, and `text`.

## Current limitations

- **No response submission:** There is no API, server, or survey-platform integration.
- **No persistence:** Responses exist only in browser memory while the current page is open; reloading or closing the page loses them.
- **Placeholder rewards:** The prize names are examples, not configured or redeemable rewards.
- **Prototype validation only:** The page provides basic required-answer checks, but it is not a production survey system.
- **Sensitive information:** One question concerns health conditions and disabilities. Do not use the prototype to collect real personal or health information.

Before using this as a real survey, connect it to an approved data-collection service and review privacy, consent, accessibility, security, and data-retention requirements.

## Development and testing

No automated test suite, linter, or build tooling is included in this repository. To check the prototype manually, open it in a browser and verify that you can:

1. Start the survey.
2. Select responses and navigate back and forward.
3. Continue past the optional questions without answering.
4. Reach the completion screen, spin the wheel, and restart.
