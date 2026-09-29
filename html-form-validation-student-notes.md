# HTML5 Form Validation: Student Study Notes

---

## Module Overview
Form validation is the process of checking if user-submitted data satisfies specific constraints before it is processed or sent to a web server. HTML5 introduced **native client-side validation**, allowing browsers to automatically check user input and display built-in error tooltips without requiring JavaScript or complex server-side scripts.

---

## 1. Introduction to Client-Side Form Validation

### Why Validate Forms?
1. **Data Integrity:** Ensures that received data conforms to expected formats (e.g., valid phone numbers, dates within valid ranges).
2. **Immediate User Feedback:** Informs users about mistakes instantly as they fill out the form.
3. **Reduced Server Load:** Prevents invalid or incomplete HTTP requests from hitting the web server.

> **Important Rule:** Client-side validation improves user experience, but **server-side validation is still mandatory** for security, as malicious users can bypass HTML5 browser checks.

---

## 2. The `required` Attribute

### Purpose & Behavior
The `required` attribute is a boolean attribute. When present on a form element, the browser **blocks form submission** if the field is left empty or unselected, highlighting the invalid field with a pop-up warning message.

### Syntax
```html
<input type="text" name="username" required>
```

### Usage Across Form Controls
* **Text / Password / Email / Number Inputs:** Must contain at least one non-whitespace character.
* **Checkboxes:** The checkbox *must* be checked (ideal for "Terms and Conditions").
* **Radio Button Groups:** At least *one* radio button in the group (sharing the same `name`) must be selected.
* **Dropdown Menus (`<select>`):** The selected `<option>` must have a non-empty `value` attribute.

#### Example:
```html
<!-- Text Input Required -->
<label for="fullname">Full Name:</label>
<input type="text" id="fullname" name="fullname" required>

<!-- Checkbox Required -->
<label>
    <input type="checkbox" name="terms" required>
    I agree to the Terms of Service
</label>

<!-- Dropdown Required (First option has empty value) -->
<label for="country">Country:</label>
<select id="country" name="country" required>
    <option value="">-- Select Country --</option>
    <option value="in">India</option>
    <option value="us">United States</option>
</select>
```

---

## 3. The `pattern` Attribute

### Purpose & Behavior
The `pattern` attribute uses **Regular Expressions (Regex)** to enforce specific structural rules for text-based inputs. If the user's input does not match the exact Regex pattern, the browser rejects the submission.

### Syntax
```html
<input type="text" name="zipcode" pattern="[0-9]{6}">
```

### Coupling with the `title` Attribute
When an input fails a `pattern` check, the browser displays a default error message ("Please match the requested format"). To provide helpful feedback, always pair `pattern` with a **`title` attribute**, which appears inside the browser's validation tooltip.

#### Example with Custom Title:
```html
<label for="pincode">6-Digit Postal Code:</label>
<input type="text" 
       id="pincode" 
       name="pincode" 
       pattern="[0-9]{6}" 
       title="Please enter exactly 6 numeric digits (e.g., 110001)" 
       required>
```

### Common Regex Pattern Reference Table

| Target Input | Pattern Value | Description / Constraint |
| :--- | :--- | :--- |
| **Numeric PIN / ZIP** | `[0-9]{6}` | Exactly 6 numeric digits |
| **Alphabetic Only** | `[A-Za-z]+` | One or more uppercase or lowercase letters |
| **Username** | `[A-Za-z0-9_]{3,15}` | Alphanumeric & underscores, 3 to 15 characters |
| **Phone Number** | `[0-9]{10}` | Exactly 10 numeric digits |
| **PAN Card (India)** | `[A-Z]{5}[0-9]{4}[A-Z]{1}` | 5 uppercase letters, 4 digits, 1 uppercase letter |

---

## 4. `min` and `max` Attributes

### Purpose & Range Types
The `min` and `max` attributes set lower and upper boundary limits for numeric, date, and range input types. If a user enters a value below `min` or above `max`, the browser displays an out-of-range error message.

### 1. Numeric Inputs (`type="number"` & `type="range"`)
```html
<label for="age">Age (18 to 60):</label>
<input type="number" id="age" name="age" min="18" max="60" required>

<label for="satisfaction">Rating (1 to 10):</label>
<input type="range" id="satisfaction" name="satisfaction" min="1" max="10" value="5">
```

