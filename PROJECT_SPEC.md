# AI Video Clipper

## 1. Problem Statement

What problem does this application solve?
Problem No. 1 - Takes Long time (1+ Hours for 1 Video) to find and clip viral moments from long videos. Time can be reduced to less than 5-10 mins / video.
Problem No. 2 - Takes long time (1-2 Hours) to post 1 video on Yt, Insta, Tiktok, X, Fb. Time can be reduced to less than 5-10 mins / video.
2-3 Hours work can be done in less 30 mins. 

Creating short-form videos from long-form content is time-consuming and requires manual editing skills.

Content creators, YouTubers, podcasters, and social media managers often need to watch lengthy videos, identify interesting moments, cut them into shorter segments, add captions, and resize them for platforms like TikTok, Instagram Reels, and YouTube Shorts.

Our application will automate this process using AI.

The goal: Build a web application that allows users to upload a long video and automatically generates multiple short, engaging clips ready to publish on social media.

## 2. Target Users

Who will use this application?
Clippers, Video Editors, Agencies, Creators 

## 3. Main Features

What can users do?
Paste a link or drop a raw take, and this app clips, edits, sizes and publishes them to all social platforms in one click.

Upload a video file (MP4/MOV) with progress indication
Automatic transcription - Automatically convert video speech into text.
AI selection of the most engaging moments (hook, complete thought, good length)
Virality or quality score with a short reason per clip
Auto-crop from 16:9 to 9:16
Auto-generated captions burned into the video
Clip preview, trim adjustment, and caption text editing
Download clips as MP4
Dashboard with project history and processing status

## 4. User Journey

Explain what happens from uploading
a video to downloading generated clips.

Sign up / log in and land on the dashboard.
Upload a long video. The file goes directly to storage, and a project is created.
Processing starts in the background. The user sees live status: Uploading → Extracting audio → Transcribing → Finding highlights → Rendering clips.
Backend pipeline (queued jobs):
FFmpeg extracts the audio
A speech-to-text API returns the transcript with timestamps
An LLM reads the transcript and returns 5-10 candidate clips (start, end, title, score)
FFmpeg cuts each segment, crops to 9:16, and burns in captions
Review: the user sees a grid of generated clips with titles and scores, and can preview each one.
Edit (light): adjust start/end times or fix caption text, then re-render.
Download individual clips or all of them.

## 5. MVP Requirements

What exactly will version 1 support?

Auth: email and password signup/login (JWT)
Input: file upload only, one video up to about 30 minutes and a size limit 500 MB, one language
Pipeline: BullMQ + Redis job queue, FFmpeg for media processing, one transcription API, one LLM API
Highlight Detection - 	AI identifies interesting moments
Output: 3-8 clips per video, 9:16, 10-60 seconds each, captions burned in, MP4 download
Editing -	Basic start/end timestamp adjustment
UI: upload page, processing status page, clips gallery with preview and download

Stack: React, Tailwind CSS, Node/Express, MongoDB, Authentication- JWT, Video Processing - FFmpeg, AI Transcription - OpenAI Audio API or another transcription provider, AI Highlight Detection - LLM API, Background Processing -	BullMQ + Redis, File Storage- S3-compatible storage or Cloudinary, all JavaScript
Limits: a simple usage cap per user to control API costs, no payments yet

## 6. Out of Scope

What features will we not build initially?

YouTube/URL import (adds download and legal complexity)
Payments, subscriptions, and billing
Full timeline video editor
Smart face tracking or speaker-aware reframing (use a simple center crop first)
Multiple caption styles, templates, brand kits, and custom fonts
B-roll, music, emojis, and animated effects
Direct publishing or scheduling to social platforms
Team workspaces, collaboration, and an API for developers
Multi-language support beyond the first language
Mobile app
Self-hosted AI models (use APIs for now)

##  V1 Product Goal

Long video → Short clips
The user uploads one video, and our application automatically:
1. Transcribes the audio.
2. Identifies 3–5 interesting moments.
3. Extracts those moments using FFmpeg.
4. Generates subtitles.
5. Converts clips into vertical format.
6. Allows the user to preview and download them.
Success criteria: A user can upload a video and receive usable, downloadable short-form clips without manually editing the video.

## Development Strategy

1. Phase 1 – Frontend foundation: React dashboard, upload interface, video preview, and clip listing.
2. Phase 2 – Backend foundation: Express server, MongoDB, authentication, and video upload.
3. Phase 3 – Video processing: Learn and integrate FFmpeg using Node.js.
4. Phase 4 – AI integration: Transcription and highlight detection.
5. Phase 5 – Clip generation: Automatically extract, resize, and caption clips.
6. Phase 6 – Finalization: Preview, editing, downloading, testing, and deployment.