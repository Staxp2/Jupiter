<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Jupiter</title>
    
    <link rel="apple-touch-icon" href="logo.png">
    <link rel="icon" type="image/png" href="logo.png">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">

    <style>
        body {
            margin: 0;
            padding: 0;
            background-color: #0b0f12;
            color: #ffffff;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
        }

        .app-header {
            width: 100%;
            max-width: 480px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 14px 20px;
            box-sizing: border-box;
            background-color: #12181d;
            border-bottom: 1px solid #1a232a;
        }

        .menu-icon {
            font-size: 22px;
            cursor: pointer;
            color: #2dd4bf;
        }

        .friends-dropdown {
            position: relative;
            display: inline-block;
        }

        .friends-btn {
            background: #182228;
            color: #2dd4bf;
            border: 1px solid #2dd4bf44;
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 13px;
            font-weight: 500;
            cursor: pointer;
        }

        .dropdown-content {
            display: none;
            position: absolute;
            right: 0;
            background-color: #182228;
            min-width: 140px;
            box-shadow: 0px 8px 16px rgba(0,0,0,0.4);
            border-radius: 10px;
            border: 1px solid #2a353d;
            z-index: 10;
            overflow: hidden;
            margin-top: 6px;
        }

        .dropdown-content button {
            color: #ffffff;
            background: none;
            padding: 10px 14px;
            text-align: left;
            border: none;
            width: 100%;
            cursor: pointer;
            font-size: 13px;
            display: block;
        }

        .dropdown-content button:hover {
            background-color: #223038;
            color: #2dd4bf;
        }

        .show { display: block; }
        .hidden { display: none !important; }

        .app-container {
            width: 100%;
            max-width: 480px;
            padding: 20px;
            box-sizing: border-box;
        }

        .welcome-title {
            margin: 0 0 4px 0;
            font-size: 26px;
            font-weight: 600;
            text-align: center;
        }

        .schedule-card-wrapper {
            background: #121212;
            border-radius: 16px;
            padding: 16px;
            box-sizing: border-box;
            box-shadow: 0 8px 24px rgba(0,0,0,0.5);
            margin-top: 20px;
        }

        /* Landing Page Picker Styles */
        .landing-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 75vh;
            text-align: center;
            padding: 20px;
        }

        .landing-title {
            font-size: 32px;
            font-weight: 700;
            margin-bottom: 8px;
            color: #ffffff;
            letter-spacing: -0.5px;
        }

        .landing-subtitle {
            font-size: 15px;
            color: #888888;
            margin-bottom: 32px;
        }

        .student-picker-list {
            display: flex;
            flex-direction: column;
            gap: 12px;
            width: 100%;
            max-width: 280px;
        }

        .student-picker-btn {
            background: #182228;
            color: #ffffff;
            border: 1px solid #2a353d;
            padding: 14px 20px;
            border-radius: 12px;
            font-size: 16px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s ease;
            box-shadow: 0 4px 12px rgba(0,0,0,0.2);
        }

        .student-picker-btn:hover {
            background-color: #223038;
            border-color: #2dd4bf;
            color: #2dd4bf;
        }
    </style>
</head>
<body>

  <header class="app-header">
    <div id="homeBtn" class="menu-icon" title="Home" style="cursor: pointer;">🏠</div>
    <div class="friends-dropdown">
      <button id="friendsBtn" class="friends-btn">👥 Friends ▼</button>
      <div id="friendsMenu" class="dropdown-content">
        <button type="button" data-user="Caleb">Caleb</button>
        <button type="button" data-user="Christos">Christos</button>
        <button type="button" data-user="Imraan">Imraan</button>
      </div>
    </div>
  </header>

  <!-- Landing Page Picker View -->
  <div id="landing-view" class="app-container landing-container">
    <h1 class="landing-title">Jupiter</h1>
    <p class="landing-subtitle">Select your profile to view schedule</p>
    <div class="student-picker-list">
      <button type="button" class="student-picker-btn" data-user="Caleb">Caleb</button>
      <button type="button" class="student-picker-btn" data-user="Christos">Christos</button>
      <button type="button" class="student-picker-btn" data-user="Imraan">Imraan</button>
    </div>
  </div>

  <!-- Schedule View -->
  <div id="schedule-view" class="app-container hidden">
    <h2 id="dynamic-greeting" class="welcome-title">Welcome.</h2>
    <div class="schedule-card-wrapper">
      <h3 id="day-title" style="margin: 0 0 16px 0; color: #aaaaaa; font-size: 15px; font-weight: 400;">📅 Schedule</h3>
      <div id="schedule-content"></div>
    </div>
  </div>

