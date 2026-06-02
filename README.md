# cyber-sec-final-
Cybersecurity Assignment
QR Code-Based IP Address & Location Tracker
Student: Narendar Reddy  |  Date: June 2026

1. Introduction
This assignment demonstrates how a QR code can be used as a social engineering vector to collect network and location information from a target device. The project was built as a cybersecurity awareness demonstration, showing how an innocent-looking QR code can redirect a user to a web page that silently gathers their public IP address and GPS coordinates.

The demonstration was tested by sharing the QR code with family members, who scanned it and consented to sharing their device information. All data was collected ethically, with full knowledge and permission of the participants.

2. Objective
•	Generate a QR code that links to a custom-built web page.
•	When scanned, collect the visitor's public IP address.
•	Request and record the visitor's GPS location (latitude and longitude).
•	Store the collected data remotely so it can be viewed by the student.
•	Demonstrate the cybersecurity risks of scanning unknown QR codes.

3. Tools and Websites Used

Tool / Service	Type	URL	Purpose
Claude (claude.ai)	AI Assistant	claude.ai	Generated all HTML/JS code for tracker and QR generator pages
GitHub	Code Hosting	github.com	Hosted the repository containing tracker.html and viewer.html
GitHub Pages	Web Hosting	pages.github.com	Published tracker.html as a live public URL for free
jsonbin.io	Data Storage API	jsonbin.io	Stored collected IP and location data remotely as JSON
ipify.org	IP Lookup API	api.ipify.org	Retrieved the visitor's public IP address via fetch()
Browser Geolocation API	Browser API	Built-in (W3C)	Requested GPS coordinates from the visitor's device
QRCode.js	JS Library	cdnjs.cloudflare.com	Generated a scannable QR code PNG from the tracker URL

4. Step-by-Step Process
Step 1 — Designing the Tracker Page
Using Claude AI, a custom HTML page (tracker.html) was generated. The page performs two main operations when a visitor taps the 'Share my info' button:
•	Fetches the visitor's public IP address from the ipify.org API.
•	Invokes the browser's built-in Geolocation API to request GPS coordinates.
•	Saves all collected data (IP, latitude, longitude, accuracy, timestamp, user agent) to a remote jsonbin.io bin via a PUT API call.

Step 2 — Setting Up Remote Data Storage (jsonbin.io)
1.	Created a free account at jsonbin.io.
2.	Generated an X-Master-Key API key from the account settings.
3.	Created a new Bin with initial content: { "entries": [] }
4.	Copied the Bin ID from the URL after creation.
5.	Inserted the API key and Bin ID into the tracker.html script section.

Step 3 — Hosting on GitHub Pages
6.	Created a free GitHub account at github.com.
7.	Created a new public repository named cyber-sec-final-.
8.	Uploaded tracker.html and viewer.html via the GitHub web interface (Add file > Upload files).
9.	Navigated to Settings > Pages and set the source branch to main / (root).
10.	Waited approximately 1-2 minutes for GitHub Pages to publish the site.
11.	The live tracker URL became: https://knarendarreddy7-hue.github.io/cyber-sec-final-/tracker.html

Step 4 — Generating the QR Code
12.	Opened generator.html locally in a browser.
13.	Pasted the live GitHub Pages URL into the input field.
14.	Clicked Generate QR Code — the page used QRCode.js to render a scannable QR PNG.
15.	Downloaded the QR code image.

Step 5 — Testing with Family Members
16.	Shared the QR code image with parents via messaging app.
17.	Parents scanned the QR code using their phone cameras.
18.	They were directed to tracker.html and tapped the 'Share my info (demo)' button.
19.	The page displayed their IP address and requested location permission.
20.	Upon granting permission, GPS coordinates were collected and saved to jsonbin.io.

Step 6 — Viewing the Results
21.	Opened viewer.html locally in a browser.
22.	Entered the jsonbin.io API key and Bin ID.
23.	Clicked Load Responses — all collected entries appeared with IP, coordinates, and a Google Maps link.

5. How the Tracker Works (Technical Overview)
The tracker page operates entirely client-side (in the visitor's browser) with two external API calls:

•	IP Collection: A fetch() call is made to https://api.ipify.org?format=json which returns the visitor's public IP address as a JSON response. This works because every HTTP request reveals the caller's IP to the server.
•	Geolocation: The browser's navigator.geolocation.getCurrentPosition() method is called. The browser displays a native permission dialog. If the user taps Allow, the device's GPS (or Wi-Fi triangulation) returns latitude, longitude, and accuracy in metres.
•	Data Storage: Both results are combined with a timestamp and user agent string, then sent to jsonbin.io using a PUT request with the X-Master-Key header for authentication.

6. Cybersecurity Observations
This project illustrates several important cybersecurity concepts:

•	QR Code Risk: QR codes are opaque — users cannot see the URL before scanning. A malicious actor could craft a QR that redirects to a phishing or data-harvesting page. This is known as QRishing.
•	IP Address Exposure: Every website a user visits automatically receives their public IP address. This can reveal the user's approximate city and ISP without any permission prompt.
•	Location Permission as a Defence: The browser's geolocation permission dialog is the only protection users have against precise location harvesting. Users should be cautious when any website requests location access.
•	Social Engineering: The effectiveness of this demo relies on trust — the target trusts the QR code source. This mirrors real-world attacks where attackers replace legitimate QR codes in public spaces.

7. Conclusion
This assignment successfully demonstrated how a QR code can be weaponised to collect sensitive device information including IP address and GPS location. The project was completed using entirely free, publicly available tools and required no advanced programming knowledge — highlighting how low the barrier to entry is for such attacks.

The key takeaway is that users should never scan QR codes from unknown or untrusted sources, and should deny location permissions to websites they do not fully trust. Awareness of these techniques is a critical part of personal cybersecurity hygiene.
<img width="468" height="609" alt="image" src="https://github.com/user-attachments/assets/e6495746-4ef3-4b05-b77c-160b3058ba25" />

