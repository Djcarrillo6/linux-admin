# Composable Interactive Linux Information Dashboard

## Concept:
[PROTOTYPE]
   - Build an interactive SPA application that allows users to run/test a set of Linux commands by executing them in real-time on a securely connected network. The results are visualized in real-time in the web application that is running in the browser and users can interact with it by clicking a various text or UI elements which would trigger a pop-up, modal, or dialog box that explains the results in the context of teaching users about Linux command result analysis.
     - Composable in that users can create their own dashboard and customize it to their needs.
     - **This might be a secondary feature after the initial prototype is completed.**

## Key Features:
   ### Linux Networking Commands:
   1. **Real-Time Network Traffic Monitoring:**
      - Commands: `netstat`, `nmap`, `lsof`.
      - Display current network traffic, including active connections and data transfer rates.
      - Visualize inbound and outbound traffic on each network interface.
   
   2. **Open Ports and Services:**
      - List all open ports and the services listening on them.
      - Highlight critical ports commonly associated with security vulnerabilities.
   
   3. **Active Connections Visualization:**
      - Show active TCP and UDP connections.
      - Display connection details such as source and destination IP addresses, ports, and connection states.
   
   4. **Network Scanning and Analysis:**
      - Integrate `nmap` to perform network scans.
      - Provide detailed reports on discovered devices, open ports, and running services.
   
   5. **Alerts and Notifications:**
      - Set up alerts for specific network events, such as new open ports or unexpected traffic spikes.
      - Send notifications via email or SMS for critical alerts.
   
   6. **Historical Data and Trends:**
      - Store historical network data for trend analysis.
      - Display trends and patterns in network activity over time.
   
   7. **Customizable Dashboard:**
      - Allow users to customize the dashboard layout and select the metrics they want to monitor.
      - Provide multiple views, such as summary, detailed, and graphical representations.
   
   
   ### Linux Permissions Commands:
      1. **User Authentication:**
         - Enable user authentication and authorization.
         - Restrict access to certain commands based on user roles or permissions.
      
      2. **File Permissions:**
         - Set file permissions for specific files or directories.
         - Restrict access to certain files or directories based on user roles or permissions.
         - Enable users to manage their own files and directories.
         - Enable users to manage other users' files and directories.
      
      3. **Group Permissions:**
         - Set group permissions for specific groups.
         - Restrict access to certain groups based on user roles or permissions.
         - Enable users to manage their own groups.
         - Enable users to manage other users' groups.
   
   
   ### Frontend:
      1. **React:**
         - Build a responsive and interactive user interface using React.
         - Allow users to run/test Linux commands in real-time.
         - Provide visual representations of network traffic, active connections, open ports, and historical data.
         - Enable users to customize the dashboard layout and select the metrics they want to monitor.
         - Provide multiple views, such as summary, detailed, and graphical representations.
      
      2. **SignalR:**
         - Enable real-time communication between frontend and backend.
      
      3. **Grafana:**
         - Create detailed graphs and visualizations.
         - Enable users to customize the dashboard layout and select the metrics they want to monitor.


## Technologies:
   - **Frontend:** React for building a responsive and interactive user interface.
   - **Backend:** .NET Core for handling data processing, API creation, and user authentication.
   - **Database:** PostgreSQL for storing network data, configuration settings, and historical logs.
   - **Visualization:** Grafana for creating detailed graphs and visualizations.
   - **Network Tools:** Integration with `netstat`, `ss`, and `nmap` for gathering network information.
   - **Alerts:** Integration with a notification service (e.g., Twilio for SMS, SendGrid for email).
   - **Real-Time Updates:** SignalR for real-time communication between backend and frontend.

## Implementation Steps: