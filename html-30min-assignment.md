# 📝 HTML Practical Assignment: The Academic Timetable
* **Time Limit:** 30 Minutes  
* **Total Marks:** 20 Marks  
* **Allowed Tools:** VS Code & Live Server  
* **Constraints:** Pure HTML only. **No CSS allowed.** Use only standard HTML table attributes (`border`, `cellpadding`, `cellspacing`, `bgcolor`) for styling.

---

## 🎯 Objective
Create a fully structured HTML page that displays an academic class schedule. You must demonstrate proper folder structures, use accurate semantic tags, apply text formatting, and master both horizontal (`colspan`) and vertical (`rowspan`) cell merging.

---

## 🏗️ Visual Layout Goal
Your final table should look exactly like this grid structure when rendered in the browser:

```text
+----------------------------------------------------------------------------------------+
|                               SEMESTER 1: CLASS TIMETABLE                              | (Spans 5 Cols)
+---------------+-------------------+--------------------+-------------------+-----------+
| Time Slot     | Monday            | Tuesday            | Wednesday         | Thursday  |
+---------------+-------------------+--------------------+-------------------+-----------+
| 09:00 - 10:00 | Web Design Theory | Database Systems   | System Analysis   | Math 101  |
+---------------+-------------------+--------------------+-------------------+-----------+
| 10:00 - 12:00 | Web Programming Lab (Spans 2 Rows)     | Network Security  | Office    |
+---------------+                                        +-------------------+ Hours     | (Spans 3 Rows)
| 11:00 - 12:00 |                                        | Operating Systems |           |
+---------------+----------------------------------------+-------------------+           |
| 12:00 - 01:00 |                        LUNCH BREAK (Spans 4 Columns)       |           |
+---------------+-------------------+--------------------+-------------------+-----------+
```

---

## 📋 Step-by-Step Requirements

### Step 1: Document Setup (3 Marks)
1. Create a new file in VS Code named `timetable.html`.
2. Write a valid **HTML5 DocType skeleton**.
3. Set the `<title>` of the browser tab to `Practical Exam: Student Timetable`.
4. Include a responsive viewport `<meta>` tag and a `<meta charset="UTF-8">` tag inside the `<head>`.

### Step 2: Page Header & Setup (3 Marks)
1. In the `<body>`, add an `<h1>` heading with the text: `HTML Semester 1 Evaluations`.
2. Write a paragraph (`<p>`) explaining what this page represents. **Bold** your name and *italicize* your student roll number using semantic tags.
3. Place a horizontal divider line (`<hr>`) beneath the paragraph to separate it from the table.

### Step 3: Table Structure & Styling (4 Marks)
1. Create a `<table>` tag. Configure it to display borders and prevent double-line borders by using these three specific attributes:
   * `border="1"`
   * `cellpadding="8"`
   * `cellspacing="0"`
2. Add a `bgcolor` attribute to the entire table set to `"lightgray"`.

### Step 4: Rowspan & Colspan Implementation (8 Marks)
1. **Row 1 (Main Header):** Create a single header cell `<th>` containing the text `SEMESTER 1: CLASS TIMETABLE`. Use `colspan` to merge it across all **5 columns**. Set its background color to `"navy"` (using `bgcolor="navy"`) and the text color to white by wrapping it in `<font color="white">`.
2. **Row 2 (Column Headers):** Create standard `<th>` headers for: `Time Slot`, `Monday`, `Tuesday`, `Wednesday`, and `Thursday`.
3. **Row 3 (9:00 Slot):** Insert regular `<td>` data cells for all classes.
4. **Row 4 & 5 (10:00 & 11:00 Slots):** 
   * Under Monday, create a cell for `Web Programming Lab` that spans **2 rows** vertically using `rowspan`. Give it a light-green background (`bgcolor="lightgreen"`).
   * Remember: Since this cell blocks Monday's slot in the row below, **do not write** a Monday cell in Row 5!
