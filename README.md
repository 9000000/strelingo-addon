# Strelingo Stremio Addon

This Stremio addon fetches subtitles for movies and series from OpenSubtitles and merges two language tracks into a single subtitle file. This is particularly useful for language learners who want to see subtitles in both their native language and the language they are learning simultaneously.

![Ekran görüntüsü 2025-04-18 142351](https://github.com/user-attachments/assets/d2441e6c-82b7-4115-876d-1af0e419f6df)

## Easy deploy to vercel
You can easily deploy this addon and host it yourself on vercel by clicking button below. The free hobby plan is more than enough for personal uses. You may need to setup vercel blob storage btw.

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/import/project?template=https://github.com/Serkali-sudo/strelingo-addon)

## Demo Live Addon Url
You can either add the Stremio addon by copying this and use add addon in stremio:
 ```bash 
 https://strelingo-addon.vercel.app/manifest.json
 ```
or visit the addon page here:  
[https://strelingo-addon.vercel.app](https://strelingo-addon.vercel.app).

## Providers
* OpenSubtitles.
* [Buta no subs Stremio addon](https://github.com/Pigamer37/buta-no-subs-stremio-addon) for better japanese subtitles (Implemented by @Pigamer37).

## Features

*   Fetches subtitles from OpenSubtitles.
*   Automatically detects the best available subtitles for two selected languages.
*   Handles Gzip compressed subtitles.
*   Detects and decodes various character encodings (using `chardet` and `iconv-lite`) to support languages with special characters.
*   Merges the main language and translation language subtitles into a single `.srt` file.
*   Formats the translation line to be *italic* and <font color="yellow">yellow</font> (configurable in `index.js`).
*   Configurable via Stremio addon settings for:
    *   Main Language (Audio Language)
    *   Translation Language (Your Language)

## Requirements

*   [Node.js](https://nodejs.org/) (Version 14 or higher recommend)
*   [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
*   You will need either vercel blob key or supabase storage credentials. Because the addon creates a brand new srt everytime and it has to host somewhere. you can put those credentials in .env (You can techinally return the subtitle as base64 but i have found that it only works for stremio 4 version, it didnt worked in stremio 5 or mobile stremio)
*   If you want vercel blob create a vercel blob in vercel and copy the token and put it in your env named BLOB_READ_WRITE_TOKEN
*   If you want supabase storage instead of vercel you will need to copy SUPABASE_URL, SUPABASE_SERVICE_KEY, SUPABASE_ANON_KEY credentials from your supabase account.


## Local Setup

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/Serkali-sudo/strelingo-addon
    cd strelingo-addon
    ```
2.  **Install dependencies:**
    ```bash
    npm install
    # or
    # yarn install
    ```

## Running the Addon Locally

1.  **Start the addon server:**
    ```bash
    npm start
    # or
    # yarn start
    ```
2.  The console will output messages indicating the server is running.

## Installing and Configuring in Stremio

1.  Ensure the addon server is running locally (see "Running the Addon Locally").
2.  Open your web browser and navigate to the addon's local address (usually `http://localhost:7000/` or the address shown in the console when you start the server).
3.  On the addon configuration page that loads:
    *   Select your desired **Main Language** (typically the language the audio is in).
    *   Select your desired **Translation Language** (typically your native language or the one you want for comparison).
4.  Click the "Install Addon" button or link displayed on the page (it might be at the bottom).
5.  Your browser might ask for permission to open the link with Stremio. Allow it.
6.  Stremio should open and prompt you to confirm the installation **with your selected configuration**. Click "Install".

The addon is now installed and configured with your chosen languages.

## Technical Details

*   **Backend:** Node.js
*   **Stremio SDK:** `stremio-addon-sdk`
*   **Subtitle Source:** OpenSubtitles API, [Buta no subs Stremio addon](https://github.com/Pigamer37/buta-no-subs-stremio-addon)
*   **HTTP Requests:** `axios`
*   **Subtitle Parsing:** `srt-parser-2`
*   **Gzip Decompression:** `pako`
*   **Character Encoding Detection:** `chardet`
*   **Character Encoding Decoding:** `iconv-lite`
