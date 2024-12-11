Application Documentation
1 Application Documentation
1.1 1. Setup Instructions
1.1.1 Prerequisites:
Before setting up the application, make sure you have the following tools installed:
• Node.js (version 14 or higher)
• npm (Node Package Manager)
• Vue.js (for the frontend)
• Express (for the backend)
• Mongoose (for MongoDB integration)
• ECharts (for visualizations)
• OAuth 2.0 Authentication setup (for API security)
1.1.2 Steps to Set Up the Application:
Frontend Setup:
1. Clone the repository:
git clone <repository-url>
cd <repository-directory>
2. Install dependencies: Navigate to the frontend directory and install all required dependencies
using npm.
cd frontend
npm install
3. Run the development server:
npm run serve
4. The application should now be accessible in your browser at http://localhost:8080.
1
Backend Setup:
1. Clone the repository: Same as frontend setup, clone the repository and navigate to the backend
directory.
2. Install dependencies: In the backend directory, install dependencies:
cd backend
npm install
3. Set up the environment variables: Create a .env file in the backend directory and add the
necessary variables:
MONGO_URI=<your-mongodb-connection-string>
OAUTH_CLIENT_ID=<your-oauth-client-id>
OAUTH_CLIENT_SECRET=<your-oauth-client-secret>
OAUTH_REDIRECT_URI=<your-oauth-redirect-uri>
4. Run the backend server:
npm start
5. The backend should be running on http://localhost:3000.
1.2 2. API Documentation
1.2.1 OAuth 2.0 Authentication
The application uses OAuth 2.0 for secure API access. Here’s how you can authenticate and access the
protected endpoints:
• Authorization URL: GET /auth/authorize
• Token URL: POST /auth/token
– Client ID: Provided in the .env file.
– Client Secret: Provided in the .env file.
– Scope: Define the required access scope for your application.
– Redirect URI: A URI that the OAuth provider will redirect users to after successful authen-
tication.
OAuth 2.0 Flow:
1. Authorize the user via the /auth/authorize endpoint.
2. Once the user is authenticated, the OAuth provider will redirect to the redirect URI.
3. Exchange the authorization code for an access token via /auth/token.
4. Use the access token to authenticate requests to protected API endpoints.
2
1.2.2 API Endpoints
1. POST /api/sites
• Description: Adds or updates a site.
• Request Body:
{
"site_id": "unique-site-id",
"site_name": "Site Name",
"parent_site": "Parent Site",
"status": "active",
"region": "Region Name",
"technology": "Technology",
"latitude": 12.345678,
"longitude": 98.7654321
}
2. GET /api/sites
• Description: Fetches all the sites.
• Response:
[
{
"site_id": "unique-site-id",
"site_name": "Site Name",
"parent_site": "Parent Site",
"status": "active",
"region": "Region Name",
"technology": "Technology",
"latitude": 12.345678,
"longitude": 98.7654321
}
]
3. GET /api/posts
• Description: Fetches posts data for analytics.
• Response:
[
{
"id": 1,
"region": "Region A",
"status": "active",
"technology": "5G",
"site_id": "unique-site-id"
}
]
3
4. GET /api/analytics
• Description: Retrieves analytics data.
• Response:
{
"status_trends": [10, 15, 5],
"technology_adoption": [30, 40, 30],
"region_distribution": [15, 20, 10]
}
5. POST /api/login
• Description: Logs in the user using OAuth 2.0 credentials.
• Request Body:
{
"oauth_token": "<access-token>"
}
1.3 3. Code Comments
Frontend:
• In the WelcomePage.vue, we have buttons (<router-link>) to navigate to different pages such as
posts, topology, and analytics. Each button is styled using scoped CSS for better visual appeal.
• The AnalyticsPage.vue uses echarts for creating dynamic charts to visualize data. Each chart
function (createRegionDistributionChart(), etc.) collects the data from the backend and ren-
ders it on the frontend using ECharts.
Backend:
• The backend API routes such as /api/sites, /api/posts, and /api/analytics are defined using
Express.
• The routes interact with a MongoDB database to fetch and manipulate data. OAuth authentication
ensures only authorized users can access certain endpoints.
1.4 4. Known Limitations
• Scalability: The application currently uses a single server for both frontend and backend. As
the number of users grows, a more distributed system (such as microservices) will be needed for
scalability.
• OAuth Integration: The OAuth implementation is relatively simple and does not support com-
plex use cases like multiple OAuth providers or role-based access control (RBAC).
• Data Visualization Limitations: Some visualizations may fail to update dynamically based on
large datasets. This can be addressed by implementing more efficient data-fetching strategies (e.g.,
lazy loading).
• Cross-Browser Compatibility: While the frontend works well on modern browsers, older
browsers (e.g., Internet Explorer) may face issues due to reliance on modern JavaScript and CSS.
4
1.5 5. Future Improvement Suggestions
• Enhanced Data Visualization: Implement real-time data updates for charts and graphs. In-
clude more chart types (e.g., heatmaps, line charts) for different analytics.
• API Security: Improve OAuth security with features like refresh tokens and scope-based access
for finer-grained control. Add rate limiting and logging for better monitoring of API access.
• Frontend User Experience: Implement a responsive design to improve user experience across
mobile devices. Add more dynamic UI elements, such as loading indicators when fetching data.
• Backend Performance: Use pagination and caching for endpoints like /api/sites to handle
large datasets efficiently. Implement background tasks for data processing to avoid blocking user
requests.
• OAuth 2.0 Improvements: Support multiple OAuth providers (e.g., Google, Facebook) for
authentication to allow more flexibility for users. Implement a role-based access control (RBAC)
system to provide different permissions for different users.
