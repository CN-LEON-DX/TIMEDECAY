# TimeDecay: Image Decay Over Time App

TimeDecay allows users to upload an image and watch a video simulation of how the image decays over time. The process is akin to natural erosion, where elements like water, wind, temperature, or other natural forces affect the image, gradually causing it to fade, distort, or be "destroyed" in creative ways.

## Main Objective of the App

- Create videos simulating the decay of images over time, influenced by natural elements like water, wind, temperature, and erosion.
- Provide customizable decay effects for the users.
- Serve as an artistic tool for exploring the passage of time and the transformation of an image.

## App Flow

### 1. Welcome Screen

When the user opens the app, they will see a simple welcome screen. Here, they can either sign up or log in via email.

**Features:**
- Email Sign-up/Login
- Google Sign-up/Login
- Apple Sign-up/Login
- After successful login, the user is redirected to the Main Dashboard.

### 2. Main Dashboard

After logging in, the user lands on the Main Dashboard. On this screen, they will see their tasks sorted by AI priority, which helps them focus on one task at a time.

**Features:**
- **Uploaded Image List:** Shows the images that the user has previously uploaded.
- **Create New Image:** Allows the user to upload a new image to create the decay simulation.
- **Edit Created Videos:** Users can revisit and edit previously created videos if necessary.
- **Save and Share Videos:** Save the generated decay videos and share them on social media platforms like Instagram, Facebook, YouTube, etc.

### 3. Upload Image

Users can upload their favorite image (e.g., portrait, landscape, family photo, etc.).

**Features:**
- Upload from gallery or take a new photo.
- Supports various image formats (JPEG, PNG, BMP).
- Displays the uploaded image with basic editing options (crop, rotate, resize).

### 4. Create Decay Simulation

Once the image is uploaded, users can select different decay effects to simulate the decay process over time.

**Features:**
- **Select Decay Effects:**
  - **Water Flow:** The image gradually becomes blurred, washed away, and loses parts due to water effects (e.g., rain, ocean waves).
  - **Wind and Time:** The image is gradually blown away, faded, or eroded over time, like being affected by wind or time itself.
  - **Erosion by Rocks:** The image cracks or breaks apart layer by layer, as if being worn down by a rough surface.
  - **Fire and Heat:** The image is burned or scorched, with parts of the image turning black or being torn over time.
  - **Time Deformation:** The image fades, gets dirty, or slowly distorts, representing the effects of time passing.
- **Adjust Simulation Speed:** Users can adjust the speed of the decay process (from a few seconds to minutes or even hours).
- **Adjust Intensity of Effects:** Users can customize the strength of each effect, e.g., light water flow, strong wind, extreme heat.
- **Preview Simulation:** Before generating the video, users can preview the decay simulation to fine-tune the effects.

### 5. Create Artistic Video

Once the decay process is complete, users can edit the video by adding background music, sound effects, and even a message.

**Features:**
- **Add Background Music:** Users can select music from an in-app library or upload their own.
- **Sound Effects:** Add sound effects like rain, wind, or fire to make the simulation more realistic.
- **Add Story or Message:** Users can include text that tells a story or adds meaning to the image. For example, a narrative like "the journey of a photo over time" or reflecting on memories fading away.

### 6. Save and Share

After the video is generated, users can save the video and share it on various social media platforms.

**Features:**
- **Save Video:** Save to personal library.
- **Share on Social Media:** Share the video on platforms like Instagram, Facebook, TikTok, YouTube, or via email.
- **Export Options:** Users can export the video in different formats (MP4, GIF) and resolutions (HD, 4K).

### 7. Explore Artistic Videos

The app provides a space where users can explore other artistic videos created by others.

**Features:**
- **Explore Videos:** Browse and discover decay videos created by other users.
- **Comment and Rate:** Users can comment on and rate videos from the community.
- **Save Favorite Videos:** Add liked videos to the user's personal collection.

## Additional Features

### A. User Personalization

- **Sign in and Manage Account:** Users can sign in using their email and manage their account (change password, view history of created videos, etc.).
- **Notifications:** Receive notifications for app updates or when a video is successfully shared.

### B. Explore and Share

- **Explore Creative Videos:** Users can discover creative videos made by others and share their feedback.
- **Viral Video Creation:** Videos with unique and impactful effects can become viral on social media platforms like Instagram, YouTube, etc.

# Tech Stack for TimeDecay App

## **Frontend (React Native for Cross-Platform)**

- **React Native** (JavaScript/TypeScript)
- **FFmpeg** (react-native-ffmpeg plugin) for video rendering
- **Image Manipulation** using libraries like `react-native-image-editor`, `react-native-opencv3`
- **Supabase Auth** for user authentication
- **Supabase Storage** for storing images and videos
- **Supabase Real-time** (optional) for notifications and updates

## **Backend (Golang for Video Processing)**

- **Golang** for image and video processing, using libraries like:
  - `go-ffmpeg`
  - `go-opencv`
  - `ImageMagick`
- **Supabase Database** (PostgreSQL) for storing user data and video metadata
- **Supabase Storage** for managing image and video files (file uploads and downloads)
- **Supabase API** (auto-generated RESTful API) for data interactions

## **Cloud & Hosting**

- **Supabase** for database, authentication, and storage
- **DigitalOcean**, **AWS**, or **Heroku** for hosting the Golang backend

-- Users Table
CREATE TABLE users (
id SERIAL PRIMARY KEY,
email VARCHAR(255) UNIQUE NOT NULL,
password_hash VARCHAR(255) NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
-- Images Table
CREATE TABLE images (
id SERIAL PRIMARY KEY,
user_id INT REFERENCES users(id) ON DELETE CASCADE,
image_url VARCHAR(255) NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
-- Videos Table
CREATE TABLE videos (
id SERIAL PRIMARY KEY,
user_id INT REFERENCES users(id) ON DELETE CASCADE,
video_url VARCHAR(255) NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
-- Decay Effects Table
CREATE TABLE decay_effects (
id SERIAL PRIMARY KEY,
name VARCHAR(50) NOT NULL,
description TEXT,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
-- User Video Preferences Table
CREATE TABLE user_video_preferences (
id SERIAL PRIMARY KEY,
user_id INT REFERENCES users(id) ON DELETE CASCADE,
video_id INT REFERENCES videos(id) ON DELETE CASCADE,
effect_id INT REFERENCES decay_effects(id),
simulation_speed INT,
intensity INT,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
-- Comments Table
CREATE TABLE comments (
id SERIAL PRIMARY KEY,
video_id INT REFERENCES videos(id) ON DELETE CASCADE,
user_id INT REFERENCES users(id) ON DELETE CASCADE,
content TEXT NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

## Optional Folder Structure