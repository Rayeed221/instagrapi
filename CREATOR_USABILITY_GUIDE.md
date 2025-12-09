# instagrapi Library - Usability & Feature Matrix

## Quick Features Overview

### What Can Professional Content Creators Do?

| Feature | Capability | Status | Complexity |
|---------|-----------|--------|-----------|
| **Post Photos** | Upload images to feed | ✅ Full | Easy |
| **Post Videos** | Upload videos to feed | ✅ Full | Easy |
| **Post Reels** | Upload short-form videos | ✅ Full | Easy |
| **Post Carousels** | Multi-photo/video posts | ✅ Full | Easy |
| **Post IGTV** | Long-form video content | ✅ Full | Easy |
| **Post to Stories** | Upload story photos/videos | ✅ Full | Easy |
| **Story Stickers** | Add interactive elements | ✅ Full | Medium |
| **Story Highlights** | Save and organize stories | ✅ Full | Easy |
| **Schedule Posts** | Automate publish times | ⚠️ Partial | Medium |
| **Edit Captions** | Modify post text | ✅ Full | Easy |
| **Delete Posts** | Remove published content | ✅ Full | Easy |
| **View Analytics** | Account & post metrics | ✅ Full | Easy |
| **Like Posts** | Engage with content | ✅ Full | Easy |
| **Comment** | Reply to posts | ✅ Full | Easy |
| **Direct Messages** | Send text/media to users | ✅ Full | Easy |
| **Follow/Unfollow** | Manage followers | ✅ Full | Easy |
| **Save Posts** | Create collections | ✅ Full | Easy |
| **Hashtag Research** | Find trending tags | ✅ Full | Easy |
| **Location Tagging** | Tag posts with locations | ✅ Full | Easy |
| **Multi-Account** | Manage multiple accounts | ✅ Full | Medium |
| **2FA Support** | Two-factor authentication | ✅ Full | Easy |
| **Session Persistence** | Save login sessions | ✅ Full | Easy |
| **Proxy Support** | Route through proxies | ✅ Full | Medium |
| **Download Content** | Save photos/videos | ✅ Full | Easy |
| **User Search** | Find profiles | ✅ Full | Easy |
| **Follower Analytics** | Track followers | ✅ Full | Easy |
| **Story Viewers** | See who viewed stories | ✅ Full | Easy |
| **Pending Messages** | Manage DM requests | ✅ Full | Easy |
| **Notes** | Create visible notes | ✅ Full | Easy |
| **Explore Feed** | Access discovery page | ✅ Full | Easy |

---

## Use Case Complexity Matrix

### Beginner (Simple API Calls)
```
✅ Single photo upload
✅ Post comment
✅ Like post
✅ Follow user
✅ Get user info
✅ View followers
✅ Simple DM send
```

**Time to implement:** 5-15 minutes
**Code lines:** 5-10 lines
**Error handling:** Basic try/except

### Intermediate (Multi-step workflows)
```
✅ Carousel posting
✅ Story with stickers
✅ Analytics collection
✅ Batch operations
✅ Multi-account posting
✅ Comment moderation
✅ Hashtag research
```

**Time to implement:** 30 minutes - 1 hour
**Code lines:** 20-50 lines
**Error handling:** Comprehensive

### Advanced (Complex automation)
```
✅ Scheduled posting system
✅ Content curation pipeline
✅ Analytics dashboards
✅ Multi-account campaigns
✅ Automated engagement loops
✅ Content performance optimization
✅ Trend monitoring systems
```

**Time to implement:** 2-8 hours
**Code lines:** 100-500 lines
**Error handling:** Production-grade

---

## API Call Categories

### Content Creation (Posting)

**Simplest Method:**
```python
cl.photo_upload(path="photo.jpg", caption="Hello!")
# Time: ~5 seconds, ~1 API call
```

**Most Complex:**
```python
cl.album_upload(paths=[...], caption="...", usertags=[...], location=...)
# Time: ~20 seconds, ~3-5 API calls, requires data preparation
```

### Content Retrieval (Downloads)

**Simplest:**
```python
cl.user_info_by_username("username")
# Time: ~1 second, 1 API call
```

