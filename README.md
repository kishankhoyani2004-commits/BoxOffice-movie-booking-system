# 🎬 BoxOffice - Movie Booking System

<img width="1349" height="1308" alt="1" src="https://github.com/user-attachments/assets/967e9174-4bdf-49cb-ac0f-39e0a5237e42" />
<img width="1366" height="642" alt="2" src="https://github.com/user-attachments/assets/8380385e-603a-497d-aba3-8d571d05610d" />
<img width="1349" height="642" alt="3" src="https://github.com/user-attachments/assets/1db41cd8-7240-492c-ae6e-e3c1d8f0c1a2" />


> A full-featured online movie ticket booking web application built with **Django** and **MySQL**. Users can browse movies, select showtimes, choose seats, and book tickets — while cinema managers can manage shows, track earnings, and handle their dashboard.

---

## 📌 Table of Contents

- [About the Project](#-about-the-project)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [Screenshots](#-screenshots)
- [Database Models](#-database-models)
- [Contributing](#-contributing)
- [License](#-license)

---

## 📖 About the Project

**BoxOffice** is a web-based movie ticket booking system that allows two types of users:

- **Regular Users** – Browse movies, select showtimes, pick seats, book tickets, and manage their bookings.
- **Cinema Managers** – Register their cinema, add movie shows, manage schedules, and track earnings via a dedicated dashboard.

The project focuses on a real-world booking workflow — from movie discovery all the way to ticket generation.

---

## 🚀 Features

### 👤 For Users
- 🔐 User Registration & Login
- 🎥 Browse all available movies with posters, ratings, genres & trailers
- 📅 View showtimes by cinema and date
- 🪑 Interactive seat selection (see booked vs available seats)
- 🎟️ Book tickets and get instant confirmation
- 📋 View all past and upcoming bookings
- 👤 Edit profile and change password

### 🏢 For Cinema Managers
- 🏟️ Register cinema with name, city, address & phone
- ➕ Add movie shows with time, date & ticket price
- 📊 Dashboard to view all active shows by movie
- 💰 Earnings page with total revenue from bookings

### 🔧 Admin Panel
- Manage movies, cinemas, shows, and bookings via Django Admin

---

## 🛠️ Tech Stack

| Layer       | Technology              |
|-------------|-------------------------|
| Backend     | Python, Django 2.2      |
| Frontend    | HTML5, CSS3, JavaScript |
| Database    | MySQL                   |
| ORM         | Django ORM              |
| Auth        | Django Built-in Auth    |
| Deployment  | Gunicorn (Heroku-ready) |
| Config      | python-decouple, dotenv |

---

## 📁 Project Structure

```
BoxOffice-movie-booking-system/
│
├── BoxOffice/               # Project settings & main URL config
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
├── accounts/                # User & Cinema Manager app
│   ├── models.py            # Cinema, Movie, Shows, Bookings models
│   ├── views.py             # Login, Register, Profile, Dashboard, Earnings
│   └── urls.py
│
├── main/                    # Public-facing app
│   ├── views.py             # Index, Movie detail, Seat selection, Booking
│   └── urls.py
│
├── templates/               # HTML templates
│   ├── base.html
│   ├── index.html
│   ├── movies.html
│   ├── seat.html
│   ├── booked.html
│   ├── ticket.html
│   ├── dashboard.html
│   ├── earnings.html
│   ├── bookings.html
│   ├── profile.html
│   ├── login.html
│   ├── register.html
│   └── register_cinema.html
│
├── static/                  # CSS styles and images
│   ├── styles/
│   └── images/
│
├── media/                   # Uploaded movie posters
├── manage.py
├── requirements.txt
├── Procfile
└── .gitignore
```

---

## ⚙️ Getting Started

### ✅ Prerequisites

Make sure you have the following installed:
- Python 3.x
- MySQL Server
- pip
- virtualenv

---

### 📦 Installation

**1. Clone the repository**
```bash
git clone https://github.com/YOUR-USERNAME/BoxOffice-movie-booking-system.git
cd BoxOffice-movie-booking-system
```

**2. Create and activate a virtual environment**
```bash
python -m venv venv

# Windows
venv\Scripts\activate

# Mac/Linux
source venv/bin/activate
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Set up the database**

Create a MySQL database:
```sql
CREATE DATABASE boxoffice;
```

**5. Configure environment variables**

Create a `.env` file in the root directory:
```env
SECRET_KEY=your-secret-key-here
DEBUG=True
DB_NAME=boxoffice
DB_USER=your-mysql-username
DB_PASSWORD=your-mysql-password
DB_HOST=localhost
DB_PORT=3306
```

**6. Update `settings.py`** with your database config (if not using `.env`):
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'boxoffice',
        'USER': 'your-username',
        'PASSWORD': 'your-password',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

**7. Run migrations**
```bash
python manage.py makemigrations
python manage.py migrate
```

**8. Create a superuser (Admin)**
```bash
python manage.py createsuperuser
```

**9. Run the development server**
```bash
python manage.py runserver
```

Visit: **http://127.0.0.1:8000**

---

## 🗃️ Database Models

### `Movie`
| Field          | Type        | Description              |
|----------------|-------------|--------------------------|
| movie_name     | CharField   | Name of the movie        |
| movie_des      | TextField   | Movie description        |
| movie_rating   | Decimal     | Rating out of 10         |
| movie_genre    | CharField   | Genre(s)                 |
| movie_duration | CharField   | Duration (e.g. 2hr 30min)|
| movie_poster   | ImageField  | Poster image             |
| movie_trailer  | CharField   | Trailer URL              |

### `Cinema`
| Field        | Type          | Description              |
|--------------|---------------|--------------------------|
| cinema_name  | CharField     | Name of the cinema       |
| city         | CharField     | City of the cinema       |
| address      | CharField     | Full address             |
| phoneno      | CharField     | Contact number           |
| user         | OneToOneField | Linked to Django User    |

### `Shows`
| Field   | Type        | Description                  |
|---------|-------------|------------------------------|
| cinema  | ForeignKey  | Linked cinema                |
| movie   | ForeignKey  | Linked movie                 |
| time    | CharField   | Show time                    |
| date    | CharField   | Show date                    |
| price   | IntegerField| Ticket price                 |

### `Bookings`
| Field  | Type       | Description                      |
|--------|------------|----------------------------------|
| user   | ForeignKey | Linked user                      |
| shows  | ForeignKey | Linked show                      |
| useat  | CharField  | Comma-separated booked seat IDs  |

---

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a new branch: `git checkout -b feature/your-feature-name`
3. Commit your changes: `git commit -m "Add your feature"`
4. Push to the branch: `git push origin feature/your-feature-name`
5. Open a Pull Request

---

## 📄 License

This project is for educational purposes only.

⭐ **If you found this project helpful, please give it a star!**