### 2. Date Inputs (`type="date"`)
Restricts selectable calendar dates to a specific range using ISO format (`YYYY-MM-DD`).
```html
<label for="booking">Event Date (October 2026 only):</label>
<input type="date" id="booking" name="booking" min="2026-10-01" max="2026-10-31" required>
```

### 3. Step Increments (`step`)
Optionally paired with `min` and `max` to control numeric intervals (e.g., even numbers, decimal currency).
```html
<!-- Allows values like 0.00, 0.25, 0.50, etc. -->
<label for="price">Price ($):</label>
<input type="number" id="price" name="price" min="0" max="100" step="0.25">
```

---

## 5. Distinction: Value Boundaries vs. Character Length

It is vital to distinguish between numeric value boundaries and text character length:

| Attribute Pair | Applicable Input Types | What it Constrains | Example |
| :--- | :--- | :--- | :--- |
| **`min` / `max`** | `number`, `range`, `date`, `time` | The **numeric value** or **chronological date** itself | `min="18"` means number must be $\ge 18$ |
| **`minlength` / `maxlength`** | `text`, `password`, `email`, `textarea` | The **number of characters** typed | `minlength="8"` means text must have $\ge 8$ characters |

---

## 6. Practical Lab Code Exercise

Save the following complete code as `form_validation_practice.html` and run it in VS Code using Live Server to test all validation features:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HTML5 Form Validation Practice</title>
</head>
<body>

    <h1>Student Registration Form</h1>
    <p>All fields marked with <strong>*</strong> are required.</p>

    <form action="https://httpbin.org/post" method="POST">

        <!-- REQUIRED & LENGTH VALIDATION -->
        <fieldset>
            <legend>Personal Information</legend>

            <p>
                <label for="username">Username * (3–12 chars):</label><br>
                <input type="text" 
                       id="username" 
                       name="username" 
                       minlength="3" 
                       maxlength="12" 
                       required>
            </p>

            <p>
                <label for="birthdate">Date of Birth * (Must be born before 2010):</label><br>
                <input type="date" 
                       id="birthdate" 
                       name="birthdate" 
                       max="2009-12-31" 
                       required>
            </p>
        </fieldset>

        <br>

        <!-- PATTERN REGEX VALIDATION -->
        <fieldset>
            <legend>Contact Verification</legend>

            <p>
                <label for="phone">10-Digit Mobile Number *:</label><br>
                <input type="tel" 
                       id="phone" 
                       name="phone" 
                       pattern="[0-9]{10}" 
                       title="Please enter a valid 10-digit mobile number containing digits 0-9 only." 
                       placeholder="9876543210" 
                       required>
            </p>

            <p>
                <label for="pincode">6-Digit Postal PIN Code *:</label><br>
                <input type="text" 
                       id="pincode" 
                       name="pincode" 
                       pattern="[0-9]{6}" 
                       title="Postal code must be exactly 6 numeric digits." 
                       required>
            </p>
        </fieldset>

        <br>

        <!-- MIN / MAX NUMERIC & RANGE VALIDATION -->
        <fieldset>
            <legend>Academic Preferences</legend>

            <p>
                <label for="semester">Current Semester * (Semesters 1 to 8):</label><br>
                <input type="number" 
                       id="semester" 
                       name="semester" 
                       min="1" 
                       max="8" 
                       required>
            </p>

            <p>
                <label for="credits">Desired Credits (Step of 3, Min 3 - Max 21):</label><br>
                <input type="number" 
                       id="credits" 
                       name="credits" 
                       min="3" 
                       max="21" 
                       step="3" 
                       value="12">
            </p>
        </fieldset>

        <br>

        <!-- REQUIRED CHECKBOX -->
        <p>
            <label>
                <input type="checkbox" name="agreement" required>
                I confirm that all provided details are accurate. *
            </label>
        </p>

        <button type="submit">Submit Registration</button>
        <button type="reset">Reset Form</button>

    </form>

</body>
</html>
```

---

## 7. Quick Revision Checklist
1. What happens when a user clicks a submit button if a `required` input is empty?
2. Why should you always pair the `pattern` attribute with a `title` attribute?
3. What is the difference between `max="10"` and `maxlength="10"`?
4. How do you restrict a date picker (`type="date"`) so that users cannot select dates in the future?
