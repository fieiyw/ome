<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Quiz Tracker</title>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #f3f6fb;
      color: #1f2937;
    }

    .container {
      max-width: 1300px;
      margin: 30px auto;
      padding: 20px;
    }

    .top-bar {
      background: #ffffff;
      border: 1px solid #dfe7f5;
      border-radius: 12px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.04);
      padding: 20px;
      margin-bottom: 20px;
    }

    .top-bar h1 {
      margin: 0 0 12px;
      font-size: 30px;
      color: #1e3a8a;
    }

    .form-grid {
      display: grid;
      grid-template-columns: repeat(5, minmax(180px, 1fr));
      gap: 12px;
      align-items: end;
    }

    .field {
      display: flex;
      flex-direction: column;
    }

    label {
      font-size: 14px;
      font-weight: 700;
      color: #374151;
      margin-bottom: 8px;
    }

    select, input, button {
      height: 42px;
      border: 1px solid #cbd5e1;
      border-radius: 8px;
      padding: 10px 12px;
      font-size: 15px;
      outline: none;
    }

    select:focus, input:focus {
      border-color: #2563eb;
      box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.12);
    }

    button {
      background: #2563eb;
      color: white;
      font-weight: 700;
      cursor: pointer;
      border: none;
      transition: 0.2s ease;
    }

    button:hover {
      background: #1d4ed8;
    }

    .sheet-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(300px, 1fr));
      gap: 20px;
    }

    .sheet {
      background: white;
      border: 1px solid #dfe7f5;
      border-radius: 12px;
      overflow: hidden;
      box-shadow: 0 2px 8px rgba(0,0,0,0.04);
    }

    .sheet-header {
      background: #eef4ff;
      padding: 14px 18px;
      border-bottom: 1px solid #dfe7f5;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    .sheet-header h2 {
      margin: 0;
      font-size: 22px;
      color: #1f2937;
    }

    table {
      width: 100%;
      border-collapse: collapse;
    }

    th, td {
      padding: 12px 14px;
      border-bottom: 1px solid #e5e7eb;
      text-align: left;
      font-size: 14px;
    }

    th {
      background: #f8fafc;
      font-weight: 700;
      color: #374151;
    }

    td {
      background: white;
    }

    .delete-btn {
      background: #ef4444;
      color: white;
      border: none;
      padding: 8px 10px;
      border-radius: 6px;
      font-size: 12px;
      cursor: pointer;
      height: auto;
    }

    .delete-btn:hover {
      background: #dc2626;
    }

    .empty {
      color: #6b7280;
      font-style: italic;
    }

    @media (max-width: 900px) {
      .form-grid, .sheet-grid {
        grid-template-columns: 1fr;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="top-bar">
      <h1>Quiz Tracker</h1>

      <div class="form-grid">
        <div class="field">
          <label for="subject">Subject</label>
          <select id="subject">
            <option value="">Choose subject</option>
            <option>Math</option>
            <option>Business</option>
            <option>Research</option>
            <option>Data Analytics</option>
          </select>
        </div>

        <div class="field">
          <label for="quizName">Quiz Number / Name</label>
          <input id="quizName" type="text" placeholder="Quiz 1 / Algebra" />
        </div>

        <div class="field">
          <label for="score">Score</label>
          <input id="score" type="number" min="0" max="100" placeholder="85" />
        </div>

        <div class="field">
          <label for="date">Date</label>
          <input id="date" type="date" />
        </div>

        <div class="field">
          <button id="addBtn">Add Entry</button>
        </div>
      </div>
    </div>

    <div class="sheet-grid">
      <div class="sheet">
        <div class="sheet-header">
          <h2>Math</h2>
        </div>
        <table>
          <thead>
            <tr>
              <th>Quiz Number / Name</th>
              <th>Score</th>
              <th>Date</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody id="Math"></tbody>
        </table>
      </div>

      <div class="sheet">
        <div class="sheet-header">
          <h2>Business</h2>
        </div>
        <table>
          <thead>
            <tr>
              <th>Quiz Number / Name</th>
              <th>Score</th>
              <th>Date</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody id="Business"></tbody>
        </table>
      </div>

      <div class="sheet">
        <div class="sheet-header">
          <h2>Research</h2>
        </div>
        <table>
          <thead>
            <tr>
              <th>Quiz Number / Name</th>
              <th>Score</th>
              <th>Date</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody id="Research"></tbody>
        </table>
      </div>

      <div class="sheet">
        <div class="sheet-header">
          <h2>Data Analytics</h2>
        </div>
        <table>
          <thead>
            <tr>
              <th>Quiz Number / Name</th>
              <th>Score</th>
              <th>Date</th>
              <th>Action</th>
            </tr>
          </thead>
          <tbody id="Data Analytics"></tbody>
        </table>
      </div>
    </div>
  </div>

  <script>
    const subjectInput = document.getElementById("subject");
    const quizInput = document.getElementById("quizName");
    const scoreInput = document.getElementById("score");
    const dateInput = document.getElementById("date");
    const addBtn = document.getElementById("addBtn");

    addBtn.addEventListener("click", () => {
      const subject = subjectInput.value.trim();
      const quiz = quizInput.value.trim();
      const score = scoreInput.value.trim();
      const date = dateInput.value;

      if (!subject || !quiz || !score || !date) {
        alert("Please fill in all fields.");
        return;
      }

      const tbody = document.getElementById(subject);
      if (!tbody) return;

      const row = document.createElement("tr");

      const quizCell = document.createElement("td");
      quizCell.textContent = quiz;

      const scoreCell = document.createElement("td");
      scoreCell.textContent = score;

      const dateCell = document.createElement("td");
      dateCell.textContent = date;

      const actionCell = document.createElement("td");
      const deleteBtn = document.createElement("button");
      deleteBtn.textContent = "Delete";
      deleteBtn.className = "delete-btn";
      deleteBtn.addEventListener("click", () => row.remove());

      actionCell.appendChild(deleteBtn);

      row.appendChild(quizCell);
      row.appendChild(scoreCell);
      row.appendChild(dateCell);
      row.appendChild(actionCell);

      tbody.appendChild(row);

      subjectInput.value = "";
      quizInput.value = "";
      scoreInput.value = "";
      dateInput.value = "";
    });
  </script>
</body>
</html>
