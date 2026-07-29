# Accessibility Case Study: Building an Accessible Carousel (Slide Show or Image Rotator) Pattern
WCAG 2.2 AA | [WAI-ARIA APG](https://www.w3.org/WAI/ARIA/apg/patterns/carousel/) | Accessibility Audit & Remediation
# Overview
Carousels are widely used across e-commerce, banking, media, education, and SaaS applications to showcase featured content. Despite their popularity, they are one of the most common sources of accessibility issues because they often rely on automatic movement, complex interactions, and insufficient support for assistive technologies.

This case study demonstrates how a non-accessible carousel was evaluated and remediated using the WAI-ARIA Authoring Practices (APG) and WCAG 2.2 Level AA recommendations. The objective was to provide an experience that is usable by keyboard users, screen reader users, people with cognitive disabilities, and users with low vision.

# Project Goal

Improve the accessibility of an image carousel so that it can be used effectively by:

1.Keyboard-only users

2.Screen reader users

3.Users with cognitive disabilities

4.Users with motor impairments

5.Users with low vision

# Standards Used

1.WCAG 2.2 Level AA

2.WAI-ARIA Authoring Practices Guide (APG)

3.Section 508

4.EN 301 549

# Accessibility Problems Identified
| Issue                              | Impact                                | WCAG  |
| ---------------------------------- | ------------------------------------- | ----- |
| Carousel auto-rotates continuously | Difficult to read content             | 2.2.2 Pause, Stop, Hide|
| No pause button                    | Users cannot stop moving content      | 2.2.2 Pause, Stop, Hide|
| Previous / Next buttons unlabeled  | Screen readers announce only "Button" | 4.1.2 Name, Role, Value|
| Hidden slides exposed              | Screen readers read invisible content | 1.3.1 Info and Relationship|
| Keyboard focus becomes confusing   | Navigation becomes difficult          | 2.4.3 Focus Order|
| No announcement when slides change | Screen reader users lose context      | 4.1.3 Status Messages|
| Pagination dots inaccessible       | Cannot navigate directly to a slide   | 2.1.1 Keyboard|
| Focus indicator missing            | Hard to identify active element       | 2.4.7 Focus Visible |

# Accessibility Audit
**Before Remediation User Impact**

**1. Keyboard Users**

**Problems**

1.Unable to efficiently move between slides.

2.Focus unexpectedly shifts during navigation.

3.Difficult to identify the current interactive element.

**Result**

Navigation becomes frustrating and inefficient.

**2. Screen Reader Users**

**Problems**

1.Hidden slides are announced.
2.Slide changes occur without notification.
3.Previous and Next buttons are not clearly identified.

**Result**

Users lose context and cannot confidently understand their location within the carousel.

**3. Users with Cognitive Accessibility**

**Problems**

1.Automatic slide movement creates distractions.
2.Users cannot pause or control animation.
3.Information changes before it can be read.

**Result**

Increased cognitive load and reduced comprehension.

**4. Visual Accessibility or Users with Low Vision**

**Problems**

1.Insufficient contrast on navigation controls.
2.Focus indicators are difficult to perceive.

**Result**

Interactive controls are harder to locate and operate.

# Accessibility Remediation
**1. Accessible Carousel Landmark**

The carousel container now has an accessible label and semantic role.

<img width="792" height="180" alt="image" src="https://github.com/user-attachments/assets/8a4d47aa-f74b-40d3-b5b1-c886ad7312d8" />


**Why?**

Allows assistive technology users to quickly identify the component.

**2. Rotation Control**

A dedicated control was introduced to start and stop automatic slide rotation.

**Added:**

a. Pause Rotation

b. Start Rotation

The button label changes depending on its action.

**Accessible Labels**

**Example:**
<img width="965" height="195" alt="image" src="https://github.com/user-attachments/assets/dbfe28d4-2403-46cb-bdc9-93eef71da59e" />

Unlike toggle buttons, the APG recommends changing the accessible label to describe the action rather than using aria-pressed

**aria-pressed state** Indicates the current "pressed" state of toggle buttons. 

Toggle buttons require a full press-and-release cycle to change their value. 

Activating it once changes the value to true, and activating it another time changes the value back to false. 

A value of mixed means that the values of more than one item controlled by the button do not all share the same value. If the attribute is not present, the button is not a toggle button.

**3. Automatic Rotation Stops**

Rotation now stops when:

1.Keyboard focus enters carousel

2.Mouse pointer hovers over carousel

3.The user activates the pause control

Auto-play does not restart automatically after interaction; it resumes only when the user explicitly starts it again, matching the APG guidance.

**4. Previous / Next Buttons**

Before

<img width="797" height="111" alt="image" src="https://github.com/user-attachments/assets/67551bcc-b0d5-416c-8388-93a37c92d825" />

After

<img width="807" height="237" alt="image" src="https://github.com/user-attachments/assets/4e229dc2-a66f-4c03-aee6-f56bbdf275d8" />

Each control now exposes a meaningful accessible name.

**5. Keyboard Navigation**
Supported interactions
| Key         | Action             |
| ----------- | ------------------ |
| Tab         | Navigate controls  |
| Shift + Tab | Reverse navigation |
| Enter       | Activate button    |
| Space       | Activate button    |
| Left Arrow  | Previous slide     |
| Right Arrow | Next slide         |

Navigation controls retain focus after activation so users can repeatedly move through slides without unexpected focus changes, consistent with the APG interaction model.

**6. Screen Reader Announcements**

Implemented

<img width="812" height="172" alt="image" src="https://github.com/user-attachments/assets/ac4bcbe1-b064-4cc4-b5be-9f3e5cf18674" />

Example announcement
<img width="905" height="122" alt="image" src="https://github.com/user-attachments/assets/aaa4f6b4-eed5-428a-80e4-6d643f2ab819" />

**aria-live property**
Indicates that an element will be updated, and describes the types of updates the user agents, assistive technologies, and user can expect from the live region.

**Values**

**1.assertive**

Indicates that updates to the region have the highest priority and should be presented to the user immediately.

**2.off (default)**

Indicates that updates to the region should not be presented to the user unless the user is currently focused on that region.

**3.polite**

Indicates that updates to the region should be presented at the next graceful opportunity, such as at the end of speaking the current sentence or when the user pauses typing.

**aria-atomic property**

Indicates whether assistive technologies will present all, or only parts of, the changed region based on the change notifications defined by the aria-relevant attribute.

When the content of a live region changes, user agents **SHOULD** examine the changed element and traverse the ancestors to find the first element with aria-atomic set, and apply the appropriate behavior for the cases below.

1.If none of the ancestors have explicitly set aria-atomic, the default is that aria-atomic is **false**, and assistive technologies will only present the changed node to the user.

2.If aria-atomic is explicitly set to false, assistive technologies will stop searching up the ancestor chain and present only the changed node to the user.

3.If aria-atomic is explicitly set to true, assistive technologies will present the entire contents of the element, including the author-defined live region label if one exists.

**7. Hidden Slides**

Inactive slides

<img width="805" height="120" alt="image" src="https://github.com/user-attachments/assets/4a922f24-b69f-4379-8984-cd4a5f8727c2" />

Benefits

1.Hidden content ignored

2.Cleaner reading experience

3.Better virtual cursor navigation

**8. Accessible Slide Picker**

Pagination dots replaced with buttons

<img width="807" height="367" alt="image" src="https://github.com/user-attachments/assets/e0ffa8dc-901f-46cc-9e2f-249f06d2ef38" />

Active slide

<img width="810" height="115" alt="image" src="https://github.com/user-attachments/assets/37d1a3c6-22d5-4cb3-9196-f10dd730a701" />

**9. Focus Management**

Focus remains on the activated control after:

1.Previous

2.Next

3.Pause

4.Slide selection

Users always know where keyboard focus is located.

**10. Focus Visible**
<img width="892" height="200" alt="image" src="https://github.com/user-attachments/assets/a28bb742-03a9-4172-b44d-b20ccbd3386b" />

Keyboard users can always identify focus.

**11. Colour Contrast**

Navigation controls were updated from a contrast ratio below WCAG AA to a compliant ratio of 4.5:1 or higher, improving visibility for users with low vision.

# Results: Before vs After
| Before                  | After                    |
| ----------------------- | ------------------------ |
| Auto-rotating content   | User-controlled rotation |
| Hidden slides announced | Hidden slides ignored    |
| Buttons unlabeled       | Accessible names added   |
| Keyboard inaccessible   | Full keyboard support    |
| No announcements        | Live region updates      |
| Weak focus indicator    | High visibility focus    |
| Low contrast controls   | WCAG AA compliant        |

# Key Learnings

1.Accessible carousels require more than adding ARIA attributes; they depend on predictable interaction, user control, and clear communication.

2.Automated tools identify many static issues but cannot verify keyboard behavior, focus management, or screen reader experience. Manual testing remains essential. 

3.Following the WAI-ARIA Authoring Practices Guide ensures that custom components behave consistently across browsers and assistive technologies.

# Example

**[1.Auto-Rotating Image Carousel Example with Buttons for Slide Control](https://www.w3.org/WAI/ARIA/apg/patterns/carousel/examples/carousel-1-prev-next/)**

<img width="1141" height="535" alt="image" src="https://github.com/user-attachments/assets/8c9dc370-f3a2-4240-a2d9-1842bda724cf" />

**[2.Auto-Rotating Image Carousel with Tabs for Slide Control Example](https://www.w3.org/WAI/ARIA/apg/patterns/carousel/examples/carousel-2-tablist/)**

<img width="1125" height="512" alt="image" src="https://github.com/user-attachments/assets/6d58714c-763a-4ece-a5a3-c90996efed5e" />

**Created by Manjree Sharma | [LinkedIn](https://www.linkedin.com/in/manjree/)**