<script>
  document.addEventListener('DOMContentLoaded', () => {
    let currentUser = null;

    const landingView = document.getElementById('landing-view');
    const scheduleView = document.getElementById('schedule-view');
    const friendsBtn = document.getElementById('friendsBtn');
    const friendsMenu = document.getElementById('friendsMenu');
    const homeBtn = document.getElementById('homeBtn');
    const greetingEl = document.getElementById('dynamic-greeting');
    const titleEl = document.getElementById('day-title');
    const contentEl = document.getElementById('schedule-content');

    function selectUser(user) {
      currentUser = user;
      landingView.classList.add('hidden');
      scheduleView.classList.remove('hidden');
      renderSchedule();
    }

    homeBtn.addEventListener('click', () => {
      currentUser = null;
      scheduleView.classList.add('hidden');
      landingView.classList.remove('hidden');
    });

    document.querySelectorAll('.student-picker-btn').forEach(button => {
      button.addEventListener('click', (e) => {
        selectUser(e.target.getAttribute('data-user'));
      });
    });

    friendsBtn.addEventListener('click', (e) => {
      e.stopPropagation();
      friendsMenu.classList.toggle('show');
    });

    document.querySelectorAll('#friendsMenu button').forEach(button => {
      button.addEventListener('click', (e) => {
        selectUser(e.target.getAttribute('data-user'));
        friendsMenu.classList.remove('show');
      });
    });

    window.addEventListener('click', () => {
      if (friendsMenu.classList.contains('show')) {
        friendsMenu.classList.remove('show');
      }
    });

    const now = new Date();
    const dateOfMonth = now.getDate();
    const dayOfWeek = now.getDay();
    const currentHour = now.getHours();

    function updateGreeting() {
      if (!currentUser) return;
      if (currentHour >= 5 && currentHour < 12) {
        greetingEl.innerText = `Good morning, ${currentUser}.`;
      } else if (currentHour >= 12 && currentHour < 17) {
        greetingEl.innerText = `Good afternoon, ${currentUser}.`;
      } else {
        greetingEl.innerText = `Good evening, ${currentUser}.`;
      }
    }

    let isDay1 = (dateOfMonth % 2 !== 0);
    let rotationTitle = isDay1 ? " (Day 1)" : " (Day 2)";

    const periodData = {
      P1: { time: "9:00 AM - 10:20 AM" },
      P2: { time: "10:25 AM - 11:40 AM" },
      LUN: { time: "11:40 AM - 12:35 PM", isLunch: true },
      P3: { time: "12:40 PM - 1:55 PM" },
      P4: { time: "2:00 PM - 3:15 PM" }
    };

    const christosColors = {
      "Science": "#2ecc71",
      "Geography": "#f1c40f",
      "Mathematics": "#3498db",
      "Dramatic Arts": "#e74c3c"
    };

    const imraanColors = {
      "Geography": "#2ecc71",
      "English, Grade 9": "#f1c40f",
      "French Immersion": "#e74c3c",
      "Computer Technology": "#3498db"
    };

    const calebColors = {
      "Mathematics": "#e74c3c",
      "Computer Technology": "#95a5a6",
      "English, Grade 9": "#3498db",
      "Dramatic Arts": "#f1c40f"
    };

    const christosA = [
      { period: "P1", name: "Science", code: "SNC1W1", teacher: "Xiao Yue Ding", room: "318" },
      { period: "P2", name: "Geography", code: "CGC1W5", teacher: "Lucia Domingues", room: "214" },
      { period: "LUN" },
      { period: "P3", name: "Mathematics", code: "MTH1W1", teacher: "Alf Scharlach", room: "307" },
      { period: "P4", name: "Dramatic Arts", code: "ADA1O5", teacher: "Sonya Ugarkovic", room: "200" }
    ];

    const christosB = [
      { period: "P1", name: "Geography", code: "CGC1W5", teacher: "Lucia Domingues", room: "214" },
      { period: "P2", name: "Science", code: "SNC1W1", teacher: "Xiao Yue Ding", room: "318" },
      { period: "LUN" },
      { period: "P3", name: "Dramatic Arts", code: "ADA1O5", teacher: "Sonya Ugarkovic", room: "200" },
      { period: "P4", name: "Mathematics", code: "MTH1W1", teacher: "Alf Scharlach", room: "307" }
    ];

    const imraanA = [
      { period: "P1", name: "Computer Technology", code: "TEJ101", teacher: "Wei Qin", room: "119" },
      { period: "P2", name: "Geography", code: "CGC1W5", teacher: "Lucia Domingues", room: "214" },
      { period: "LUN" },
      { period: "P3", name: "English, Grade 9", code: "ENL1W1", teacher: "Sylvia Kirkley", room: "311" },
      { period: "P4", name: "French Immersion", code: "FIF1D5", teacher: "Leah Raghunath", room: "114" }
    ];

    const imraanB = [
      { period: "P1", name: "Geography", code: "CGC1W5", teacher: "Lucia Domingues", room: "214" },
      { period: "P2", name: "Computer Technology", code: "TEJ101", teacher: "Wei Qin", room: "119" },
      { period: "LUN" },
      { period: "P3", name: "French Immersion", code: "FIF1D5", teacher: "Leah Raghunath", room: "114" },
      { period: "P4", name: "English, Grade 9", code: "ENL1W1", teacher: "Sylvia Kirkley", room: "311" }
    ];

    const calebA = [
      { period: "P1", name: "Computer Technology", code: "TEJ101", teacher: "Wei Qin", room: "119" },
      { period: "P2", name: "English, Grade 9", code: "ENL1W1", teacher: "Sylvia Kirkley", room: "311" },
      { period: "LUN" },
      { period: "P3", name: "Mathematics", code: "MTH1W1", teacher: "Alf Scharlach", room: "307" },
      { period: "P4", name: "Dramatic Arts", code: "ADA1O5", teacher: "Sonya Ugarkovic", room: "200" }
    ];

    const calebB = [
      { period: "P1", name: "English, Grade 9", code: "ENL1W1", teacher: "Sylvia Kirkley", room: "311" },
      { period: "P2", name: "Computer Technology", code: "TEJ101", teacher: "Wei Qin", room: "119" },
      { period: "LUN" },
      { period: "P3", name: "Dramatic Arts", code: "ADA1O5", teacher: "Sonya Ugarkovic", room: "200" },
      { period: "P4", name: "Mathematics", code: "MTH1W1", teacher: "Alf Scharlach", room: "307" }
    ];

    function createClassCard(cls, info) {
      if (info.isLunch) {
        return `<div style="background: #1e1e1e; padding: 10px; border-radius: 8px; margin-bottom: 8px; text-align: center; border: 1px dashed #333333;"><strong style="color: #888888; font-size: 13px;">LUNCH</strong><p style="margin: 2px 0 0 0; color: #777777; font-size: 11px;">${info.time}</p></div>`;
      }
      
      let color = "#3498db";
      if (currentUser === 'Christos') {
        color = christosColors[cls.name] || "#3498db";
      } else if (currentUser === 'Imraan') {
        color = imraanColors[cls.name] || "#3498db";
      } else if (currentUser === 'Caleb') {
        color = calebColors[cls.name] || "#3498db";
      }

      return `<div style="background: #1e1e1e; padding: 12px 14px; border-radius: 10px; margin-bottom: 8px; border-left: 4px solid ${color}; box-shadow: 0 2px 4px rgba(0,0,0,0.2);"><div style="display: flex; justify-content: space-between; align-items: start;"><div><strong style="color: ${color}; font-size: 14px;">${cls.name}</strong><p style="margin: 3px 0 0 0; color: #aaaaaa; font-size: 11px;">${cls.code} • ${cls.teacher}</p></div><div style="text-align: right;"><strong style="color: #ffffff; font-size: 13px;">Room ${cls.room}</strong><p style="margin: 3px 0 0 0; color: #888888; font-size: 10px;">${info.time}</p></div></div></div>`;
    }

    function renderSchedule() {
      if (!currentUser) return;
      updateGreeting();
      let activeDayOfWeek = (dayOfWeek === 0 || dayOfWeek === 6) ? 1 : dayOfWeek;
      
      if (activeDayOfWeek >= 1 && activeDayOfWeek <= 5) {
        titleEl.innerText = `📅 ${currentUser}'s Schedule` + rotationTitle;
        
        let activeClasses;
        if (currentUser === 'Christos') {
          activeClasses = isDay1 ? christosA : christosB;
        } else if (currentUser === 'Imraan') {
          activeClasses = isDay1 ? imraanA : imraanB;
        } else {
          activeClasses = isDay1 ? calebA : calebB;
        }

        let html = '';
        activeClasses.forEach(cls => { html += createClassCard(cls, periodData[cls.period]); });
        contentEl.innerHTML = html;
      } else {
        titleEl.innerText = "🎉 Weekend!";
        contentEl.innerHTML = `<div style="background: #1e1e1e; padding: 20px; border-radius: 10px; text-align: center; color: #aaaaaa; border: 1px solid #333333;"><p style="margin: 0; font-size: 14px;">No classes today. Enjoy your break!</p></div>`;
      }
    }
  });
</script>

</body>
</html
