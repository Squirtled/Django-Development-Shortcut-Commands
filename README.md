
# Django Development Shortcut Commands

This README provides instructions on setting up and using a series of shortcut commands for common Django tasks. These commands are defined in your `.zshrc` file to streamline your Django development process.

## Setting Up the Commands

1. **Open Your `.zshrc` File:**

   ```bash
   nano ~/.zshrc
   ```

2. **Add the Following Functions:**

   Copy and paste the following functions into your `.zshrc` file:

   ```bash
   function runserver() {
       local port=${1:-8000}
       python manage.py runserver 0.0.0.0:$port
   }

   function migrate() {
       python manage.py makemigrations
       python manage.py migrate
   }

   function createsuperuser() {
       python manage.py createsuperuser
   }

   function collectstatic() {
       python manage.py collectstatic --noinput
   }

   function djangoshell() {
       python manage.py shell
   }

   function clearmigrations() {
       local app=${1}
       if [ -z "$app" ]; then
           echo "Please specify an app name."
       else
           find ./$app/migrations -path "*/migrations/*.py" -not -name "__init__.py" -delete
           find ./$app/migrations -path "*/migrations/*.pyc"  -delete
       fi
   }

   function runtests() {
       python manage.py test
   }

   function makemigrations() {
       local app=${1}
       if [ -z "$app" ]; then
           python manage.py makemigrations
       else
           python manage.py makemigrations $app
       fi
   }

   function showmigrations() {
       python manage.py showmigrations
   }

   function startapp() {
       local app=${1}
       if [ -z "$app" ]; then
           echo "Please specify an app name."
       else
           python manage.py startapp $app
       fi
   }

   function check() {
       python manage.py check
   }

   function dbshell() {
       python manage.py dbshell
   }
   ```

3. **Save and Close the `.zshrc` File:**

   - Save the file by pressing `CTRL + O`, then press `Enter` to confirm.
   - Close the file by pressing `CTRL + X`.

4. **Reload Your `.zshrc` File:**

   To apply the changes, reload your `.zshrc` file by running:

   ```bash
   source ~/.zshrc
   ```

## Usage

### Running the Django Development Server

```bash
runserver [port]
```
- `port` (optional): The port number to run the server on. Defaults to 8000.

### Running Migrations

```bash
migrate
```
Runs `makemigrations` and `migrate`.

### Creating a Superuser

```bash
createsuperuser
```
Creates a new superuser account.

### Collecting Static Files

```bash
collectstatic
```
Collects static files without requiring input.

### Opening the Django Shell

```bash
djangoshell
```
Opens the Django interactive shell.

### Clearing Migrations

```bash
clearmigrations [app]
```
- `app`: The name of the app whose migrations you want to clear.

### Running Tests

```bash
runtests
```
Runs the test suite.

### Making Migrations for a Specific App

```bash
makemigrations [app]
```
- `app` (optional): The name of the app to make migrations for. If not specified, runs `makemigrations` for all apps.

### Showing Migrations

```bash
showmigrations
```
Shows the status of all migrations.

### Starting a New App

```bash
startapp [app]
```
- `app`: The name of the new app to create.

### Checking for Errors

```bash
check
```
Checks the project for any errors.

### Opening the Database Shell

```bash
dbshell
```
Opens the database shell.

## Contribution

Feel free to contribute by suggesting new shortcuts or improvements to existing ones!

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
