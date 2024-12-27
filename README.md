# football-matches-<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="موقع فووتبوول - تابع نتائج المباريات وأهم الأخبار">
    <title>فووتبوول - مباريات مباشرة</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <header>
        <h1>فووتبوول</h1>
        <p>مرجعك الأول لمتابعة المباريات والأخبار الرياضية</p>
    </header>

    <main>
        <section id="live-scores">
            <h2>نتائج المباريات المباشرة</h2>
            <div id="scores-container">جاري تحميل النتائج...</div>
        </section>
        <section id="news">
            <h2>أهم الأخبار</h2>
            <div id="news-container">جاري تحميل الأخبار...</div>
        </section>
    </main>

    <footer>
        <p>حقوق النشر © 2024 فووتبوول. جميع الحقوق محفوظة.</p>
    </footer>

    <script src="app.js"></script>
</body>
</html>body {
    font-family: Arial, sans-serif;
    line-height: 1.6;
    margin: 0;
    padding: 0;
    background-color: #f4f4f4;
    color: #333;
}

header {
    text-align: center;
    background: #0056b3;
    color: white;
    padding: 20px 0;
}

h1 {
    margin: 0;
}

main {
    padding: 20px;
}

section {
    margin-bottom: 20px;
    padding: 10px;
    background: #fff;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

footer {
    text-align: center;
    padding: 10px;
    background: #0056b3;
    color: white;
    position: relative;
    bottom: 0;
    width: 100%;
}// رقم API الخاص بك
const apiKey = "0ba5c54383ad4be7b0d84d5f166fd1bb";

// تحميل نتائج المباريات
async function fetchScores() {
    const scoresContainer = document.getElementById("scores-container");
    try {
        const response = await fetch(`https://api.football-data.org/v2/matches`, {
            headers: {
                "X-Auth-Token": apiKey
            }
        });
        const data = await response.json();
        scoresContainer.innerHTML = "";
        data.matches.forEach(match => {
            const matchDiv = document.createElement("div");
            matchDiv.textContent = `${match.homeTeam.name} vs ${match.awayTeam.name} - ${match.score.fullTime.homeTeam}:${match.score.fullTime.awayTeam}`;
            scoresContainer.appendChild(matchDiv);
        });
    } catch (error) {
        scoresContainer.textContent = "تعذر تحميل النتائج. تحقق من الاتصال بالإنترنت أو رقم الـ API.";
    }
}

// تحميل الأخبار
async function fetchNews() {
    const newsContainer = document.getElementById("news-container");
    try {
        const response = await fetch(`https://newsapi.org/v2/top-headlines?category=sports&apiKey=${apiKey}`);
        const data = await response.json();
        newsContainer.innerHTML = "";
        data.articles.forEach(article => {
            const articleDiv = document.createElement("div");
            articleDiv.innerHTML = `<h3>${article.title}</h3><p>${article.description}</p>`;
            newsContainer.appendChild(articleDiv);
        });
    } catch (error) {
        newsContainer.textContent = "تعذر تحميل الأخبار. تحقق من الاتصال بالإنترنت أو رقم الـ API.";
    }
}

// استدعاء الدوال عند تحميل الصفحة
document.addEventListener("DOMContentLoaded", () => {
    fetchScores();
    fetchNews();
});
