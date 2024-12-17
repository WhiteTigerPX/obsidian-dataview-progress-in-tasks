```dataview
TABLE WITHOUT ID
    "<span style='white-space: nowrap;'>" + key + "</span>" as Files,
    "<div style='display: flex; align-items: center; gap: 15px; width: 75%;'>" +
        "<progress style='flex-grow: 1; height: 8px;' max=100 value=" + (100 * length(filter(rows.tasks, (r) => r.completed)) / length(rows)) + ">" +
        "</progress>" +
        "<span style='font-size: 14px; color: #555; white-space: nowrap;'>" +
            length(filter(rows.tasks, (r) => r.completed)) + " / " + length(rows) +
        "</span>" +
    "</div>" AS Progress
FROM "relative/path/to/your/folder" //Must be replaced
FLATTEN file.tasks as tasks
GROUP BY file.link
WHERE length(rows) > length(filter(rows.tasks, (r) => r.completed)) // Change to >= to include notes with all tasks completed
SORT key ASC
```
