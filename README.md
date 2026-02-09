<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Northview College | Events</title>

<style>

body {
    margin: 0;
    font-family: "Segoe UI", sans-serif;
    background: #0f172a;
    color: #e5e7eb;
}


header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 30px;
    background: #020617;
    border-bottom: 2px solid #14b8a6;
}

.brand {
    display: flex;
    align-items: center;
}

.brand img {
    margin-right: 12px;
}

nav a {
    color: #e5e7eb;
    margin-left: 20px;
    text-decoration: none;
    font-weight: 500;
}

nav a:hover {
    color: #14b8a6;
}


.filters {
    display: flex;
    gap: 12px;
    padding: 20px 30px;
    background: #020617;
}

.filters input,
.filters select {
    padding: 10px;
    background: #020617;
    border: 1px solid #14b8a6;
    color: #e5e7eb;
    border-radius: 6px;
}


.events {
    padding: 30px;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 20px;
}

.event-card {
    background: #020617;
    border: 1px solid #14b8a6;
    padding: 20px;
    border-radius: 10px;
    transition: transform 0.3s;
}

.event-card:hover {
    transform: translateY(-5px);
}

.event-card h3 {
    color: #14b8a6;
}

.event-card button {
    margin-top: 12px;
    padding: 10px;
    width: 100%;
    background: #14b8a6;
    border: none;
    color: #020617;
    font-weight: bold;
    cursor: pointer;
    border-radius: 6px;
}


.pagination {
    text-align: center;
    margin-bottom: 30px;
}

.pagination button {
    padding: 8px 16px;
    background: #14b8a6;
    border: none;
    color: #020617;
    font-weight: bold;
    margin: 0 5px;
    border-radius: 6px;
}


footer {
    background: #020617;
    text-align: center;
    padding: 20px;
    border-top: 2px solid #14b8a6;
}

footer a {
    color: #14b8a6;
    margin: 0 10px;
    text-decoration: none;
}
</style>
</head>

<body>


<header>
    <div class="brand">
        <img src="https://via.placeholder.com/45" alt="Logo">
        <h2>Northview College</h2>
    </div>
    <nav>
        <a href="#">Home</a>
        <a href="#">Events</a>
        <a href="#">Admissions</a>
        <a href="#">Contact</a>
    </nav>
</header>


<section class="filters">
    <input type="text" id="searchInput" placeholder="Search events...">
    <select id="categoryFilter">
        <option value="All">All Categories</option>
        <option value="Sports">Sports</option>
        <option value="Workshop">Workshop</option>
        <option value="Guest Lecture">Guest Lecture</option>
    </select>
    <select id="dateFilter">
        <option value="All">All Dates</option>
        <option value="Today">Today</option>
        <option value="Week">This Week</option>
    </select>
</section>


<section id="eventsContainer" class="events"></section>


<div class="pagination">
    <button onclick="prevPage()">Previous</button>
    <span id="pageInfo"></span>
    <button onclick="nextPage()">Next</button>
</div>


<footer>
    <p>📞 +91 98765 43210 | ✉ info@northviewcollege.edu</p>
    <a href="#">LinkedIn</a>
    <a href="#">Facebook</a>
    <a href="#">Twitter</a>
</footer>

<script>

const events = [
    { title: "Football Tournament", date: "2026-02-06", category: "Sports", description: "Inter-college football championship" },
    { title: "AI Workshop", date: "2026-02-08", category: "Workshop", description: "Hands-on artificial intelligence training" },
    { title: "Cybersecurity Talk", date: "2026-02-10", category: "Guest Lecture", description: "Expert insights from industry leaders" },
    { title: "Basketball League", date: "2026-02-12", category: "Sports", description: "Annual college basketball league" },
    { title: "Web Dev Bootcamp", date: "2026-02-15", category: "Workshop", description: "Frontend & backend essentials" },
    { title: "Startup Guest Talk", date: "2026-02-18", category: "Guest Lecture", description: "Entrepreneurship guidance" }
];

let currentPage = 1;
const perPage = 5;


function filterEvents() {
    let filtered = [...events];
    const search = searchInput.value.toLowerCase();
    const cat = categoryFilter.value;
    const dateOpt = dateFilter.value;
    const today = new Date();

    filtered = filtered.filter(e =>
        e.title.toLowerCase().includes(search) || e.date.includes(search)
    );

    if (cat !== "All") filtered = filtered.filter(e => e.category === cat);

    if (dateOpt === "Today") {
        filtered = filtered.filter(e => new Date(e.date).toDateString() === today.toDateString());
    }

    if (dateOpt === "Week") {
        filtered = filtered.filter(e => {
            const diff = (new Date(e.date) - today) / (1000*60*60*24);
            return diff >= 0 && diff <= 7;
        });
    }

    renderEvents(filtered);
}

function renderEvents(list) {
    eventsContainer.innerHTML = "";
    const start = (currentPage - 1) * perPage;
    list.slice(start, start + perPage).forEach(e => {
        eventsContainer.innerHTML += `
            <div class="event-card">
                <h3>${e.title}</h3>
                <p><b>Date:</b> ${e.date}</p>
                <p>${e.description}</p>
                <button>View Details</button>
            </div>
        `;
    });
    pageInfo.textContent = `Page ${currentPage}`;
}

function nextPage() { currentPage++; filterEvents(); }
function prevPage() { if (currentPage > 1) currentPage--; filterEvents(); }

searchInput.oninput = categoryFilter.onchange = dateFilter.onchange = () => {
    currentPage = 1;
    filterEvents();
};

filterEvents();
</script>

</body>
</html>
# North-View-College-Event