**Most Complex:**
```python
cl.user_medias(user_id, amount=0)  # Gets ALL posts (can take minutes)
# Time: ~30 seconds - 2 minutes, 10-50+ API calls
```

### Analytics

**Simplest:**
```python
cl.account_info()
# Time: ~1 second, 1 API call
# Returns: Basic stats (followers, following, posts)
```

**Most Complex:**
```python
for media in user_medias:
    cl.insights_media(media.pk)  # Batch analytics
# Time: ~30 seconds - 5 minutes (depends on post count)
# Multiple sequential API calls
```

### Engagement

**Simplest:**
```python
cl.media_like(media_id)
# Time: ~1 second, 1 API call
```

**Most Complex:**
```python
cl.media_comments()  # Get all comments
cl.comment_bulk_delete()  # Delete multiple
cl.media_likers()  # Get all likers
# Time: ~10 seconds, 3+ API calls
```

---

## Rate Limiting Behavior

### Safe Thresholds

| Operation | Safe Frequency | Hard Limit | Recovery |
|-----------|--------|-----------|----------|
| Photo Upload | 1 per 30 mins | 4+ per hour | 1-24 hours |
| Story Upload | 1 per 5 mins | 30+ per hour | 1-6 hours |
| Like | 1 per 5 secs | 300+ per hour | 15 mins - 1 hour |
| Comment | 1 per 10 secs | 100+ per hour | 1-24 hours |
| Follow | 1 per 30 secs | 150+ per hour | 1 hour |
| DM Send | 1 per 5 secs | 200+ per day | 24 hours |
| Get Followers | 1 per 1 min | 20 requests | 15 mins |

### Rate Limit Response Handling

```python
from instagrapi.exceptions import ClientThrottledError, ClientRequestTimeout

try:
    cl.photo_upload(path, caption)
except ClientThrottledError as e:
    print(f"Rate limited: {e}")
    # Wait 60-300 seconds before retry
    time.sleep(300)
except ClientRequestTimeout:
    print("Request timeout, retrying...")
    time.sleep(10)
```

---

## Memory & Performance Impact

### Small Accounts (< 1,000 followers)
- **Memory usage:** 10-50 MB
- **API calls per minute:** 1-5
- **Recommended batch size:** 10-20 posts
- **Performance:** ✅ Excellent on standard machines

### Medium Accounts (1,000 - 100,000 followers)
- **Memory usage:** 50-200 MB
- **API calls per minute:** 2-10
- **Recommended batch size:** 5-10 posts
- **Performance:** ✅ Good, use session pooling

### Large Accounts (100,000+ followers)
- **Memory usage:** 200-500 MB
- **API calls per minute:** 1-3 (heavily rate limited)
- **Recommended batch size:** 1-5 posts
- **Performance:** ⚠️ Use distributed workers

---

## Authentication Methods Comparison

| Method | Best For | Security | Persistence | 2FA Support |
|--------|----------|----------|-------------|-------------|
| Username/Password | Initial setup | ⚠️ Low | Manual | ✅ Yes |
| Session ID | Automation | ✅ High | Auto | ✅ Yes |
| Token | APIs | ✅ High | Auto | ⚠️ Limited |
| Proxy | Distributed | ✅ Highest | Manual | ✅ Yes |

---

## Content Type Specifications

### Photos
```
Formats: JPG, PNG, GIF, WebP
Minimum: 600x600 pixels
Maximum: 8000x8000 pixels
Recommended: 1080x1080 pixels
Feed max file size: 8 MB
Story max file size: 15 MB
```

### Videos
```
Formats: MP4, MOV
Duration: 3 seconds - 10 minutes (feed/reel)
Duration: 3 - 60 seconds (story)
Min resolution: 600x600 pixels
Max resolution: 4096x4096 pixels
Recommended: 1080x1920 (vertical)
Max file size: 100 MB
Frame rate: 23-60 fps
```

### Carousels
```
Min items: 2
Max items: 10
Mixed types: Photos + Videos allowed
Max total size: 150 MB
Max per item: 100 MB
```

### Reels
```
Duration: 15 seconds - 10 minutes
Resolution: Min 600x600, Max 4096x4096
Recommended: 1080x1920
File size: Max 100 MB
Format: MP4, MOV
Frame rate: 23-60 fps
Audio: Required for best engagement
```

