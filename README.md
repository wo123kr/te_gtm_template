# 🚀 Thinking Engine - All-in-One GTM Template

A comprehensive Google Tag Manager template for the Thinking Engine JavaScript SDK that combines initialization and all event tracking features in a single, user-friendly template.

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![GTM Template Gallery](https://img.shields.io/badge/GTM-Template%20Gallery-4285f4.svg)](https://tagmanager.google.com/gallery/)

## ✨ Features

### 🎯 **One Template, All Features**
Unlike traditional templates that require separate initialization and event tags, this all-in-one template provides:

- **🚀 SDK Initialization**: Complete SDK setup with advanced configuration options
- **📊 Event Tracking**: All types of event tracking in one place
- **👤 User Management**: Comprehensive user identification and attribute management
- **🌍 Properties Management**: Global and page-specific property handling
- **🔧 Advanced Features**: Time tracking, first-time events, and data operations

### 🎨 **Enhanced User Experience**
- **Intuitive UI**: Emoji-coded categories and clear field descriptions
- **Smart Validation**: Real-time input validation with helpful error messages
- **Contextual Help**: Detailed explanations and examples for each feature
- **Organized Sections**: Logical grouping with collapsible sections

### 📋 **Supported Tag Types**

#### 🚀 **Initialization**
- SDK initialization with customizable configuration
- Auto-tracking settings (page show/hide, single-page pageview, element click)
- Auto-track common properties (static props applied to all auto-collected events)
- Remote config fetch toggle (`disableRConfig`)
- Debug logging controls

#### 📊 **Event Tracking**
- **Basic Events** (`track`): Standard event transmission
- **First-time Events** (`trackFirst`): Prevent duplicate first-time actions
- **Update Events** (`trackUpdate`): Modify existing events
- **Overwrite Events** (`trackOverwrite`): Replace event data completely
- **Time Events** (`timeEvent`): Start timing for duration measurement

#### 👤 **User Management**
- **Login/Logout** (`login`, `logout`): User session management
- **Guest ID** (`setDistinctId`): Anonymous user tracking
- **User Properties**:
  - `userSet`: Set/update user attributes
  - `userSetOnce`: Set attributes only once
  - `userAdd`: Increment numeric attributes
  - `userUnset`: Remove specific attribute values
  - `userDel`: Delete multiple attributes
  - `userDelete`: Remove all user attributes
  - `userAppend`: Add values to array attributes
  - `userUniqAppend`: Add unique values to arrays

#### 🌍 **Properties Management**
- **Global Properties** (`setSuperProperties`): Apply to all events
- **Remove Global Properties** (`unsetSuperProperties`, `clearSuperProperties`)
- **Page Properties** (`setPageProperty`): Page-specific context

#### 🖱️ **Auto-collection & SPA** *(new in v2.1.0)*
- **Element Click Tracking** (`trackLink`): bind click listeners to elements by tag / class / id
- **Single-Page View Refresh** (`autoTrackSinglePage`): re-trigger page view on SPA route changes

> Auto-collected events `ta_pageview` (SDK v2.4.0+) and `ta_page_click` (SDK v2.5.0+) are configured in the **Initialization** tag's auto-tracking settings and are **off by default** (opt-in) to avoid unexpected data volume.

## 🛠️ **Installation & Usage**

### 1. Import Template
1. In Google Tag Manager, go to **Templates** → **Tag Templates**
2. Click **New** → **Import**
3. Select the `Thinking Engine.tpl` file
4. **Save** the template

### 2. Create SDK Initialization Tag
1. Create a new tag using the "Thinking Engine" template
2. Select **🚀 초기화 (init)** as tag type
3. Configure required settings:
   - **App ID**: Your Thinking Engine project ID
   - **Server URL**: Data collection endpoint (use default)
   - **Instance Name**: SDK instance name (default: "ta")
4. Set trigger to fire on all pages
5. **Save** and **Submit**

### 3. Create Event Tracking Tags
1. Create additional tags for specific events
2. Select appropriate tag type (track, login, userSet, etc.)
3. Configure event-specific parameters
4. Set appropriate triggers
5. **Save** and **Submit**

## 📖 **Configuration Examples**

### Basic Event Tracking
```
Tag Type: 📊 기본 이벤트 전송 (track)
Event Name: button_click
Event Properties:
  - button_id: "cta_button"
  - page_section: "header"
```

### User Login
```
Tag Type: 👤 로그인 (login)
Account ID: {{User ID Variable}}
```

### User Properties
```
Tag Type: ⚙️ 사용자 속성 설정 (userSet)
User Properties:
  - membership_level: "premium"
  - preferred_language: "ko"
```

### Global Properties
```
Tag Type: 🌍 공통 속성 설정 (setSuperProperties)
Global Properties:
  - app_version: "2.1.0"
  - platform: "web"
```

## 🔧 **Advanced Features**

### First-time Event Tracking
Prevent duplicate tracking of important one-time actions:
```
Tag Type: 📊 최초 이벤트 (trackFirst)
Event Name: app_install
First Check ID: {{User ID}} (optional)
```

### Time-based Tracking
Measure duration between events:
```
1. Start timing: Tag Type: 📊 이벤트 시간측정 (timeEvent)
   Event Name: video_play

2. Send timed event: Tag Type: 📊 기본 이벤트 전송 (track)
   Event Name: video_play
   (Duration will be automatically included)
```

### Page-specific Properties
Set context that applies only to current page:
```
Tag Type: 🌍 페이지 공통 속성 설정 (setPageProperty)
Page Properties:
  - page_category: "product"
  - content_type: "detail"
```

### Element Click Tracking (`trackLink`)
Bind click listeners to elements matching tag/class/id rules:
```
Tag Type: 🖱️ 요소 클릭 추적 (trackLink)
Event Name: link_click
Element Rules:
  - tag: a
  - tag: button
  - class: cta-button
Event Properties:
  - section: "header"
```
> Listeners are attached only to elements present when the tag fires. For elements created later (e.g. after route changes), fire `trackLink` again.

### Single-Page App Page Views (`autoTrackSinglePage`)
Re-trigger a page view on SPA route changes (fire on a History Change trigger):
```
Tag Type: 📄 단일 페이지 조회 갱신 (autoTrackSinglePage)
```

### Auto-collected Events (Initialization tag)
Enable in the init tag's **🤖 자동 수집 설정** group:
```
☑ 📄 ta_pageview   (single-page view, SDK v2.4.0+)
☑ 🖱️ ta_page_click (element click, SDK v2.5.0+)
🔧 Common properties: source = {{Traffic Source}}
```

## 🎯 **Best Practices**

### 1. **Initialization First**
- Always create and deploy the initialization tag before any tracking tags
- Use the same instance name across all tags

### 2. **Organized Naming**
- Use clear, consistent event names (e.g., `button_click`, `page_view`)
- Follow naming conventions: lowercase with underscores

### 3. **Property Management**
- Use global properties for app-wide context (version, platform)
- Use page properties for page-specific context
- Use user properties for user-specific attributes

### 4. **Testing & Debugging**
- Enable debug logging during development
- Test in Preview mode before publishing
- Verify data in Thinking Engine dashboard

## 🔍 **Troubleshooting**

### Common Issues

**"SDK not found" Error**
- Ensure initialization tag fires before tracking tags
- Check that the same instance name is used across all tags
- Verify App ID and server URL are correct

**Events Not Appearing**
- Check network tab for successful API calls
- Verify event name follows naming conventions
- Enable debug logging to see detailed execution logs

**Validation Errors**
- Review error messages for specific field requirements
- Ensure required fields are populated
- Check data formats match expected patterns

## 📚 **Additional Resources**

- [Thinking Engine Documentation](https://docs.thinkingdata.cn/)
- [GTM Template Development Guide](https://developers.google.com/tag-platform/tag-manager/templates)
- [JavaScript SDK Reference](https://docs.thinkingdata.cn/ta-manual/latest/installation/client_sdk/js_sdk_installation/js_sdk_installation.html)

## 🤝 **Contributing**

Contributions are welcome! Please feel free to submit issues and enhancement requests.

## 📄 **License**

This project is licensed under the Apache License, Version 2.0. See the [LICENSE](LICENSE) file for details.

---

**Template Version**: 2.1.0  
**Compatible with**: Thinking Engine JavaScript SDK (`thinkingdata-browser` v2.x; `ta_pageview` requires v2.4.0+, `ta_page_click` requires v2.5.0+)  
**GTM Template API Version**: Latest  