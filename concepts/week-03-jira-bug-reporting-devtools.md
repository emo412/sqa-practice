# Week 03 — Jira, Professional Bug Reporting and Browser DevTools

**Study date:** 17 November 2026  
**Program:** 24-week SQA job-preparation plan  
**Session:** Week 3, Day 1  
**Status:** Learning and assessment completed; evidence capture remains a separate local task.

## 1. Jira fundamentals

### Key terms

- **Project:** A workspace in Jira used to organize and track related work.
- **Issue:** A trackable work item in a project.
- **Bug:** An issue type used to report unexpected behavior or a defect.
- **Task:** A unit of work that needs to be completed.
- **Story:** A requirement or feature expressed from a user's perspective.
- **Summary:** A short title describing the issue.
- **Description:** Detailed context, steps, and supporting information.
- **Priority:** How urgently the issue should be addressed.
- **Assignee:** The person responsible for handling the issue.
- **Status:** The issue's current position in its workflow.

A Jira issue type describes the kind of work item. A workflow describes the statuses and transitions through which that issue moves.

### Practical scope

The study covered project and issue concepts, issue creation, and the information used to document bugs. This note does not claim that live Jira tickets were created.

## 2. Professional bug reporting

A useful bug report gives another person enough information to understand, investigate, and reproduce the problem.

### Core fields

1. **Bug ID:** A unique identifier assigned by the tracking system.
2. **Title:** A concise description of the observed failure.
3. **Environment:** Operating system, browser, device, application version, and relevant configuration.
4. **Preconditions:** Required state before executing the test.
5. **Steps to reproduce:** Ordered, precise actions.
6. **Test data:** Inputs used during reproduction.
7. **Expected result:** What the system should do.
8. **Actual result:** What the system actually did.
9. **Severity:** The impact of the defect on the system or user.
10. **Priority:** The urgency with which the defect should be fixed.
11. **Evidence:** Screenshots, recordings, logs, or other supporting material.

### Severity versus priority

- **Severity** measures the impact of a defect.
- **Priority** indicates how urgently it should be fixed.

Example: a spelling error in a homepage campaign banner may have low severity but high priority if the campaign is due to launch shortly.

### Practice scenario: login accepts an incorrect password

**Scenario:** A login form accepts an incorrect password and opens the dashboard.

| Field | Practice value |
|---|---|
| Title | Login succeeds when an incorrect password is entered |
| Environment | Simulated scenario; browser and OS versions not verified |
| Preconditions | A registered account exists; user is logged out |
| Test data | Registered username and an incorrect password |
| Steps | Open login page; enter registered username and incorrect password; select Login |
| Expected result | Access is denied and an appropriate validation message is displayed |
| Actual result | Dashboard opens and the user is authenticated |
| Severity | Critical, because authentication can be bypassed |
| Priority | High |
| Evidence | Not available — simulated scenario |

**Reporting discipline:** Do not invent environment details or claim that a screenshot, recording, or log exists. Clearly label simulated data and unavailable evidence.

### Reproduction checklist

If a developer cannot reproduce a reported defect, verify and provide:

- Exact environment and application version.
- Preconditions and account or system state.
- Exact test data.
- Numbered reproduction steps.
- Expected and actual results.
- Relevant screenshots, recordings, or console/network logs, when available.

## 3. Browser DevTools

Browser DevTools helps a tester inspect page structure, styling, browser errors, and communication between the browser and server.

### Main panels studied

| Panel | QA use |
|---|---|
| Elements | Inspect the DOM/HTML structure and CSS styling; temporarily modify page markup or styles |
| Console | Inspect JavaScript errors, warnings, and log messages |
| Network | Inspect HTTP requests and responses, including URL, method, status, resource type, and response data |

### Network inspection record

The main Wikipedia page request was inspected:

| Field | Observed value |
|---|---|
| Request URL | `https://www.wikipedia.org/` |
| Method | `GET` |
| Status | `304 Not Modified` |
| Resource type | Document (`Doc`) |
| Content-Type | `text/html` |

**Interpretation:** HTTP 304 means the cached representation can be reused because the resource has not changed according to the server's validation. It is not, by itself, an error.

For button behavior, inspect the Elements panel for the button's markup and relevant event listeners, then inspect Network—especially Fetch/XHR—for a request triggered by the click. Check the request URL, method, status, and response.

### Console observation

No visible errors or warnings were observed in the Console during the page inspection. This is a limited observation from that browsing session; it does not prove that the entire website is free of JavaScript errors.

### Elements inspection: Wikipedia homepage

The inspected markup included:

```html
<img
  class="central-featured-logo"
  src="portal/wikipedia.org/assets/img/Wikipedia-logo-v2.png"
  srcset="portal/wikipedia.org/assets/img/Wikipedia-logo-v2@2x.png 2x"
  width="200"
  height="183"
  alt
>
```

Observed attributes:

- Tag: `img`
- Class: `central-featured-logo`
- Default image source: `Wikipedia-logo-v2.png`
- High-density source: `Wikipedia-logo-v2@2x.png`
- Width attribute: `200`
- Height attribute: `183`
- Alternative text: empty

An empty `alt` attribute is not automatically a defect; it can be appropriate for a decorative image. The tester must assess the image's purpose and accessibility context before reporting it.

The surrounding structure also included a `div.central-textlogo` container, an `h1.central-textlogo-wrapper` heading, a `span` for the Wikipedia wordmark, and a `strong` element for the slogan.

## 4. Assessment result

The learner correctly identified:

- Elements as the panel for inspecting HTML/DOM and styling.
- Network as the panel for checking requests and responses.
- Request URL, HTTP method, status code, and response as important request details.
- Fetch/XHR as a useful Network filter for API requests.

**Final active-recall assessment:** Passed.

## 5. Evidence and completion notes

- DevTools inspection and verbal assessment: completed.
- Console observation and Network request details: recorded above.
- Local screenshot capture: not attached to this repository commit.
- Jira ticket creation: not claimed.
- Live bug reproduction: not claimed; the login example was simulated.

## 6. Key QA reminders

- Distinguish an HTML tag from its CSS class names.
- Distinguish the DOM element from the image file it references.
- A 304 response is not automatically a failure.
- A visible validation message does not prove a test passed if an unintended action still occurred.
- Keep bug reports factual, reproducible, and explicit about assumptions or missing evidence.