5. **Row 4, 5 & 6 (Office Hours):**
   * Under Thursday, create an `Office Hours` cell starting at 10:00 that spans **3 rows** vertically using `rowspan`. Give it a warm yellow background (`bgcolor="gold"`).
   * Remember to omit Thursday's cell in both Row 5 and Row 6!
6. **Row 6 (Lunch Break Recess):**
   * At 12:00, create a cell that says `LUNCH BREAK` and spans **4 columns** horizontally using `colspan`. Use a light-cyan background (`bgcolor="cyan"`). Highlight the text using the `<mark>` tag.

### Step 5: External Hyperlink (2 Marks)
1. Below the table, add another horizontal line (`<hr>`).
2. Add an anchor link (`<a>`) that points to the official university portal `https://www.w3schools.com` (as a placeholder).
3. Ensure the link opens in a **brand new tab** using the correct target attribute.

---

## 📊 Grading Rubric (For Teacher Reference)
| Component | Metric | Marks |
| :--- | :--- | :--- |
| **Skeleton & Head** | Valid DocType, UTF-8 charset, viewport, and title | 3 Marks |
| **Header Elements** | Headings, semantic formatting (`<strong>`/`<em>`), `<hr>` line | 3 Marks |
| **Table Attributes** | Pure HTML borders, paddings, cellspacing, and background | 4 Marks |
| **Cell Merging** | Flawless horizontal (`colspan`) and vertical (`rowspan`) configurations | 8 Marks |
| **Hyperlinks** | Anchor tag with external target redirection | 2 Marks |
| **Total** | | **20 Marks** |

---
---

# 🔑 Teacher's Solution Key (Do not distribute!)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Practical Exam: Student Timetable</title>
</head>
<body>

    <h1>HTML Semester 1 Evaluations</h1>
    <p>Submitted by: <strong>Student Name</strong> | Roll Number: <em>A079-2026</em></p>
    <hr>

    <table border="1" cellpadding="8" cellspacing="0" bgcolor="lightgray">
        <!-- Row 1: Merged Title Header -->
        <tr>
            <th colspan="5" bgcolor="navy">
                <font color="white">SEMESTER 1: CLASS TIMETABLE</font>
            </th>
        </tr>

        <!-- Row 2: Header Labels -->
        <tr>
            <th>Time Slot</th>
            <th>Monday</th>
            <th>Tuesday</th>
            <th>Wednesday</th>
            <th>Thursday</th>
        </tr>

        <!-- Row 3: 09:00 - 10:00 Slot -->
        <tr>
            <td><strong>09:00 - 10:00</strong></td>
            <td>Web Design Theory</td>
            <td>Database Systems</td>
            <td>System Analysis</td>
            <td>Math 101</td>
        </tr>

        <!-- Row 4: 10:00 - 11:00 Slot (Starts both rowspans) -->
        <tr>
            <td><strong>10:00 - 11:00</strong></td>
            <td rowspan="2" bgcolor="lightgreen">Web Programming Lab</td>
            <td>Network Security</td>
            <td>Operating Systems</td>
            <td rowspan="3" bgcolor="gold">Office Hours</td>
        </tr>

        <!-- Row 5: 11:00 - 12:00 Slot (Omit Monday and Thursday) -->
        <tr>
            <td><strong>11:00 - 12:00</strong></td>
            <td>Network Security</td>
            <td>Operating Systems</td>
        </tr>

        <!-- Row 6: 12:00 - 01:00 Slot (Colspan Lunch Break, Omit Thursday) -->
        <tr>
            <td><strong>12:00 - 01:00</strong></td>
            <td colspan="4" bgcolor="cyan" align="center">
                <mark><strong>LUNCH BREAK</strong></mark>
            </td>
        </tr>
    </table>

    <hr>
    <p>Need help? Visit the <a href="https://www.w3schools.com" target="_blank">W3Schools Web Portal</a> for documentation.</p>

</body>
</html>
```
