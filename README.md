# **Digital Detective**

The **Digital Detective** is a CLI tool designed for Open Source Intelligence (OSINT) gathering. It allows users to search for personal information, IP addresses, and usernames across various APIs and public sources. The tool validates gathered data through cross-referencing and saves the results to files while displaying them in the terminal.

---

## **Key Features**

### **1. Full-Name Search**
- **What It Does**: Fetches personal information (name, city, phone) using APIs and web scraping.
- **How It Works**:
  - Uses the SerpAPI (`get_personal_info` in `name_search.py`) to gather data.
  - Scrapes public directory websites like Fonecta using BeautifulSoup (`get_personal_info_from_fonecta` in `name_search.py`).
  - Results are cross-referenced for accuracy using `cross_reference_name_results` in `cli_name.py`.

### **2. IP Search**
- **What It Does**: Retrieves location and ISP information for a given IP address.
- **How It Works**:
  - Fetches data from the IP-API and IP-Location API (`get_ip_info_ipapi` and `get_ip_info_iplocation` in `ip_search.py`).
  - Validates results using `cross_reference_ip_results` in `cli_ip.py`.

### **3. Username Search**
- **What It Does**: Checks for username mentions across multiple platforms.
- **How It Works**:
  - Uses Sherlock (`get_username_mentions_sherlock` in `username_search.py`) to search for usernames on platforms like Twitter, Facebook, and Instagram.
  - Complements Sherlock with Social Analyzer (`get_username_mentions_analyzer` in `username_search.py`) for additional insights.
  - Results are cross-referenced using `cross_reference_username_results` in `cli_username.py`.

### **4. Cross-Referencing**
- **What It Does**: Validates data accuracy by comparing results from multiple APIs.
- **How It Works**:
  - Compares fields like name, address, and phone number for name searches.
  - Matches ISP and location data for IP searches.
  - Checks for consistency in username mentions across platforms.

### **5. Caching and Rate Limiting**
- **What It Does**: Reduces redundant API calls and handles rate limits.
- **How It Works**:
  - Introduces delays using `time.sleep` in `rate_cache_time.py`.
  - Caches API responses in the api_cache directory to minimize redundant requests.

### **6. Secure API Key Management**
- **What It Does**: Protects sensitive information using environment variables.
- **How It Works**:
  - Loads API keys from the .env file using the `dotenv` library in `utils.py`.

### **7. Error Handling**
- **What It Does**: Manages API errors and cases where no data is found.
- **How It Works**:
  - Implements `try-except` blocks in all API-related functions.
  - Provides user-friendly error messages in the terminal.

### **8. Rich Output**
- **What It Does**: Displays search results in visually appealing tables.
- **How It Works**:
  - Uses the `rich` library to create structured and colorful terminal output.

---

## **Directory Structure**

```
digital-detective/
├── api_cache/  
├── results/  
├── src/                                         # Source code directory
│   ├── api/                                     # API-related modules
│   │   ├── ip_search.py                         # Module for IP search functionality
│   │   ├── name_search.py                       # Module for full-name search functionality
│   │   ├── rate_cache_time.py                   # Handles caching and rate-limiting
│   │   ├── username_search.py                   # Module for username search functionality
│   ├── cli_ip.py                                # CLI module for IP search
│   ├── cli_name.py                              # CLI module for name search
│   ├── cli_username.py                          # CLI module for username search
│   ├── cli.py                                   # Main CLI module
│   ├── utils.py                                 # Utility functions and variables
├── tests/                                       # Unit tests directory
│   ├── test_ip_search.py                        # Unit tests for IP search functionality
│   ├── test_name_search.py                      # Unit tests for name search functionality
│   ├── test_username_search.py                  # Unit tests for username search functionality
├── .env                                         # Environment variables file
├── .gitignore                                   # Git ignore file
├── Summary_of _the_Project.pdf                  # Summary of the project
├── commands.md                                  # Shortcut to commands
├── README.md                                    # Project overview and documentation
├── requirements.txt                             # Project dependencies
└── run_tests.sh                                 # Script to run all tests
```

---

## **Setup and Installation Instructions**

1. **Clone the Repository**:
    ```bash
    git clone https://gitea.koodsisu.fi/lauralevisto/digital-detective.git
    cd digital-detective
    ```

2. **Create and Activate a Virtual Environment**:
    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3. **Install Dependencies**:
    ```bash
    pip install -r requirements.txt
    ```

4. **Set Up Environment Variables**:
    Create a `.env` file in the root directory and add your API keys:
   ```properties
   SERPAPI_KEY=your_serpapi_key
   ```

5. **Run the Tool**:
    ```bash
    python3 src/cli.py --help
    ```

