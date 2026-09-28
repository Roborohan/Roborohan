## 👋 Hi, I'm Rohan

I'm currently on the **Digital Futures Frontier Academy** as a Data & AI Consultant, working towards the Certified Associate Data Analyst with Python (PCAD) after having achieved the Google Cloud's Generative AI Leader (GAIL) certification. Before that I spent a year and a half in IT support and QA Testing, and before that I read Computer Science at the University of Birmingham.

Most of what's here is project work, in the order I built it.

---

### 🎬 Beyond the Crowd Score — predicting one viewer's film ratings

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?style=flat&logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat&logo=streamlit&logoColor=white)
![Firestore](https://img.shields.io/badge/Firestore-FFCA28?style=flat&logo=firebase&logoColor=black)

*September 2026 · [Roborohan/Letterboxd-Regression-Capstone](https://github.com/Roborohan/Letterboxd-Regression-Capstone) · [live app](https://beyond-the-crowd-score.streamlit.app/)*

My capstone. Almost five years of my own Letterboxd ratings — 1,192 of them — enriched with TMDB metadata, to ask whether a model can predict what one person will think of a film better than the crowd score can, and say why.

The model is built up in layers, each knowing a little more: a constant, the crowd score alone, the film's details, my viewing history, then plot keywords. Tested on the 239 most recent films, held out by date so it never learns from my future, the final random forest is 0.111★ closer than the crowd score (95% CI 0.059–0.166) and ranks films nearly twice as well — while the crowd score on its own barely beats guessing the same rating every time. Because a forest's prediction is a weighted average of the films it learned from, the app can show which of my rated films each prediction leaned on.

The most useful result was the one that didn't flatter me. I packaged the steps into a pipeline and ran it on two friends' exports: one agrees with the crowd more than I do and gains nothing, and the other's gain can't be resolved on 426 films. Three people, three answers — the pipeline travels, the finding is one person's. The review text I spent real time on added nothing either.

That's why the app now lets anyone find out for themselves. Upload a Letterboxd export and the same pipeline runs on it in the background — TMDB matching, the full model ladder and its test against the crowd, the watchlist — usually in a few minutes, and every page of the app then shows your own films. It's one pipeline serving two front ends: the command line writes files, the app queues uploads and keeps results in Firestore under a private link. The export itself is never stored, results are deleted after 90 days unused, and film lookups go through a cache every upload shares, so each new one only fetches the films nobody has uploaded before.

A solo project: data collection and TMDB matching, the modelling, the portable pipeline, the Streamlit app, and the upload service behind it.

---

### 📞 Swan Teleco — churn prediction and customer risk scoring

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?style=flat&logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)

*September 2026 · [Bhumgara/df_swan_consulting](https://github.com/Bhumgara/df_swan_consulting)*

A churn model for a telecoms provider, built on a quarter of single customer view data covering 7,043 customers. It scores every remaining customer on their likelihood of leaving, ranks them for a targeted mailer campaign, and quantifies which products and contract types actually drive churn.

Logistic regression over 17 attributes, cross-validated at 0.856 AUC, chosen over a gradient boosted tree because the coefficients read directly as odds ratios — which is what turns a model into a recommendation about where to spend money. The outputs are a ranked list of the 500 highest-risk customers and a banded risk register for all 5,174, sorted for lookup so a service agent can find someone mid-call.

The most useful thing it surfaced was that price isn't the driver. Average revenue rises across the risk bands, which looks like high-value customers leaving — until you split by internet service and find that within fibre, the riskiest customers pay $85 a month and the safest $101. Fibre costs twice what DSL does and fills the high-risk bands, so the apparent price effect was really the product underneath it.

I built the model and both customer lists, and ran the driver analysis behind the product recommendations.

---

### 🌍 WHO Life Expectancy — modelling under a privacy constraint

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![statsmodels](https://img.shields.io/badge/statsmodels-4051B5?style=flat)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat&logo=streamlit&logoColor=white)

*August 2026 · [Roborohan/WHO-Life-Expectancy](https://github.com/Roborohan/WHO-Life-Expectancy)*

Two linear regression models estimating national life expectancy from WHO figures for 179 countries: one using every available statistic, and one with all health data withheld. A prediction function asks the user for consent and picks between them.

The full model beat the client's accuracy benchmark comfortably and the restricted one fell well short, which was expected. The interesting part was that the cost isn't shared evenly — the restricted model is several times worse for the countries with the lowest life expectancy than for the highest, and most of its predictive weight lands on regional dummies. A privacy-preserving model ends up substituting geography for evidence, and failing hardest where accuracy matters most.

I built the prediction functions, worked through the feature engineering, ran the cross-validation and analysed model performance.

---

### 🎤 EventIntelligence — UK touring markets for a developing act

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat&logo=streamlit&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-E97627?style=flat&logo=tableau&logoColor=white)

*August 2026 · [jb661/eventintelligence](https://github.com/jb661/eventintelligence)*

A dashboard for an artist management agency, built in two days against a live client brief. The premise: some cities are saturated with acts in a given genre while others are underserved, and live event data should be able to tell them apart.

Data comes from the Ticketmaster Discovery API through a standalone ingestion script, so the dashboard runs against current listings rather than a fixed snapshot. Saturation is measured with a location quotient comparing each city's share of a genre against the national share — which identifies a city under-programming a genre relative to the size of its own live scene, rather than just noticing that it isn't London.

I built the market size, genre concentration and venue activity pages, including the location quotient analysis.

---

### 🏦 Moneycraft — marketing spend analysis

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458?style=flat&logo=pandas&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-E97627?style=flat&logo=tableau&logoColor=white)

*July 2026 · [oum4r/df-moneycraft-G2](https://github.com/oum4r/df-moneycraft-G2)*

Three years of customer, spend and account closure data for a retail bank, with one question behind it: which acquisition channels are worth funding?

The difficulty was that recently acquired customers hadn't had time to leave yet, so the newest channels looked like the most loyal ones. We modelled retention with survival curves that account for how long each customer had actually been observed, then compared projected lifetime value against acquisition cost. The recommendation was to close the weakest channel, reinvest in referral and online, and retire an introductory fee waiver that turned out to be buying customers who left.

I produced two of the five findings, and was named best presenter at the showcase.

---

<details>
<summary><b>🎬 Ticket To Love</b> — film-matching dating app · <i>Oct 2022 – Apr 2023</i></summary>

<br>

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Django](https://img.shields.io/badge/Django-092E20?style=flat&logo=django&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat&logo=sqlite&logoColor=white)

[Roborohan/Ticket-To-Love](https://github.com/Roborohan/Ticket-To-Love)

A dating app that matches people on their taste in films rather than their photographs. Users build a list of favourites through the OMDb API, and a k-means clustering model groups them by taste to suggest matches, with an encrypted chat once two people connect.

My final-year project, and the one I learned the most from — largely because I rewrote it. The first version was an Express app, and partway through I moved the whole thing to Django to get a real user model and an admin interface rather than continuing to hand-roll them. Deciding to throw away two months of working code was harder than writing the replacement.

</details>

<details>
<summary><b>🎨 Doodl</b> — collaborative drawing app · <i>Mar – May 2022</i></summary>

<br>

![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat&logo=mongodb&logoColor=white)

[lianghuihe/Doodl-App](https://github.com/lianghuihe/Doodl-App)

A browser-based drawing app with user accounts, a public gallery, and likes and reporting on submitted doodles. Built in Node and Express with MongoDB by a nine-person team over six weeks, working to a set of client requirements.

My contribution ran to around 112 commits across the drawing canvas, the gallery and the account system. It was my first experience of a codebase big enough that nobody understood all of it, which turned out to be the useful part.

</details>

---

### Background

**University of Birmingham** — BSc Computer Science with Honours (2:1), 2020–2023. Machine Learning, Data Science, NLP, Software Development, Cyber Security.

**Personal Group** — IT Admin Support, 2024–2026. Ticket resolution across first and second line, client platform configuration and data migration, Jira administration, and a spell covering interim release management across full and hotfix deployments.

### Away from the screen

Films and TV, reading, music, racket sports, and travel. I write structured reviews of most of what I watch and read, which is either a hobby or a compulsion depending on who you ask.

### Get in touch

[LinkedIn](https://www.linkedin.com/in/rohan-sharma2001/)
