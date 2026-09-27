# Collaborative Editing in Syncfusion ASP.NET MVC PDF Viewer

This sample demonstrates real-time collaborative editing in the Syncfusion ASP.NET MVC PDF Viewer. It uses the Syncfusion Collaborator client library along with a Node.js Collaboration Server to synchronize PDF Viewer actions between multiple users in real time.

Users can collaborate on the same PDF room and see shared changes to:

- Annotations, such as comments, highlights, drawings, and stamps
- Form field interactions and value updates
- Page Organizer operations, such as page reordering and page changes

All users who need to collaborate must open the client with the same room ID.

## Prerequisites

- **Visual Studio 2019 / 2022** or **Visual Studio Code / Code Studio** with .NET Framework 4.7.2+ support / IIS Express
- **Node.js** 14 or later and **npm**
- A **Redis** instance reachable by the Collaboration Server
- Two or more browser tabs or windows for testing collaboration

## Project Structure

```text
Collaborative Editing/
├── Client/    # ASP.NET MVC PDF Viewer application (.NET Framework)
│   ├── Client.slnx
│   └── Client/
│       ├── Client.csproj
│       ├── Controllers/
│       │   └── HomeController.cs
│       └── Views/
│           └── Home/
│               └── Index.cshtml    # PDF Viewer and collaboration logic
└── Server/    # Node.js Collaboration Server and PDF storage APIs
```

## Run the Sample Locally

### 1. Start the Collaboration Server

Open a terminal window and navigate to the `Server` folder:

```bash
cd Server
npm install
npm start
```

The server listens on:

```text
http://localhost:8081
```

The client is configured to connect to this server in `Client/Client/Views/Home/Index.cshtml` via the `SERVICE_URL` setting:

```javascript
const SERVICE_URL = 'http://localhost:8081/';
```

If the server port or host changes, update `SERVICE_URL` in `Client/Client/Views/Home/Index.cshtml` to match.

### 2. Run the ASP.NET MVC Client

1. Open `Client/Client.slnx` or `Client/Client/Client.csproj` in **Visual Studio**.
2. Restore NuGet packages (right-click the Solution and select **Restore NuGet Packages**).
3. Build the solution (**Build** > **Build Solution** or `Ctrl+Shift+B`).
4. Run the application using **IIS Express** (**Debug** > **Start Without Debugging** or `Ctrl+F5`).

The application will launch in your default browser at a local IIS Express address, for example:

```text
http://localhost:port/
```

## Test Collaborative Editing

1. Open the application in the first browser tab or window.
2. The viewer will load the document and generate a unique room ID if none was specified. Check the collaboration status bar at the top or the browser URL. The room ID is passed as the `id` query parameter, for example:

   ```text
   http://localhost:port/?id=3tlfqgkp854
   ```

3. Copy the URL including the `?id=...` query parameter.
4. Open a second browser tab or window (or private/incognito window).
5. Paste the URL containing the same room ID:

   ```text
   http://localhost:port/?id=3tlfqgkp854
   ```

6. Verify that the collaboration status bar in both sessions indicates they are connected to the same room.
7. Perform actions in either browser session (add annotations, edit form fields, or organize pages) and verify that changes sync in real time across sessions.

If no `id` parameter is provided in the URL, a new room ID is automatically generated. Always share the full URL with the `?id=<room-id>` parameter so all participants join the same collaboration room.

## Collaboration Notes

- The room ID identifies the shared collaboration session. Users with different room IDs work in separate sessions.
- Keep the Node.js Collaboration Server running while testing real-time synchronization.
- The Collaboration Server uses Redis to persist and synchronize collaboration operations.
- For a hosted deployment, host the ASP.NET MVC application (e.g., in IIS or Azure App Service) and the Node.js Collaboration Server. Update `SERVICE_URL` in `Views/Home/Index.cshtml` to the hosted server URL and configure a shared Redis instance.
- Avoid using `localhost` in production client configurations because it resolves to the individual client machine.

## Useful Commands / Actions

| Component | Action | Description |
|---|---|---|
| `Server` | `npm install` | Install Collaboration Server dependencies |
| `Server` | `npm start` | Start the Collaboration Server on port 8081 |
| `Client` | Visual Studio Build / Run | Build and run the ASP.NET MVC application with IIS Express |
| `Client` | NuGet Restore | Restore NuGet packages defined in `packages.config` |

## Troubleshooting

- **The client cannot connect to collaboration:** Confirm that the Node.js server is running on port `8081` and that `SERVICE_URL` in `Client/Client/Views/Home/Index.cshtml` matches the server URL.
- **Users do not see each other's changes:** Confirm that both browser windows are using the exact same `?id=<room-id>` query parameter in the URL and that Redis is accessible to the server.
- **A new room is created automatically:** Ensure the URL includes `?id=<room-id>`. If omitted, the application generates a fresh room ID.
