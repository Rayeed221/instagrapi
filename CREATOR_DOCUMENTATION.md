# Instagram Content Creator Guide - instagrapi Library

**Last Updated:** December 9, 2025
**Library Version:** Latest from GitHub
**Repository:** https://github.com/adw0rd/instagrapi

---

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Professional Use Cases](#professional-use-cases)
3. [Installation & Setup](#installation--setup)
4. [Authentication](#authentication)
5. [Content Creation & Posting](#content-creation--posting)
6. [Engagement & Analytics](#engagement--analytics)
7. [Community Management](#community-management)
8. [Advanced Features](#advanced-features)
9. [Best Practices](#best-practices)
10. [API Reference](#api-reference)
11. [Troubleshooting](#troubleshooting)
12. [External Resources](#external-resources)

---

## Executive Summary

**instagrapi** is a Python library that provides programmatic access to Instagram's Private API. It enables professional content creators to:

- Automate content posting across multiple formats (photos, videos, reels, stories)
- Access detailed analytics and performance metrics
- Manage community interactions (comments, DMs, follows)
- Create dynamic content workflows
- Scale content management operations
- Maintain engagement with audiences programmatically

**Key Strengths:**
- Full-featured API wrapper (80+ methods)
- Support for modern Instagram features (Reels, Highlights, Collections)
- 2FA security support
- Multi-account management
- Session persistence
- Proxy support for distributed operations

**Target Users:**
- Professional content creators
- Content agencies
- Marketing teams
- Community managers
- Influencers with multiple accounts
- Automated content management systems

---

## Professional Use Cases

### 1. **Automated Content Publishing Workflow**

**Use Case:** Post pre-planned content at optimal times across multiple formats

```
Creator Dashboard → Schedule Posts → API Publishes → Analytics Tracking
```

**Components:**
- Photo posting (feed + stories)
- Video/Reel publishing
- Album (carousel) uploads
- Batch scheduling
- Caption templates
- Hashtag management

**Relevant Methods:**
- `cl.photo_upload()` - Feed photos
- `cl.video_upload()` - Feed videos
- `cl.album_upload()` - Carousels
- `cl.clip_upload()` - Reels
- `cl.photo_upload_to_story()` - Story photos
- `cl.video_upload_to_story()` - Story videos

---

### 2. **Multi-Account Management**

**Use Case:** Manage content across multiple creator accounts or brand accounts

```
Account A → Scheduled Posts
Account B → Scheduled Posts
Account C → Scheduled Posts
```

**Key Features:**
- Login/logout between accounts
- Session persistence per account
- Separate settings management
- Independent analytics per account

**Relevant Methods:**
- `cl.login()` - Authenticate account
- `cl.dump_settings()` - Save session
- `cl.load_settings()` - Load session
- `cl.relogin()` - Re-authenticate

---

### 3. **Community Engagement & Moderation**

**Use Case:** Manage audience interactions programmatically

```
Comments → Filter/Moderate → Respond → Track Engagement
```

**Components:**
- Comment monitoring and filtering
- Comment moderation
- DM management
- Follow/unfollow automation
- Engagement tracking

**Relevant Methods:**
- `cl.media_comments()` - Get post comments
- `cl.media_comment()` - Post reply
- `cl.direct_threads()` - Get DM threads
- `cl.direct_send()` - Send messages
- `cl.comment_bulk_delete()` - Delete comments
- `cl.media_likers()` - Track engagement

---

### 4. **Analytics & Performance Tracking**

**Use Case:** Collect and analyze content performance metrics

```
Posts → Collect Data → Analyze Trends → Optimize Strategy
```

**Metrics Available:**
- Account-level insights (followers, reach, impressions)
- Per-post metrics (likes, comments, saves, shares)
- Follower growth
- Engagement rates
- Story performance

**Relevant Methods:**
- `cl.insights_account()` - Account analytics
- `cl.insights_media()` - Post-level metrics
- `cl.insights_media_feed_all()` - Batch media insights
- `cl.media_likers()` - Like data
- `cl.media_comments()` - Comment metrics

---

### 5. **Story Highlights & Collections Management**

**Use Case:** Curate and organize evergreen content

```
Stories → Highlights → Collections → Persistent Content Library
```

**Use Cases:**
- Save best-performing posts
- Create highlight reels from stories
- Organize content by category
- Build content libraries

**Relevant Methods:**
- `cl.highlight_create()` - Create highlight
- `cl.highlight_edit()` - Update highlight
- `cl.media_save()` - Save posts
- `cl.collections()` - Manage collections
- `cl.collection_medias()` - Get saved posts

---

### 6. **Hashtag Research & Strategy**

**Use Case:** Optimize reach through hashtag strategy

```
Research Hashtags → Get Performance Data → Plan Content → Track Results
```

**Available Data:**
- Hashtag popularity
- Top/recent posts
- Related hashtags
- Post counts
- Engagement metrics

**Relevant Methods:**
- `cl.hashtag_info()` - Hashtag statistics
- `cl.hashtag_medias_top()` - Top posts (hashtag)
- `cl.hashtag_medias_recent()` - Recent posts (hashtag)
- `cl.hashtag_related_hashtags()` - Related hashtags
- `cl.hashtag_follow()` - Follow hashtags

---

### 7. **Location-Based Content Strategy**

**Use Case:** Leverage location data for local engagement

```
Location Search → Get Posts → Analyze → Target Local Audience
```

**Features:**
- Location discovery
- Location-based posts
- Geo-tagging
- Local hashtags
- Location guides

**Relevant Methods:**
- `cl.location_search()` - Find locations
- `cl.location_info()` - Location details
- `cl.location_medias_top()` - Top location posts
- `cl.location_medias_recent()` - Recent location posts
- Post upload with location tagging

---

### 8. **Content Repurposing & Distribution**

**Use Case:** Download, modify, and redistribute content

```
Download Content → Process → Republish → Cross-Platform Distribution
```

**Download Options:**
- Photos (any resolution)
- Videos/Reels (high quality)
- Albums (all resources)
- Stories (before expiration)
- IGTV content

**Relevant Methods:**
- `cl.photo_download()` - Download photos
- `cl.video_download()` - Download videos
- `cl.album_download()` - Download carousels
- `cl.clip_download()` - Download reels
- `cl.story_download()` - Download stories

---

### 9. **Trend Monitoring & Competitive Analysis**

**Use Case:** Monitor trends and competitor activity

```
Follow Competitors → Track Hashtags → Monitor Explore Page → Identify Trends
```

**Monitoring Capabilities:**
- User media tracking
- Hashtag monitoring
- Explore feed analysis
- Reels timeline
- Related hashtag tracking

**Relevant Methods:**
- `cl.user_medias()` - Track user posts
- `cl.hashtag_medias_reels()` - Trending reels
- `cl.explore_reels()` - Explore page
- `cl.reels()` - Reel timeline
- `cl.hashtag_related_hashtags()` - Trend discovery

---

### 10. **Direct Message Campaigns**

**Use Case:** Run targeted DM campaigns and customer service

```
Audience Segment → Draft Message → Send via API → Track Responses
```

**DM Capabilities:**
- Text messages
- Media sharing (photos, videos)
- Thread management
- Pending message handling
- Presence tracking
- Message reactions

**Relevant Methods:**
- `cl.direct_send()` - Text messages
- `cl.direct_send_photo()` - Photo DMs
- `cl.direct_send_video()` - Video DMs
- `cl.direct_threads()` - Get conversations
- `cl.direct_message_seen()` - Mark seen

---

## Installation & Setup

### System Requirements

```
Python: >= 3.9
Platform: Linux, macOS, Windows
```

### Installation Methods

#### Option 1: Install from PyPI (Stable Release)

```bash
pip install instagrapi
```

#### Option 2: Install from GitHub (Latest Development)

```bash
git clone https://github.com/adw0rd/instagrapi.git
cd instagrapi
pip install -e .
```

#### Option 3: Install with Optional Dependencies

```bash
# For video processing support
pip install instagrapi[video]

# For all features
pip install instagrapi[all]
```

### Project Dependencies

The library requires:

```
requests==2.32.5          # HTTP client
PySocks==1.7.1            # Proxy support
pydantic==2.12.4          # Data validation
moviepy==1.0.3            # Video processing
pycryptodomex==3.23.0     # Encryption
```

### Verify Installation

```python
from instagrapi import Client

# Should complete without errors
cl = Client()
print(f"instagrapi version: {cl.__class__.__module__}")
```

---

## Authentication

### Basic Login

**File Reference:** `instagrapi/mixins/auth.py`

```python
from instagrapi import Client

cl = Client()
cl.login(username="your_username", password="your_password")

# Get authenticated user ID
print(f"Logged in as user ID: {cl.user_id}")
```

### Session Persistence

Save and load sessions to avoid repeated logins:

```python
# Save session after login
cl.login(username="your_username", password="your_password")
cl.dump_settings("session.json")

# Load session in future runs
from instagrapi import Client
cl = Client()
cl.load_settings("session.json")

# Verify session is valid
print(cl.account_info())
```

### Two-Factor Authentication (2FA)

**Supported Methods:**
- TOTP (Time-based One-Time Password) - Authenticator apps
- SMS verification
- Email verification

```python
from instagrapi import Client

cl = Client()

# Login will pause for 2FA
try:
    cl.login(
        username="your_username",
        password="your_password",
        # Will prompt for verification code if 2FA is enabled
    )
except Exception as e:
    print(f"2FA required: {e}")
    # Provide verification code manually
    verification_code = input("Enter 2FA code: ")
    cl.login(
        username="your_username",
        password="your_password",
        verification_code=verification_code
    )
```

### Multi-Account Setup

```python
from instagrapi import Client

# Account 1
cl1 = Client()
cl1.login(username="account1_username", password="account1_password")
cl1.dump_settings("account1_session.json")

# Account 2
cl2 = Client()
cl2.login(username="account2_username", password="account2_password")
cl2.dump_settings("account2_session.json")

# Later: Load accounts as needed
cl_account1 = Client()
cl_account1.load_settings("account1_session.json")

cl_account2 = Client()
cl_account2.load_settings("account2_session.json")
```

### Proxy Configuration

For distributed operations or anonymity:

```python
from instagrapi import Client

cl = Client(proxy="http://proxy_server:port")
# or
cl = Client(proxy="socks5://socks_server:port")
```

---

## Content Creation & Posting

### Photo Upload to Feed

**File Reference:** `instagrapi/mixins/photo.py`

```python
from instagrapi import Client

cl = Client()
cl.load_settings("session.json")

# Simple upload
media = cl.photo_upload(
    path="/path/to/photo.jpg",
    caption="Check out this amazing content! 📸\n#photography #content"
)

print(f"Post ID: {media.id}")
print(f"Posted at: {media.taken_at}")
```

**Advanced Upload with Metadata:**

```python
from instagrapi.types import Location, Usertag

# With location tagging
location = Location(
    pk=213988663,  # Location ID
    name="New York, New York"
)

# Tag users in photo
usertags = [
    Usertag(
        user=User(pk=123456789, username="friend_username"),
        x=0.5,  # X coordinate (0-1)
        y=0.5   # Y coordinate (0-1)
    )
]

media = cl.photo_upload(
    path="/path/to/photo.jpg",
    caption="Amazing collaboration! 🤝",
    location=location,
    usertags=usertags
)
```

### Photo Upload to Stories

```python
from instagrapi.types import StoryMention, StoryLink, StoryHashtag

# Simple story
story = cl.photo_upload_to_story(
    path="/path/to/photo.jpg",
    caption="Check my story!"
)

# Story with interactive elements
story = cl.photo_upload_to_story(
    path="/path/to/photo.jpg",
    caption="New content incoming!",
    mentions=[
        StoryMention(
            user=User(pk=123456789, username="collaborator"),
            x=0.5,
            y=0.5
        )
    ],
    links=[
        StoryLink(
            webUri="https://example.com/shop",
            x=0.5,
            y=0.5,
            width=1.0,
            height=0.3
        )
    ],
    hashtags=[
        StoryHashtag(
            hashtag=Hashtag(name="photography"),
            x=0.5,
            y=0.5
        )
    ]
)
```

### Video Upload to Feed

**File Reference:** `instagrapi/mixins/video.py`

```python
# Simple video upload
media = cl.video_upload(
    path="/path/to/video.mp4",
    caption="New video content! 🎥\n#video #content"
)

# Upload with custom thumbnail
media = cl.video_upload(
    path="/path/to/video.mp4",
    caption="Epic video!",
    thumbnail="/path/to/thumbnail.jpg"
)
```

### Reel/Clip Upload (With Music)

**File Reference:** `instagrapi/mixins/clip.py`

```python
# Upload as Reel
media = cl.clip_upload(
    path="/path/to/reel.mp4",
    caption="Check out my latest reel! 🎬",
    thumbnail="/path/to/thumbnail.jpg"
)

# Upload Reel with music (if music parameters available)
media = cl.clip_upload_as_reel_with_music(
    path="/path/to/reel.mp4",
    caption="New music reel!",
    music_params={
        "music_canonical_id": "music_id",
        "music_info": "track_info"
    }
)
```

### Album/Carousel Upload

**File Reference:** `instagrapi/mixins/album.py`

```python
# Upload carousel (multiple photos/videos)
media = cl.album_upload(
    paths=[
        "/path/to/photo1.jpg",
        "/path/to/photo2.jpg",
        "/path/to/video.mp4",
        "/path/to/photo3.jpg"
    ],
    caption="Carousel post! Swipe to see more ➡️\n#carousel #content"
)

print(f"Carousel ID: {media.id}")
print(f"Resources: {len(media.resources)}")
```

### Story with Custom Background (StoryBuilder)

**File Reference:** `instagrapi/story.py`

```python
from instagrapi.story import StoryBuilder

# Create story with background
builder = StoryBuilder(
    path="/path/to/background.jpg",
    caption="Check this out!"
)

# Add text overlay
story_build = builder.photo(
    max_duration=15,
    font="Arial",
    fontsize=100,
    color="white",
    link="https://example.com"
)

# Upload built story
uploaded_story = cl.photo_upload_to_story(
    path=story_build.path,
    caption="Custom story"
)
```

### IGTV Upload

**File Reference:** `instagrapi/mixins/igtv.py`

```python
media = cl.igtv_upload(
    path="/path/to/video.mp4",
    title="New IGTV Episode",
    caption="Long-form video content here!",
    thumbnail="/path/to/thumbnail.jpg"
)
```

### Batch Upload Workflow

```python
from pathlib import Path
from datetime import datetime, timedelta

# Schedule posts with time intervals
posts = [
    {"path": "photo1.jpg", "caption": "Post 1"},
    {"path": "photo2.jpg", "caption": "Post 2"},
    {"path": "video.mp4", "caption": "Post 3"}
]

# Upload with delays to avoid rate limiting
import time

for idx, post in enumerate(posts):
    try:
        media = cl.photo_upload(
            path=post["path"],
            caption=post["caption"]
        )
        print(f"✓ Uploaded: {post['path']}")

        # Wait between posts (avoid rate limiting)
        if idx < len(posts) - 1:
            time.sleep(60)  # Wait 60 seconds between posts

    except Exception as e:
        print(f"✗ Failed: {post['path']} - {e}")
```

---

## Engagement & Analytics

### Accessing Analytics

**File Reference:** `instagrapi/mixins/insights.py`

#### Account-Level Insights

```python
# Get overall account metrics
insights = cl.insights_account()

# Returns metrics like:
# - followers_count
# - reach
# - impressions
# - website_clicks
# - phone_call_clicks
# - email_clicks
# - text_message_clicks
# - profile_views
```

#### Post-Level Insights

```python
# Get metrics for specific post
post_insights = cl.insights_media(media_pk=123456789)

# Available metrics:
# - engagement (likes + comments + shares)
# - impressions
# - reach
# - shares
# - saves
# - comments_count
# - likes_count
# - profile_views (if video)
# - video_views (if video)
# - exits (if video)
# - replies (if video)
```

#### Batch Analytics

```python
# Get insights for multiple posts
insights = cl.insights_media_feed_all(
    post_type="REEL",          # ALL, FEED, IGTV, REEL
    time_frame="ONE_WEEK",     # ONE_DAY, ONE_WEEK, ONE_MONTH, TWO_MONTHS, THREE_MONTHS, SIX_MONTHS
    data_ordering="REACH_COUNT", # REACH_COUNT, ENGAGEMENT_COUNT, SAVE_COUNT, SHARE_COUNT, LIKE_COUNT, COMMENT_COUNT, PROFILE_VIEW_COUNT
    count=10                    # Number of posts
)

# Analyze trending posts
for media_insight in insights:
    print(f"Post: {media_insight['media_id']}")
    print(f"Reach: {media_insight['reach']}")
    print(f"Engagement: {media_insight['engagement']}")
```

### Like Management

```python
# Like a post
cl.media_like(media_id=123456789)

# Unlike a post
cl.media_unlike(media_id=123456789)

# Get who liked a post
likers = cl.media_likers(media_id=123456789)
for user in likers:
    print(f"{user.username} ({user.full_name})")

# Get user's liked media
liked_posts = cl.liked_medias(amount=21)
for media in liked_posts:
    print(f"Liked: {media.caption_text[:50]}")
```

### Comment Management

**File Reference:** `instagrapi/mixins/comment.py`

```python
# Get all comments on a post
comments = cl.media_comments(media_id=123456789, amount=50)

for comment in comments:
    print(f"{comment.user.username}: {comment.text}")

# Post a comment reply
new_comment = cl.media_comment(
    media_id=123456789,
    text="Thanks for sharing! 🙌"
)

# Like a comment
cl.comment_like(comment_pk=comment.pk)

# Pin your comment
cl.comment_pin(media_id=123456789, comment_pk=comment.pk)

# Delete offensive comments
cl.comment_bulk_delete(
    media_id=123456789,
    comment_pks=[comment1.pk, comment2.pk]
)
```

### Follower Tracking

```python
# Get followers list
followers = cl.user_followers(user_id=cl.user_id, amount=100)

for follower in followers:
    print(f"{follower.username} - {follower.full_name}")

# Get following list
following = cl.user_following(user_id=cl.user_id, amount=100)

# Search followers by username
search_results = cl.search_followers(
    user_id=cl.user_id,
    query="john"
)

# Track follower changes
import json
from pathlib import Path

def save_followers_snapshot():
    followers = cl.user_followers(user_id=cl.user_id, amount=0)
    follower_list = [
        {"username": f.username, "user_id": f.pk}
        for f in followers
    ]

    with open("followers.json", "w") as f:
        json.dump(follower_list, f)

    return follower_list

# Compare snapshots to find new/lost followers
old_followers = {f["user_id"] for f in json.load(open("followers.json"))}
new_followers = {f.pk for f in cl.user_followers(user_id=cl.user_id, amount=0)}

new_fans = new_followers - old_followers
lost_followers = old_followers - new_followers

print(f"New followers: {len(new_fans)}")
print(f"Lost followers: {len(lost_followers)}")
```

### Story Analytics

```python
# Get story viewers
story_viewers = cl.story_viewers(story_pk=123456789)

for viewer in story_viewers:
    print(f"{viewer.username} viewed at {viewer.taken_at}")

# Track story performance across time
story_views = []
for user in story_viewers:
    story_views.append({
        "username": user.username,
        "viewed_at": user.taken_at
    })

# Analyze peak viewing times
from collections import Counter

hours = Counter(v["viewed_at"].hour for v in story_views)
peak_hour = hours.most_common(1)[0][0]
print(f"Peak story viewing hour: {peak_hour}:00")
```

---

## Community Management

### Direct Message Management

**File Reference:** `instagrapi/mixins/direct.py`

#### Get Conversations

```python
# Get all DM threads
threads = cl.direct_threads(amount=20)

for thread in threads:
    print(f"Thread: {thread.thread_title or thread.users[0].username}")
    print(f"Last message: {thread.last_permanent_item.text if thread.last_permanent_item else 'No messages'}")
```

#### Send Messages

```python
# Send text message
cl.direct_send(
    text="Hey! Check out my latest content 🎥",
    user_ids=[123456789]
)

# Send to multiple users
cl.direct_send(
    text="New post available!",
    user_ids=[user1_id, user2_id, user3_id]
)

# Send photo via DM
cl.direct_send_photo(
    path="/path/to/photo.jpg",
    user_ids=[123456789]
)

# Send video via DM
cl.direct_send_video(
    path="/path/to/video.mp4",
    user_ids=[123456789]
)
```

#### Manage Pending Requests

```python
# Get pending DM requests
pending = cl.direct_pending_inbox(amount=20)

for thread in pending:
    print(f"Pending from: {thread.users[0].username}")

# Approve pending request
cl.direct_pending_approve(thread_id=thread.id)
```

#### Message Reactions

```python
# Mark message as seen
cl.direct_message_seen(thread_id=thread.id, message_id=message.id)

# Send typing indicator
cl.direct_send_seen(thread_id=thread.id)
```

### Hashtag Management

**File Reference:** `instagrapi/mixins/hashtag.py`

```python
# Research hashtag performance
hashtag_info = cl.hashtag_info(name="photography")

print(f"Hashtag: #{hashtag_info.name}")
print(f"Post count: {hashtag_info.media_count}")
print(f"Following: {hashtag_info.is_following}")

# Get top posts for hashtag
top_posts = cl.hashtag_medias_top(name="photography", amount=9)

for post in top_posts:
    print(f"Post: {post.caption_text[:50]}")
    print(f"Likes: {post.like_count}")

# Get recent posts
recent = cl.hashtag_medias_recent(name="photography", amount=27)

# Find related hashtags
related = cl.hashtag_related_hashtags(name="photography")
for hashtag in related:
    print(f"#{hashtag.name} - {hashtag.media_count} posts")

# Follow/unfollow hashtags
cl.hashtag_follow(hashtag="photography")  # Will show in explore
cl.hashtag_unfollow(hashtag="photography")
```

### Location-Based Engagement

```python
# Find locations
locations = cl.location_search(lat=40.7128, lng=-74.0060)  # New York

for location in locations:
    print(f"{location.name} - {location.address}")

# Get posts from location
location_posts = cl.location_medias_recent(
    location_pk=locations[0].pk,
    amount=27
)

# Tag posts with location
from instagrapi.types import Location

location = Location(
    pk=213988663,
    name="New York, New York",
    address="New York, NY, United States"
)

cl.photo_upload(
    path="photo.jpg",
    caption="Amazing view!",
    location=location
)
```

### Follow/Unfollow Automation

```python
# Follow user
cl.user_follow(user_id=123456789)

# Unfollow user
cl.user_unfollow(user_id=123456789)

# Follow users who follow you
my_followers = cl.user_followers(user_id=cl.user_id, amount=100)

for follower in my_followers:
    try:
        cl.user_follow(user_id=follower.pk)
        print(f"Followed {follower.username}")
    except Exception as e:
        print(f"Failed to follow {follower.username}: {e}")
```

---

## Advanced Features

### Story Highlights

**File Reference:** `instagrapi/mixins/highlight.py`

```python
# Get all highlights
highlights = cl.user_highlights(user_id=cl.user_id)

for highlight in highlights:
    print(f"Highlight: {highlight.title}")

# Create new highlight
highlight = cl.highlight_create(
    title="Best Moments",
    story_pks=[story1_pk, story2_pk, story3_pk],
    cover_path="/path/to/cover.jpg"
)

# Edit highlight
cl.highlight_edit(
    highlight_pk=highlight.pk,
    title="Top Highlights",
    story_pks=[story1_pk, story2_pk, story4_pk]
)

# Add stories to existing highlight
cl.highlight_add_stories(
    highlight_pk=highlight.pk,
    story_pks=[story5_pk]
)

# Remove stories
cl.highlight_remove_stories(
    highlight_pk=highlight.pk,
    story_pks=[story1_pk]
)

# Delete highlight
cl.highlight_delete(highlight_pk=highlight.pk)
```

### Collections & Saved Posts

**File Reference:** `instagrapi/mixins/collection.py`

```python
# Get all collections
collections = cl.collections()

for collection in collections:
    print(f"Collection: {collection.title}")

# Save post to collection
cl.media_save(
    media_id=123456789,
    collection_pk=collection.pk  # Optional: specify collection
)

# Get posts in collection
saved_posts = cl.collection_medias(
    collection_pk=collection.pk,
    amount=50
)

# Unsave post
cl.media_unsave(media_id=123456789)
```

### Account Settings Management

**File Reference:** `instagrapi/mixins/account.py`

```python
# Get account info
account = cl.account_info()

print(f"Username: {account.username}")
print(f"Full Name: {account.full_name}")
print(f"Biography: {account.biography}")
print(f"Followers: {account.follower_count}")

# Edit profile
cl.account_edit(
    username="new_username",
    full_name="New Full Name",
    biography="New bio with #hashtags and links",
    external_url="https://mywebsite.com"
)

# Update profile picture
cl.account_change_picture(path="/path/to/profile_pic.jpg")

# Set account to private
cl.account_set_private()

# Set account to public
cl.account_set_public()

# Change password
cl.change_password(
    old_password="old_pass",
    new_password="new_pass"
)
```

### Content Download & Repurposing

```python
# Download photo
cl.photo_download(
    media_pk=123456789,
    folder="downloaded_content"
)

# Download video
cl.video_download(
    media_pk=123456789,
    folder="downloaded_content"
)

# Download carousel
cl.album_download(
    media_pk=123456789,
    folder="downloaded_content"
)

# Download Reel
cl.clip_download(
    media_pk=123456789,
    folder="downloaded_content"
)

# Batch download user's posts
def backup_user_content(username):
    user = cl.user_info_by_username(username)
    medias = cl.user_medias(user_id=user.pk, amount=0)

    for media in medias:
        try:
            if media.media_type == 1:  # Photo
                cl.photo_download(media_pk=media.pk, folder="backup")
            elif media.media_type == 2:  # Video
                cl.video_download(media_pk=media.pk, folder="backup")
            elif media.media_type == 8:  # Album
                cl.album_download(media_pk=media.pk, folder="backup")
        except Exception as e:
            print(f"Failed to download {media.pk}: {e}")

backup_user_content("username")
```

### Notes Feature

```python
# Create a note visible to followers
cl.create_note(
    text="Currently working on something big... 👀",
    audience=0  # 0: All followers, 1: Close friends
)

# Get your notes
notes = cl.get_notes()

for note in notes:
    print(f"Note: {note.text}")

# Delete note
cl.delete_note(note_id=note.id)
```

### Explore & Trends

**File Reference:** `instagrapi/mixins/explore.py`, `timeline.py`

```python
# Get Reels from explore
explore_reels = cl.explore_reels(amount=10)

for reel in explore_reels:
    print(f"Reel: {reel.caption_text[:50]}")
    print(f"Engagement: {reel.like_count + reel.comment_count}")

# Get reels feed
reels_feed = cl.reels(amount=20)

# Get timeline reels
timeline_reels = cl.reels_timeline_media(amount=10)

# Follow trending content
for reel in explore_reels[:5]:
    try:
        cl.media_like(reel.id)
        if reel.user:
            cl.user_follow(reel.user.pk)
    except Exception as e:
        print(f"Failed: {e}")
```

---

## Best Practices

### 1. Rate Limiting & Delay Management

```python
import time
import random
from instagrapi import Client

# Initialize with delay range
cl = Client(delay_range=[1, 3])  # Random delay between 1-3 seconds

# Manual delay management
for i in range(10):
    try:
        cl.photo_upload(path=f"photo_{i}.jpg", caption=f"Post {i}")
        # Random delay between requests
        time.sleep(random.uniform(30, 60))
    except Exception as e:
        print(f"Rate limited: {e}")
        time.sleep(300)  # Wait 5 minutes on rate limit
```

### 2. Error Handling & Retry Logic

```python
from instagrapi.exceptions import ClientError, ClientLoginRequired
import time

def upload_with_retry(path, caption, max_retries=3):
    for attempt in range(max_retries):
        try:
            media = cl.photo_upload(path=path, caption=caption)
            return media
        except ClientLoginRequired:
            print("Session expired, re-logging in...")
            cl.relogin()
        except ClientError as e:
            if attempt < max_retries - 1:
                wait_time = 2 ** attempt  # Exponential backoff
                print(f"Attempt {attempt + 1} failed, retrying in {wait_time}s...")
                time.sleep(wait_time)
            else:
                raise

# Usage
try:
    media = upload_with_retry("photo.jpg", "Great content!")
    print(f"Successfully uploaded: {media.id}")
except Exception as e:
    print(f"Upload failed after retries: {e}")
```

### 3. Session Management Best Practices

```python
from pathlib import Path
import json

class InstagramBot:
    def __init__(self, session_file="session.json"):
        self.session_file = session_file
        self.cl = Client()

    def authenticate(self, username, password):
        """Authenticate or load existing session"""
        if Path(self.session_file).exists():
            print(f"Loading existing session from {self.session_file}")
            self.cl.load_settings(self.session_file)
        else:
            print(f"Creating new session for {username}")
            self.cl.login(username=username, password=password)
            self.cl.dump_settings(self.session_file)

    def safe_operation(self, operation_func):
        """Execute operation with session refresh on failure"""
        try:
            return operation_func()
        except ClientLoginRequired:
            print("Session expired, refreshing...")
            self.cl.relogin()
            self.cl.dump_settings(self.session_file)
            return operation_func()

# Usage
bot = InstagramBot("my_account_session.json")
bot.authenticate(username="your_username", password="your_password")

def upload_post():
    return bot.cl.photo_upload(path="photo.jpg", caption="Hello!")

result = bot.safe_operation(upload_post)
```

### 4. Content Scheduling Workflow

```python
import json
from datetime import datetime, timedelta
from pathlib import Path

class ContentScheduler:
    def __init__(self, schedule_file="schedule.json"):
        self.schedule_file = schedule_file
        self.cl = Client()
        self.cl.load_settings("session.json")

    def load_schedule(self):
        """Load scheduled posts"""
        if Path(self.schedule_file).exists():
            with open(self.schedule_file) as f:
                return json.load(f)
        return []

    def save_schedule(self, schedule):
        """Save scheduled posts"""
        with open(self.schedule_file, "w") as f:
            json.dump(schedule, f, indent=2, default=str)

    def publish_scheduled_posts(self):
        """Check and publish due posts"""
        schedule = self.load_schedule()
        now = datetime.now()

        for idx, post in enumerate(schedule):
            scheduled_time = datetime.fromisoformat(post["scheduled_time"])

            if scheduled_time <= now and not post.get("published"):
                try:
                    media = self.cl.photo_upload(
                        path=post["path"],
                        caption=post["caption"]
                    )
                    post["published"] = True
                    post["published_at"] = now.isoformat()
                    post["media_id"] = media.id
                    print(f"✓ Published: {post['caption'][:30]}")
                except Exception as e:
                    print(f"✗ Failed to publish: {e}")

        self.save_schedule(schedule)
        return [p for p in schedule if p.get("published")]

# Usage
scheduler = ContentScheduler()

# Add posts to schedule
scheduler.save_schedule([
    {
        "path": "photo1.jpg",
        "caption": "Morning post",
        "scheduled_time": (datetime.now() + timedelta(hours=2)).isoformat()
    },
    {
        "path": "photo2.jpg",
        "caption": "Evening post",
        "scheduled_time": (datetime.now() + timedelta(hours=12)).isoformat()
    }
])

# Run periodically (e.g., every 5 minutes)
published = scheduler.publish_scheduled_posts()
```

### 5. Data Export for Analytics

```python
import csv
import json
from datetime import datetime

def export_post_analytics(user_id, output_file="analytics.csv"):
    """Export all post analytics to CSV"""

    medias = cl.user_medias(user_id=user_id, amount=0)

    with open(output_file, 'w', newline='', encoding='utf-8') as csvfile:
        fieldnames = ['media_id', 'type', 'caption', 'posted_at', 'likes', 'comments', 'saves', 'reach', 'impressions']
        writer = csv.DictWriter(csvfile, fieldnames=fieldnames)

        writer.writeheader()
        for media in medias:
            try:
                insights = cl.insights_media(media_pk=media.pk)

                row = {
                    'media_id': media.id,
                    'type': media.media_type,
                    'caption': media.caption_text[:100] if media.caption_text else '',
                    'posted_at': media.taken_at,
                    'likes': media.like_count,
                    'comments': media.comment_count,
                    'saves': insights.get('saves', 0),
                    'reach': insights.get('reach', 0),
                    'impressions': insights.get('impressions', 0)
                }
                writer.writerow(row)
                print(f"Exported: {media.id}")
            except Exception as e:
                print(f"Failed to export {media.id}: {e}")

# Usage
export_post_analytics(user_id=cl.user_id)
```

### 6. Multi-Account Management Pattern

```python
class MultiAccountManager:
    def __init__(self):
        self.accounts = {}

    def add_account(self, username, password, session_name=None):
        """Add and authenticate account"""
        session_name = session_name or username
        cl = Client()
        cl.login(username=username, password=password)
        cl.dump_settings(f"{session_name}_session.json")
        self.accounts[session_name] = cl

    def load_account(self, session_name):
        """Load existing account"""
        if session_name not in self.accounts:
            cl = Client()
            cl.load_settings(f"{session_name}_session.json")
            self.accounts[session_name] = cl
        return self.accounts[session_name]

    def post_to_all_accounts(self, path, caption):
        """Post same content to all accounts"""
        results = {}
        for session_name, cl in self.accounts.items():
            try:
                media = cl.photo_upload(path=path, caption=caption)
                results[session_name] = {"status": "success", "media_id": media.id}
            except Exception as e:
                results[session_name] = {"status": "failed", "error": str(e)}
        return results

# Usage
manager = MultiAccountManager()
manager.add_account("account1", "password1", "brand_account")
manager.add_account("account2", "password2", "personal_account")

results = manager.post_to_all_accounts(
    path="photo.jpg",
    caption="Same post for all accounts!"
)
```

### 7. Logging & Monitoring

```python
import logging
from datetime import datetime

# Setup logging
logging.basicConfig(
    level=logging.INFO,
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s',
    handlers=[
        logging.FileHandler('instagram_bot.log'),
        logging.StreamHandler()
    ]
)

logger = logging.getLogger(__name__)

def monitored_operation(operation_name):
    def decorator(func):
        def wrapper(*args, **kwargs):
            logger.info(f"Starting: {operation_name}")
            try:
                result = func(*args, **kwargs)
                logger.info(f"Completed: {operation_name}")
                return result
            except Exception as e:
                logger.error(f"Failed: {operation_name} - {str(e)}")
                raise
        return wrapper
    return decorator

@monitored_operation("Photo Upload")
def upload_photo(path, caption):
    return cl.photo_upload(path=path, caption=caption)

# Usage
try:
    upload_photo("photo.jpg", "Hello!")
except Exception:
    logger.error("Upload failed, check log for details")
```

---

## API Reference

### Authentication Methods

| Method | Purpose | Reference |
|--------|---------|-----------|
| `login()` | Authenticate with username/password | auth.py |
| `relogin()` | Re-authenticate existing session | auth.py |
| `load_settings()` | Load saved session | auth.py |
| `dump_settings()` | Save current session | auth.py |

### Content Upload Methods

| Method | Content Type | Reference |
|--------|--------------|-----------|
| `photo_upload()` | Feed photo | photo.py |
| `video_upload()` | Feed video | video.py |
| `album_upload()` | Carousel (multi-photo/video) | album.py |
| `clip_upload()` | Reel | clip.py |
| `igtv_upload()` | IGTV | igtv.py |
| `photo_upload_to_story()` | Story photo | photo.py |
| `video_upload_to_story()` | Story video | video.py |

### Content Download Methods

| Method | Content Type | Reference |
|--------|--------------|-----------|
| `photo_download()` | Download photo | photo.py |
| `video_download()` | Download video | video.py |
| `album_download()` | Download carousel | album.py |
| `clip_download()` | Download reel | clip.py |
| `story_download()` | Download story | story.py |

### Analytics Methods

| Method | Purpose | Reference |
|--------|---------|-----------|
| `insights_account()` | Account metrics | insights.py |
| `insights_media()` | Post metrics | insights.py |
| `insights_media_feed_all()` | Batch post metrics | insights.py |
| `media_likers()` | Who liked a post | media.py |
| `story_viewers()` | Who viewed a story | story.py |

### Engagement Methods

| Method | Purpose | Reference |
|--------|---------|-----------|
| `media_like()` | Like post | media.py |
| `media_unlike()` | Unlike post | media.py |
| `media_comment()` | Comment on post | comment.py |
| `media_comments()` | Get post comments | comment.py |
| `comment_like()` | Like comment | comment.py |
| `story_like()` | Like story | story.py |

### User Methods

| Method | Purpose | Reference |
|--------|---------|-----------|
| `user_info()` | Get user profile by ID | user.py |
| `user_info_by_username()` | Get user profile by username | user.py |
| `user_follow()` | Follow user | user.py |
| `user_unfollow()` | Unfollow user | user.py |
| `user_followers()` | Get followers list | user.py |
| `user_following()` | Get following list | user.py |

### Direct Message Methods

| Method | Purpose | Reference |
|--------|---------|-----------|
| `direct_send()` | Send text message | direct.py |
| `direct_send_photo()` | Send photo via DM | direct.py |
| `direct_send_video()` | Send video via DM | direct.py |
| `direct_threads()` | Get DM conversations | direct.py |
| `direct_messages()` | Get messages in thread | direct.py |

### Hashtag Methods

| Method | Purpose | Reference |
|--------|---------|-----------|
| `hashtag_info()` | Get hashtag stats | hashtag.py |
| `hashtag_medias_top()` | Top posts (hashtag) | hashtag.py |
| `hashtag_medias_recent()` | Recent posts (hashtag) | hashtag.py |
| `hashtag_follow()` | Follow hashtag | hashtag.py |

### Complete Method List

For a complete list of all 80+ available methods, see:
- **File:** `instagrapi/mixins/*.py` (28 feature modules)
- **Repository:** https://github.com/adw0rd/instagrapi
- **Documentation:** https://adw0rd.github.io/instagrapi/

---

## Troubleshooting

### Common Issues & Solutions

#### 1. Login Failures

**Issue:** "Challenge required" or "Login failed"

**Solutions:**
```python
# Try with verification code
try:
    cl.login(username, password)
except Exception as e:
    if "challenge" in str(e).lower():
        verification_code = input("Enter verification code: ")
        cl.login(username, password, verification_code=verification_code)

# Try relogin
cl.relogin()

# Check if account is using 2FA
# Enable authenticator app and use TOTP codes
```

#### 2. Rate Limiting (Action Blocked)

**Issue:** "Action blocked" or "Too many requests"

**Solutions:**
```python
# Add delays between requests
import time
import random

time.sleep(random.uniform(30, 120))  # Random 30-120 second delay

# Use delay_range in Client
cl = Client(delay_range=[5, 15])

# Reduce request frequency
# Spread operations across multiple sessions
```

#### 3. Session Expired

**Issue:** "Login required" errors

**Solutions:**
```python
from instagrapi.exceptions import ClientLoginRequired

try:
    result = cl.photo_upload(path, caption)
except ClientLoginRequired:
    cl.relogin()
    result = cl.photo_upload(path, caption)
```

#### 4. Media Download Fails

**Issue:** "Download failed" or "Cannot find media"

**Solutions:**
```python
# Media might be deleted
try:
    cl.photo_download(media_pk)
except Exception as e:
    if "404" in str(e) or "not found" in str(e).lower():
        print("Media no longer exists")
    else:
        raise

# Try with different media_pk format
# Use media.pk instead of media.id
```

#### 5. Story Upload Issues

**Issue:** Stories upload fails

**Solutions:**
```python
# Ensure image dimensions (1080x1920 recommended)
# Use PIL to resize
from PIL import Image

img = Image.open("photo.jpg")
img = img.resize((1080, 1920), Image.Resampling.LANCZOS)
img.save("photo_resized.jpg")

cl.photo_upload_to_story("photo_resized.jpg")
```

#### 6. Proxy Issues

**Issue:** Connection through proxy fails

**Solutions:**
```python
# Verify proxy format
# HTTP: http://proxy_ip:port
# SOCKS5: socks5://proxy_ip:port
# With auth: http://user:pass@proxy_ip:port

cl = Client(proxy="http://proxy.example.com:8080")

# Test connectivity
try:
    account = cl.account_info()
    print("Proxy working!")
except Exception as e:
    print(f"Proxy issue: {e}")
```

### Debug Mode

```python
import logging

# Enable debug logging
logging.basicConfig(level=logging.DEBUG)

# instagrapi logger
logging.getLogger("instagrapi").setLevel(logging.DEBUG)

# Now all API calls are logged
cl = Client()
cl.login(username, password)
```

---

## External Resources

### Official Resources

- **GitHub Repository:** https://github.com/adw0rd/instagrapi
- **PyPI Package:** https://pypi.org/project/instagrapi/
- **Official Documentation:** https://adw0rd.github.io/instagrapi/
- **Issue Tracker:** https://github.com/adw0rd/instagrapi/issues
- **Discussions:** https://github.com/adw0rd/instagrapi/discussions

### Instagram Resources

- **Instagram Developer:** https://www.instagram.com/developer/
- **Instagram Business Suite:** https://business.instagram.com/
- **Creator Studio:** https://business.facebook.com/creatorstudio
- **Analytics Guide:** https://help.instagram.com/788388387972460

### Python Resources

- **Python Official Docs:** https://docs.python.org/3/
- **Pydantic Docs:** https://docs.pydantic.dev/
- **Requests Library:** https://docs.python-requests.org/

### Community Resources

- **Stack Overflow:** https://stackoverflow.com/questions/tagged/instagrapi
- **Reddit:** https://www.reddit.com/r/Instagram/
- **GitHub Discussions:** https://github.com/adw0rd/instagrapi/discussions

### Related Libraries

- **Instabot:** https://github.com/instabotinstagram/instabot
- **InstaPy:** https://github.com/InstaPy/InstaPy
- **python-instagram:** https://github.com/Instagram/python-instagram

### Security & Best Practices

- **Instagram Terms of Service:** https://help.instagram.com/581066165797487
- **API Abuse Prevention:** https://help.instagram.com/477434105621119
- **Account Security:** https://www.instagram.com/accounts/login/
- **Python Security:** https://python.readthedocs.io/en/latest/library/security_warnings.html

---

## Document Metadata

```json
{
  "title": "Instagram Content Creator Guide - instagrapi Library",
  "version": "1.0.0",
  "updated": "2025-12-09",
  "author": "Instagram Creator Community",
  "license": "Creative Commons Attribution 4.0",
  "target_audience": ["Professional Content Creators", "Content Agencies", "Marketing Teams", "Developers"],
  "keywords": ["Instagram", "API", "Content Creation", "Automation", "Analytics", "Community Management"],
  "compatibility": {
    "python_version": ">= 3.9",
    "library_version": "Latest",
    "platforms": ["Linux", "macOS", "Windows"]
  },
  "document_structure": {
    "sections": 12,
    "code_examples": 50+,
    "methods_documented": 80+,
    "use_cases": 10
  }
}
```

---

## How to Use This Documentation

### For Content Creators:
1. Start with **[Professional Use Cases](#professional-use-cases)** to identify your needs
2. Follow **[Installation & Setup](#installation--setup)** to get started
3. Jump to relevant sections based on your use case
4. Refer to **[Best Practices](#best-practices)** for production-ready code

### For AI Systems:
- Each section has a **"File Reference"** indicating source code location
- Code examples are self-contained and directly executable
- **[API Reference](#api-reference)** provides method signatures
- Links to GitHub files enable source code inspection

### For Developers:
- **[API Reference](#api-reference)** provides complete method documentation
- **[External Resources](#external-resources)** links to detailed guides
- **[Troubleshooting](#troubleshooting)** covers common integration issues
- Follow patterns in **[Best Practices](#best-practices)** for production deployments

