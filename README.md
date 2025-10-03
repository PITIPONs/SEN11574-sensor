Project Overview

This project demonstrates how to measure heart rate (BPM) using an ESP32 and send the results to Google Sheets via a deployed Google Apps Script Web App. The system records heartbeats every 5 seconds and every 1 minute, applying a filtering and calculation method to ensure stable results.

Features
Reads pulse sensor values through the ESP32’s ADC pin.
Applies a moving average filter to reduce sensor noise.
Detects heartbeats and calculates BPM (Beats Per Minute).
Records data at two intervals:
  Every 5 seconds (instantaneous BPM)
  Every 1 minute (average BPM)
Sends results directly to Google Sheets via an HTTP request.
Includes retry logic for stable network communication.

Formula for BPM
The calculation of BPM is based on detected beats per unit of time:

𝐵𝑃𝑀 = Number of Beats Detected in Interval × 60,000
                    Interval in milliseconds

For the 1-minute interval, the formula simplifies to
	​
𝐵𝑃𝑀 = Total Beats Detected in 60 seconds

Code Explanation
WiFi Initialization
  Connects ESP32 to the specified WiFi network.
  
Pulse Detection
  Reads analog values from the sensor.
  Filters data using a moving average to minimize noise.
  Detects a heartbeat when the signal exceeds a threshold.
  
BPM Calculation
  Counts the number of detected beats within 5 seconds and 1 minute.
  Converts counts into BPM values.
  
Data Transmission
  Sends BPM values to Google Sheets through HTTP GET requests.
  If a request fails, retries are attempted up to 3 times.
  
Google Apps Script
  A simple doGet() function processes incoming parameters and appends them into designated sheets (BPM_5s and BPM_1min).