6. **Deactivate the Virtual Environment**:
    ```bash
    deactivate
    ```

(OPTIONAL)
```
## **If you would like to run the program**

Before running the program, ensure you have installed all the required tools and set up necessary accounts:

### **Prerequisites**
- **Sherlock**:
  - Install Sherlock by cloning its repository:
    ```bash
    git clone https://github.com/sherlock-project/sherlock.git
    cd sherlock
    python3 -m pip install -r requirements.txt
    ```
  - Add Sherlock to your system's PATH or ensure the  directory is accessible.

- **Social Analyzer**:
  - Install Social Analyzer by cloning its repository:
    ```bash
    git clone https://github.com/qeeqbox/social-analyzer.git
    cd social-analyzer
    python3 -m pip install -r requirements.txt
    ```
  - Ensure Social Analyzer is configured properly (e.g., `sites.json` is up-to-date).

- **SerpAPI Account**:
  - Create an account on [SerpAPI](https://serpapi.com/).
  - Obtain your API key and add it to the  file:
    ```properties
    SERPAPI_KEY=your_serpapi_key
    ```
```
---

## **Usage Guide**

### **CLI Options**:
```bash
python3 src/cli.py --help
```
- `-n` or `--name`: Perform a full-name search.
- `-ip` or `--ip`: Perform an IP search.
- `-un` or `--username`: Perform a username search.

### **Examples**:

1. **Full-Name Search**:
    ```bash
    python3 src/cli.py -n "Dwight Schrute"
    ```

2. **IP Search**:
    ```bash
    python3 src/cli.py -ip 8.8.8.8
    ```

3. **Username Search**:
    ```bash
    python3 src/cli.py -un "@recyclops"
    ```

---

## **Tools and Libraries**

This project leverages several tools and libraries to perform OSINT gathering, data validation, and secure API integration:

### **Core Tools**
1. **Sherlock**:
   - **Purpose**: Searches for usernames across platforms like Twitter, Facebook, Instagram, TikTok, and LinkedIn.
   - **Where It Is Used**: 
     - Runs as a subprocess in `username_search.py` to check for username mentions.
   - **Why Chosen**: Sherlock is a widely used OSINT tool for username enumeration, offering extensive platform coverage and reliable results.

2. **Social Analyzer**:
   - **Purpose**: Searches for username mentions across multiple platforms and analyzes social media activity.
   - **Where It Is Used**: 
     - Used in `username_search.py` to complement Sherlock by providing additional insights into username mentions.
   - **Why Chosen**: Social Analyzer supports a wide range of platforms and provides detailed analysis, making it a valuable addition to username searches.

### **3. BeautifulSoup**
- **Purpose**: Scrapes publicly available personal information (e.g., name, address, phone) from directory websites.
- **Where It Is Used**: 
  - Used in `name_search.py` to parse HTML responses and extract relevant data from Fonecta and other directory websites.
- **Why Chosen**: BeautifulSoup is lightweight, efficient, and widely used for web scraping tasks. It allows for easy parsing of static HTML content to extract structured data.
#### **Handling Anti-Scraping Measures**
Fonecta may have implemented anti-scraping measures, such as:
- **CAPTCHAs**: If a CAPTCHA is present, the HTML response will not contain the expected data.
- **Dynamic Content Loading**: If the data is loaded via JavaScript, the static HTML response will not include the required `<script>` tag.
**Important Note**:  
Using tools like Selenium to bypass these measures may violate Fonecta's Terms of Service (ToS). Users are strongly advised to:
- Review and comply with Fonecta's ToS.
- Avoid bypassing protections like CAPTCHAs or JavaScript-based content loading.
- Use publicly available data responsibly and ethically.
- Seek permission or use an official API (if available) for accessing data.
This tool is intended for ethical use only and should not be used to extract sensitive or private information, such as personal addresses or phone numbers, without proper authorization.

4. **SerpAPI**:
   - **Purpose**: Fetches Google search results for full-name searches.
   - **Where It Is Used**: 
     - Used in `name_search.py` to extract snippets, phone numbers, and city information from search results.
   - **Why Chosen**: SerpAPI provides structured and reliable Google search results, simplifying data extraction.

5. **api_cache**:
   - **Purpose**: Caches API responses to reduce redundant requests and handle rate-limiting.
   - **Where It Is Used**: 
     - Implemented in `rate_cache_time.py` to store and retrieve cached responses for all API-related modules.
   - **Why Chosen**: Improves performance and ensures compliance with API rate limits by minimizing unnecessary requests.

---

### **Supporting Libraries**
1. **dotenv**:
   - **Purpose**: Manages sensitive information (e.g., API keys) securely using environment variables.
   - **Where It Is Used**: 
     - Loads API keys from the .env file in `utils.py`.
   - **Why Chosen**: Ensures sensitive information is not hard-coded into the source code, improving security.

