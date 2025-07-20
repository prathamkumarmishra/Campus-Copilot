# Campus-Copilot
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Campus Copilot</title>
  <style>
    body {
  font-family: "Segoe UI", sans-serif;
  margin: 0;
  background-color: #f4f4f4;
  color: #333;
}

.container {
  max-width: 1100px;
  margin: auto;
  padding: 20px;
}

h1 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 20px;
}

.grid {
  display: grid;
  gap: 20px;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
}

.card {
  background-color: #fff;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.card h2 {
  font-size: 1.5rem;
  margin-bottom: 10px;
}

ul {
  padding-left: 20px;
}

li {
  margin-bottom: 8px;
}

  </style>
</head>
<body>
  <div class="container">
    <h1>Campus Copilot Dashboard</h1>

    <div class="grid">
      <section class="card" id="classSchedule">
        <h2>Today's Classes</h2>
        <ul id="classList"></ul>
      </section>

      <section class="card" id="reminders">
        <h2>Reminders</h2>
        <ul id="reminderList"></ul>
      </section>

      <section class="card" id="notices">
        <h2>College Notices</h2>
        <ul id="noticeList"></ul>
      </section>
    </div>
  </div>

  <script>
    // Sample data
const classes = [
  { subject: "Maths", time: "10:00 AM" },
  { subject: "DBMS", time: "12:00 PM" },
  { subject: "Physics", time: "3:00 PM" }
];

const reminders = [
  "Submit assignment by 5 PM",
  "Pay exam fee by Friday"
];

const notices = [
  "📢 Sports meet on 25th July",
  "📢 Workshop on AI this Saturday"
];

// Insert into HTML
function populateList(id, items) {
  const list = document.getElementById(id);
  items.forEach(item => {
    const li = document.createElement("li");
    li.textContent = typeof item === "string" ? item : `${item.subject} - ${item.time}`;
    list.appendChild(li);
  });
}

populateList("classList", classes);
populateList("reminderList", reminders);
populateList("noticeList", notices);

  </script>
</body>
</html>
import React, { useEffect, useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { CalendarDays, Bell, Clock, BookOpen } from "lucide-react";
import { format } from "date-fns";

const events = [
  {
    type: "Class",
    title: "Data Structures Lecture",
    time: "10:00 AM",
    date: "2025-07-20",
    location: "Room 102",
  },
  {
    type: "Club",
    title: "Robotics Club Meetup",
    time: "3:00 PM",
    date: "2025-07-21",
    location: "Lab 4",
  },
  {
    type: "Deadline",
    title: "Assignment Submission - DBMS",
    time: "11:59 PM",
    date: "2025-07-22",
  },
  {
    type: "Notice",
    title: "Mid-sem Exam Schedule Released",
    date: "2025-07-19",
  },
];

const iconMap = {
  Class: <BookOpen className="w-5 h-5 text-blue-500" />,
  Club: <Bell className="w-5 h-5 text-green-500" />,
  Deadline: <Clock className="w-5 h-5 text-red-500" />,
  Notice: <CalendarDays className="w-5 h-5 text-yellow-500" />,
};

export default function CampusCopilot() {
  const [today, setToday] = useState(format(new Date(), "yyyy-MM-dd"));
  const [filteredEvents, setFilteredEvents] = useState([]);

  useEffect(() => {
    const upcoming = events.filter((event) => event.date >= today);
    setFilteredEvents(upcoming);
  }, [today]);

  return (
    <div className="p-4 max-w-3xl mx-auto">
      <h1 className="text-2xl font-bold mb-4">Campus Copilot</h1>
      <p className="mb-6 text-gray-600">Your Personal College Assistant</p>
      <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
        {filteredEvents.map((event, index) => (
          <Card key={index} className="shadow-md">
            <CardContent className="flex items-center gap-4 p-4">
              <div>{iconMap[event.type]}</div>
              <div>
                <h3 className="font-semibold text-lg">{event.title}</h3>
                <p className="text-sm text-gray-500">
                  {event.date} {event.time && `at ${event.time}`}
                </p>
                {event.location && (
                  <p className="text-sm text-gray-500">Location: {event.location}</p>
                )}
              </div>
            </CardContent>
          </Card>
        ))}
      </div>
      <div className="mt-6 text-center">
        <Button>Sync with Google Calendar</Button>
      </div>
    </div>
  );
}




<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Campus Copilot</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Inter', sans-serif;
      margin: 0;
      padding: 0;
      background: #f4f6fa;
      color: #333;
    }

    header {
      background: #2e7d32;
      color: white;
      padding: 1rem 2rem;
      text-align: center;
      font-size: 1.5rem;
      font-weight: 600;
    }

    .container {
      display: grid;
      grid-template-columns: 1fr 3fr;
      gap: 20px;
      padding: 2rem;
    }

    .sidebar {
      background: white;
      padding: 1rem;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }

    .content {
      background: white;
      padding: 1rem;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }

    .section {
      margin-bottom: 1.5rem;
    }

    .section h2 {
      font-size: 1.25rem;
      margin-bottom: 0.5rem;
    }

    input, select, button {
      width: 100%;
      padding: 0.5rem;
      margin-top: 0.5rem;
      margin-bottom: 1rem;
      border-radius: 8px;
      border: 1px solid #ccc;
    }

    button {
      background-color: #2e7d32;
      color: white;
      font-weight: 600;
      cursor: pointer;
    }

    .reminder-list {
      list-style-type: none;
      padding: 0;
    }

    .reminder-item {
      background: #e8f5e9;
      margin-bottom: 0.5rem;
      padding: 0.75rem;
      border-radius: 8px;
    }
  </style>
