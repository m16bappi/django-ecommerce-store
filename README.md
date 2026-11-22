# Django E-commerce Store

A full-stack e-commerce web app built with Django. Customers can browse a product catalog, pick product variations, manage a cart, register and log in, and check out with PayPal. Orders and payments are recorded per user.

![Python](https://img.shields.io/badge/Python-3-3776AB?logo=python&logoColor=white)
![Django](https://img.shields.io/badge/Django-3.2-092E20?logo=django&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?logo=sqlite&logoColor=white)
![Heroku](https://img.shields.io/badge/Heroku-ready-430098?logo=heroku&logoColor=white)

## Features

- **Product catalog**: products grouped by category, with stock tracking, images and slug-based URLs
- **Variations**: color and size options per product, carried into the cart and order
- **Search**: keyword search across products
- **Cart**: add, decrease and remove items; works for guests and logged-in users; item count shown site-wide
- **Accounts**: custom user model, registration with email activation link, login/logout, password reset by email, user dashboard
- **Checkout**: billing details form, order summary, PayPal payment, order confirmation page
- **Orders and payments**: order status (new, accepted, completed, cancelled) and payment records linked to each user
- **Admin**: manage products, categories, variations, carts, orders and users through the Django admin

## Tech stack

| Layer | Tools |
|---|---|
| Backend | Python, Django 3.2 |
| Frontend | Django templates, HTML, CSS, JavaScript |
| Forms | django-crispy-forms |
| Database | SQLite (development) |
| Media | Pillow for product images |
| Deployment | Gunicorn, WhiteNoise, Heroku `Procfile` |
| Payments | PayPal |

## Project structure

```
pycom/      project settings and root URLs
core/       home page
store/      products, variations, search, product details
category/   product categories
carts/      cart and cart items, checkout page
accounts/   custom user model, auth, activation, password reset, dashboard
orders/     orders, payments, order completion
context/    context processors (category menu, cart item count)
templates/  HTML templates
static/     CSS, JS, fonts, images
```

## Getting started

```bash
git clone https://github.com/m16bappi/django-ecommerce-store.git
cd django-ecommerce-store

python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt

python manage.py migrate
python manage.py createsuperuser
python manage.py runserver
```

Open http://127.0.0.1:8000. Add categories and products from http://127.0.0.1:8000/admin.

To send activation and password-reset emails, set `EMAIL_HOST_USER` and `EMAIL_HOST_PASSWORD` in `pycom/settings.py` (Gmail SMTP is configured by default).

## Main routes

| URL | Page |
|---|---|
| `/` | Home |
| `/store/` | All products |
| `/store/<category>/` | Products in a category |
| `/store/<category>/<product>/` | Product details |
| `/store/search/` | Search results |
| `/cart/` | Cart |
| `/cart/checkout/` | Checkout |
| `/accounts/register/`, `/accounts/login/` | Sign up and sign in |
| `/accounts/dashboard/` | User dashboard |
| `/orders/` | Place order and pay |

## Deployment

The repo includes a `Procfile` for Heroku:

```
web: gunicorn pycom.wsgi --log-file -
```

WhiteNoise serves compressed static files in production. Run `python manage.py collectstatic` before deploying.
