# The Y2K & Y2K38 Bug: A Journey Through Time and Storage Limits

**Group WDA** — Bantillo, Airon Matthew F. · Chavez, Max Benedict B. · Chiu, Kristopher Lance A. · Ponce, Jean Rondel R. · Santiago, Juan Ramon B.

A virtual exhibit exploring the Y2K and Y2K38 bugs through interactive visualizations. Built with Astro and React.

[Proposal Document (Google Docs)](https://docs.google.com/document/d/1KCnWIysS6aAWw4uJ-eVQevVSCrbUeSrRp5RZ-RqUPNM/edit?tab=t.0)

---

## Phase 1: Wireframing & Content Creation

**Status:** Complete

### Summary

- Created wireframes and content for the exhibit
- Developed layout designs for the exhibit pages

### Wireframes

![title page](src/assets/phase1-wireframing/title-page.png)
_Title page — Entry screen for the exhibit_

### Aha Moments

- Discovered how the Y2K38 bug relates to class discussions on signed integer overflow

### Challenges

- Learning new front end technologies such as Astro, React, etc.
- Deciding which specific content belongs in each page (e.g., Landing page, Timeline page, Failure states)

### Creative Decisions

- Decided to create wireframes using pixel art style in Figma

---

## Phase 2: Project Setup & Scaffolding

**Status:** Complete

### Summary

- Set up project with Astro, React, and MDX integrations
- Configured global styles, layouts, and GitHub Pages deployment
- Removed template example pages and components

### Aha Moments

- Learned how the template works — just fill up an `.mdx` file and it renders as a page
- Learned how Astro works — content-first, zero JS by default, components hydrate only when needed
- Understood how `client:load` directive tells Astro to hydrate React components

### Challenges

- Trying to understand how the existing codebase works

### Creative Decisions

- Decided to add one exhibit page with the slug `/y2k-38`

---

## Phase 3: Building Title Page

**Status:** Complete

### Summary

- Created TitlePage component with retro TV screen aesthetic
- Implemented hero section with logo, description, and navigation buttons
- Integrated component into y2k-38.mdx exhibit page
- Applied custom CSS styling for background and typography

### Aha Moments

- Learned how to use the layouts of this template:
    - Layouts provide page structure (header, footer, navigation)
    - MDX files specify layout in frontmatter
    - Components can be imported and composed within MDX
    - Layout receives content via `<slot />` component

### Challenges

- Applying the custom design (retro TV screen aesthetic) to the existing layout structure

### Creative Decisions

- Applied the design by creating a separate TitlePage component and importing it into the MDX file, rather than modifying the layout itself

---

## Phase 4: Countdown & Overflow Effects

**Status:** Complete

### Summary

- Implemented Unix epoch forward counter approaching the Y2K38 overflow boundary
- Created interactive scrubber/timeline with play/stop and speed controls (1x, 2x, 4x, 8x)
- Implemented 2's complement conversion for signed 32-bit integer display
- Added three-tier glitch effect system (teaser, full glitch, overflow pulse)
- Created warning text display with timed flash animation

### Aha Moments

- Learned how 2's complement works: unsigned values greater than 2^31-1 become negative via subtraction (subtracting 2^32)
- Understood timer mechanics: how setInterval, speed controls, and scrubber interaction work together for smooth animation

### Challenges

- Timer synchronization: Issues with play/stop/speed controls and glitch pausing/resuming

### Creative Decisions

- Designed three-tier glitch system: teaser glitch (pre-overflow), full glitch (at overflow), overflow pulse
- Implemented warning text timing: showing warning on play-start and timeline loop
- Applied visual design choices: CSS animations, colors, and pixel font styling for retro aesthetic

---

## Phase 5: Glitch Effects Expansion

**Status:** Complete

### Summary

- Synchronized glitch effects across GlobeCarousel and Y2k38Info using custom events
- Added teaser, full glitch, overflow, and negative aftermath states with CSS animations
- Implemented "INTEGER OVERFLOW DETECTED" and "EPOCH CORRUPTED" text overlays

### Aha Moments

- Custom events enable real-time coordination between independent components
- CSS filters and keyframe animations create convincing glitch aesthetics
- Multi-state transitions require careful timing to feel organic

### Challenges

- Syncing glitch triggers across components without lag or visual glitches
- Balancing visual intensity with usability during overflow states
- Designing distinct yet cohesive effects for each glitch tier

### Creative Decisions

- Expanded to four-tier glitch system (teaser → full glitch → overflow → negative aftermath)
- Used custom events for loose coupling between components
- Applied CRT-style distortion via CSS filters and text shadows

---

# Phase 0: Proposal

## Theme

In the early age of computers, back in the 1960s to the 1980s, storage in computers was very limited and costly. To save space, several computer programmers stored only the last two digits of the year (e.g., 1971 is stored as `71`). At that time, however, many computer scientists had already identified an issue: when the year 2000 arrived, software that relied on operating on dates seemed to break, a bug known as the **Y2K (Year 2000) bug**.

The Y2K bug was anticipated in several computer systems across the globe, which occurred when dealing with dates beyond December 31, 1999. This means that the year 2000 will be stored as `00`, which computers can misinterpret as 1900. This becomes highly problematic for systems with this date representation scheme. For example, in banks, instead of the interest from borrowings being calculated for plus one day, it will be calculated for minus 100 years.

Widespread panic surfaced as the year 2000 approached. With global action and millions of dollars spent throughout the 90s, the world's scientists changed the year representation to 4 digits, resolving the bug. Although many legacy applications still experienced errors, the transition occurred with no incident.

In a similar manner, many scientists are now predicting the **Y2K38 bug**, which is related to how the date is stored. Currently, systems represent dates in time elapsed since January 1, 1970 (Unix Epoch) using a 32-bit signed integer. The issue is on **January 19, 2038, at exactly 03:14:07 UTC**, 2,147,483,647 seconds will have elapsed since January 1, 1970. This number is the maximum value for a 32-bit signed integer. The next second will overflow into -2,147,483,648, which computers may interpret as December 13, 1901, causing the same problems anticipated from the Y2K bug.

At present, many scientists and developers are preparing for this through upgrading to 64-bit time tracking and code rebases. Unlike Y2K, where there was panic, however, preparation has been done early, being a quiet, ongoing reorganization into the future.

## Proposed Interactive Elements

### 1. Timeline Slider

**Educational Impact:** The goal for this animation is to enlighten users on code and storage limitations with regard to dates and their real-world consequences on everyday systems. Through interacting with this element, the users will be able to learn about how dates are stored, how truncation and 32-bit integers work and why they are necessary, and how computers perceive time.

**Features:**

- This interactive element will feature a draggable slider allowing for navigation across a timeline of events spanning the late 20th century to 2038 in relation to the Y2K and the Y2K38 Bug.
- Two critical points in the timeline are highlighted: **January 1, 2000**, and **January 19, 2038**.
- As the user hits the two critical points in the timeline, animations are played to show how different industries are affected by the bug (Banking, Healthcare, Telecommunications, Aviation, Retail).
- These animations are accompanied by textual explanations and actual mathematical calculations as the system clock overflows.
- Overflow animations will also be shown (truncation for Y2K, and binary sign-flip for Y2K38).

**User Flow:**

| Stage                | Interaction & Visuals                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Discovery**        | Once the user lands on the page, they will see a horizontal timeline slider starting in the late 1900s, along with a textual background on how dates are stored during that time. As they slide through the timeline, operational data from different industries are shown to be normal and stable.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| **Y2K Crossing**     | As the user drags the slider past January 1, 2000, the UI changes into a failure state accompanied by animations of how industries were affected by the Y2K bug.<br/>**Banking** — Accumulated interest payments will be seen dropping below 0 as the date reverts to 1900.<br/>**Healthcare** — The ages of patients in hospital databases will be subtracted by 99.<br/>**Telecommunications** — Phone calls that started on December 31, 1999, and ended on January 1, 2000, will be billed for a 99-year phone call as 99 gets subtracted from 00.<br/>**Aviation** — Several airplanes will be grounded as they are labeled as almost 99 years overdue for their strictly scheduled maintenance.<br/>**Retail** — Cash registers print receipts with the date January 1, 1900. The transaction software freezes to defend against data corruption as it registers an invalid date. |
| **Intermediate Era** | As the user continues sliding past the 2000s, the animations stabilize and show the corrected and patched data.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| **Y2K38 Crossing**   | As the user drags the timeline past January 19, 2038, a second round of animations appears showing how the industries could encounter the same problems as systems interpret the date as December 13, 1901.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

### 2. Unix Epoch Clock

**Educational Impact:** This element aims to show users how computers store time at a low level. It will feature the concepts of Epoch time as a standard date representation scheme, how 32-bit signed integers work, and how expanding to 64-bit increases the numeric limit.

**Features:**

- Multi-format clock showing current time: Date & Time (UTC), Date & Time (PST), Unix Epoch, Unix Epoch 32-bit binary.
- Button to fast-forward to **January 19, 2038, 03:14:07 UTC**. A button to step one second forward to see the time break the 32-bit signed integer ceiling.
- Button to trigger display state-driven UI overlays containing explanatory information of why the bug occurs, and another to trigger an architectural upgrade to 64-bit integer.

**User Flow:**

1. **Real Time Monitoring:** Users will first encounter the Unix Epoch Clock showing current time in different formats (UTC, PST, Unix Epoch, Unix Epoch 32-bit Binary).
2. **Fast Forward to 2038:** The user clicks a fast forward to 2038 button that shifts the clock to January 19, 2038, 03:14:07 UTC and pauses. Unix timestamp will read `2147483647`, while the 32-bit binary will read `0111 1111 1111 1111 1111 1111 1111 1111`.
3. **Overrun:** The user clicks a button to go to the next second and the date suddenly reverts to December 13, 1901 with the Unix and 32-bit binary shifting to `-2147483648` and `1000 0000 0000 0000 0000 0000 0000 0000` respectively.
4. **Explanation:** The user clicks a button that shows a popup explaining what caused the date to roll back to specifically December 13, 1901.
5. **System Upgrade:** The user clicks a button to upgrade the Unix Epoch storage to 64-bit and the clock reverts to its expected values.

## Tech Stack Plan

| Category            | Tech                                                     |
| ------------------- | -------------------------------------------------------- |
| Framework & Runtime | Node.js 26, Astro 6 (@astrojs/mdx, @astrojs/react)       |
| Frontend            | React 19 (via Astro integration)                         |
| Animation           | GSAP (GreenSock) — Overflow animations & timeline slider |
| Deployment          | GitHub Pages (Static site export)                        |

## Tentative Snapshot Guide

### Theme & Vibe

| Aspect    | Description                                              |
| --------- | -------------------------------------------------------- |
| Vibe      | Space / Universal                                        |
| Art Style | Minimalist Flat Design with heavy use of Vector elements |

![Color Palette](src/assets/phase0-proposal/Color_Palette.png)

### Typography

| Use            | Font                       |
| -------------- | -------------------------- |
| Headers        | Poppins (Bold / Black)     |
| Body / Content | Poppins (Regular / Medium) |

### Layout

- **Landing page** — Entry point to the exhibit.
- **Timeline page (Up to 2038)** — Users scroll to gradually increase the timeline and get more information about what is happening at a certain timestamp.
- **Prevent the catastrophe page** — After reaching the 2038 limit, users are given a choice to explore an alternate timeline where the Y2K bug is addressed. They are redirected to another timeline page with different content (particularly the binary display).
- **Navigation** — Navigation bar and footer across all pages.
- **Timeline information** displayed in UTC, PST, Unix Epoch, and Unix Epoch 32-bit Binary.

### Accessibility

- **Contrast:** The team will ensure ease of visual navigation by implementing contrast between the space/galaxy-themed background and the more vibrantly colored foreground elements.
- **Responsive and Interactive Design:** Users can scroll to rewind or advance the timeline. Buttons and icons appear per timestamp for comprehensive explanations.
- **Desktop and Mobile Responsiveness:** Compatible for both mobile and desktop with a cohesive layout. Mobile users are encouraged to rotate to landscape for a better timeline experience.

## Low-Fidelity Wireframes

The proposed user interface was designed with the following low-fidelity mockups:

![Begin Exploration](src/assets/phase0-proposal/Begin%20exploration%20-%20Low%20fidelity%20%5BDesktop%5D.png)
_Begin Exploration — Entry point to the exhibit_

![32-bit Timeline](src/assets/phase0-proposal/32-bit%20timeline%20-%20Low%20fidelity%20%5BDesktop%5D.png)
_32-bit Timeline — Default timeline view_

![32-bit Timeline Break](src/assets/phase0-proposal/32-bit%20timeline%20break%20-%20Low%20fidelity%20%5BDesktop%5D.png)
_32-bit Timeline Break — Overflow failure state_

![32-bit Timeline End](src/assets/phase0-proposal/32-bit%20timeline%20_%20end%20Low%20fidelity%20%5BDesktop%5D.png)
_32-bit Timeline End — Terminal overflow state_

![64-bit Timeline](src/assets/phase0-proposal/64-bit%20timeline%20-%20Low%20fidelity%20%5BDesktop%5D.png)
_64-bit Timeline — Post-upgrade resolved state_

![Explore 64-bit Timeline](src/assets/phase0-proposal/Explore%20another%20timeline%20%2864-bit%29%20-%20Low%20fidelity%20%5BDesktop%5D.png)
_Explore 64-bit Timeline — Branching alternative timeline_

## Project Structure

```text
/
├── public/
├── src/
│   ├── assets/          # Images and static assets
│   ├── components/      # React and Astro components
│   ├── layouts/         # Page layouts
│   ├── pages/           # Route pages (including exhibit.mdx)
│   └── styles/          # Global styles
├── package.json
└── astro.config.mjs
```

## Commands

| Command             | Action                                     |
| ------------------- | ------------------------------------------ |
| `npm install`       | Install dependencies                       |
| `npm run dev`       | Start local dev server at `localhost:4321` |
| `npm run build`     | Build production site to `./dist/`         |
| `npm run preview`   | Preview build locally                      |
| `npm run astro ...` | Run Astro CLI commands                     |

---

# AI Usage

## Tools Used

- **OpenCode** — AI-assisted programming with spec-driven development
    - Models: MiMo V2.5, Claude (Anthropic)
    - Used for: component implementation, debugging, code assistance

## Design & Content

- **Figma** — All exhibit content and visual design
    - [Figma Design File](https://www.figma.com/design/1q23iaEq8g1RFSozDMizUD/CSARCH2?node-id=0-1&p=f&t=R7O76k45ZUSCmusg-0)
- **Google Docs** — Proposal document
    - [Proposal Document](https://docs.google.com/document/d/1KCnWIysS6aAWw4uJ-eVQevVSCrbUeSrRp5RZ-RqUPNM/edit?tab=t.0)

## Architecture & Design

- Architecture decisions based on the provided Astro template
- Coding design structure and architecture designed by the team developers

---

# References

National Geographic Society. (n.d.). Y2K bug. National Geographic. Retrieved July 7, 2026, from https://education.nationalgeographic.org/resource/Y2K-bug/
(Note: Educational entries that are continually updated and lack a publication date require a retrieval date in APA 7. Some archived versions of this page list specific contributing educators [e.g., Rutledge, K., et al.], but citing the National Geographic Society as the corporate author is standard for their encyclopedia entries).

Inventive HQ. (2025, February 20). Y2038 bug: Will your systems crash on January 19, 2038? https://inventivehq.com/blog/year-2038-problem-explained

Vartak, S. (2026, April 2). The year 2038 problem: The next “Y2K” waiting to happen? Medium. https://medium.com/@shubhamvartak01/the-year-2038-problem-the-next-y2k-waiting-to-happen-2ba3fdc72ea5
