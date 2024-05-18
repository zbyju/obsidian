**Analýza chování uživatelů na webu: sběr dat a metriky, typy doporučovacích systémů, jejich evaluace, výhody a nevýhody.**

# Web Usage
- Discover usage patterns
- Extract useful information from logs
- Find interests of users

1. Data collection + Preprocessing
2. Pattern discovery
3. Pattern analysis

## Input Data
Main source: **server logs** containing: time, IP, resource + parameters, status, method, user agent, headers, cookies
Other sources: content data (html, images), structure data (links, structure of website), user data (user profile, demographics)

## Collecting
- Explicit
	- = filling forms, questionnaires, ratings, ...
	- simplest
	- high quality
	- privacy concerns
	- low amount
	- low motivation for users
- Implicit
	- inferring information from user interactions
	- = clicks, interactions, accessing, gesture, posture, eye tracking, ...
	- non-invasive way
	- difficulty interpreting