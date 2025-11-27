# SF SUPERNOVA - Information Architecture Document

**Version:** 1.0  
**Date:** 26 November 2025

---

## Table of Contents

- [Executive Summary](#executive-summary)
- [1. Site Structure Overview](#1-site-structure-overview)
- [2. Navigation Systems](#2-navigation-systems)
- [3. Content Taxonomy & Classification](#3-content-taxonomy--classification)
- [4. User Journeys & Scenarios](#4-user-journeys--scenarios)
- [5. Search & Filtering Systems](#5-search--filtering-systems)
- [6. Page Templates & Components](#6-page-templates--components)
- [7. SEO & Discoverability Architecture](#7-seo--discoverability-architecture)
- [8. Responsive & Accessibility Considerations](#8-responsive--accessibility-considerations)
- [9. Content Management & Scalability](#9-content-management--scalability)
- [10. Analytics & Measurement](#10-analytics--measurement)
- [11. Future IA Enhancements](#11-future-ia-enhancements)
- [12. Appendices](#12-appendices)
- [13. Document Control](#13-document-control)

---

## Executive Summary

### Purpose & Scope

### Key Architectural Principles

---

## 1. Site Structure Overview

### 1.1 Information Hierarchy

#### 1.1.1 Level 0: Homepage

The homepage serves as the primary entry point and value demonstration layer, designed to immediately establish credibility and guide users toward their intent (browse, search, or discover). Key components include hero messaging ("Discover the overlooked masterpieces of golden age sci-fi"), featured content carousels (recent articles, new releases, curated collections), and clear navigation pathways to core site sections. The homepage must achieve bounce rate <60% and communicate SF Supernova's unique value proposition within 5 seconds of landing.

#### 1.1.2 Level 1: Primary Navigation Categories

Primary navigation consists of five core sections accessible from global header: **Discover** (browse by era, theme, author, format), **Library** (digital product catalog with ebooks and audiobooks), **Articles** (editorial content, reviews, author profiles), **Membership** (tier comparison and benefits), and **About** (mission, founder story, contact). Each primary category serves distinct user intents—Discover supports exploration, Library enables commerce, Articles builds trust through content, Membership drives recurring revenue, and About establishes authenticity. Maximum 3 clicks required from homepage to any content or product detail page.

#### 1.1.3 Level 2: Sub-Categories & Browse Pages

Sub-categories provide faceted navigation within primary sections: Discover includes Era pages (1920s-1980s by decade), Theme pages (30+ categories like Time Travel, Space Opera, Dystopia), Author Directory (alphabetical with filters), and Format pages (novels, short stories, radio dramas). Library divides into Ebooks, Audiobooks, Collections/Bundles, and New Releases, each with sorting and filtering capabilities. Articles segment into Reviews, Author Profiles, Historical Context, and Curated Lists. All browse pages feature consistent filtering UI, clear breadcrumbs, and related content recommendations.

#### 1.1.4 Level 3: Content Detail Pages

Detail pages represent final destination for user intent fulfillment with four primary templates: **Work/Book Detail** (product pages with description, metadata, purchase/download CTA, samples, and related works), **Article Detail** (editorial content with reading time, author byline, social sharing, and email capture), **Author Profile** (biography, bibliography, influence relationships, and available products), and **Collection/Bundle** (curated sets with value proposition, included works, and purchase options). Each template optimizes for both user engagement (discovery, reading) and conversion (email capture, purchase, membership signup).

#### 1.1.5 Level 4: Utility & Support Pages

Utility pages support user account management, commerce, and legal compliance: **Account Dashboard** (membership status, purchase history, credits, settings), **Checkout Flow** (cart, payment, confirmation), **Member Content** (exclusive articles, benefits overview), **Search Results** (unified search across all content types), and **Legal/Support** (Terms of Service, Privacy Policy, Refund Policy, Contact/FAQ). These pages prioritize functionality over discovery, with minimal distraction and clear task-completion pathways. Member dashboard provides self-service for subscription management to minimize support overhead.

### 1.2 URL Structure & Taxonomy

#### 1.2.1 URL Design Principles

All URLs follow SEO-first conventions with human-readable slugs, hierarchical structure reflecting content relationships, and consistent patterns for predictability. URLs prioritize discoverability (targeting long-tail searches like "1950s dystopian science fiction") while maintaining technical best practices including lowercase only, hyphens as separators, and no unnecessary parameters. The structure supports both user comprehension (breadcrumb generation) and search engine indexing (clear topical hierarchy). Maximum URL depth is 4 levels to balance organization with crawlability and user trust.

#### 1.2.2 Primary URL Patterns

Homepage resides at root (`/`), primary navigation categories use single-level paths (`/discover`, `/library`, `/articles`, `/membership`, `/about`). Product catalog follows `/library/{format}/{slug}` pattern (e.g., `/library/ebooks/foundation-asimov`, `/library/audiobooks/time-machine-wells`). Editorial content uses `/articles/{type}/{slug}` structure (e.g., `/articles/reviews/neuromancer-review`, `/articles/authors/isaac-asimov-biography`). All slugs incorporate primary keywords for SEO while remaining concise and readable.

#### 1.2.3 Taxonomy-Based URLs

Browse pages follow hierarchical taxonomy: `/discover/era/{decade}` (e.g., `/discover/era/1950s`), `/discover/theme/{theme-slug}` (e.g., `/discover/theme/time-travel`), `/discover/author/{author-slug}` (e.g., `/discover/author/asimov-isaac`). Collections use `/library/collections/{collection-slug}` (e.g., `/library/collections/golden-age-essentials`). Taxonomy URLs support breadcrumb navigation and enable faceted filtering without query parameters for clean, shareable URLs. Author URLs use lastname-firstname convention for alphabetical sorting and collision avoidance.

#### 1.2.4 Dynamic & Filter URLs

Filtered browse results append query parameters to base taxonomy URLs: `/discover/theme/space-opera?era=1960s&format=audiobook&sort=popularity`. Search results use `/search?q={query}&type={content-type}` pattern with URL-encoded queries. Pagination follows `/discover/era/1950s?page=2` convention. Filter parameters use semantic names (era, theme, format, author, length) and support multiple values via comma separation (`format=ebook,audiobook`). All filtered URLs include canonical tags pointing to unfiltered base URL to prevent duplicate content penalties.

#### 1.2.5 Canonical URL Rules

Each content piece has exactly one canonical URL regardless of discovery path, with all alternate access routes (filtered views, search results, cross-references) specifying canonical via meta tag. Product pages canonicalize to `/library/{format}/{slug}` even when accessed via collections or themes. Author pages canonicalize to `/discover/author/{author-slug}` regardless of era or theme entry point. Pagination pages beyond page 1 self-canonicalize to prevent consolidation. Trailing slashes are enforced consistently (with slash) via 301 redirects, and all http:// URLs redirect to https:// for security and SEO.

## 2. Navigation Systems

### 2.1 Global Navigation

#### 2.1.1 Primary Navigation Menu

Five primary categories displayed in persistent header: **Discover** (browse by era/theme/author), **Library** (ebooks/audiobooks/collections), **Articles** (reviews/profiles/guides), **Membership** (tier comparison/benefits), and **About** (mission/contact/FAQ). Navigation remains visible during scroll (sticky header) with clear visual hierarchy prioritizing Discover and Library as primary traffic drivers. Each menu item triggers hover/click states revealing either dropdown content (desktop) or expanding panels (mobile). Visual design uses retro-futuristic typography with accent color highlighting active section.

#### 2.1.2 Secondary Utility Navigation

Right-aligned utility items include **Search icon** (global search overlay trigger), **Account/Login** (user dashboard access or signin modal), and **Cart icon** (product purchase counter with mini-cart preview). Free users see "Join Now" CTA button; members see account avatar with membership tier badge. Search icon prominence reflects SEO-driven acquisition strategy. All utility items maintain accessibility standards (ARIA labels, keyboard navigation) and responsive behavior collapsing to hamburger menu on mobile breakpoints.

#### 2.1.3 Mobile Navigation Patterns

Mobile navigation (<768px) collapses primary menu into hamburger icon positioned top-left, opening full-screen overlay with stacked menu items and nested accordions for subcategories. Search promoted to top of mobile menu as first interactive element. Utility items (account, cart) remain visible in collapsed header. Menu uses slide-in animation from left with semi-transparent backdrop, closable via X button, backdrop tap, or back gesture. Touch targets minimum 44px for iOS accessibility compliance.

#### 2.1.4 Mega Menu Structure

**Discover** and **Library** categories trigger mega menus (desktop only) displaying 3-column layouts: Browse dimensions (era/theme/author), Featured collections (curated entry points with thumbnails), and Quick links (popular destinations). Mega menus include visual previews (cover art thumbnails, era badges) to aid scannability and reduce cognitive load. Each column limited to 8-10 items maximum to prevent overwhelming users. Mega menu appears on hover with 200ms delay to prevent accidental triggers, remains open during mouse movement within bounds.

#### 2.1.5 Navigation States & Behaviors

Active section highlighted via accent color underline and bold weight; hover states use color transition (300ms) and subtle underline animation. Dropdown indicators (chevrons) rotate 180° when expanded using CSS transforms. Keyboard navigation supports tab through all items, Enter/Space to activate, Escape to close menus. Focus states include visible outline meeting WCAG 2.1 AA standards. Mega menus close when clicking outside bounds, navigating to new page, or pressing Escape; behavior includes smooth fade-out (200ms) for polished experience.

### 2.2 Contextual Navigation

#### 2.2.1 Breadcrumb Navigation

#### 2.2.2 Related Content Links

#### 2.2.3 In-Page Navigation (Table of Contents)

#### 2.2.4 Previous/Next Navigation

#### 2.2.5 Cross-Sell & Upsell Navigation









### 2.3 Footer Navigation

#### 2.3.1 Footer Menu Structure

#### 2.3.2 Legal & Policy Links

#### 2.3.3 Social Media & Community Links

#### 2.3.4 Newsletter Signup

#### 2.3.5 Site Credits & Branding


## 3. Content Taxonomy & Classification

### 3.1 Primary Taxonomies

### 3.2 Metadata Schema

---

## 4. User Journeys & Scenarios

### 4.1 Primary User Personas

### 4.2 Key User Flows

---

## 5. Search & Filtering Systems

### 5.1 Global Search

### 5.2 Faceted Filtering

---

## 6. Page Templates & Components

### 6.1 Homepage Template

### 6.2 Book Detail Page Template

### 6.3 Browse Landing Page Template

---

## 7. SEO & Discoverability Architecture

### 7.1 SEO-Optimized URL Strategy

### 7.2 Internal Linking Strategy

### 7.3 Structured Data (Schema.org)

---

## 8. Responsive & Accessibility Considerations

### 8.1 Mobile-First Navigation

### 8.2 Accessibility Architecture

---

## 9. Content Management & Scalability

### 9.1 Content Ingestion Workflow

### 9.2 Scalability Considerations

---

## 10. Analytics & Measurement

### 10.1 Key Metrics by Page Type

### 10.2 User Behavior Tracking

---

## 11. Future IA Enhancements

### 11.1 Phase 2 Features

### 11.2 Technical Enhancements

---

## 12. Appendices

### 12.1 Complete Sitemap

### 12.2 Glossary of Terms

---

## 13. Document Control

### 13.1 Version History

### 13.2 Approvals & Sign-Off

### 13.3 Document Maintenance

---

**End of Document**