name: Metrics
on:
  # Schedule daily updates
  schedule: [{cron: "0 0 * * *"}]
  # (Optional) Run workflow manually
  workflow_dispatch:
  # (Optional) Run workflow when pushing on master/main
  push: {branches: ["master", "main"]}
jobs:
  github-metrics:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: lowlighter/metrics@latest
        with:
          # Your GitHub token
          token: ${{ secrets.METRICS_TOKEN }}

          # Options
          user: ${{ github.repository_owner }}
          template: classic
          base: header, activity, community, repositories, metadata
          config_timezone: Asia/Kolkata # Change this to your timezone
          
          # --- Replicating the Screenshot Visuals ---
          
          # 1. The Isometric Contribution Calendar (Right side 3D grid)
          plugin_isocalendar: yes
          plugin_isocalendar_duration: half-year

          # 2. Coding Habits (Charts in middle)
          plugin_habits: yes
          plugin_habits_from: 200
          plugin_habits_days: 14
          plugin_habits_facts: yes
          plugin_habits_charts: yes

          # 3. Languages (Bar at bottom right)
          plugin_languages: yes
          plugin_languages_ignored: >-
            html, css
          plugin_languages_details: lines, percentage

          # 4. Tech Stack Icons (Bottom Left)
          plugin_topics: yes
          plugin_topics_limit: 0
          plugin_topics_mode: icons

          # 5. PageSpeed (Top Right Gauges)
          # Note: This usually requires a separate Google API key for real data, 
          # but this enables the visual block.
          plugin_pagespeed: yes
          plugin_pagespeed_url: .user.website

          # 6. Music (Apple Music block)
          # Note: This requires setup. Changing to 'random' for now so it works instantly.
          plugin_music: yes
          plugin_music_provider: apple

          # 7. Projects
          plugin_projects: yes
          plugin_projects_limit: 4
