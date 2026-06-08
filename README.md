# Rootstock App Build Notes

## App name

**Rootstock 🌱 Personal Network Manager**

## Website

Live site:
[https://sunying12.github.io/zotnet/](https://sunying12.github.io/zotnet/)

## What this app is

Rootstock is a lightweight personal CRM for managing people I meet through conferences, work, fundraising, collaborations, friendships, and general life. The goal is to help me remember who people are, why they matter, what we talked about, and what I need to follow up on.

I started this as a simple HTML file and gradually turned it into a usable web app hosted through GitHub Pages, with ongoing improvements to data storage, interactions, trash/restore behavior, and follow-up tracking.

## Why I built it

I wanted a private relationship manager that was simpler and more personal than a full business CRM. I needed a place to track:

* people I meet at conferences
* collaborators, mentors, peers, funders, and professional contacts
* personal notes about people
* personality types and communication styles
* interaction history
* follow-up tasks
* when I last contacted someone
* who I should reconnect with soon

The app is meant to support intentional relationship building instead of letting important contacts disappear into emails, notes, or memory.

## Main features

### People / contact management

Each person can have a profile with:

* name
* company or organization
* role/title
* email
* relationship category
* tags
* notes
* why they matter
* how to engage them
* personality information

The app reports an error if I try to add the same name twice. This prevents accidental duplicate contacts.

### Personality guide

I added a personality guide section so I can track and think about different communication styles. The app includes:

* MBTI types
* DISC types
* Enneagram
* general identification tips

This is meant to help me remember how to communicate with different people in a more thoughtful way.

### Interactions

Interactions are notes tied to a specific person. They are not supposed to be independent records floating around by themselves.

Each interaction can include:

* person
* interaction type
* date
* notes about what we talked about
* sentiment
* follow-up status
* action needed
* due date
* completed checkbox

Interactions show up under the person’s profile, so when I click a person I can see the full relationship history.

### Editable interactions

I added the ability to edit interactions because sometimes I need to correct or add more notes after logging something.

This matters because relationship notes are living records. I may remember more details later, or I may need to update the action item or due date.

### Follow-up and action-needed tracking

The app includes follow-up tracking so I can mark whether an interaction needs action.

Follow-up fields include:

* needs follow-up checkbox
* action needed
* due date
* completed checkbox

The dashboard can show open follow-up items so I know what needs attention.

### Reconnect soon

The reconnect section automatically shows people I have not contacted recently.

The current logic is:

* the app checks each person’s most recent interaction
* if they have no interactions, it uses their created date
* if it has been 30+ days since the last contact, they show up under Reconnect Soon
* the people who have gone the longest without contact appear first

This is meant to remind me to maintain relationships, not just collect contacts.

### People tab interaction summary

The People tab now shows:

* how many interactions are associated with each person
* the last contacted date
* “Never contacted” if there are no interactions yet

This helps me quickly scan my network and see who I have actually followed up with.

### CSV export

The app includes CSV export so I can back up or move data.

CSV export should include people and interaction-related fields. One earlier issue was that interaction history was not being recorded in the CSV file, so that became a feature to fix.

### Trash bin and restore system

I added a trash bin because I did not want to accidentally delete someone’s contact information.

Trash behavior:

* deleted people go to Trash instead of being permanently removed immediately
* Trash items are kept for 30 days
* deleted people can be restored
* after 30 days, items are deleted permanently
* deleted interactions also go to Trash
* deleted interaction notes can be restored
* if a person is deleted, their linked interactions are caught by Trash too
* if the person is restored, their interactions are restored too

This prevents accidental loss of important relationship history.

### Smaller delete buttons

I made delete buttons smaller and less prominent across the app so deletion is harder to do accidentally.

The app should make adding and editing easy, but deleting should feel more intentional.

## Data and storage

### Local storage

The app uses browser localStorage as an offline/local backup method. This means the data can persist in the browser even without a backend.

Local storage is useful for simple testing and offline backup, but it is not ideal as the only storage method because data can be browser/device-specific.

### Firebase / Google API

I added Firebase cloud sync so the app can store data in the cloud instead of only in the browser.

Firebase is connected through a Google/Firebase API configuration.

Important note: I had a GitHub secret scanning warning about a Google API key being visible in the HTML file. For a public GitHub Pages app, the Firebase API key may appear in frontend code, but it should still be protected by:

* Firebase security rules
* domain restrictions
* authentication if needed
* revoking/rotating exposed keys if GitHub flags them
* checking Google Cloud logs for suspicious use

The real security protection should come from Firebase rules and authentication, not from trying to hide a frontend Firebase config key in a static HTML file.

## Hosting and deployment

The app is hosted on GitHub Pages.

Project link:
[https://sunying12.github.io/zotnet/](https://sunying12.github.io/zotnet/)

Build path:

1. I started with a simple HTML file.
2. I wanted to put it online.
3. I used GitHub Pages to host the app.
4. GitHub was confusing at first, so I downloaded GitHub Desktop.
5. I used GitHub Desktop to update and push files.
6. I added Firebase for cloud storage.
7. I kept updating the HTML file and pushing updated versions through GitHub.
8. The current app is like a v1 model that works, but I am still improving usability and data safety.

## Key development lessons

### 1. Start simple

The app began as one HTML file. That made it easy to experiment quickly.

### 2. Add features one at a time

Features were added gradually:

* people records
* personality guide
* duplicate-name validation
* interactions
* follow-ups
* trash bin
* restore behavior
* CSV export
* Firebase/cloud sync
* better UI
* smaller delete buttons

### 3. Be careful with data relationships

One major issue was that people and interactions were initially too independent.

The better structure is:

* people are the main records
* interactions belong to people
* follow-ups belong to interactions
* trash must preserve both people and interactions

This is important because if I delete or restore a person, their interaction history should not disappear.

### 4. Deletion needs safety

Deleting data should not be instant or easy to do accidentally. That is why I added:

* trash bin
* 30-day restore window
* smaller delete buttons
* separate restore logic for contacts and interactions

### 5. A CRM needs history, not just contacts

The most useful part of the app is not just storing names. The value is in tracking:

* what we talked about
* when we last connected
* what I promised to do
* what needs follow-up
* how the relationship is developing

## Current version concept

The current app is a working v1 personal CRM.

It includes:

* Firebase cloud sync
* offline/localStorage backup
* trash/restore system
* duplicate-name validation
* CSV exports
* personality guide
* reconnect reminders
* improved UI
* person-linked interactions
* editable interactions
* follow-up/action-needed checkboxes
* deleted interaction restore
* last-contacted tracking
* interaction count per person

## Future improvements

Possible next improvements:

* add login/authentication so only I can access the app
* improve Firebase security rules
* restrict Firebase API key usage
* add import from CSV
* add better search across notes and interactions
* add reminders by due date
* add “priority contacts”
* add conference/event grouping
* add relationship strength score
* add tags for investors, collaborators, customers, friends, etc.
* add backup/export all data as JSON
* eventually split the app into separate files instead of one large HTML file

## Summary

Rootstock is a personal relationship CRM I built from a simple HTML file into a more functional web app. It helps me track people, personality types, interaction history, follow-ups, reconnect reminders, and deleted items safely.


