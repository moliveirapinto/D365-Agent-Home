# 🏠 D365 Agent Home - Contact Center Dashboard

<div align="center">

**A modern, feature-rich homepage for Dynamics 365 Contact Center agents**

![Status](https://img.shields.io/badge/status-active-success.svg)
![Version](https://img.shields.io/badge/version-1.0-blue.svg)
![Platform](https://img.shields.io/badge/platform-Dynamics%20365-orange.svg)

[Features](#-features) • [Installation](#-installation) • [Usage](#-usage) • [Configuration](#-configuration) • [Support](#-support)

</div>

---

## 📋 Overview

D365 Agent Home is a comprehensive, real-time dashboard designed specifically for Dynamics 365 Contact Center agents. It provides a centralized, intuitive interface that displays critical information at a glance, enabling agents to work more efficiently and deliver exceptional customer service.

Say hello to the new Contact Center agent homepage! 👋

### ✨ Why D365 Agent Home?

- **🎯 Centralized Dashboard**: All essential information in one place
- **⚡ Real-time Updates**: Live presence status, metrics, and queue information
- **🎨 Modern UI/UX**: Clean, responsive design with smooth animations
- **📊 Performance Insights**: Track your productivity and customer satisfaction
- **👥 Team Awareness**: See your team's availability and status
- **🔔 Smart Notifications**: Stay on top of overdue tasks and priorities

---

## 🚀 Features

### 📊 Performance Metrics Dashboard
- **Active Cases Counter**: Real-time count of your open cases
- **Resolved Cases Today**: Track your daily resolution metrics
- **Pending Tasks**: Monitor outstanding tasks with overdue alerts
- **Satisfaction Score (CSAT)**: View your customer satisfaction ratings with trend analysis
- **Automatic Fallback**: Switches to "Cases This Month" metric when CSAT data is unavailable

### 🟢 Real-time Presence Management
- **Live Status Tracking**: Integrates with Dynamics 365 Omnichannel presence
- **Status Duration Timer**: See how long you've been in your current status
- **Multiple Status Support**: Available, Busy, Do Not Disturb, Away, Offline, Break
- **Visual Indicators**: Color-coded badges with pulsing animations
- **Automatic Updates**: Polls presence status every second for real-time accuracy

### 📋 Task & Case Management
- **My Tasks**: Quick view of pending tasks with priority indicators (High/Medium/Low)
- **Recent Cases**: Display active cases with customer information and status
- **Quick Actions**: One-click access to create cases, tasks, and search knowledge base
- **Due Date Tracking**: Visual indicators for overdue and due-today tasks
- **Click to Open**: Direct navigation to tasks and cases in Dynamics 365

### 👥 Team Collaboration
- **Team Agents View**: See all agents in your organization
- **Queue Filtering**: Filter agents by specific queues
- **Search Functionality**: Quickly find team members by name
- **Status Grouping**: Agents organized by availability (Available, Busy, Away)
- **Collapsible Groups**: Expandable/collapsible status sections for better organization
- **Online/Offline Tabs**: Separate views for active and offline agents

### ⚡ Performance Statistics
- **Average Response Time**: Time from case creation to first response
- **Average Resolution Time**: Time from case creation to resolution
- **Trend Analysis**: Compare current performance against historical data
- **Smart Calculations**: Automatically handles missing data with fallback logic

### 🎨 User Experience
- **Responsive Design**: Works seamlessly on all screen sizes
- **Smooth Animations**: Polished transitions and hover effects
- **Modern UI Components**: Card-based layout with gradient accents
- **Accessibility**: Clean typography and color contrast
- **Loading States**: Elegant spinners and empty state messages

---

## 💻 Installation

### Prerequisites

- **Dynamics 365** environment with Omnichannel for Customer Service
- **System User** account with appropriate permissions
- Access to **Dynamics 365 Web Resources**

### Deployment Steps

1. **Download the Files**
   ```bash
   git clone https://github.com/moliveirapinto/D365-Agent-Home.git
   cd D365-Agent-Home
   ```

2. **Upload to Dynamics 365**
   - Navigate to **Settings** > **Customizations** > **Customize the System**
   - Go to **Web Resources** > **New**
   - Upload `Agent Home.html` as a Web Resource
   - Upload `square-cursor.svg` as a Web Resource (if using custom cursor)
   - Set appropriate **Display Name** and **Name** (e.g., `cr123_/AgentHome.html`)
   - Click **Save** and **Publish**

3. **Configure as Homepage**
   - Go to **Settings** > **Administration** > **System Settings**
   - Navigate to the **General** tab
   - Set the web resource URL as the default dashboard for agents
   
   *OR*
   
   - Add as a custom page in **App Designer**
   - Include in your **Customer Service workspace** app

4. **Set Permissions**
   - Ensure agents have **Read** permissions on:
     - `incident` (Cases)
     - `task` (Tasks)
     - `systemuser` (Users)
     - `queue` (Queues)
     - `queuemembership` (Queue Membership)
     - `msdyn_agentstatus` (Agent Status)
     - `msdyn_customerfeedbacksurveyresponse` (CSAT Survey)

---

## 🎯 Usage

### First Time Setup

1. **Open the Dashboard**: Navigate to the Agent Home page in your D365 environment
2. **Automatic Initialization**: The dashboard will automatically:
   - Detect your user identity
   - Load your current presence status
   - Fetch your active cases and tasks
   - Display team members in your queues
   - Calculate performance metrics

### Daily Workflow

1. **Monitor Your Metrics**: Check your active cases, resolved count, and pending tasks
2. **Manage Tasks**: Click on tasks to view details or mark complete
3. **Handle Cases**: Click on cases to open and work on them
4. **Quick Actions**: Use the Quick Actions panel to create new cases or tasks
5. **Team Awareness**: Check team availability before transferring cases
6. **Track Performance**: Monitor your response and resolution times

### Status Management

The presence status is automatically synchronized with Dynamics 365 Omnichannel:
- Changes reflect in real-time (1-second polling)
- Duration timer shows how long you've been in current status
- Visual color coding: Green (Available), Red (Busy), Yellow (Away), etc.

---

## ⚙️ Configuration

### Customizing Metrics

The dashboard supports flexible metric configuration:

- **CSAT Metric**: Automatically displays when survey response data is available
- **Monthly Cases Fallback**: Shows "Cases This Month" when CSAT data is unavailable
- **Trend Calculations**: Compares current period against previous period

### Queue Configuration

Agents see team members based on shared queue membership:
- Queues with special characters (#, <, >) are automatically filtered out
- "Copilot Studio" agents are excluded from the team view
- Queue dropdown populates automatically with all available queues

### Presence Polling

Default polling interval: **1 second**

To adjust (modify in code):
```javascript
// Change polling interval (milliseconds)
presenceCheckInterval = setInterval(checkPresence, 1000); // 1 second
```

---

## 🏗️ Technical Architecture

### Technology Stack
- **Frontend**: Pure HTML5, CSS3, JavaScript (ES6+)
- **Integration**: Dynamics 365 Web API, Xrm.WebApi
- **Data Sources**: 
  - Dynamics 365 entities (incident, task, systemuser, queue, etc.)
  - Omnichannel presence API (CCaaS_GetPresence)
  - Customer feedback survey responses

### Key Components

1. **Xrm Context Detection**: Automatically detects and connects to D365 context
2. **Presence Monitor**: Real-time polling of agent status via custom API
3. **Metrics Calculator**: Aggregates case and task data with smart fallbacks
4. **Team Viewer**: Fetches and displays agent presence across queues
5. **Navigation Handler**: Deep linking to D365 forms and views

### API Integrations

- `CCaaS_GetPresence`: Custom API for presence status retrieval
- `msdyn_agentstatus`: Agent login and presence tracking
- `incident`: Case management
- `task`: Task management
- `systemuser`: User information
- `queue` & `queuemembership`: Queue assignments
- `msdyn_customerfeedbacksurveyresponse`: CSAT data

---

## 🎨 Customization

### Branding & Colors

Edit the CSS gradient colors in the HTML file:

```css
/* Header gradient */
background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);

/* Status colors */
--status-bg: linear-gradient(135deg, #107c10 0%, #0e6b0e 100%);
```

### Adding Custom Metrics

Add new metric cards by duplicating the metric-card structure:

```html
<div class="metric-card" style="--card-color: #your-color;">
    <div class="metric-header">
        <div class="metric-label">Your Metric</div>
        <span class="metric-badge">Badge</span>
    </div>
    <div class="metric-value" id="yourMetric">-</div>
    <div class="metric-trend">...</div>
</div>
```

---

## 🔒 Security & Permissions

### Required Security Roles
- **Customer Service Representative** or equivalent
- **Read** access to all entity types used by the dashboard
- **Omnichannel Agent** role for presence features

### Data Privacy
- Dashboard only displays data accessible to the logged-in user
- No data is stored locally or transmitted outside D365
- All API calls use D365 security context

---

## 🐛 Troubleshooting

### Dashboard Shows "Loading..."
- **Cause**: Not running within Dynamics 365 context
- **Solution**: Ensure the page is accessed via D365 web resource URL

### Presence Status Not Updating
- **Cause**: CCaaS_GetPresence API not available or permissions issue
- **Solution**: Verify Omnichannel is configured and user has agent status record

### "No agents found" in Team View
- **Cause**: No other active users or queue membership issues
- **Solution**: Check queue assignments and user access permissions

### Metrics Show "N/A"
- **Cause**: No data available or API permission issues
- **Solution**: Verify entity permissions and create test data

### CSAT Score Not Showing
- **Cause**: No survey responses in the current month
- **Solution**: Dashboard automatically switches to "Cases This Month" metric

---

## 📈 Roadmap

Future enhancements planned:
- [ ] Configurable dashboard widgets
- [ ] Historical trend charts
- [ ] Export metrics to Excel
- [ ] Custom filters and views
- [ ] Dark mode support
- [ ] Notification preferences
- [ ] Integration with Teams

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit issues, fork the repository, and create pull requests for any improvements.

### Development Guidelines
1. Test all changes in a D365 sandbox environment first
2. Maintain code comments for complex logic
3. Follow existing code style and structure
4. Update README for any new features

---

## 📄 License

This project is available for use within Dynamics 365 environments. Please ensure compliance with your organization's policies regarding custom development.

---

## 💬 Support

For questions, issues, or feature requests:
- **Issues**: [GitHub Issues](https://github.com/moliveirapinto/D365-Agent-Home/issues)
- **Discussions**: [GitHub Discussions](https://github.com/moliveirapinto/D365-Agent-Home/discussions)

---

## 🙏 Acknowledgments

Built with ❤️ for Dynamics 365 Contact Center agents worldwide.

Special thanks to the D365 community for continuous support and feedback!

---

<div align="center">

**Made with 💜 for Contact Center Excellence**

⭐ Star this repo if you find it helpful!

</div>