</head>

<body>
  <header>Campus Copilot – Your Personal College Assistant</header>
  <div class="container">
    <div class="sidebar">
      <div class="section">
        <h2>Add Reminder</h2>
        <input type="text" id="title" placeholder="Reminder Title">
        <input type="datetime-local" id="datetime">
        <button onclick="addReminder()">Add</button>
      </div>
      <div class="section">
        <h2>Upcoming Reminders</h2>
        <ul id="reminderList" class="reminder-list"></ul>
      </div>
    </div>
    <div class="content">
      <div class="section">
        <h2>College Notices</h2>
        <p>- Midterm results released</p>
        <p>- New event: Tech Fest 2025 (Aug 1)</p>
      </div>
      <div class="section">
        <h2>Club Events</h2>
        <p>- Robotics Club Meet: July 25, 4 PM</p>
        <p>- Literary Club Debate: July 27, 2 PM</p>
      </div>
      <div class="section">
        <h2>Class Schedule</h2>
        <p>- Mon 9 AM: DBMS</p>
        <p>- Tue 11 AM: AI/ML</p>
        <p>- Wed 1 PM: Web Development</p>
      </div>
    </div>
  </div>

  <script>
    function addReminder() {
      const title = document.getElementById("title").value;
      const datetime = document.getElementById("datetime").value;

      if (!title || !datetime) {
        alert("Please enter both title and date/time");
        return;
      }

      const reminderList = document.getElementById("reminderList");
      const li = document.createElement("li");
      li.className = "reminder-item";
      li.textContent = `${title} – ${new Date(datetime).toLocaleString()}`;
      reminderList.appendChild(li);

      // Clear inputs
      document.getElementById("title").value = "";
      document.getElementById("datetime").value = "";

      // Optional: set system notification (only works if granted)
      if ("Notification" in window && Notification.permission === "granted") {
        setTimeout(() => {
          new Notification("Reminder: " + title);
        }, new Date(datetime) - new Date());
      }
    }

    // Ask for notification permission
    if ("Notification" in window && Notification.permission !== "granted") {
      Notification.requestPermission();
    }
  </script>
</body>

</html>

