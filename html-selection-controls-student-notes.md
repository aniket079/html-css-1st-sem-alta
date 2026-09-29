# HTML Study Notes: Selection Controls (Radio Buttons, Checkboxes & Labels)

---

## 1. Introduction to Selection Controls

Selection controls allow users to choose options from a pre-defined set of choices rather than typing freeform text. This reduces input errors, speeds up form completion, and ensures data consistency for server-side processing.

In HTML forms, the two most fundamental selection controls are:
1. **Radio Buttons (`type="radio"`)**: Used when the user must choose **exactly one** option from a group of mutually exclusive choices.
2. **Checkboxes (`type="checkbox"`)**: Used when the user can select **zero, one, or multiple** independent options.

---

## 2. Radio Buttons (`type="radio"`)

### 2.1 Purpose & Behavior
Radio buttons are designed for **mutually exclusive** selections. Selecting one radio button in a group automatically deselects any previously selected radio button in that same group.

```html
<input type="radio" name="gender" id="male" value="male">
```

### 2.2 The Grouping Mechanism (`name` Attribute)
The most critical rule of radio buttons is that **all options belonging to the same question must share the exact same `name` attribute value**. 

* If radio buttons share the same `name`, the browser treats them as a unified group and enforces single selection.
* If radio buttons have different `name` attributes, the browser treats them as independent inputs, allowing multiple selections (which breaks the logic of a radio group).

```html
<!-- CORRECT: Shared name "payment" creates a mutually exclusive group -->
<input type="radio" name="payment" id="card" value="card">
<input type="radio" name="payment" id="cash" value="cash">
<input type="radio" name="payment" id="upi" value="upi">
```

### 2.3 Essential Attributes for Radio Buttons

| Attribute | Type | Description |
| :--- | :--- | :--- |
| `name` | String | **Required.** Groups radio buttons together. Must match across options in the same group. |
| `value` | String | **Required.** The data value sent to the server when this specific option is submitted. |
| `checked` | Boolean | Pre-selects this radio button when the page loads. Only one radio per group should have `checked`. |
| `required` | Boolean | Forces the user to select at least one option in the group before submitting the form. |
| `disabled` | Boolean | Prevents user interaction and excludes the field from form submission. |

> ⚠️ **Key Rule:** Unlike text inputs where `value` is typed by the user, for radio buttons **you must explicitly supply the `value` attribute** in your HTML. If omitted, the browser submits the default text `"on"` instead of meaningful data.

---

## 3. Checkboxes (`type="checkbox"`)

### 3.1 Purpose & Behavior
Checkboxes allow users to make **independent binary choices** (Yes/No, True/False) or select **multiple items** from a list. Selecting one checkbox does NOT affect the state of any other checkbox.

```html
<input type="checkbox" name="subscribe" id="subscribe" value="yes">
```

### 3.2 Single vs. Multiple Checkbox Groups

#### Case A: Single Standalone Checkbox (Binary Choice)
Used for terms of service, newsletter opt-ins, or single confirmation flags.

```html
<input type="checkbox" name="terms" id="terms" value="accepted" required>
<label for="terms">I agree to the Terms and Conditions</label>
```

#### Case B: Multiple Checkbox Group (Multi-Selection)
Used when users can pick multiple options from a set (e.g., hobbies, skills, food toppings). Each input shares a logical name or uses array-style naming depending on the backend language.

```html
<input type="checkbox" name="hobbies" id="coding" value="coding">
<label for="coding">Coding</label>

<input type="checkbox" name="hobbies" id="sports" value="sports">
<label for="sports">Sports</label>

<input type="checkbox" name="hobbies" id="music" value="music">
<label for="music">Music</label>
```

### 3.3 Essential Attributes for Checkboxes

| Attribute | Type | Description |
| :--- | :--- | :--- |
| `name` | String | Identifies the input field in the submitted form data. |
| `value` | String | The data value sent to the server if the checkbox is checked upon submission. |
| `checked` | Boolean | Pre-checks the checkbox when the page loads. Multiple checkboxes can have `checked`. |
| `required` | Boolean | For a single checkbox (like Terms & Conditions), forces the user to check it before submission. |
| `disabled` | Boolean | Disables the checkbox, making it unclickable and un-submittable. |

> 📌 **Server Submission Behavior:** Unchecked checkboxes are **not sent** in the HTTP request payload at all. Only checkboxes that are actively checked at the time of submission send their `name=value` pairs to the server.

---

## 4. The `<label>` Element & Binding Techniques

### 4.1 Why Labels are Essential for Selection Controls
For radio buttons and checkboxes, small click targets can be difficult to select (especially on mobile touchscreens or for users with motor impairments). 

The `<label>` element provides two major benefits:
1. **Target Expansion:** Clicking the text inside the `<label>` automatically toggles/selects the associated input element.
2. **Accessibility (Screen Readers):** Screen readers read the label text aloud when the user focuses on the input element.

---

### 4.2 Binding Technique 1: Explicit Binding (Recommended)
Connects the `<label>` to the `<input>` using matching `for` and `id` attributes.

* The `for` attribute on the `<label>` **must exactly match** the `id` attribute on the `<input>`.

```html
<!-- Explicit Binding -->
<input type="radio" name="plan" id="basic_plan" value="basic">
<label for="basic_plan">Basic Membership ($10/mo)</label>
```

---