### Stories
```
Duration: 1 - 15 seconds
Resolution: 1080x1920 (vertical)
Format: JPG/PNG (photos), MP4/MOV (videos)
Max file size: 15 MB
Stickers: 5+ types available
```

---

## Automation Patterns

### Pattern 1: Scheduled Publishing
**Setup time:** 30 minutes
**Code complexity:** 50 lines
**Reliability:** ✅ High

```python
# Pseudo-code
schedule_file = "posts.json"
while True:
    posts = load_posts(schedule_file)
    for post in posts:
        if post.scheduled_time <= now() and not post.published:
            cl.photo_upload(post.path, post.caption)
            post.published = True
    save_posts(schedule_file, posts)
    sleep(5 * 60)  # Check every 5 minutes
```

### Pattern 2: Analytics Collection
**Setup time:** 1 hour
**Code complexity:** 100 lines
**Reliability:** ✅ High

```python
# Pseudo-code
while True:
    insights = cl.insights_account()
    medias = cl.user_medias(cl.user_id, amount=10)
    for media in medias:
        media_insights = cl.insights_media(media.pk)
        save_to_database(media, media_insights)
    sleep(24 * 3600)  # Daily
```

### Pattern 3: Engagement Automation
**Setup time:** 2 hours
**Code complexity:** 150 lines
**Reliability:** ⚠️ Medium (rate limits)

```python
# Pseudo-code
hashtags = ["photography", "nature"]
while True:
    for hashtag in hashtags:
        posts = cl.hashtag_medias_recent(hashtag, amount=5)
        for post in posts:
            cl.media_like(post.id)
            sleep(random(5, 15))
    sleep(3600)  # Hourly
```

### Pattern 4: Comment Management
**Setup time:** 1.5 hours
**Code complexity:** 120 lines
**Reliability:** ✅ High

```python
# Pseudo-code
while True:
    medias = cl.user_medias(cl.user_id, amount=5)
    for media in medias:
        comments = cl.media_comments(media.id, amount=50)
        for comment in comments:
            if is_spam(comment.text):
                cl.comment_bulk_delete(media.id, [comment.pk])
                print(f"Deleted spam: {comment.text}")
            elif should_reply(comment.text):
                cl.media_comment(media.id, generate_reply())
                sleep(random(10, 30))
    sleep(3600)  # Hourly
```

---

## Integration Patterns

### Web Application Integration
```python
from flask import Flask, request

app = Flask(__name__)
cl = Client()
cl.load_settings("session.json")

@app.route('/api/upload', methods=['POST'])
def upload():
    file = request.files['file']
    caption = request.form['caption']

    try:
        media = cl.photo_upload(
            path=file.filename,
            caption=caption
        )
        return {"status": "success", "media_id": media.id}
    except Exception as e:
        return {"status": "error", "message": str(e)}, 400
```

### Scheduled Tasks (APScheduler)
```python
from apscheduler.schedulers.background import BackgroundScheduler

scheduler = BackgroundScheduler()

@scheduler.scheduled_job('cron', hour=10, minute=0)
def daily_post():
    cl.photo_upload("daily_photo.jpg", "Daily post!")

scheduler.start()
```

### Database Logging
```python
import sqlite3

def log_action(action, details):
    conn = sqlite3.connect('instagram.db')
    c = conn.cursor()
    c.execute('''INSERT INTO actions
                 (timestamp, action, details)
                 VALUES (datetime('now'), ?, ?)''',
              (action, json.dumps(details)))
    conn.commit()
    conn.close()

# Usage
media = cl.photo_upload(path, caption)
log_action("upload", {"media_id": media.id, "caption": caption})
```

---

## Limitations & Constraints

### Functional Limitations

| Feature | Limitation | Workaround |
|---------|-----------|-----------|
| Story Deletion | Limited to 24 hours | Archive to highlights first |
| Edit Caption | Limited metadata changes | Repost if major changes needed |
| Bulk Operations | Rate-limited significantly | Spread over time with delays |
| Real-time Notifications | Not available via API | Poll periodically |
| Scheduled Posts | Must implement manually | Use external scheduler |
| Analytics History | Limited to recent data | Archive data regularly |

