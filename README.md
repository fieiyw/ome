<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Quiz Tracker</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: #f8f9fa;
      color: #202124;
    }

    .container {
      max-width: 1200px;
      margin: 30px auto;
      padding: 20px;
    }

    h1 {
      text-align: center;
      color: #1f2937;
      margin-bottom: 30px;
      font-size: 32px;
    }

    .input-section {
      background: white;
      padding: 25px;
      border-radius: 8px;
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12);
      margin-bottom: 30px;
    }

    .input-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 15px;
      align-items: end;
    }

    .form-group {
      display: flex;
      flex-direction: column;
    }

    label {
      font-size: 13px;
      font-weight: 600;
      color: #5f6368;
      margin-bottom: 8px;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    select, input {
      padding: 12px;
      border: 1px solid #dadce0;
      border-radius: 4px;
      font-size: 14px;
      background: white;
      color: #202124;
      transition: all 0.2s;
      font-family: 'Segoe UI', sans-serif;
    }

    select:hover, input:hover {
      border-color: #b3b6b7;
      box-shadow: 0 1px 1px rgba(0, 0, 0, 0.1);
    }

    select:focus, input:focus {
      outline: none;
      border-color: #4285f4;
      box-shadow: 0 1px 3px rgba(66, 133, 244, 0.3);
    }

    button {
      padding: 12px 24px;
      background: #4285f4;
      color: white;
      border: none;
      border-radius: 4px;
      font-size: 14px;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.2s;
      align-self: flex-end;
    }

    button:hover {
      background: #357ae8;
      box-shadow: 0 2px 4px rgba(66, 133, 244, 0.3);
    }

    button:active {
      background: #2d5ac8;
    }

    .sheets-container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
      gap: 20px;
    }

    .sheet {
      background: white;
      border-radius: 8px;
      overflow: hidden;
      box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12);
      transition: all 0.3s;
    }

    .sheet:hover {
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
    }

    .sheet-header {
      background: linear-gradient(135deg, #4285f4 0%, #357ae8 100%);
      color: white;
      padding: 16px;
      font-size: 16px;
      font-weight: 600;
      cursor: pointer;
      display: flex;
      justify-content: space-between;
      align-items: center;
      user-select: none;
    }

    .sheet-header:hover {
      background: linear-gradient(135deg, #357ae8 0%, #2d5ac8 100%);
    }

    .toggle-icon {
      font-size: 18px;
      transition: transform 0.3s;
    }

    .sheet-header.collapsed .toggle-icon {
      transform: rotate(-90deg);
    }

    .sheet-content {
      max-height: 1000px;
      overflow: hidden;
      transition: max-height 0.3s ease-in-out;
    }

    .sheet-content.collapsed {
      max-height: 0;
    }

    table {
      width: 100%;
      border-collapse: collapse;
    }

    thead {
      background: #f8f9fa;
      border-bottom: 2px solid #dadce0;
    }

    th {
      padding: 12px;
      text-align: left;
      font-weight: 600;
      color: #5f6368;
      font-size: 13px;
    }

    td {
      padding: 12px;
      border-bottom: 1px solid #e8e8e8;
      font-size: 14px;
    }

    tbody tr:hover {
      background: #f8f9fa;
    }

    .delete-btn {
      background: #ea4335;
      color: white;
      border: none;
      padding: 6px 12px;
      border-radius: 4px;
      font-size: 12px;
      cursor: pointer;
      transition: all 0.2s;
      font-weight: 600;
    }

    .delete-btn:hover {
      background: #d33425;
      box-shadow: 0 1px 3px rgba(234, 67, 53, 0.3);
    }

    .empty-message {
      padding: 20px;
      text-align: center;
      color: #9aa0a6;
      font-size: 14px;
    }

    @media (max-width: 768px) {
      .input-grid {
        grid-template-columns: 1fr;
      }

      button {
        align-self: stretch;
      }

      .sheets-container {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>📚 Quiz Tracker</h1>

    <div class="input-section">
      <div class="input-grid">
        <div class="form-group">
          <label for="subject">Subject</label>
          <select id="subject">
            <option value="">Select a subject</option>
            <option value="Math">Math</option>
            <option value="Business">Business</option>
            <option value="Research">Research</option>
            <option value="DataAnalytics">Data Analytics</option>
          </select>
        </div>

        <div class="form-group">
          <label for="quizName">Quiz Number / Name</label>
          <input id="quizName" type="text" placeholder="e.g., Quiz 1, Algebra" />
        </div>

        <div class="form-group">
          <label for="score">Score</label>
          <input id="score" type="number" min="0" max="100" placeholder="e.g., 85" />
        </div>

        <div class="form-group">
          <label for="date">Date</label>
          <input id="date" type="date" />
        </div>

        <button id="addBtn">Add Entry</button>
      </div>
    </div>

    <div class="sheets-container">
      <div class="sheet">
        <div class="sheet-header" onclick="toggleSheet(this)">
          <span>📐 Math</span>
          <span class="toggle-icon">▼</span>
        </div>
        <div class="sheet-content">
          <table>
            <thead>
              <tr>
                <th>Quiz Name</th>
                <th>Score</th>
                <th>Date</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody id="Math"></tbody>
          </table>
          <div id="Math-empty" class="empty-message">No quizzes yet. Add one above!</div>
        </div>
      </div>

      <div class="sheet">
        <div class="sheet-header" onclick="toggleSheet(this)">
          <span>💼 Business</span>
          <span class="toggle-icon">▼</span>
        </div>
        <div class="sheet-content">
          <table>
            <thead>
              <tr>
                <th>Quiz Name</th>
                <th>Score</th>
                <th>Date</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody id="Business"></tbody>
          </table>
          <div id="Business-empty" class="empty-message">No quizzes yet. Add one above!</div>
        </div>
      </div>

      <div class="sheet">
        <div class="sheet-header" onclick="toggleSheet(this)">
          <span>🔬 Research</span>
          <span class="toggle-icon">▼</span>
        </div>
        <div class="sheet-content">
          <table>
            <thead>
              <tr>
                <th>Quiz Name</th>
                <th>Score</th>
                <th>Date</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody id="Research"></tbody>
          </table>
          <div id="Research-empty" class="empty-message">No quizzes yet. Add one above!</div>
        </div>
      </div>

      <div class="sheet">
        <div class="sheet-header" onclick="toggleSheet(this)">
          <span>📊 Data Analytics</span>
          <span class="toggle-icon">▼</span>
        </div>
        <div class="sheet-content">
          <table>
            <thead>
              <tr>
                <th>Quiz Name</th>
                <th>Score</th>
                <th>Date</th>
                <th>Action</th>
              </tr>
            </thead>
            <tbody id="DataAnalytics"></tbody>
          </table>
          <div id="DataAnalytics-empty" class="empty-message">No quizzes yet. Add one above!</div>
        </div>
      </div>
    </div>
  </div>

  <script>
    const subjectInput = document.getElementById("subject");
    const quizInput = document.getElementById("quizName");
    const scoreInput = document.getElementById("score");
    const dateInput = document.getElementById("date");
    const addBtn = document.getElementById("addBtn");

    const subjects = ["Math", "Business", "Research", "DataAnalytics"];

    // Load data from localStorage
    function loadData() {
      subjects.forEach(subject => {
        const data = JSON.parse(localStorage.getItem(`quiz_${subject}`) || "[]");
        const tbody = document.getElementById(subject);
        const emptyMsg = document.getElementById(`${subject}-empty`);
        
        tbody.innerHTML = "";
        if (data.length === 0) {
          emptyMsg.style.display = "block";
        } else {
          emptyMsg.style.display = "none";
          data.forEach((entry, index) => {
            const row = createRow(subject, entry, index);
            tbody.appendChild(row);
          });
        }
      });
    }

    function createRow(subject, entry, index) {
      const row = document.createElement("tr");

      const quizCell = document.createElement("td");
      quizCell.textContent = entry.quiz;

      const scoreCell = document.createElement("td");
      scoreCell.textContent = entry.score;

      const dateCell = document.createElement("td");
      dateCell.textContent = entry.date;

      const actionCell = document.createElement("td");
      const deleteBtn = document.createElement("button");
      deleteBtn.className = "delete-btn";
      deleteBtn.textContent = "Delete";
      deleteBtn.onclick = () => deleteEntry(subject, index);

      actionCell.appendChild(deleteBtn);

      row.appendChild(quizCell);
      row.appendChild(scoreCell);
      row.appendChild(dateCell);
      row.appendChild(actionCell);

      return row;
    }

    function deleteEntry(subject, index) {
      const data = JSON.parse(localStorage.getItem(`quiz_${subject}`) || "[]");
      data.splice(index, 1);
      localStorage.setItem(`quiz_${subject}`, JSON.stringify(data));
      loadData();
    }

    addBtn.addEventListener("click", () => {
      const subject = subjectInput.value.trim();
      const quiz = quizInput.value.trim();
      const score = scoreInput.value.trim();
      const date = dateInput.value;

      if (!subject || !quiz || !score || !date) {
        alert("Please fill in all fields.");
        return;
      }

      if (score < 0 || score > 100) {
        alert("Score must be between 0 and 100.");
        return;
      }

      // Save to localStorage
      const data = JSON.parse(localStorage.getItem(`quiz_${subject}`) || "[]");
      data.push({ quiz, score, date });
      localStorage.setItem(`quiz_${subject}`, JSON.stringify(data));

      // Clear inputs
      subjectInput.value = "";
      quizInput.value = "";
      scoreInput.value = "";
      dateInput.value = "";

      // Reload data
      loadData();
    });

    function toggleSheet(header) {
      header.classList.toggle("collapsed");
      const content = header.nextElementSibling;
      content.classList.toggle("collapsed");
    }

    // Load data on page load
    loadData();
  </script>
</body>
</html>
