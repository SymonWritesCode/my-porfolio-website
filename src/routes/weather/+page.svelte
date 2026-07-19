<script>
  import { base } from '$app/paths';
  // Cities Mock Data
  const citiesWeather = {
    "london": {
      name: "London",
      country: "United Kingdom",
      temp: 14,
      condition: "Rainy",
      humidity: 82,
      wind: 18,
      uv: 2,
      hourly: [
        { time: "12 PM", temp: 14, icon: "rain" },
        { time: "2 PM", temp: 15, icon: "rain" },
        { time: "4 PM", temp: 14, icon: "cloudy" },
        { time: "6 PM", temp: 13, icon: "cloudy" },
        { time: "8 PM", temp: 12, icon: "clear" }
      ],
      forecast: [
        { day: "Mon", temp: 15, condition: "Rainy", icon: "rain" },
        { day: "Tue", temp: 16, condition: "Cloudy", icon: "cloudy" },
        { day: "Wed", temp: 18, condition: "Partly Cloudy", icon: "partly-cloudy" },
        { day: "Thu", temp: 17, condition: "Rainy", icon: "rain" },
        { day: "Fri", temp: 19, condition: "Sunny", icon: "sunny" }
      ]
    },
    "tokyo": {
      name: "Tokyo",
      country: "Japan",
      temp: 26,
      condition: "Sunny",
      humidity: 55,
      wind: 8,
      uv: 8,
      hourly: [
        { time: "12 PM", temp: 26, icon: "sunny" },
        { time: "2 PM", temp: 27, icon: "sunny" },
        { time: "4 PM", temp: 25, icon: "sunny" },
        { time: "6 PM", temp: 23, icon: "clear" },
        { time: "8 PM", temp: 21, icon: "clear" }
      ],
      forecast: [
        { day: "Mon", temp: 27, condition: "Sunny", icon: "sunny" },
        { day: "Tue", temp: 28, condition: "Sunny", icon: "sunny" },
        { day: "Wed", temp: 26, condition: "Partly Cloudy", icon: "partly-cloudy" },
        { day: "Thu", temp: 25, condition: "Rainy", icon: "rain" },
        { day: "Fri", temp: 27, condition: "Sunny", icon: "sunny" }
      ]
    },
    "new york": {
      name: "New York",
      country: "United States",
      temp: 22,
      condition: "Cloudy",
      humidity: 68,
      wind: 12,
      uv: 4,
      hourly: [
        { time: "12 PM", temp: 22, icon: "cloudy" },
        { time: "2 PM", temp: 23, icon: "cloudy" },
        { time: "4 PM", temp: 22, icon: "partly-cloudy" },
        { time: "6 PM", temp: 20, icon: "partly-cloudy" },
        { time: "8 PM", temp: 18, icon: "clear" }
      ],
      forecast: [
        { day: "Mon", temp: 23, condition: "Cloudy", icon: "cloudy" },
        { day: "Tue", temp: 25, condition: "Partly Cloudy", icon: "partly-cloudy" },
        { day: "Wed", temp: 24, condition: "Sunny", icon: "sunny" },
        { day: "Thu", temp: 22, condition: "Rainy", icon: "rain" },
        { day: "Fri", temp: 21, condition: "Sunny", icon: "sunny" }
      ]
    },
    "sydney": {
      name: "Sydney",
      country: "Australia",
      temp: 18,
      condition: "Sunny",
      humidity: 60,
      wind: 14,
      uv: 5,
      hourly: [
        { time: "12 PM", temp: 18, icon: "sunny" },
        { time: "2 PM", temp: 19, icon: "sunny" },
        { time: "4 PM", temp: 17, icon: "sunny" },
        { time: "6 PM", temp: 15, icon: "clear" },
        { time: "8 PM", temp: 14, icon: "clear" }
      ],
      forecast: [
        { day: "Mon", temp: 19, condition: "Sunny", icon: "sunny" },
        { day: "Tue", temp: 20, condition: "Sunny", icon: "sunny" },
        { day: "Wed", temp: 18, condition: "Partly Cloudy", icon: "partly-cloudy" },
        { day: "Thu", temp: 17, condition: "Cloudy", icon: "cloudy" },
        { day: "Fri", temp: 16, condition: "Rainy", icon: "rain" }
      ]
    },
    "paris": {
      name: "Paris",
      country: "France",
      temp: 19,
      condition: "Partly Cloudy",
      humidity: 62,
      wind: 10,
      uv: 5,
      hourly: [
        { time: "12 PM", temp: 19, icon: "partly-cloudy" },
        { time: "2 PM", temp: 21, icon: "sunny" },
        { time: "4 PM", temp: 20, icon: "partly-cloudy" },
        { time: "6 PM", temp: 18, icon: "cloudy" },
        { time: "8 PM", temp: 16, icon: "clear" }
      ],
      forecast: [
        { day: "Mon", temp: 21, condition: "Partly Cloudy", icon: "partly-cloudy" },
        { day: "Tue", temp: 23, condition: "Sunny", icon: "sunny" },
        { day: "Wed", temp: 22, condition: "Rainy", icon: "rain" },
        { day: "Thu", temp: 20, condition: "Cloudy", icon: "cloudy" },
        { day: "Fri", temp: 19, condition: "Sunny", icon: "sunny" }
      ]
    },
    "reykjavik": {
      name: "Reykjavik",
      country: "Iceland",
      temp: 2,
      condition: "Snowy",
      humidity: 90,
      wind: 22,
      uv: 1,
      hourly: [
        { time: "12 PM", temp: 2, icon: "snowy" },
        { time: "2 PM", temp: 2, icon: "snowy" },
        { time: "4 PM", temp: 1, icon: "snowy" },
        { time: "6 PM", temp: 0, icon: "cloudy" },
        { time: "8 PM", temp: -1, icon: "clear" }
      ],
      forecast: [
        { day: "Mon", temp: 2, condition: "Snowy", icon: "snowy" },
        { day: "Tue", temp: 1, condition: "Snowy", icon: "snowy" },
        { day: "Wed", temp: 3, condition: "Cloudy", icon: "cloudy" },
        { day: "Thu", temp: 0, condition: "Snowy", icon: "snowy" },
        { day: "Fri", temp: -2, condition: "Clear", icon: "clear" }
      ]
    }
  };

  // Helper to generate dynamic weather for searched cities
  function generateWeather(cityName) {
    const sanitized = cityName.trim().toLowerCase();
    const hash = sanitized.split("").reduce((acc, char) => acc + char.charCodeAt(0), 0);
    const conditions = ["Sunny", "Cloudy", "Rainy", "Snowy", "Partly Cloudy"];
    const condition = conditions[hash % conditions.length];
    
    let baseTemp = 10 + (hash % 20); // 10 to 29
    if (condition === "Snowy") baseTemp = -5 + (hash % 10); // -5 to 4
    if (condition === "Sunny") baseTemp = 20 + (hash % 15); // 20 to 34
    
    const humidity = 40 + (hash % 50); // 40% to 90%
    const wind = 5 + (hash % 25); // 5 to 30 km/h
    const uv = condition === "Sunny" ? 6 + (hash % 5) : 1 + (hash % 4);
    
    const hourly = [];
    const conditionIcons = {
      "Sunny": "sunny",
      "Cloudy": "cloudy",
      "Rainy": "rain",
      "Snowy": "snowy",
      "Partly Cloudy": "partly-cloudy"
    };

    for (let i = 0; i < 5; i++) {
      const hours = [12, 2, 4, 6, 8];
      const time = `${hours[i]} ${i < 4 ? 'PM' : 'PM'}`;
      const tempOffset = Math.sin(i) * 2;
      hourly.push({
        time,
        temp: Math.round(baseTemp + tempOffset),
        icon: conditionIcons[condition] || "sunny"
      });
    }
    
    const days = ["Mon", "Tue", "Wed", "Thu", "Fri"];
    const forecast = days.map((day, idx) => {
      const cond = conditions[(hash + idx) % conditions.length];
      let temp = baseTemp + Math.sin(idx) * 3;
      if (cond === "Snowy") temp = Math.min(temp, 2);
      return {
        day,
        temp: Math.round(temp),
        condition: cond,
        icon: conditionIcons[cond] || "sunny"
      };
    });
    
    return {
      name: cityName.charAt(0).toUpperCase() + cityName.slice(1),
      country: "Meteorological Station",
      temp: baseTemp,
      condition,
      humidity,
      wind,
      uv,
      hourly,
      forecast
    };
  }

  // Reactive State (Svelte 5 Runes)
  let searchQuery = $state("");
  let selectedCity = $state("london");

  // Derived state for selected city weather
  let weatherData = $derived(
    citiesWeather[selectedCity.toLowerCase()] || generateWeather(selectedCity)
  );

  function handleSearch(e) {
    e.preventDefault();
    if (searchQuery.trim()) {
      selectedCity = searchQuery.trim();
      searchQuery = "";
    }
  }

  function selectCity(city) {
    selectedCity = city;
  }