### API Limitations

```
Maximum followers to fetch: Theoretically unlimited
                          Practically: 10,000-50,000 (time-limited)

Maximum posts to fetch: Unlimited, but rate-limited

Maximum batch size: 10 items recommended (carousel)

Concurrent requests: 1-5 safely (more causes rate limits)

Data retention: 90 days for analytics

Session lifetime: 30-60 days typically
```

### Platform-Imposed Restrictions

- **Action Blocks:** Triggered by unusual activity patterns
- **Rate Limiting:** Graduated throttling after 10-20 actions/minute
- **Account Flags:** For excessive automation (>100 actions/day)
- **IP Blocks:** If many failed logins detected
- **Shadow Banning:** Posts not shown to non-followers

---

## Success Metrics for Content Creators

### Key Metrics You Can Track

```python
# Engagement Rate
engagement_rate = (likes + comments + shares) / followers

# Reach vs Impressions
reach = unique_viewers
impressions = total_views

# Save Rate
save_rate = saves / impressions

# Comment Sentiment
# Manual analysis of cl.media_comments()

# Follower Growth
growth_rate = (followers_today - followers_yesterday) / followers_yesterday

# Best Posting Times
# Analyze peak viewing times from story_viewers()

# Content Performance Ranking
# Sort by cl.insights_media_feed_all()
```

### Example Analytics Dashboard

```python
def generate_weekly_report():
    insights = cl.insights_account()
    medias = cl.user_medias(cl.user_id, amount=20)

    report = {
        "period": "last_7_days",
        "followers": insights.get('followers_count'),
        "follower_change": 0,  # Calculate from history
        "total_reach": 0,
        "total_impressions": 0,
        "average_engagement_rate": 0,
        "top_post": None,
        "best_posting_time": None
    }

    for media in medias:
        m_insights = cl.insights_media(media.pk)
        report["total_reach"] += m_insights.get("reach", 0)
        report["total_impressions"] += m_insights.get("impressions", 0)

    return report
```

---

## Comparison with Official Instagram API

### instagrapi vs Instagram Graph API

| Feature | instagrapi | Graph API | Notes |
|---------|-----------|-----------|-------|
| Photo Upload | ✅ Yes | ✅ Yes | instagrapi: feed, story, direct |
| Video Upload | ✅ Yes | ✅ Yes | instagrapi: feed, story, reel |
| Reels | ✅ Yes | ❌ No | Exclusive to instagrapi |
| Stories | ✅ Yes | ✅ Limited | instagrapi: stickers, interactive |
| Analytics | ✅ Yes | ✅ Yes | instagrapi: more detailed |
| Direct Messages | ✅ Yes | ❌ No | Exclusive to instagrapi |
| Comments | ✅ Yes | ✅ Yes | |
| Likes | ✅ Yes | ⚠️ Limited | |
| Hashtag Research | ✅ Yes | ⚠️ Limited | |
| Location Tagging | ✅ Yes | ✅ Yes | |
| Download Content | ✅ Yes | ❌ No | Exclusive to instagrapi |
| Follower Lists | ✅ Yes | ❌ No | Exclusive to instagrapi |
| Rate Limits | ⚠️ Strict | ✅ Generous | Graph API: 200 calls/hour |
| Approval Required | ❌ No | ✅ Yes | instagrapi: private API |
| Account Risk | ⚠️ Medium | ✅ Low | instagrapi: use responsibly |

---

## Recommended Architecture

### For Solo Creators

```
Single Server
    ├── instagrapi Client (single account)
    ├── Schedule File (JSON)
    ├── Log File
    └── Database (SQLite)
```

**Setup time:** 1-2 hours
**Cost:** Free
**Scalability:** Good for 1 account

### For Agencies (Multi-Account)

```
Application Server
    ├── Account 1 (instagrapi Client)
    ├── Account 2 (instagrapi Client)
    ├── Account N (instagrapi Client)
    └── Schedule Queue (Redis/RabbitMQ)

Database Server
    ├── Analytics
    ├── Scheduling
    └── Audit Logs

Cache Server (Redis)
    └── Session Cache
```

