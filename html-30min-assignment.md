# 📝 HTML Practical Assignment: The Academic Timetable
* **Time Limit:** 30 Minutes  
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



</body>
</html>
```
