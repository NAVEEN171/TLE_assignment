# TLE_assignment

# Competitive Programming Contest Tracker

A full-stack MERN application that helps programmers keep track of coding contests across multiple platforms, discover solutions, and manage their competitive programming journey.

## 🌟 Features

- **Multi-Platform Support**: Track contests from CodeChef, CodeForces, and LeetCode
- **Real-Time Updates**: Contests are updated every 24 hours via automated scraping
- **Advanced Filtering System**: Filter contests by status, platform, date range, duration, and more
- **Contest Solutions**: Automatically fetches high-quality YouTube solutions for past contests
- **Saved Contests**: Save contests to revisit them later
- **Dark Mode Support**: Toggle between light and dark themes
- **Fully Responsive**: Works seamlessly across all devices

## 🏗️ Architecture

This project consists of three repositories:

1. **Frontend**: [https://github.com/NAVEEN171/Contests-tracker-frontend](https://github.com/NAVEEN171/Contests-tracker-frontend)
2. **Backend**: [https://github.com/NAVEEN171/Contests-tracker-backend](https://github.com/NAVEEN171/Contests-tracker-backend)
3. **Scraper**: [https://github.com/NAVEEN171/Contests-scraper](https://github.com/NAVEEN171/Contests-scraper)

### Tech Stack

- **Frontend**: React.js, Redux, CSS
- **Backend**: Node.js, Express.js, MongoDB (mostly on Aggregations)
- **Scraper**: Python, Playwright (Web Scraping), YouTube Data API

## 📊 Data Flow & Scraping Process

### Contest Data Scraping

1. The scraper fetches contest data from CodeChef, CodeForces, and LeetCode
2. It compares newly scraped data with existing data in local JSON files
3. If changes are detected, an "update" field is created with attributes needing updates
4. Modified contests are added to `need_update.json`
5. New contests are uploaded to the database while existing ones are updated
6. The entire process is logged in detail for monitoring and debugging

### YouTube Solutions Gathering

1. After contest data is scraped, the system retrieves past contests from the database
2. It filters for contests that:
   - Started more than 24 hours ago
   - Have been attempted for solutions fewer than twice
3. The scraper fetches YouTube video links for these contests
4. Videos are sorted by view count to prioritize high-quality solutions
5. Contest records are updated with the YouTube solution links
6. This data is stored in `need_upload.json` before being committed to the database

## 🔍 Filtering System

The application implements a comprehensive filtering system that uses search parameters synced with filter states:

1. **Contest Status**: Active, Upcoming, Expired
2. **Platform Filter**: CodeChef, CodeForces, LeetCode
3. **Active Contests Toggle**: Show only currently active contests
4. **Solutions Toggle**: Show only contests with available solutions
5. **Date Range Filter**: Find contests within specific dates
6. **Duration Filter**: Filter contests by their length (e.g., 3 hours)
7. **Latest First Sorting**: Sort contests by start time (enabled by default)

## 💾 MongoDB Aggregation

The backend uses MongoDB's aggregation framework for efficient data processing and retrieval, ensuring that the application remains performant even with large datasets.

## 🔄 Optimization

- **24-Hour Scrape Cycle**: The scraper runs once every 24 hours to minimize unnecessary API calls
- **Smart YouTube Fetching**: Solution videos are fetched after a 24-hour delay to ensure quality content
- **Two-Attempt System**: The system makes up to two attempts to find solutions for each contest
- **Incremental Updates**: Only modified fields are updated in the database to reduce overhead

## 🚀 Getting Started

### Prerequisites

- Node.js (v14+)
- MongoDB
- YouTube Data API key (for solution scraping)

### Installation

1. Clone all three repositories:
```bash
git clone https://github.com/NAVEEN171/Contests-tracker-frontend
git clone https://github.com/NAVEEN171/Contests-tracker-backend
git clone https://github.com/NAVEEN171/Contests-scraper
```

2. Install dependencies:
```bash
# For frontend and backend
cd Contests-tracker-frontend && npm install
cd Contests-tracker-backend && npm install

# For scraper (Python-based)
cd Contests-scraper
pip install -r requirements.txt  # or install required dependencies
```

3. Configure environment variables for each component (refer to each repository for specific requirements)

4. Start the application:
```bash
# Start backend
cd Contests-tracker-backend
npm start

# Start frontend
cd Contests-tracker-frontend
npm start

# Run scraper (or set up as a cron job)
cd Contests-scraper
python scraper.py
```

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📞 Contact

For any questions or feedback, please open an issue in the respective repository.