**Setup time:** 4-8 hours
**Cost:** $10-50/month
**Scalability:** Excellent for 10-100 accounts

### For Automation at Scale

```
Load Balancer
    ├── Worker 1 (instagrapi)
    ├── Worker 2 (instagrapi)
    └── Worker N (instagrapi)

Central Services
    ├── Job Queue (Celery)
    ├── Database (PostgreSQL)
    ├── Cache (Redis)
    └── Message Broker (RabbitMQ)

Monitoring
    ├── Logging (ELK Stack)
    ├── Metrics (Prometheus)
    └── Alerts (AlertManager)
```

**Setup time:** 1-2 weeks
**Cost:** $100-500/month
**Scalability:** Unlimited

---

## Security Considerations

### Credential Management

```python
import os
from dotenv import load_dotenv

load_dotenv()

username = os.getenv("INSTAGRAM_USERNAME")
password = os.getenv("INSTAGRAM_PASSWORD")

# ✅ Good
cl.login(username, password)

# ❌ Bad - hardcoded credentials
cl.login("my_user@example.com", "my_password_123")
```

### Session Security

```python
# Rotate sessions periodically
import os
from pathlib import Path
import shutil

def rotate_session(session_file="session.json"):
    if Path(session_file).exists():
        backup = f"{session_file}.{datetime.now().timestamp()}.backup"
        shutil.copy(session_file, backup)
        # Keep only 3 most recent backups
        backups = sorted(glob(f"{session_file}.*.backup"))
        for old_backup in backups[:-3]:
            os.remove(old_backup)
```

### Rate Limit Abuse Prevention

```python
# Implement request throttling
from ratelimit import limits, sleep_and_retry
import time as time_module

@sleep_and_retry
@limits(calls=100, period=3600)  # 100 calls per hour
def safe_api_call(func):
    return func()

# Usage
safe_api_call(lambda: cl.photo_upload(path, caption))
```

---

## Document Structure for AI Fetching

### How to Structure Queries

**To fetch specific information, use:**
```
"Find <SECTION> in CREATOR_DOCUMENTATION.md"
"Look up <METHOD> in API Reference"
"Check <USE_CASE> in Professional Use Cases"
"What is the <FEATURE>? (See CREATOR_USABILITY_GUIDE.md)"
```

**Examples:**
- "Find photo upload example in CREATOR_DOCUMENTATION.md"
- "Look up insights_media in API Reference"
- "Check analytics collection in best practices"
- "What is the rate limit for likes?"

---

## Quick Start by Use Case

### I want to post photos automatically
**Files to read:**
- Installation section → Photo Upload section → Scheduling code example
**Time:** 15 minutes
**Difficulty:** Easy

### I want to analyze my account performance
**Files to read:**
- Analytics & Analytics Methods section → Sample code
**Time:** 20 minutes
**Difficulty:** Easy

### I want to manage multiple accounts
**Files to read:**
- Multi-Account Management use case → Multi-account code pattern
**Time:** 30 minutes
**Difficulty:** Medium

### I want to automate engagement
**Files to read:**
- Community Management section → Engagement Automation pattern
**Time:** 1 hour
**Difficulty:** Medium

### I want to build a production system
**Files to read:**
- Best Practices section → Recommended Architecture
**Time:** 2-4 hours
**Difficulty:** Advanced

---

## Troubleshooting Decision Tree

```
Problem: Can't login
├─ Check: Valid credentials?
├─ Check: 2FA enabled?
│   └─ Solution: Use verification_code parameter
└─ Check: Account blocked?
    └─ Solution: Try different proxy/IP

Problem: Posts fail to upload
├─ Check: File format correct?
├─ Check: File size < limit?
├─ Check: Rate limited?
│   └─ Solution: Wait 1-24 hours
└─ Check: Action blocked?
    └─ Solution: Wait and try different content

Problem: Can't get analytics
├─ Check: Account is business account?
├─ Check: Data within 90 days?
├─ Check: Rate limited?
└─ Check: Media older than 90 days?
    └─ Solution: Archive to database

Problem: Rate limiting errors
├─ Check: How many actions/minute?
├─ Add delays between requests
└─ Use exponential backoff
```