</script>

<svelte:head>
  <title>SkyFlow | Advanced Weather Hub</title>
  <meta name="description" content="A real-time meteorological portal showing dynamic climate visualization, atmospheric indicators, and forecasts." />
</svelte:head>

<div class="weather-page">
  <!-- Nav header -->
  <header class="weather-nav">
    <a href="{base}/" class="back-btn">
      <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
        <path stroke-linecap="round" stroke-linejoin="round" d="M15 19l-7-7 7-7" />
      </svg>
      <span>Back to Portfolio</span>
    </a>
    <div class="weather-logo">
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="var(--color-accent-secondary)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
        <path d="M12 2v2M4.93 4.93l1.41 1.41M20 12h2M17.66 17.66l1.41 1.41M12 22v-2M6.34 17.66l-1.41 1.41M2 12h2M14 12a4 4 0 1 1-8 0" />
        <path d="M20 15.66A4 4 0 0 0 18 10h-1.26a6 6 0 1 0-7.74 7.66" />
      </svg>
      <span class="text-gradient">SkyFlow Weather</span>
    </div>
  </header>

  <!-- Weather Application Hub -->
  <main class="weather-container">
    
    <!-- Left Column: Search & Current Weather -->
    <div class="column-left">
      <!-- Search Panel -->
      <div class="search-card glass-panel">
        <form class="search-form" onsubmit={handleSearch}>
          <label for="weather-search" class="visually-hidden">Search city weather</label>
          <input 
            type="text" 
            id="weather-search"
            placeholder="Search any city..." 
            class="search-input" 
            bind:value={searchQuery}
            required
          />
          <button type="submit" class="search-submit-btn" aria-label="Submit search">
            <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
              <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
            </svg>
          </button>
        </form>

        <!-- Quick Select Chips -->
        <div class="quick-cities">
          {#each ["London", "New York", "Tokyo", "Sydney", "Reykjavik"] as city}
            <button 
              type="button" 
              class="city-chip" 
              class:active={selectedCity.toLowerCase() === city.toLowerCase()}
              onclick={() => selectCity(city.toLowerCase())}
            >
              {city}
            </button>
          {/each}
        </div>
      </div>

      <!-- Current Weather Display -->
      <div class="current-weather-card glass-panel" style="margin-top: 24px;">
        <div class="weather-visual-container">
          {#if weatherData.condition === "Sunny"}
            <div class="weather-art">
              <svg viewBox="0 0 100 100" class="weather-icon-lg">
                <defs>
                  <radialGradient id="sunGlow" cx="50%" cy="50%" r="50%">
                    <stop offset="0%" stop-color="hsl(45, 100%, 65%)" stop-opacity="1"/>
                    <stop offset="100%" stop-color="hsl(30, 100%, 50%)" stop-opacity="0.2"/>
                  </radialGradient>
                </defs>
                <circle cx="50" cy="50" r="30" fill="url(#sunGlow)" class="pulse-sun" />
                <g class="spin-sun">
                  {#each Array(8) as _, i}
                    <line x1="50" y1="12" x2="50" y2="2" stroke="hsl(45, 100%, 60%)" stroke-width="4.5" stroke-linecap="round" transform="rotate({i * 45} 50 50)" />
                  {/each}
                </g>
              </svg>
            </div>
          {:else if weatherData.condition === "Cloudy"}
            <div class="weather-art">
              <svg viewBox="0 0 100 100" class="weather-icon-lg">
                <defs>
                  <linearGradient id="cloudGrad" x1="0%" y1="0%" x2="0%" y2="100%">
                    <stop offset="0%" stop-color="hsl(240, 10%, 85%)" />
                    <stop offset="100%" stop-color="hsl(240, 10%, 55%)" />
                  </linearGradient>
                </defs>
                <path d="M25,65 a15,15 0 0,1 12,-12 a22,22 0 0,1 38,-3 a17,17 0 0,1 6,33 l-56,0 a15,15 0 0,1 0,-15 z" fill="url(#cloudGrad)" class="drift-cloud-slow" transform="scale(0.85) translate(10, 10)" opacity="0.6" />
                <path d="M25,65 a15,15 0 0,1 12,-12 a22,22 0 0,1 38,-3 a17,17 0 0,1 6,33 l-56,0 a15,15 0 0,1 0,-15 z" fill="url(#cloudGrad)" class="drift-cloud" />
              </svg>
            </div>
          {:else if weatherData.condition === "Rainy"}
            <div class="weather-art">
              <svg viewBox="0 0 100 100" class="weather-icon-lg">
                <defs>
                  <linearGradient id="rainCloudGrad" x1="0%" y1="0%" x2="0%" y2="100%">
                    <stop offset="0%" stop-color="hsl(220, 10%, 65%)" />
                    <stop offset="100%" stop-color="hsl(220, 10%, 40%)" />
                  </linearGradient>
                </defs>
                <g class="rain-drops">
                  {#each Array(6) as _, i}
                    <line x1={32 + i * 8} y1="55" x2={29 + i * 8} y2="75" stroke="hsl(200, 100%, 70%)" stroke-width="2.5" stroke-linecap="round" class="rain-drop" style="animation-delay: {i * 0.15}s" />
                  {/each}
                </g>
                <path d="M25,65 a15,15 0 0,1 12,-12 a22,22 0 0,1 38,-3 a17,17 0 0,1 6,33 l-56,0 a15,15 0 0,1 0,-15 z" fill="url(#rainCloudGrad)" class="shiver-cloud" />
              </svg>
            </div>
          {:else if weatherData.condition === "Snowy"}
            <div class="weather-art">
              <svg viewBox="0 0 100 100" class="weather-icon-lg">
                <defs>
                  <linearGradient id="snowCloudGrad" x1="0%" y1="0%" x2="0%" y2="100%">
                    <stop offset="0%" stop-color="hsl(240, 10%, 90%)" />
                    <stop offset="100%" stop-color="hsl(240, 10%, 75%)" />
                  </linearGradient>
                </defs>
                <g class="snow-flakes">
                  {#each Array(6) as _, i}
                    <circle cx={32 + i * 8} cy="60" r="2.5" fill="hsl(0, 0%, 100%)" class="snow-flake" style="animation-delay: {i * 0.25}s" />
                  {/each}
                </g>
                <path d="M25,65 a15,15 0 0,1 12,-12 a22,22 0 0,1 38,-3 a17,17 0 0,1 6,33 l-56,0 a15,15 0 0,1 0,-15 z" fill="url(#snowCloudGrad)" />
              </svg>
            </div>
          {:else}
            <!-- Partly Cloudy -->
            <div class="weather-art">
              <svg viewBox="0 0 100 100" class="weather-icon-lg">
                <defs>
                  <radialGradient id="sunGlowPC" cx="50%" cy="50%" r="50%">
                    <stop offset="0%" stop-color="hsl(45, 100%, 65%)" />
                    <stop offset="100%" stop-color="hsl(30, 100%, 50%)" stop-opacity="0.1"/>
                  </radialGradient>
                  <linearGradient id="cloudGradPC" x1="0%" y1="0%" x2="0%" y2="100%">
                    <stop offset="0%" stop-color="hsl(240, 10%, 90%)" />
                    <stop offset="100%" stop-color="hsl(240, 10%, 65%)" />
                  </linearGradient>
                </defs>
                <circle cx="62" cy="38" r="22" fill="url(#sunGlowPC)" class="pulse-sun" />
                <path d="M20,70 a13,13 0 0,1 10,-10 a19,19 0 0,1 33,-3 a15,15 0 0,1 5,28 l-48,0 a13,13 0 0,1 0,-15 z" fill="url(#cloudGradPC)" class="drift-cloud-pc" />
              </svg>
            </div>
          {/if}
        </div>

        <div class="weather-temp-display">
          <h2 class="city-name">{weatherData.name}</h2>
          <p class="country-name">{weatherData.country}</p>
          <div class="weather-temp-num">{weatherData.temp}°C</div>
          <p class="weather-condition-text">{weatherData.condition}</p>
        </div>
      </div>
    </div>

    <!-- Right Column: Details & Forecasts -->
    <div class="column-right">
      <!-- 3 Metrics Cards Grid -->
      <div class="details-grid">
        <!-- Humidity -->
        <div class="detail-card glass-panel">
          <div class="detail-header">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="var(--color-accent-secondary)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M12 2.69l5.66 5.66a8 8 0 1 1-11.31 0z"></path>
            </svg>
            <span>Humidity</span>
          </div>
          <div class="detail-value">{weatherData.humidity}%</div>
          <div class="bar-container">
            <div class="bar-fill" style="width: {weatherData.humidity}%"></div>
          </div>
        </div>

        <!-- Wind speed -->
        <div class="detail-card glass-panel">
          <div class="detail-header">
            <svg class="rotate-wind" xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="var(--color-accent-secondary)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" style="animation-duration: {Math.max(1, 10 - weatherData.wind/3)}s">
              <path d="M9.59 4.59A2 2 0 1 1 11 8H2m10.59 11.41A2 2 0 1 0 14 16H2m15.73-8.27A2.5 2.5 0 1 1 19.5 12H2"></path>
            </svg>
            <span>Wind speed</span>
          </div>
          <div class="detail-value">{weatherData.wind} <span style="font-size: 0.9rem; font-weight: 500; color: var(--text-muted);">km/h</span></div>
          <div class="bar-container">
            <div class="bar-fill" style="width: {Math.min(100, (weatherData.wind / 50) * 100)}%"></div>
          </div>
        </div>

        <!-- UV Index -->
        <div class="detail-card glass-panel">
          <div class="detail-header">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="var(--color-accent-secondary)" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <circle cx="12" cy="12" r="5"></circle>
              <line x1="12" y1="1" x2="12" y2="3"></line>
              <line x1="12" y1="21" x2="12" y2="23"></line>
              <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"></line>
              <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"></line>
              <line x1="1" y1="12" x2="3" y2="12"></line>
              <line x1="21" y1="12" x2="23" y2="12"></line>
              <line x1="4.22" y1="19.78" x2="5.64" y2="18.36"></line>
              <line x1="18.36" y1="5.64" x2="19.78" y2="4.22"></line>
            </svg>
            <span>UV Index</span>
          </div>
          <div class="detail-value">{weatherData.uv}</div>
          <div class="bar-container">
            <div class="bar-fill" style="width: {(weatherData.uv / 12) * 100}%"></div>
          </div>
        </div>
      </div>

      <!-- Hourly Forecast Slider -->
      <div class="hourly-section">
        <h3 class="section-title-sm">Hourly Forecast</h3>
        <div class="hourly-scroll">
          {#each weatherData.hourly as hr}
            <div class="hourly-card glass-panel">
              <span class="hourly-time">{hr.time}</span>
              <div class="hourly-icon-wrap">
                {#if hr.icon === 'sunny'}
                  <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="none" viewBox="0 0 24 24" stroke="hsl(45, 100%, 60%)" stroke-width="2">
                    <circle cx="12" cy="12" r="5" fill="hsl(45, 100%, 60%)" fill-opacity="0.3"></circle>
                    <line x1="12" y1="1" x2="12" y2="3"></line>
                    <line x1="12" y1="21" x2="12" y2="23"></line>
                    <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"></line>
                    <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"></line>
                    <line x1="1" y1="12" x2="3" y2="12"></line>
                    <line x1="21" y1="12" x2="23" y2="12"></line>
                  </svg>
                {:else if hr.icon === 'cloudy'}
                  <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="none" viewBox="0 0 24 24" stroke="hsl(240, 5%, 70%)" stroke-width="2">
                    <path d="M18 10h-1.26A8 8 0 1 0 9 20h9a5 5 0 0 0 0-10z"></path>
                  </svg>
                {:else if hr.icon === 'rain'}
                  <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="none" viewBox="0 0 24 24" stroke="hsl(200, 100%, 65%)" stroke-width="2">
                    <path d="M17 18.66L18 20M12 18.66L13 20M7 18.66L8 20M20 10a8 8 0 1 0-16 0h16z"></path>
                  </svg>
                {:else if hr.icon === 'snowy'}
                  <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="none" viewBox="0 0 24 24" stroke="hsl(180, 100%, 90%)" stroke-width="2">
                    <path d="M20 17.58A5 5 0 0 0 18 8h-1.26A8 8 0 1 0 4 16.25"></path>
                    <line x1="8" y1="16" x2="8.01" y2="16"></line>
                    <line x1="12" y1="16" x2="12.01" y2="16"></line>
                  </svg>
                {:else}
                  <!-- Partly Cloudy -->
                  <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="none" viewBox="0 0 24 24" stroke="hsl(45, 100%, 75%)" stroke-width="2">
                    <path d="M12 2v2M4.93 4.93l1.41 1.41M20 12h2" />
                    <path d="M20 15.66A4 4 0 0 0 18 10h-1.26a6 6 0 1 0-7.74 7.66" />
                  </svg>
                {/if}
              </div>
              <span class="hourly-temp">{hr.temp}°</span>
            </div>
          {/each}
        </div>
      </div>

      <!-- 5-Day Forecast -->
      <div class="forecast-section">
        <h3 class="section-title-sm">5-Day Forecast</h3>
        <div class="forecast-list">
          {#each weatherData.forecast as dayForecast}
            <div class="forecast-row glass-panel">
              <span class="forecast-day">{dayForecast.day}</span>
              <div class="forecast-cond-wrap">
                {#if dayForecast.icon === 'sunny'}
                  <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="none" viewBox="0 0 24 24" stroke="hsl(45, 100%, 60%)" stroke-width="2">
                    <circle cx="12" cy="12" r="5" fill="hsl(45, 100%, 60%)" fill-opacity="0.3"></circle>
                    <line x1="12" y1="1" x2="12" y2="3"></line>
                    <line x1="12" y1="21" x2="12" y2="23"></line>
                    <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"></line>
                    <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"></line>
                  </svg>
                {:else if dayForecast.icon === 'cloudy'}
                  <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="none" viewBox="0 0 24 24" stroke="hsl(240, 5%, 70%)" stroke-width="2">
                    <path d="M18 10h-1.26A8 8 0 1 0 9 20h9a5 5 0 0 0 0-10z"></path>
                  </svg>
                {:else if dayForecast.icon === 'rain'}
                  <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="none" viewBox="0 0 24 24" stroke="hsl(200, 100%, 65%)" stroke-width="2">
                    <path d="M17 18.66L18 20M12 18.66L13 20M7 18.66L8 20M20 10a8 8 0 1 0-16 0h16z"></path>
                  </svg>
                {:else if dayForecast.icon === 'snowy'}
                  <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="none" viewBox="0 0 24 24" stroke="hsl(180, 100%, 90%)" stroke-width="2">
                    <path d="M20 17.58A5 5 0 0 0 18 8h-1.26A8 8 0 1 0 4 16.25"></path>
                    <line x1="8" y1="16" x2="8.01" y2="16"></line>
                    <line x1="12" y1="16" x2="12.01" y2="16"></line>
                  </svg>
                {:else}
                  <!-- Partly Cloudy -->
                  <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="none" viewBox="0 0 24 24" stroke="hsl(45, 100%, 75%)" stroke-width="2">
                    <path d="M12 2v2M4.93 4.93l1.41 1.41M20 12h2" />
                    <path d="M20 15.66A4 4 0 0 0 18 10h-1.26a6 6 0 1 0-7.74 7.66" />
                  </svg>
                {/if}
                <span class="forecast-cond-name">{dayForecast.condition}</span>
              </div>
              <span class="forecast-temp">{dayForecast.temp}°C</span>
            </div>
          {/each}
        </div>
      </div>
    </div>
  </main>
</div>

<style>
  .visually-hidden {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    border: 0;
  }

  .weather-page {
    min-height: 100vh;
    padding: 120px 24px 60px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 30px;
  }

  .weather-nav {
    width: 100%;
    max-width: 1100px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
  }

  .back-btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid var(--glass-border);
    padding: 10px 20px;
    border-radius: 30px;
    color: var(--text-primary);
    text-decoration: none;
    font-weight: 600;
    font-size: 0.9rem;
    transition: transform var(--transition-smooth), background var(--transition-smooth);
  }

  .back-btn:hover {
    transform: translateX(-4px);
    background: rgba(255, 255, 255, 0.1);
  }

  .weather-logo {
    display: inline-flex;
    align-items: center;
    gap: 10px;
    font-size: 1.25rem;
    font-weight: 800;
  }

  .weather-container {
    width: 100%;
    max-width: 1100px;
    display: grid;
    grid-template-columns: 1fr 1.5fr;
    gap: 30px;
  }

  /* Left Column Content */
  .column-left {
    display: flex;
    flex-direction: column;
  }

  /* Search & Selector */
  .search-card {
    padding: 24px;
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .search-form {
    position: relative;
    display: flex;
    width: 100%;
  }

  .search-input {
    width: 100%;
    padding: 14px 54px 14px 20px;
    background: rgba(255, 255, 255, 0.03);
    border: 1px solid var(--glass-border);
    border-radius: 30px;
    color: var(--text-primary);
    font-family: inherit;
    font-size: 1rem;
    transition: border-color var(--transition-smooth), box-shadow var(--transition-smooth);
  }

  .search-input:focus {
    outline: none;
    border-color: var(--color-accent-secondary);
    box-shadow: 0 0 15px rgba(0, 255, 255, 0.15);
  }

  .search-submit-btn {
    position: absolute;
    right: 6px;
    top: 50%;
    transform: translateY(-50%);
    background: var(--gradient-accent);
    border: none;
    width: 38px;
    height: 38px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--bg-primary);
    cursor: pointer;
    transition: opacity var(--transition-smooth);
  }

  .search-submit-btn:hover {
    opacity: 0.9;
  }

  .quick-cities {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
  }

  .city-chip {
    background: rgba(255, 255, 255, 0.04);
    border: 1px solid var(--glass-border);
    color: var(--text-secondary);
    padding: 6px 14px;
    border-radius: 20px;
    font-size: 0.85rem;
    font-weight: 500;
    cursor: pointer;
    transition: all var(--transition-smooth);
  }

  .city-chip:hover {
    border-color: rgba(255, 255, 255, 0.2);
    color: var(--text-primary);
  }

  .city-chip.active {
    background: var(--gradient-accent);
    color: var(--bg-primary);
    border-color: transparent;
    font-weight: 600;
  }

  /* Weather Display */
  .current-weather-card {
    padding: 40px 30px;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    position: relative;
    overflow: hidden;
  }

  .weather-visual-container {
    height: 150px;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 20px;
  }

  .city-name {
    font-size: 2.2rem;
    font-weight: 800;
    margin-bottom: 4px;
    letter-spacing: -0.5px;
  }

  .country-name {
    font-size: 0.85rem;
    color: var(--text-muted);
    text-transform: uppercase;
    letter-spacing: 1.5px;
    margin-bottom: 24px;
  }

  .weather-temp-display {
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .weather-temp-num {
    font-size: 5rem;
    font-weight: 800;
    line-height: 1;
    letter-spacing: -2px;
    background: linear-gradient(180deg, var(--text-primary) 50%, var(--text-secondary));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .weather-condition-text {
    font-size: 1.3rem;
    font-weight: 700;
    color: var(--color-accent-secondary);
    margin-top: 12px;
    letter-spacing: -0.3px;
  }

  /* SVG animations */
  .weather-icon-lg {
    width: 140px;
    height: 140px;
  }

  .pulse-sun {
    animation: pulse-sun-key 4s ease-in-out infinite alternate;
    transform-origin: center;
  }

  .spin-sun {
    animation: spin 45s linear infinite;
    transform-origin: center;
  }

  .drift-cloud {
    animation: drift-key 8s ease-in-out infinite alternate;
  }

  .drift-cloud-slow {
    animation: drift-key 14s ease-in-out infinite alternate;
  }

  .drift-cloud-pc {
    animation: drift-pc-key 7s ease-in-out infinite alternate;
    transform-origin: center;
  }

  .shiver-cloud {
    animation: shiver-key 3.5s ease-in-out infinite alternate;
  }

  @keyframes pulse-sun-key {
    0% { transform: scale(1); filter: drop-shadow(0 0 10px rgba(255, 200, 0, 0.4)); }
    100% { transform: scale(1.08); filter: drop-shadow(0 0 25px rgba(255, 150, 0, 0.8)); }
  }

  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }

  @keyframes drift-key {
    0% { transform: translateX(-6px); }
    100% { transform: translateX(6px); }
  }

  @keyframes drift-pc-key {
    0% { transform: translateX(-4px) translateY(2px); }
    100% { transform: translateX(4px) translateY(-2px); }
  }

  @keyframes shiver-key {
    0%, 100% { transform: translateY(0) scale(1); }
    50% { transform: translateY(-3px) scale(1.02); }
  }

  /* Rain effect animation */
  .rain-drop {
    animation: rain-fall-key 0.9s linear infinite;
  }

  @keyframes rain-fall-key {
    0% { transform: translateY(-15px) translateX(2px); opacity: 0; }
    30% { opacity: 0.8; }
    100% { transform: translateY(15px) translateX(-2px); opacity: 0; }
  }

  /* Snow effect animation */
  .snow-flake {
    animation: snow-fall-key 2.8s linear infinite;
  }

  @keyframes snow-fall-key {
    0% { transform: translateY(-20px) translateX(0px); opacity: 0; }
    20% { opacity: 0.8; }
    50% { transform: translateY(0px) translateX(4px); }
    80% { opacity: 0.8; }
    100% { transform: translateY(20px) translateX(-2px); opacity: 0; }
  }

  /* Details Grid */
  .details-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    margin-bottom: 28px;
  }

  .detail-card {
    padding: 22px;
    display: flex;
    flex-direction: column;
    gap: 14px;
  }

  .detail-header {
    display: flex;
    align-items: center;
    gap: 8px;
    color: var(--text-secondary);
    font-size: 0.8rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.8px;
  }

  .detail-value {
    font-size: 2rem;
    font-weight: 800;
    letter-spacing: -0.5px;
  }

  /* Slider / Gauge UI */
  .bar-container {
    width: 100%;
    height: 6px;
    background: rgba(255, 255, 255, 0.08);
    border-radius: 3px;
    overflow: hidden;
  }

  .bar-fill {
    height: 100%;
    background: var(--gradient-accent);
    border-radius: 3px;
    transition: width 0.5s ease-out;
  }

  .rotate-wind {
    animation: spin 5s linear infinite;
    transform-origin: center;
  }

  /* Hourly Forecast */
  .hourly-section {
    margin-bottom: 28px;
  }

  .section-title-sm {
    font-size: 1.15rem;
    font-weight: 800;
    margin-bottom: 16px;
    color: var(--text-primary);
    letter-spacing: -0.3px;
  }

  .hourly-scroll {
    display: flex;
    gap: 12px;
    overflow-x: auto;
    padding-bottom: 12px;
    scroll-snap-type: x mandatory;
  }

  .hourly-scroll::-webkit-scrollbar {
    height: 6px;
  }

  .hourly-card {
    flex: 0 0 96px;
    padding: 18px 12px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
    text-align: center;
    scroll-snap-align: start;
    border-radius: 14px;
  }

  .hourly-time {
    font-size: 0.75rem;
    color: var(--text-muted);
    font-weight: 600;
  }

  .hourly-temp {
    font-size: 1.15rem;
    font-weight: 700;
  }

  /* 5-Day Forecast */
  .forecast-list {
    display: flex;
    flex-direction: column;
    gap: 12px;
  }

  .forecast-row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 16px 24px;
    border-radius: var(--border-radius);
    transition: background var(--transition-smooth), border-color var(--transition-smooth);
    border: 1px solid rgba(255, 255, 255, 0.03);
  }

  .forecast-row:hover {
    background: rgba(255, 255, 255, 0.02);
    border-color: rgba(255, 255, 255, 0.08);
  }

  .forecast-day {
    flex: 1;
    font-weight: 600;
    font-size: 0.95rem;
  }

  .forecast-cond-wrap {
    flex: 1.5;
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .forecast-cond-name {
    font-size: 0.9rem;
    color: var(--text-secondary);
  }

  .forecast-temp {
    font-weight: 700;
    font-size: 1.15rem;
    text-align: right;
  }

  /* Responsive layouts */
  @media (max-width: 900px) {
    .weather-container {
      grid-template-columns: 1fr;
    }

    .details-grid {
      grid-template-columns: 1fr;
    }
  }
</style>
