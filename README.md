# Fan Hub Plus — Laravel End-to-End

Fan Hub Plus is implemented as a Laravel 11 application using the supplied Fan Hub Plus UI/UX as the public visual layer and the existing DB-connected Admin Panel as the administration layer.

## Stack
- Laravel 11
- PHP 8.2+
- MySQL
- Blade views for the supplied public UI
- HTML5 / CSS3 / JavaScript / Font Awesome
- Laravel sessions and CSRF protection

## Important: UI preservation
The supplied frontend design has been preserved. The original HTML pages are now Laravel Blade views under `resources/views/site/`, while the original CSS, JavaScript, images and other frontend assets remain under `public/site/assets/`.

Public page URLs intentionally remain `/site/*.html` so existing relative asset paths and frontend navigation continue to work.

## Main flows
- Visitor browsing across fandom pages
- Login / registration
- Database-backed search
- Database-backed articles and article details
- Events and event API
- Characters and character API
- Merchandise API
- User dashboard/profile
- Favorite fandom categories
- Bookmarks
- Fan submissions with admin approval/rejection
- Feedback with admin management
- Media ratings (1–5)
- Password reset using a database-backed 15-minute tokenized link
- Admin content management
- Admin analytics, notifications, settings, chatbot FAQ and release management
- Dynamic sitemap at `/sitemap.xml`

## Installation
1. Create a MySQL database named `fan_hub_plus` (or change `.env`).
2. Copy `.env.example` to `.env` if needed.
3. Set `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD` for your MySQL installation.
4. Run:

```bash
composer install
php artisan key:generate
php artisan migrate --seed
php artisan storage:link
php artisan optimize:clear
php artisan serve
```

5. Open:
- Public site: `http://127.0.0.1:8000/`
- User login: `http://127.0.0.1:8000/site/login.html`
- Admin login: `http://127.0.0.1:8000/admin/login`
- Sitemap: `http://127.0.0.1:8000/sitemap.xml`

## Seed credentials
Admin:
- Email: `admin@fanhubplus.com`
- Password: `password`

Test user:
- Email: `test@example.com`
- Password: `password`

Change these credentials before deployment.

## SRS alignment
The implementation covers the SRS core scope: authentication/session management, personalized dashboard, category-based content exploration, search, multimedia/content administration, character profiles, articles, events, merchandise showcase, feedback, bookmarks, fan submissions, admin control, dark/light UI support, responsive UI, and sitemap. Optional AI chatbot functionality is represented through the existing FAQ/knowledge-base administration and frontend bot UI.

The SRS explicitly states that merchandise is display/discovery only and does not require actual purchasing, payment or order processing; therefore no checkout/payment workflow is included.

## Database
Laravel migrations are the authoritative schema files. The database includes users, categories, content, articles, characters, events, merchandise, bookmarks, ratings, feedback, fan submissions, chatbot queries/FAQs, view logs and admin support tables.

## Notes
- SMTP is not required for local password reset testing. The reset endpoint generates a secure, time-limited tokenized URL; when deployed, this endpoint can be connected to SMTP/mail notifications.
- The project keeps the Admin UI and public Fan Hub UI visually isolated so admin CSS does not overwrite public-site CSS.