### 4.3 Binding Technique 2: Implicit Binding (Nested)
Wraps the `<input>` element directly inside the `<label>` element. No `for` or `id` attributes are strictly necessary, though `id` is often still included for CSS or JavaScript reference.

```html
<!-- Implicit Binding -->
<label>
    <input type="checkbox" name="newsletter" value="weekly">
    Subscribe to Weekly Newsletter
</label>
```

---

## 5. Grouping Controls with `<fieldset>` and `<legend>`

When presenting a group of related radio buttons or checkboxes, use `<fieldset>` to draw a structural boundary around them and `<legend>` to provide a clear section title. This provides semantic context for accessibility tools.

```html
<fieldset>
    <legend>Select Your T-Shirt Size:</legend>
    
    <input type="radio" name="size" id="size_s" value="S">
    <label for="size_s">Small (S)</label>

    <input type="radio" name="size" id="size_m" value="M" checked>
    <label for="size_m">Medium (M)</label>

    <input type="radio" name="size" id="size_l" value="L">
    <label for="size_l">Large (L)</label>
</fieldset>
```

---

## 6. Comparison: Radio Buttons vs. Checkboxes

| Feature | Radio Buttons (`type="radio"`) | Checkboxes (`type="checkbox"`) |
| :--- | :--- | :--- |
| **Selection Type** | Single selection (Mutually Exclusive). | Multiple selections (Independent choices). |
| **User Options** | Choose 1 from $N$ options. | Choose 0, 1, or up to $N$ options. |
| **`name` Attribute** | **Must be identical** across all options in the group. | Usually identical for a multi-choice group, or unique for standalone toggles. |
| **Default Visual Shape** | Circular button with an inner dot when selected. | Square box with a checkmark ($\checkmark$) when selected. |
| **Deselection** | Cannot deselect a radio button by clicking it again; must click another radio in the group. | Clicking a checked checkbox toggles it back to unchecked. |
| **Server Data** | Sends exactly 1 `name=value` pair for the chosen radio. | Sends `name=value` pairs **only for checked** checkboxes. |

---

## 7. Practical Hands-On Lab Code

Save the code below as **`html_selection_controls_practice.html`** in VS Code and open it with **Live Server** to see radio buttons, checkboxes, and labels working together in a complete form structure.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HTML Selection Controls Practice</title>
</head>
<body>

    <h1>Course Registration & Preferences</h1>
    <p>Please complete your registration details below.</p>
    <hr>

    <form action="https://httpbin.org/post" method="POST">

        <!-- STUDENT INFORMATION -->
        <p>
            <label for="student_name">Full Name:</label><br>
            <input type="text" id="student_name" name="student_name" placeholder="Enter your full name" required>
        </p>

        <!-- RADIO BUTTON GROUP 1: BATCH SELECTION -->
        <fieldset>
            <legend>Select Your Preferred Class Batch (Choose One):</legend>
            
            <p>
                <input type="radio" id="batch_morning" name="class_batch" value="morning" required>
                <label for="batch_morning">Morning Batch (09:00 AM - 12:00 PM)</label>
            </p>
            <p>
                <input type="radio" id="batch_afternoon" name="class_batch" value="afternoon">
                <label for="batch_afternoon">Afternoon Batch (01:00 PM - 04:00 PM)</label>
            </p>
            <p>
                <input type="radio" id="batch_evening" name="class_batch" value="evening" checked>
                <label for="batch_evening">Evening Batch (05:00 PM - 08:00 PM)</label>
            </p>
        </fieldset>

        <br>

        <!-- CHECKBOX GROUP 2: SUBJECT ELECTIVES -->
        <fieldset>
            <legend>Select Your Elective Modules (Choose Any):</legend>
            
            <p>
                <input type="checkbox" id="module_html" name="electives" value="html_css" checked>
                <label for="module_html">HTML5 & CSS3 Web Layouts</label>
            </p>
            <p>
                <input type="checkbox" id="module_js" name="electives" value="javascript">
                <label for="module_js">JavaScript Programming Basics</label>
            </p>
            <p>
                <input type="checkbox" id="module_python" name="electives" value="python">
                <label for="module_python">Python Fundamentals</label>
            </p>
            <p>
                <input type="checkbox" id="module_sql" name="electives" value="sql_db">
                <label for="module_sql">Relational Databases & SQL</label>
            </p>
        </fieldset>

        <br>

        <!-- STANDALONE CHECKBOX: TERMS AND CONDITIONS -->
        <p>
            <input type="checkbox" id="agree_terms" name="agree_terms" value="yes" required>
            <label for="agree_terms">I confirm that all provided information is accurate and I agree to the code of conduct.</label>
        </p>

        <!-- FORM ACTION BUTTONS -->
        <p>
            <button type="submit">Submit Registration</button>
            <button type="reset">Reset Form</button>
        </p>

    </form>

</body>
</html>
```

---

## 8. Quick Revision Checklist

Before submitting or testing your forms, verify the following:

- [ ] Do all radio buttons belonging to the same question share the **exact same `name` attribute**?
- [ ] Have you explicitly assigned a `value` attribute to every `<input type="radio">` and `<input type="checkbox">`?
- [ ] Does every radio button and checkbox have a corresponding `<label>` bound via `for` and `id`?
- [ ] Are groups of related selection controls enclosed within a `<fieldset>` with a descriptive `<legend>`?
- [ ] Do you understand why unchecked checkboxes do not appear in the submitted HTTP request data?
