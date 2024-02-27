from flask import Flask, render_template, request

app = Flask(__name__)

notes = []
@app.route('/', methods=["GET", "POST"])
def index():
    if request.method == "POST":
        note = request.form.get("note")
        notes.append(note)
    return render_template("home.html", notes=notes)


if __name__ == '__main__':
    app.run(debug=True)


#for home.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Note Taking App</title>
</head>
<body>
    <h1>Add a Note:</h1>
    <form method="POST">
        <input type="text" name="note" placeholder="Enter a note...">
        <button type="submit">Add Note</button>
    </form>
    <h2>Notes:</h2>
    <ul>
        {% for note in notes %}
            <li>{{ note }}</li>
        {% endfor %}
    </ul>
</body>
</html>
