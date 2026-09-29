# HTML Form Controls: Text Inputs & Attributes

---

## 1. Introduction to Single-Line Text Inputs
In HTML forms, the `<input>` element is the most versatile and frequently used form control. It is an **empty (void) element**, meaning it does not have a closing tag (`</input>`).

The visual presentation and data validation of an `<input>` element are determined primarily by its **`type`** attribute.

---

## 2. Text Box (`type="text"`)

### 2.1 Purpose & Use Cases
The standard text box is used for collecting single-line plain text from the user. Common examples include:
* First Name / Last Name
* Username
* Search queries
* Street addresses or city names

### 2.2 Basic Syntax
A text input should **always** be paired with a `<label>` element for accessibility and usability.

```html
<label for="username">Username:</label>
<input type="text" id="username" name="username">
```

> **Accessibility Rule:** Clicking on a `<label>` whose `for` attribute matches an `<input>`'s `id` attribute automatically shifts cursor focus directly into the text box.

---

## 3. Password Field (`type="password"`)

### 3.1 Purpose & Visual Masking
The password field is designed specifically for sensitive authentication credentials. 

When a user types into a `type="password"` field, the browser automatically masks the characters, replacing them with dots (`•`), bullets, or asterisks (`*`).

```html
<label for="user_pass">Password:</label>
<input type="password" id="user_pass" name="user_pass">
```

### 3.2 Critical Security Note
* **Masking is NOT Encryption:** The visual masking of a `type="password"` input only protects against **shoulder surfing** (people standing behind the user looking at the screen).
* When the form is submitted, the raw, unencrypted plain-text password is sent over the network unless the form is served over **HTTPS** and secured at the backend layer.

---

## 4. Key Input Attributes

Attributes modify the behavior, appearance, and validation constraints of text inputs. Below is an exhaustive reference of core attributes:

| Attribute | Description | Example |
| :--- | :--- | :--- |
| **`name`** | Defines the variable key sent to the server upon submission (`name=value`). **Inputs without a `name` attribute will NOT be submitted.** | `name="first_name"` |
| **`value`** | Specifies the initial default value or holds the text entered by the user. | `value="John Doe"` |
| **`placeholder`** | Displays a short hint inside the field before the user types. Disappears on user input. | `placeholder="Enter your email"` |
| **`required`** | A boolean attribute that prevents form submission if the field is empty. | `required` |
| **`maxlength`** | Sets the maximum number of characters allowed in the field. | `maxlength="15"` |
| **`minlength`** | Sets the minimum number of characters required before submission is allowed. | `minlength="6"` |
| **`size`** | Sets the physical visual width of the input field in terms of character count. | `size="30"` |
| **`autofocus`** | Automatically places the cursor in this input box when the web page loads. | `autofocus` |
| **`autocomplete`** | Controls whether the browser offers auto-fill suggestions (`on`, `off`, `username`, `current-password`, `new-password`). | `autocomplete="off"` |
| **`readonly`** | Prevents the user from modifying the value, but **the value IS STILL sent** when submitted. | `readonly` |
| **`disabled`** | Disables the field completely (grayed out). **Disabled inputs are NOT sent** upon submission. | `disabled` |
| **`pattern`** | Defines a Regular Expression (Regex) that the input value must match to be valid. | `pattern="[A-Za-z]{3,}"` |

---

## 5. `readonly` vs. `disabled`: Comparison

Understanding the distinction between `readonly` and `disabled` is a key exam and practical skill:

```html
<!-- Readonly: User cannot edit, but "USER-123" WILL be sent to server -->
<input type="text" name="user_id" value="USER-123" readonly>

<!-- Disabled: User cannot edit, and "SYSTEM_OFF" WILL NOT be sent to server -->
<input type="text" name="status" value="SYSTEM_OFF" disabled>
```

| Feature | `readonly` | `disabled` |
| :--- | :--- | :--- |
| **User Editable?** | No | No |
| **Focusable / Clickable?** | Yes | No |
| **Included in Form Submission Data?** | **YES** | **NO** |
| **Visual Styling** | Standard or subtle border | Grayed out (faded) |

---

## 6. Placeholder vs. Label

⚠️ **Common Mistake:** Beginners often use `placeholder` *instead* of a `<label>` to save visual space on screen.

* **Why this is bad practice:**
  1. Once the user starts typing, the placeholder text disappears, leaving the user with no visual confirmation of what the field was for.
  2. Screen readers for visually impaired users rely on `<label>` elements to announce field names properly.
  3. Browsers cannot auto-fill forms reliably without proper `<label>` elements.

---

## 7. Practical Lab Code: Complete Login & Registration Form

Below is a complete, runnable HTML file demonstrating text boxes, password fields, and all discussed attributes in action.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Text Inputs & Attributes Practice</title>
</head>
<body>

    <h1>User Registration & Account Form</h1>
    <hr>

    <form action="/submit_account" method="POST">

        <!-- Personal Details Section -->
        <fieldset>
            <legend>Personal Information</legend>

            <!-- Standard Text Box with Autofocus, Required, and Placeholder -->
            <p>
                <label for="fullname">Full Name:</label><br>
                <input type="text" 
                       id="fullname" 
                       name="fullname" 
                       placeholder="e.g., Alex Smith" 
                       required 
                       autofocus>
            </p>

            <!-- Text Box with Character Length Constraints -->
            <p>
                <label for="username">Username (6 to 12 chars):</label><br>
                <input type="text" 
                       id="username" 
                       name="username" 
                       minlength="6" 
                       maxlength="12" 
                       placeholder="Choose a username" 
                       required>
            </p>
        </fieldset>

        <br>

        <!-- Security Section -->
        <fieldset>
            <legend>Security Credentials</legend>

            <!-- Password Input -->
            <p>
                <label for="password">New Password:</label><br>
                <input type="password" 
                       id="password" 
                       name="password" 
                       minlength="8" 
                       autocomplete="new-password" 
                       required>
            </p>

            <!-- Password Input with Pattern Restriction (Regex) -->
            <p>
                <label for="pin">4-Digit Security PIN:</label><br>
                <input type="password" 
                       id="pin" 
                       name="pin" 
                       maxlength="4" 
                       pattern="[0-9]{4}" 
                       placeholder="e.g., 1234" 
                       required>
            </p>
        </fieldset>

        <br>

        <!-- System Information (Readonly & Disabled Examples) -->
        <fieldset>
            <legend>System Parameters</legend>

            <!-- Readonly Attribute (Value sent on submission) -->
            <p>
                <label for="account_type">Account Type (Readonly):</label><br>
                <input type="text" 
                       id="account_type" 
                       name="account_type" 
                       value="Student Basic Plan" 
                       readonly>
            </p>

            <!-- Disabled Attribute (Value NOT sent on submission) -->
            <p>
                <label for="system_code">Internal System ID (Disabled):</label><br>
                <input type="text" 
                       id="system_code" 
                       name="system_code" 
                       value="SYS-9908" 
                       disabled>
            </p>
        </fieldset>

        <br>

        <!-- Form Submission Controls -->
        <button type="submit">Create Account</button>
        <button type="reset">Clear Form</button>

    </form>

</body>
</html>
```

---

## 8. Summary & Self-Check Questions

1. What is the key difference between `<input type="text">` and `<input type="password">`?
2. Why is masking in a password field **not** considered data encryption?
3. What happens when a user submits a form containing an `<input>` element that lacks a `name` attribute?
4. Explain the difference in behavior between the `readonly` and `disabled` attributes upon form submission.
5. Why should a `placeholder` attribute never replace a `<label>` element?