2. **requests**:
   - **Purpose**: Handles HTTP requests to APIs.
   - **Where It Is Used**: 
     - Used in all API-related modules (e.g., `name_search.py`, `ip_search.py`, `username_search.py`) to fetch data from external APIs.
   - **Why Chosen**: Simple, reliable, and widely used for making HTTP requests in Python.

3. **argparse**:
   - **Purpose**: Parses command-line arguments for the CLI tool.
   - **Where It Is Used**: 
     - Used in `cli.py` to handle user input and call the appropriate search functions.
   - **Why Chosen**: Built-in Python library for command-line argument parsing, requiring no additional dependencies.

4. **time**:
   - **Purpose**: Implements delays to handle rate-limiting.
   - **Where It Is Used**: 
     - Used in `rate_cache_time.py` to introduce delays between API requests.
   - **Why Chosen**: Simple and effective for managing time-based operations.

5. **rich**:
   - **Purpose**: Creates visually appealing ASCII tables and styled terminal output.
   - **Where It Is Used**: 
     - Used in CLI modules (e.g., `cli_ip.py`, `cli_name.py`, `cli_username.py`) to display search results in a structured and colorful format.
   - **Why Chosen**: Enhances the user experience by making terminal output more readable and engaging.

6. **re**:
   - **Purpose**: Validates and extracts phone numbers using regex.
   - **Where It Is Used**: 
     - Used in `name_search.py` to extract and validate phone numbers from text.
   - **Why Chosen**: Regex is a powerful and efficient tool for pattern matching and data validation.

7. **json**:
   - **Purpose**: Processes JSON responses from APIs and Fonecta.
   - **Where It Is Used**: 
     - Used in `name_search.py`, `ip_search.py`, and `username_search.py` to parse and process API responses.
   - **Why Chosen**: Built-in Python library for handling JSON data, making it easy to work with structured API responses.

---

## **Ethical Considerations**

This project adheres to ethical guidelines for web scraping and OSINT gathering. Below are the key considerations and how they are addressed:

### **1. Web Scraping**
- **Concern**: Scraping websites without permission can violate terms of service and overload servers.
- **Solution**:
  - The tool only scrapes publicly available data.
  - It respects `robots.txt` files and avoids excessive requests to servers.

### **2. Data Privacy**
- **Concern**: Collecting personal information can infringe on privacy rights.
- **Solution**:
  - The tool only gathers data that is publicly available and voluntarily shared by users.
  - It does not store or share data beyond the scope of the project.

### **3. Legal and Ethical Restrictions on Name Searches**
- **Concern**: Scraping personal information (e.g., names, addresses, phone numbers) from websites like Fonecta may violate privacy laws, terms of service, or ethical guidelines.
- **Solution**:
  - The tool uses BeautifulSoup to extract publicly available data but respects anti-scraping measures such as CAPTCHAs and dynamic content loading.
  - Users are strongly advised to:
    - Review and comply with Fonecta's Terms of Service.
    - Avoid bypassing protections like CAPTCHAs or JavaScript-based content loading.
    - Use publicly available data responsibly and ethically.
    - Seek permission or use an official API (if available) for accessing data.
  - The tool is intended for ethical use only and should not be used to find sensitive information like private addresses or phone numbers.

### **4. Rate Limiting**
- **Concern**: Exceeding API rate limits can lead to throttling or bans.
- **Solution**:
  - The tool implements delays between API requests using `time.sleep`.
  - It caches API responses to minimize redundant requests.

### **5. Sensitive Information Protection**
- **Concern**: Hard-coding API keys in the source code can expose them to unauthorized access.
- **Solution**:
  - API keys are stored in a .env file and accessed securely using the `dotenv` library.
  - The .env file is excluded from version control using .gitignore.

### **6. Ethical Use of Data**
- **Concern**: OSINT tools can be misused for malicious purposes.
- **Solution**:
  - The tool is intended for educational and ethical purposes only.
  - Users are encouraged to comply with local laws and ethical guidelines when using the tool.

---

## **Testing**

Run all tests using the `run_tests.sh` script:
```bash
chmod +x run_tests.sh
./run_tests.sh
```
---

## **Disclaimer**

This tool is intended for **educational and ethical purposes only**. Users are strongly advised to:
- Comply with all applicable laws and regulations in their jurisdiction.
- Respect the terms of service of any websites or APIs accessed using this tool.
- Avoid using this tool for malicious purposes, such as unauthorized data collection or privacy violations.

The developer of this tool is not responsible for any misuse or legal consequences arising from its use.

---

##

Laura Levistö

05/2025