# Naver News Alert Bot

This project monitors Naver's mobile news search for articles related to a specified keyword (in this case, **대덕전자**) and sends notifications with new news links to a designated Telegram chat via a Telegram bot. The script periodically checks for new articles and ensures that only unique, previously unsent news links are notified.

## Features

- **News Monitoring:**  
  Periodically fetches the latest news results from Naver's mobile search page using the provided keyword.

- **Duplicate Filtering:**  
  Compares current news links against previously sent links to ensure that notifications only include new content.

- **Telegram Notifications:**  
  Uses the Telegram Bot API to send each new news link to a specified chat ID. If there are no new news articles, it sends a message stating "새로운 뉴스 없음" (No new news).

- **Scheduled Updates:**  
  Leverages APScheduler to run the news check at regular intervals (every hour).

## How It Works

1. **Extracting Links:**  
   The `extract_links` function constructs a URL for Naver's mobile news search based on the specified search keyword. It then fetches and parses the HTML content with BeautifulSoup to extract the top five news links.

2. **Filtering New Content:**  
   The function compares the extracted links with a maintained list (`old_links`) to filter out any links that have already been sent.

3. **Sending Telegram Messages:**  
   The `send_links` function sends each new link via the Telegram bot. If no new links are found, it sends a "no new news" message.

4. **Scheduling with APScheduler:**  
   After an initial check, APScheduler schedules the `send_links` function to run every hour, ensuring continuous monitoring for new articles.

## Setup and Usage

1. **Install Dependencies:**  
   Ensure you have the following libraries installed:
   ```bash
   pip install requests beautifulsoup4 python-telegram-bot apscheduler
   ```

2. **Configuration:**  
   - Update the `token` variable with your Telegram Bot API token.
   - Set the `id` variable to your Telegram chat ID.
   - Adjust the `search_word` variable if you want to monitor a different keyword.

3. **Run the Script:**  
   Simply run the script. It will immediately perform an initial news check and send any new links. The script will then continue to check for updates every hour.

## Important Notes

- **Secure Your Credentials:**  
  Ensure your Telegram bot token and chat ID are kept secure.

- **HTML Structure Changes:**  
  If Naver updates the structure of its mobile news page, you may need to adjust the BeautifulSoup selectors accordingly.

- **Scheduling Interval:**  
  The current scheduling interval is set to one hour. Modify the APScheduler configuration if you require a different interval.
