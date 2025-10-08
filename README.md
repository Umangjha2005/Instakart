# InstaKart E‑Commerce Web Application

This repository contains the source code and configuration for the **InstaKart** mini project.  InstaKart is a full‑stack e‑commerce web application that lets users browse clothing products, add items to a shopping cart and place orders.  The application is built with **React** on the front‑end and **Spring Boot** on the back‑end, with **MySQL** used as the relational database.  This README provides setup instructions, dependency information and guidelines for hosting the project on GitHub.

## Contents

The project is organized into two main directories:

* `backend/` – Spring Boot project containing REST controllers, services, entities and configuration files.
* `frontend/` – React application containing components, pages and client‑side routing.

In addition, a `database` directory can store SQL scripts for creating the schema and seeding sample data.

## Prerequisites

To build and run the project locally you will need the following software installed:

1. **Java Development Kit (JDK) 17 or later** – Spring Boot is built on the Java platform.  Download from [Adoptium](https://adoptium.net/) or [Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
2. **Node.js and npm** – Required to build and run the React front‑end.  Download from [nodejs.org](https://nodejs.org/).  The project was tested with Node.js 18 and npm 8.
3. **MySQL Server** – A relational database engine.  Install MySQL 8 and create a database (e.g., `instakart_db`) with a user and password.
4. **Git** – Used for version control and hosting the project on GitHub.

## Configuration

### MySQL Database

1. Start your MySQL server and create a new database:

   ```sql
   CREATE DATABASE instakart_db;
   CREATE USER 'instakart_user'@'localhost' IDENTIFIED BY 'strong_password';
   GRANT ALL PRIVILEGES ON instakart_db.* TO 'instakart_user'@'localhost';
   FLUSH PRIVILEGES;
   ```

2. Import the provided SQL schema (if available):

   ```sh
   mysql -u instakart_user -p instakart_db < database/schema.sql
   ```

3. Optionally seed the database with sample products using `database/sample_data.sql`.

### Back‑End (Spring Boot)

1. Navigate to the `backend` directory:

   ```sh
   cd backend
   ```

2. Copy the `.env.example` file to `.env` and update database credentials and JWT secrets:

   ```sh
   cp .env.example .env
   # Edit .env to set SPRING_DATASOURCE_URL, USERNAME, PASSWORD, JWT_SECRET, etc.
   ```

3. Build and run the application using Maven or Gradle.  For Maven:

   ```sh
   ./mvnw clean package
   java -jar target/instakart-0.0.1-SNAPSHOT.jar
   ```

   The API will start on `http://localhost:8080`.

### Front‑End (React)

1. Open a new terminal and navigate to the `frontend` directory:

   ```sh
   cd frontend
   ```

2. Install dependencies using npm:

   ```sh
   npm install
   ```

3. Copy the `.env.example` file to `.env` and set the API base URL.  For local development the URL should be `http://localhost:8080/api`.

4. Start the development server:

   ```sh
   npm start
   ```

   The React app will run on `http://localhost:3000` and proxy API requests to the Spring Boot server.

## Running the Application

After completing the configuration steps above, you can run both the back‑end and front‑end concurrently:

1. **Start MySQL** – ensure the MySQL service is running and accessible.
2. **Launch Spring Boot** – in the `backend` directory run the jar file as shown above.  The API should be reachable on `http://localhost:8080/api`.
3. **Launch React** – in the `frontend` directory run `npm start`.  The client will open in your default browser.  You can browse products, register as a user, add items to your cart and complete a checkout using the mock payment gateway.

## Deploying and Hosting

### Hosting on GitHub

1. Create a new repository on [GitHub](https://github.com/new).  Name it `instakart` or another descriptive name.
2. Initialize the repository locally in the project root:

   ```sh
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin https://github.com/<your-username>/<repo-name>.git
   git branch -M main
   git push -u origin main
   ```

3. Your code will now be hosted on GitHub.  You can share the repository link with your instructor or collaborators.  Update the repository’s README if you make changes to setup or dependencies.

### Deploying to a Server

For production deployment, consider packaging the back‑end as a Docker image and serving the front‑end as static files:

1. **Dockerize the back‑end:** create a `Dockerfile` in the `backend` directory that copies the jar file and runs it.  Use a multi‑stage build to minimize the image size.
2. **Build the React app:** run `npm run build` in the `frontend` directory.  This creates a `build/` folder containing static files.
3. **Serve the front‑end:** use an Nginx container or a static hosting service such as Netlify or Vercel.  Copy the contents of `build/` to the web server’s root.
4. **Database:** host the MySQL database on a managed service like Amazon RDS, or run it in a Docker container.  Update your environment variables to point to the production database.

Alternatively, you can deploy the entire stack to cloud platforms such as **Heroku**, **AWS Elastic Beanstalk** or **Azure App Service**.  These platforms provide managed services for Java applications and databases.

## Zipped Source Code

If your instructor requires a zipped copy of the project, compress the entire repository (excluding node_modules and target folders) into a zip file.  On Linux/macOS:

```sh
zip -r instakart_project.zip . -x "*/node_modules/*" -x "*/target/*" -x "*.env"
```

Submit `instakart_project.zip` or upload it to your GitHub repository’s releases section.

## Contributing

Forks and pull requests are welcome.  Feel free to open issues or suggest improvements.

## License

Specify a license for your project (e.g., MIT, Apache 2.0) in a `LICENSE` file.
