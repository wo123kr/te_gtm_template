# 🚀 Thinking Engine GTM Template — All-in-One Google Tag Manager tag template for the Thinking Engine JavaScript SDK

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![GTM Template Gallery](https://img.shields.io/badge/GTM-Template%20Gallery-4285f4.svg)](https://tagmanager.google.com/gallery/)

For teams that want to install the Thinking Engine (TE) JavaScript SDK and send events through Google Tag Manager, without editing site code.
Instead of separate initialization and event tags, one template covers SDK initialization and every tracking feature — you just pick a **tag type**. Field labels in the GTM UI are in Korean.

## ✨ Features
- **🚀 Initialization (`init`)**: App ID, server URL, SDK CDN URL, instance name (default `ta`), debug logging, remote config fetch toggle (`disableRConfig`), disabling selected preset properties
- **🤖 Auto-collection** (init tag): `ta_page_show` / `ta_page_hide`, `ta_pageview` (SDK v2.4.0+), `ta_page_click` (SDK v2.5.0+). `ta_pageview` / `ta_page_click` are **off by default** (opt-in) to avoid unexpected data volume. Optional static common properties for all auto-collected events.
- **📊 Events**: `track`, `pageview` (sends `ta_pageview` manually), `trackFirst`, `trackUpdate`, `trackOverwrite`, `timeEvent`
- **🖱️ Clicks & SPA** *(new in v2.1.0)*: `trackLink` (click listeners by tag / class / id), `autoTrackSinglePage` (re-trigger page view on SPA route changes)
- **👤 Users**: `login`, `logout`, `setDistinctId`; user properties `userSet`, `userSetOnce`, `userAdd`, `userUnset`, `userDel`, `userDelete`, `userAppend`, `userUniqAppend`
- **🌍 Properties**: `setSuperProperties`, `unsetSuperProperties`, `clearSuperProperties`, `setPageProperty`
- **🎨 UX**: emoji-coded categories, collapsible groups, field hints with examples, input validation

## 📌 Status
- Stable. Template version **2.1.0** (see [metadata.yaml](metadata.yaml) change notes).
- Last commit: 2026-06-14.
- Compatible with Thinking Engine JavaScript SDK `thinkingdata-browser` v2.x (`ta_pageview` requires v2.4.0+, `ta_page_click` requires v2.5.0+).

## 🛠️ Quick Start
No build step and no automated tests — `template.tpl` itself is the deliverable.

1. **Import the template** — GTM → **Templates** → **Tag Templates** → **New** → **Import** → select `template.tpl` → **Save**.
2. **Create the initialization tag** — new tag with the "Thinking Engine" template, tag type **🚀 초기화 (init)**:
   - **App ID** (required): your Thinking Engine project ID
   - **Server URL** (required): data collection endpoint (keep the default unless told otherwise)
   - **Instance Name**: SDK instance name (default `ta`)
   - Trigger: **All Pages** → **Save**
3. **Create event tags** — pick a tag type (`track`, `login`, `userSet`, …), fill in its parameters, set triggers.
4. **Verify & publish** — GTM **Preview** mode + SDK debug logging, check data arrives in the Thinking Engine dashboard, then **Submit**.

## 🗂️ Structure
```
template.tpl    # the GTM template (TERMS_OF_SERVICE, INFO, TEMPLATE_PARAMETERS, SANDBOXED_JS, WEB_PERMISSIONS, TESTS)
metadata.yaml   # Template Gallery metadata and per-version change notes
README.md
LICENSE         # Apache 2.0
```

## ⚙️ Configuration
No environment variables. App ID, server URL and all other options are entered in the GTM tag fields.
New SDK methods must be registered in the template's `WEB_PERMISSIONS` before they can be called.

## 📖 Details

### Configuration examples
```
Tag Type: 📊 기본 이벤트 전송 (track)
Event Name: button_click
Event Properties:  button_id: "cta_button", page_section: "header"

Tag Type: 👤 로그인 (login)
Account ID: {{User ID Variable}}

Tag Type: ⚙️ 사용자 속성 설정 (userSet)
User Properties:   membership_level: "premium", preferred_language: "ko"

Tag Type: 🌍 공통 속성 설정 (setSuperProperties)
Global Properties: app_version: "2.1.0", platform: "web"

Tag Type: 🌍 페이지 공통 속성 설정 (setPageProperty)
Page Properties:   page_category: "product", content_type: "detail"
```

### First-time events (`trackFirst`)
Prevent duplicate tracking of one-time actions:
```
Tag Type: 📊 최초 이벤트 (trackFirst)
Event Name: app_install
First Check ID: {{User ID}} (optional)
```

### Duration (`timeEvent` → `track`)
```
1. Tag Type: 📊 이벤트 시간측정 (timeEvent)   Event Name: video_play
2. Tag Type: 📊 기본 이벤트 전송 (track)       Event Name: video_play   (duration is added automatically)
```

### Element clicks (`trackLink`)
```
Tag Type: 🖱️ 요소 클릭 추적 (trackLink)
Event Name: link_click
Element Rules:  tag: a / tag: button / class: cta-button
Event Properties:  section: "header"
```
> Listeners are attached only to elements present when the tag fires. For elements created later (e.g. after route changes), fire `trackLink` again.

### SPA page views
- `autoTrackSinglePage` tag type (📄 단일 페이지 조회 갱신): fire it on a **History Change** trigger.
- Or enable auto-collection in the init tag's **🤖 자동 수집 설정** group:
```
☑ 📄 ta_pageview   (SDK v2.4.0+)
☑ 🖱️ ta_page_click (SDK v2.5.0+)
🔧 Common properties: source = {{Traffic Source}}
```

### Best practices
- Deploy the initialization tag before any tracking tag, and use the **same instance name** in every tag.
- Event names: clear, lowercase with underscores (e.g. `button_click`).
- Global properties for app-wide context, page properties for page context, user properties for user attributes.
- Enable debug logging and test in Preview mode before publishing.

### Troubleshooting
- **"SDK not found"**: the init tag must fire before tracking tags; instance names must match; check App ID and server URL.
- **Events not appearing**: check the network tab for successful requests, check event naming, enable debug logging.
- **Validation errors**: read the field error message, fill required fields, check value formats.

## 📚 More
- [metadata.yaml](metadata.yaml) — version history (change notes)
- [Thinking Engine Documentation](https://docs.thinkingdata.cn/)
- [JavaScript SDK Reference](https://docs.thinkingdata.cn/ta-manual/latest/installation/client_sdk/js_sdk_installation/js_sdk_installation.html)
- [GTM Template Development Guide](https://developers.google.com/tag-platform/tag-manager/templates)

## 🤝 Contributing
Contributions are welcome! Please feel free to submit issues and enhancement requests.

## 📄 License
Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE).
