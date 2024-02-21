
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quản lý thông tin sinh viên</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f1f1f1;
            margin: 0;
            padding: 0;
        }
        .container {
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        h2 {
            text-align: center;
            color: #333;
        }
        form {
            margin-bottom: 20px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            color: #555;
        }
        input[type="text"], input[type="date"], input[type="number"] {
            width: calc(100% - 12px);
            padding: 8px;
            margin-top: 5px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box;
        }
        input[type="submit"], input[type="button"] {
            width: 100%;
            background-color: #4CAF50;
            color: white;
            padding: 10px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        input[type="submit"]:hover, input[type="button"]:hover {
            background-color: #45a049;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #f2f2f2;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>Quản lý thông tin sinh viên</h2>

    <form id="studentForm">
        <input type="hidden" id="editIndex" value="-1">
        <label for="studentID">Mã sinh viên:</label>
        <input type="text" id="studentID" name="studentID" required>

        <label for="fullName">Họ và tên:</label>
        <input type="text" id="fullName" name="fullName" required>

        <label for="dob">Ngày sinh:</label>
        <input type="date" id="dob" name="dob" required>

        <label for="class">Lớp học:</label>
        <input type="text" id="class" name="class" required>

        <label for="gpa">Điểm GPA:</label>
        <input type="number" id="gpa" name="gpa" min="0" max="10" step="0.01" required>

        <input type="submit" value="Thêm sinh viên">
    </form>

    <table id="studentTable">
        <thead>
            <tr>
                <th>Mã SV</th>
                <th>Họ và tên</th>
                <th>Ngày sinh</th>
                <th>Lớp học</th>
                <th>Điểm GPA</th>
                <th>Thao tác</th>
            </tr>
        </thead>
        <tbody id="studentTableBody">
        </tbody>
    </table>
</div>

<script>
    document.getElementById("studentForm").addEventListener("submit", function(event) {
        event.preventDefault();

        var editIndex = document.getElementById("editIndex").value;
        var studentID = document.getElementById("studentID").value;
        var fullName = document.getElementById("fullName").value;
        var dob = document.getElementById("dob").value;
        var classValue = document.getElementById("class").value;
        var gpa = document.getElementById("gpa").value;

        if (editIndex == "-1") {
            var newRow = document.getElementById("studentTableBody").insertRow();
            newRow.innerHTML = "<td>" + studentID + "</td><td>" + fullName + "</td><td>" + dob + "</td><td>" + classValue + "</td><td>" + gpa + "</td><td><input type='button' value='Chỉnh sửa' onclick='editRow(this)'></td>";
        } else {
            var table = document.getElementById("studentTable");
            var row = table.rows[parseInt(editIndex) + 1];
            row.cells[0].innerHTML = studentID;
            row.cells[1].innerHTML = fullName;
            row.cells[2].innerHTML = dob;
            row.cells[3].innerHTML = classValue;
            row.cells[4].innerHTML = gpa;
            row.cells[5].innerHTML = "<input type='button' value='Chỉnh sửa' onclick='editRow(this)'>";
            document.getElementById("editIndex").value = "-1";
        }
        
        document.getElementById("studentForm").reset();
    });

    function editRow(btn) {
        var row = btn.parentNode.parentNode;
        var cells = row.cells;
        document.getElementById("studentID").value = cells[0].innerHTML;
        document.getElementById("fullName").value = cells[1].innerHTML;
        document.getElementById("dob").value = cells[2].innerHTML;
        document.getElementById("class").value = cells[3].innerHTML;
        document.getElementById("gpa").value = cells[4].innerHTML;
        document.getElementById("editIndex").value = row.rowIndex - 1;
    }
</script>

</body>
</html>
